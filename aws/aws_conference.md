https://github.com/aws/containers-roadmap/projects/1

### ECS

Copilot - V2 Command Line Interface for ECS
Capacity Providers
AWS CloudFormation blue/green deployments for ECS
New ECS console
EBS support
Service Meshes AWS App Mesh

### Fargate

EFS support
Ephemeral storage up to 20GB
Volume encryption for ECS and EKS
Native logging for EKS/Fargate (Firelens)

### ECR

ECR PrivateLink in China regions and GovCloud (US-EAST)
Support OCI artifcat storage and retrieval (e.g. Helm charts) in ECR
Cross-region and cross-account replication

### AWS App Mesh

Cross-account mesh support
Ingress support with Virtual Gateway
mTLS support
SPIFFE/SPIRE support for mTLS
OPA support
Integration with AWS Lambda

### Cloud Map

### EKS

50% Price Reduction
GovCloud (US)
Envelope encryption for secrets with AWS KMS
CDK for Kubernetes - cdk8S
EC2 Inf1 Instances
EFS CSI Driver GA
K8S service Cluster IP Range
Security Groups for pods
EKS/Fargate region expansion

### Amazon Red Hat Openshift H2 2020

### Docker CLI and Amazon ECS/Fargate Integration

---

### CDK

cdk8s - bridges declarative YAML with familiar programming languages

### YAML
1. Cannot express logic (loops)
2. Loose coupled

---

### Fargate

Task and Pod isolation (1 task/pod: 1VM)
No EC2 instance to manage, patch, scale, deploy, etc

### 1.4 Platform

1. EFS integration
2. 20GB ephemeral volume
3. New task ENI flows
4. CAP_SYS_PTRACE Linux capability
5. containerd

---

### Persistent Storage for Containers

1. Stateful application
2. Share date with other containers or other microservices
3. Machine Learning
4. Data Science Tools