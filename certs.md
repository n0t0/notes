### Generate a Cert Signing Request
### This would create a CSR for the username “<user>”, belonging to two groups, “app1” and “app2”.

https://kubernetes.io/docs/concepts/cluster-administration/certificates/

$ openssl req -new -key <user>.pem -out <user>-csr.pem -subj "/CN=<user>/O=app1/O=app2"

