### Generate a Cert Signing Request
### This would create a CSR for the username “<user>”, belonging to two groups, “app1” and “app2”.

https://kubernetes.io/docs/concepts/cluster-administration/certificates/

$ openssl req -new -key <user>.pem -out <user>-csr.pem -subj "/CN=<user>/O=app1/O=app2"


### Create New User
```
sudo apt install openssl
openssl genrsa -out edward.pem 2048
openssl req -new -key edward.pem -out edward-csr.pem -subj "/CN=edward/O=myteam/"
openssl x509 -req -in edward-csr.pem -CA ca.crt -CAkey ca.key -CAcreateserial -out edward.crt -days 10000
```

### Add New Context
```
kubectl config set-credentials edward --client-certificate=edward.crt --client-key=edward.pem
kubectl config set-context edward --cluster=kubernetes.newtech.academy --user edward
```

### 

$ openssl genrsa -aes256 -out private.pem
$ openssl rsa -in private.pem -outfrom PEM -pubout -out putlic.pem


### Obtain Dashboard-user Token

$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user-token | awk '{print $1}')