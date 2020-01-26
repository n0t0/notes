### Cluster Maintenance
### Troubleshooting

$ kube-controller-manager --pod-eviction-timeout=5m0s

$ kubectl drain node-1
$ kubectl cordon node-2
$ kubectl uncordon node-1

### Kubernetes Releases 

- v1.16 -- current
- v1.15 -- supported
- v1.14 -- supported
- v1.13 -- un-supported

### Cluster Upgrade Process

- upgrade one minor version at a time
- v1.13 to v1.14 -- correct
- v1.13 to 1.16  -- not-recommended

$ kubectl upgrade plan
$ kubectl upgrade apply

- when upgrading, master is upgrading first and apiserver, scheduler, and controller are temporary down
- nodes - all at the same time - strategy 1
- nodes - one at the time - strategy 2
- nodes - add new versioned nodes - strategy 3

- steps to update to v1.13

1. $ apt-get upgrade -y kubeadm=1.12.0-00
2. $ kubeadm upgrade apply v1.12.0
3. $ apt-get upgrade -y kubelet=1.12.0-00
4. $ systemctl restart kubelet
5. $ kubeadm upgrade node config --kubelet-version v1.12.0
6. $ systemctl restart kubelet

### Backup and Restore

- resource
* VELERE 3rd party

https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster

https://www.youtube.com/watch?v=qRPNuT080Hk

### Security

### Secure Hosts

- root disabled
- password based authentication disalbed 
- ssh key based auth

### Authentication

- local users,pass,userID

### TLS Certs  

- openssl 

$ kubectl get csr
$ kubectl certificate approve jane

### Kubeconfig

- contexts: 

$ kubectl config view

### API Groups

- /version
- /api (got verbs)

- kube proxy is not kubectl proxy

### RBAC

$ kubectl get roles

$ kubectl get rolebinding

$ kubectl auth can-i create deployment
$ kubectl auth can-i delete nodes
$ kubectl auth can-i create deploymentse --as dev-user

### Roles

$ kubectl api-resources --namespaced=true/false

### Security Images

$ kubectl create secret docker-registry regcred \
    --docker-server=
    --docker-username=
    --docker-password=
    --docker-email=

### Security Context

- runAsUser 1000

### Network Policy

- allow traffic only from specific pod

- flannel does not support network policies

### Network

### Linux Networking

$ ip addr add 192.168.1.11/24 dev eth0
$ ip route add 192.168.2.0/24 via 192.168.1.1
$ ip route add default via 192.168.2.1

$ cat /proc/sys/net/ipv4/ip_forward=1

### DNS

$ ls /etc/kubernetes/addons on master node

$ nslookup www.google.com
$ dig

### Network Namespaces

$ ip netns add <namespace>

$ ip netns --> list namespaces
$ ip netns exec <namespace> ip link
$ ip -n <namespace> link

$ arp
$ route

$ iplink add <veth-red> type veth peer name <veth-blue>
$ iplink set <veth-red> netns <red>
$ iplink set <veth-blue> netns <blue>

### Docker Networking

### Container Networking Interface (CNI)

- rkt 
- mesos
- kubernetes - creates container under --> docker run --network=none

### Cluster Nodes

### Pod Networking

### CNI in Kubernetes

### CNI weave

### IAM (IP address management)

### Service Networking

### Ingress

### Pod Presets

- inject kubernetes resources like secrets, configmaps, volumes, and envs
- when injecting env vars and volumemounts, the pod preset will apply
- the changes to all containers within the pod

### Kubectl Advanced

$ kubectl create deployment sample --image naginx --dry-run -o yaml
$ kubectl create job sample --image naginx --dry-run -o yaml

### StatefullSets

- runs stateful applications, that need stable pod hostname
- podnames will have sticky identity e.g. podname-0, podname-1, podname-2
- allows stateful apps stable storage
- allows statefull app to order the startup and teardown

### Nodes

$ kubectl get nodes -o wide
$ kubectl get pods -o json
$ kubectl get pods -o=jsonpath='{   .items[0].spec.containers[0].image }'
$ kubectl get nodes -o=jsonpath='{.items[*].metadatada.name}'

### Mocl

$ kubectl run --generator=run-pod/v1 elephant --image=redis --dry-run -o yaml > elephant

$ kubectl run nginx-deploy --image=nginx:1.16 --replicas=1 --record
$ kubectl get deployments .
$ kubectl rollout history deployment nginx-deploy
$ kubectl set image deployment/nginx-deploy nginx-deploy=nginx:1.17 --record


$ kubectl api-version | grep certif
$ kubectl create role developer --resource-pods --verbs-create,list,get,update,create --namespace=development
$ kubectl describe role developer -n developmnet

$ kubectl create reolebinding developer-role-binding --role=developer --user=john --namespace=developer

$ kubectl expose pod nginx-resolver --name=nginx-resolver-service --port=80 --target-port=80 --type=ClusterIP

$ kubectl get svc

### Custom Resource Definitions

- extention of the Kubernetes API
- extend the functionality of the Kube cluster

### Resource Quotas

- devide cluster in namespaces

- requests.cpu
- requests.mem
- requests.storage
- limits.cpu
- limits.memory

### User Management 

- 2 types

- normal user --> this user is not managed using object
- client certificates
- bearer tokens
- authentication proxy
- http basic authe
- open ID
- webhooks

- service user - manager by an object in kubernetes - used to authenticate within the cluster (cluster)
- using Service Account Tokens --> storewd in Secrets
- service users are specific to a namespace

### Kubetest - Tests

- e2e: ~1000
- Full e2e = ~1000 Test / 12 Hours

- conformance: ~160
- Conformance = ~164 Test / 1.5 Hours
- sonobuoy

