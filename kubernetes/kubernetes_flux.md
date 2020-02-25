### Install on CentOS

$ sudo yum install epel-release
$ sudo yum install snapd
$ sudo systemctl enable --now snapd.socket
$ sudo ln -s /var/lib/snapd/snap /snap

$ sudo snap install fluxctl

### Flux Installation
```
$ kubectl create ns flux
export USER=iivanov

$ fluxctl install \
--git-user=${USER} \
--git-email=${USER}@propeller.ibaset.com \
#--git-url=git@ibaset.com:${USER}/flux-demo \
--git-url=git.ibaset.com:${USER}/flux-demo \
--git-path=namespace,workloads \
--namespace=flux | kubectl apply -f -
```

### Check Status
```
kubectl -n flux rollout status deployment/flux
```

### SSH Setup
```
fluxctl identity --k8s-fwd-ns flux
```

### Sync repo Manually
```
fluxctl sync --k8s-fwd-ns flux
```
