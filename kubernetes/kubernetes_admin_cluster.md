## Gen
### Cluster Config

$ kubectl config view
$ kubectl cluster-info

### Pod

- a Pod describes an application running on Kubernetes
- a Pod can contain one or more tigthly coupled containers, that make up an app

### Pod State / Pod Status

$ kubectl get pods

- Running
- Pending
- Succeeded
- Failed
- Unknown

### Pod Condition

$ kubectl describe <pod>

- PodScheduled
- Ready
- Initiliazed
- Unschedulable
- ContainersReady

### Container Statuses

$ kubectl get pod <pod> -o yaml

- Running
- Terminating
- Waiting

### Pod Lifecycle

- initContainers:
- licecycle: postStart: :l/r-probes: :preStop

$ watch n1 kubectl get pods

### Multi-container PODs

- sidecar
- adapter
- ambassador

### Deployments

- Replica Set is next-gen ReplicationController
- Deployment declaration in Kube allows you to do app deployments and updates
- When using Deployment, you define the state of your app (kube will match desired state)

- Create a Deployment
- Update a Deployment
- Do rolling update (zero downtime)
- Roll Back to a prev version
- Pause/Resume a deployment (roll-out to only a certain percentage)

### Volumes/Storage

- volumes within pod-definition
- persistent volumes (PVs)

- stateless
- statefull

- NFS
- Cephfs
- auto provisioned volumes

### Services

- when using Deployments, when updaing the image version, pods are terminated and new pods take the place of older pods 
- that's why Pods hould never be accesssed directly, but always throught a Service
- a Service is a logical bridge between the `mortal` pods and other services or end-users

### Service Type

- ClusterIP (default) --> reachable inside the cluster only
- NodePort --> outside the cluster, through IPs on the nodes themselves
- LoadBalancer (cloud)
- ExternalName --> adds CNAME DNS record to CoreDNS only

- Ingress

### Service Discovery (advanced) with DNS

- /etc/kubernetes/addons - on master node
- to make DNS work, a pod will need a Service definition

$ nslookup www.google.com
$ dig
$ host app1-service.default.svc.cluster.local

### Ingress

- inbound connection to the cluster
- IngressController

### Kube DNS

<hostname>.<namespace>.svc.cluster.local
web-service.apps.svc.cluster.local

10.107.37.188 --> IP
cluster.local --> Root
svc --> Type
apps --> Namespace
web-service --> Hostname

### External DNS

- for every hostname in ingress; it will create a new record to send traffic to your loadbalancer
- On Cloud, use 1 LoadBalancer that captures all the external traffic and
- sends it to a ingress controller

### CNI in Kubernetes

- CNI (Calico, Weave)
- an overlay network (flannel)
- rkt
- mesos
- kubernetes - creates container under --> docker run --network=none

### Network Policy

- allow traffic only from specific pod
- flannel does not support network policies

### Linux Networking

$ ip addr add 192.168.1.11/24 dev eth0
$ ip route add 192.168.2.0/24 via 192.168.1.1
$ ip route add default via 192.168.2.1

$ cat /proc/sys/net/ipv4/ip_forward=1

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

### TLS on AWS ELB

- TLS termination
- annotations

### TLS Certs

- openssl

$ kubectl get csr
$ kubectl certificate approve jane

### Interpod Affinity and Anti-Affinity

- good for co-located pods
- e.g. redis pods running on the same node as app1 pod

- topology domain
- topologyKey

- (take some computing power in +100 nodes cluster)

### Healthchecks

- run a command in a container periodically
- livenessProbes
- periodic checks on a URL (HTTP)

$ kubectl create namespace <myspace>

- set a default namespace to launch resources in:
$ export CONTEXT=$(kubectl config view|awk '/current-context/{print $2}')
$ kubectl config set-context $CONTEXT --namespace=<myspace>

### liveness/readiness/startupProbes

- livenessProbes indicate whether the container is running --> if the check fails, the container will be restarted
- readinessProbes indicate whether the container is ready to serve requests --> if the check fails, the container will not be restarted, but the Pod's IP address will be removed from the Service, so it'll not serve any requests anymore

### Custom Resource Definitions

- extention of the Kubernetes API
- extend the functionality of the Kube cluster

### Resource Quotas

- devide cluster in namespaces

- requests capacity --> minimum amount of resources the pod needs
- resource limit -> limit
- use default quotas**

- requests.cpu
- requests.mem
- requests.storage
- limits.cpu
- limits.memory

$ kubectl describe quota/computer-quota --namespace=<myspace>
$ kubectl describe limits <mylimits> --namespace=<myspace>

### Namespaces

- create virtual cluster within same physical servers
- logically separates cluster
- resource name must be unique wihin single namespace
- can limit resources on a per namespace basis (e.g. marketing team can only
use a maximum of 1GiB of memory)

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

### Add a Users

- on master node:
$ openssl genrsa -out iivanov.pem 2048
$ openssl req -new -key iivanov.pem -out iivano-csr.pem -subj "/CN=iivanov/0=myteam/"
$ sudo openssl x509 -req -in iivanov-csr.pem -CA /var/lib/localkube/certs/ca.crt -CAkey /var/lib/localkube/certs/ca.key -CAcreateserial -out iivanov.crt -days 10000
$ cat iivanov.crt
$ cat iivnaov.pem
- add *.crt and *.pem to ~/.kube/config
- create *.crt and *.pem in ~/.kube/iivanov.key|.crt

### Authentication

- local users,pass,userID

### API Groups

- /version
- /api (got verbs)

- kube proxy is not kubectl proxy

### Roles

$ kubectl api-resources --namespaced=true/false

### RBAC

- Role (single namespace) and ClusterRole (cluster-wide)
- RoleBinding (single namespace) and ClusterRoleBindig (cluster-wide)

$ kubectl get roles

$ kubectl get rolebinding

$ kubectl auth can-i create deployment
$ kubectl auth can-i delete nodes
$ kubectl auth can-i create deploymentse --as dev-user

- webhook --> sends autorhozation request to an exnternal REST interface

- role
- roleBinding
- clusterRole
- clusterRoleBinding

$ kubectl config view
$ kubectl config set-context --cluster=*.* --user edward
$ kubectl config use-context edward
$ kubectl config get contexts

### Admission Controllers

- intercept requests setn to kubernetes API server

$ kube-apiserver --enable-admission-plugins=NamespaceLifecycle,...

- NamespaceLifecycle
- LimitRanger
- ServiceAccount
- DefaultStorageClass
- DefaultTolerationSeconds
- NodeRestriction
- **MutatingAdmissionWebhook
- **ValidatingAdmissionWebhook
- ResourceQuota
- PodSecurityPolicy

### Getting a Token

$ kubectl -n kubernetes-dashboard get secret
$ kubectl -n kubernetes-dashboard describe secrets kubernetes-dashboard-token-x9nd8

## Cluster Maintenance
### Nodes

$ kubectl get nodes -o wide
$ kubectl get pods -o json
$ kubectl get pods -o=jsonpath='{   .items[0].spec.containers[0].image }'
$ kubectl get nodes -o=jsonpath='{.items[*].metadatada.name}'

### Volume Maintenance

$ kubectl get pv | tail -n+2 | awk '{print $1}' | xargs -I{} kubectl patch pv {} -p '{"metadata":{"finalizers": null}}'
$ kubectl patch pv mongodb-data-pv03 --patch "$(cat mongodb-patch.yaml)"

### Node Maintenance

- Node Controller --> assigns IP space, node list, health of the node

$ kubectl drain <node> --grace-period=600

### Taints - Node

$ kubectl taint nodes node-name key=value:<taint-effect>
$ kubectl taint nodes Node1 key=blue:NoSchedule
$ kubectl taint nodes master node-role.kubernetes.io/master:NoSchedule- --> remove taints

$ kubectl get nodes
$ kubectl get <masterNode> -o yaml --> /taint

### Troubleshooting

$ kube-controller-manager --pod-eviction-timeout=5m0s

$ kubectl drain node-1
$ kubectl cordon node-2
$ kubectl uncordon node-1

### Kubernetes Releases

- v1.17 -- ~
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

### etcd

- used by kubernetes as data backend
- k/v store

### Raft consensus algorithm

https://raft.github.io

### Backup and Restore

- resource
* VELERE 3rd party

https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster

https://www.youtube.com/watch?v=qRPNuT080Hk

## Security
### Secure Hosts

- root disabled
- password based authentication disalbed
- ssh key based auth

### Security Context

- runAsUser 1000

### Security Images

$ kubectl create secret docker-registry regcred \
    --docker-server=
    --docker-username=
    --docker-password=
    --docker-email=

### Pod Security Policies

- deny using privileged mode in pods
- control what volumes can be mounted
- containers can't run as root but within <UID/GID> range

$ kubectl edit cluster
$ kubectl get podsecuritypolicy

## Advanced
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

### Mocl

$ kubectl run --generator=run-pod/v1 elephant --image=redis --dry-run -o yaml > elephant

$ kubectl run nginx-deploy --image=nginx:1.16 --replicas=1 --record
$ kubectl get deployments .
$ kubectl rollout history deployment nginx-deploy
$ kubectl set image deployment/nginx-deploy nginx-deploy=nginx:1.17 --record
$ kubectl rollout restart deployment/<deployment>


$ kubectl api-version | grep certif
$ kubectl create role developer --resource-pods --verbs-create,list,get,update,create --namespace=development
$ kubectl describe role developer -n developmnet

$ kubectl create reolebinding developer-role-binding --role=developer --user=john --namespace=developer

$ kubectl expose pod nginx-resolver --name=nginx-resolver-service --port=80 --target-port=80 --type=ClusterIP

$ kubectl get svc

### Kubetest - Tests

- e2e: ~1000
- Full e2e = ~1000 Test / 12 Hours

- conformance: ~160
- Conformance = ~164 Test / 1.5 Hours
- sonobuoy

### Packaging and Deploying
### Helm

- package manager for kubernetes
- a chart is a collection of files that describe a set of kubernetes resources
- charts use templates that are typicaly developed by a package maintainer

```
$ helm init
$ helm reset
$ helm install
$ heml search --> search for a chart
$ helm list
$ helm upgrade
$ helm rollback
```

- helm allows for upgrades and rollbacks
- helm charts are version controlled

### Create Helm Charts

```
$ helm create <mychart> --> creates a directory /mychart
```

- Chart.yaml
- values.yaml
- templates/ --> deployment.yaml, service,yaml

:split _helpers.tpl


### Helm Chart repository using AWS S3

- create a .sh script

### Building and Deploying a Helm Chart with Jenkins

- aws roles to read from s3 and deploy to cluster
- serviceAcccount
- build pipeline script
- deploy pipeline sciprt

### Skaffold

- command line tool for continuous development of applications running on kubernetes
- skaffold will build, push, and deploying to kubernetes cluster
- very pluggable - builds with Kaniko and Bazel or custom builds
- for developeres and me

### Serverless in Kubernetes

- OpenFaas
- Kubeless**
    - HTML functions
    - Scheduled
    - PubSub (kafka)
    - AWS Kinesis
- Fission
- OpenWhisk