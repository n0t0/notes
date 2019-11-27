### Create a Certificate

aws acm request-certificate --domain-name <domainname.com>

### Load Balancer 

aws elb create-load-balancer-listeners --load-balancer-name <ELB-name> --listeners "Protocol=HTTPS,LoadBalancerPort=443,InstasnceProtocol=HTTP,InstanceProtocol=80,SSLCertificateId=<ARN>"

