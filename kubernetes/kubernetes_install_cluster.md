### CLUSTER PREQ ###

#### Enable Virtualization

- this is done on vcenter after the node is turned off; edit settings, and enable the following under CPU section

1. Hardware virtualization
2. Performance Counters

#### Disable swap

$ sudo swapoff -a

### Install Docker 

- https://docs.docker.com/install/linux/docker-ce/centos/

### Networking, Firewalls, Installing kubeadm, kubelet, kubectl, cgroups

1. verify unique MAC address per node

$ sudo cat /sys/class/dmi/id/product_uuid

2. allow ports

- workers ports in use --> 30000 - 32767

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#check-required-ports

- on control-plane nodes

TCP	Inbound	6443*	Kubernetes API server	All
TCP	Inbound	2379-2380	etcd server client API	kube-apiserver, etcd
TCP	Inbound	10250	Kubelet API	Self, Control plane
TCP	Inbound	10251	kube-scheduler	Self
TCP	Inbound	10252	kube-controller-manager	Self

$ sudo firewall-cmd --permanent --add-port=6443/tcp
$ sudo firewall-cmd --permanent --add-port=2379-2380/tcp
$ sudo firewall-cmd --permanent --add-port=10250/tcp
$ sudo firewall-cmd --permanent --add-port=10251/tcp
$ sudo firewall-cmd --permanent --add-port=10252/tcp

$ sudo firewall-cmd --reload

- on worker nodes

TCP	Inbound	10250	Kubelet API	Self, Control plane
TCP	Inbound	30000-32767	NodePort Services**	All

$ sudo firewall-cmd --permanent --add-port=10250/tcp
$ sudo firewall-cmd --permanent --add-port=30000-32767/tcp


3. install kubelet, kubeadm, kubectl 

```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

# Set SELinux in permissive mode (effectively disabling it)
$ setenforce 0
$ sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

$ sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

$ sudo systemctl enable --now kubelet

4. route traffic
```
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```

$ sudo sysctl --system

5. configure cgroups (if you are not using Docker, but different CRI, e.g. containerd, lxd, cri-o, frakti)

KUBELET_EXTRA_ARGS=--cgroup-driver=<value>

6. enable and start 

$ sudo systemctl enable kubelet
$ sudo systemctl start kubelet 

### Configure a Load Balancer

- HAProxy

add frontend:

frontend k8s-api
    bind 10.1.52.148:443
    bind 0.0.0.0:443
    mode tcp
    option tcplog
    timeout client 300000
    default_backend k8s-api

add backend:

backend k8s-api
    mode tcp
    option tcplog
    option tcp-check
        timeout server 300000
    balance roundrobin
    default-server inter 10s downinter 5s rise 2 fall 2 slowstart 60s maxconn 250 maxqueue 256 weight 100

    server apiserver1 <server_ip>:6443 check
    server apiserver2 <server_ip>:6443 check
    server apiserver3 <server_ip>:6443 check


### Init 

$ sudo kubeadm init --control-plane-endpoint "<load_banacer_ip>:6443" --upload-certs
$ sudo kubeadm init --control-plane-endpoint "10.1.52.139:6443" --upload-certs

### flannel network

$ sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --control-plane-endpoint "10.1.52.148:6443" --upload-certs

### calico (Use this one)

$ sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --control-plane-endpoint "10.1.52.143:6443" --upload-certs

$ sudo kubeadm init --pod-network-cidr=172.16.0.0/16 --control-plane-endpoint "10.1.52.143:8001" --upload-certs

$ kubectl apply -f https://docs.projectcalico.org/v3.10/manifests/calico.yaml

#### After initialization

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of the control-plane node running the following command on each as root:

  kubeadm join 10.1.52.139:6443 --token m8v0y0.vgvnzyukqcmdntpl \
    --discovery-token-ca-cert-hash sha256:e53ad229fe45013468caa3450c2dd0f97fcd5dfb269809ae41f0d4bfd84f6616 \
    --control-plane --certificate-key 6513ba167e3697b3ee394b6dfdc4617da5668b326121f10adbcb3908ccf3f500

Please note that the certificate-key gives access to cluster sensitive data, keep it secret!
As a safeguard, uploaded-certs will be deleted in two hours; If necessary, you can use
"kubeadm init phase upload-certs --upload-certs" to reload certs afterward.

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 10.1.52.139:6443 --token 6995vq.8kljc1d5h2idjddn \
    --discovery-token-ca-cert-hash sha256:e53ad229fe45013468caa3450c2dd0f97fcd5dfb269809ae41f0d4bfd84f6616



sudo kubeadm join 10.1.52.139:6443 --token 97ianr.pp6sojlpgje3y4y4 \
    --discovery-token-ca-cert-hash sha256:e53ad229fe45013468caa3450c2dd0f97fcd5dfb269809ae41f0d4bfd84f6616

### List and Create token (24hrs TTL)

$ kubeadm list token
$ kubeadm create token
$ kubeadm token create --print-join-command

### Add a Network Addon

- flannel
https://www.weave.works/docs/net/latest/kubernetes/kube-addon/

### Tear Down a Cluster

$ kubectl drain <node name> --delete-local-data --force --ignore-daemonsets
$ kubectl drain usav1svkubt7.ambrygenetics.local --delete-local-data --force --ignore-daemonsets
$ kubectl delete node <node name>

$ kubeadm reset 

### Schedulable 

$ kubeadm manage-nodes <node> --schedulable 
$ kubectl uncordon <node>

### Uninstall 

$ sudo yum install -y kubelet kubeadm kubectl
$ sudo yum remove -y kubelet kubeadm kubectl
$ sudo yum install -y kubelet-1.16.3 kubeadm-1.16.3 kubectl-1.16.3

$ kubeadm join pre-flight 10.10.9.87:6443 --token zrlao5.04km7esh7vb289dh \
    --discovery-token-ca-cert-hash sha256:5e4b1a9d53585bfe8a24088fb17690546f01f6a2c173b6de5aabb3f7870a66dc