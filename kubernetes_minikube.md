#######################
#######################
### Minikube

### Install kubectl

1. curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
2. chmod +x ./kubectl
3. sudo mv ./kubectl /usr/local/bin/kubectl

### Install a Hypervisor

---

### Install Minikube

1. curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
2. sudo install minikube /usr/local/bin

### Ports

30000 - 32767

### Events

$ kubectl get events

### Logs

$ kubectl logs my-custom-scheduler --name-space=kube-system
$ kubectl logs -f event-simulator-pod


### Set proxy if behind one

https_proxy=<my proxy> minikube start --docker-env http_proxy=<my proxy> --docker-env https_proxy=<my proxy> --docker-env no_proxy=192.168.99.0/24

### Start kube with non default driver

minikube start --vm-drive=<driver_name>

### Start Minikube

$ sudo minikube start --vm-driver=none

### Configure `none` driver as default 

$ sudo minikube config set vm-driver none

### Use docker native commands in kubernetes

eval $(minikube docker-env)

### kubectl

$ kubectl run hell-minikube
$ kubectl cluster-info 
$ kubectl get nodes
$ kubectl describe node <node> | grep -i taint

### Monitoring

$ kubectl top node 
$ kubectl top pod

### Access a deployment by exposing the service

kubectl expose deployment hello-minikube --type=NodePort

### Get the URL of the exposed service

$ curl $(minikube service hello-minikube --url)
$ minikube service hello-minikube --url

### Delete the deployment 

$ kubectl delete deployment hello-minikube

### Stop the local Minikube cluster

$ minikube stop

### Delete the local Minukube cluster

$ minikube delete

kubeadm join 172.31.68.187:6443 --token zbcrvz.m32clg7b3hs1tiub \
    --discovery-token-ca-cert-hash sha256:6b9d6870e24f69794d9d969e9b1f72849712b431deeda4b2e4195a1f4188cd17

