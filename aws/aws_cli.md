### IAM

$ aws iam list-users

### KeyPair

aws ec2 create-key-pair --key-name aws-devops --query 'KeyMaterial' --output text > ~/.ssh/aws-devops.pem

aws ec2 describe-key-pairs --key-name <keyname>

### Security Groups

aws ec2 create-security-group --group-name <iivanov_SG_us-west-2> --description <description>

aws ec2 authorize-security-group-ingress --group-id sg-0c93d4f4835fd8cc3 --protocol tcp --port 80 --cidr 64.58.145.95/32

aws ec2 authorize-security-group-ingress --group-id sg-0c93d4f4835fd8cc3 --protocol tcp --port 5432 --cidr 0.0.0.0/0 --source-group sg-0c93d4f4835fd8cc3

aws ec2 authorize-security-group-ingress --group-id <groupID> --protocol tcp --port 6379 --cidr 0.0.0.0/0 --source-group <groupID>

### ECS - Create a ECS Cluster

aws ecs create-cluster --cluster-name itdev-qa --region --default-launch-type EC2 --config-name itdev-qa-conf

aws ecs list-clusters

aws ecs describe-clusters --clusters itdev-qa

aws ecs describe-container-instances --cluster itdev-test --container-instances arn:aws:ecs:us-west-2:696327054069:container-instance/af6dced1-f54e-4540-88b1-6409ab5f8c20


### ECS - Task

aws ecs register-task-definition --cli-input-json file://web-task-definition.json
aws ecs list-task-definitions
aws ecs describe-task-definition --task-definition web:1
aws ecs derigister-task-definition --task-definition web:1
aws ecs register-task-definition --generate-cli-skeleton

aws ecs run-task --cluster itdev-test --task-definition web --count 1 


### ECS - Service

aws ecs create-service --cluster itdev-test --service-name web --task-definition web --desired-count 1

aws ecs list-services --cluster itdev-test

aws ecs create-service --cluster itdev-test --service-name web --task-definition web --desired-count 0
aws ecs delete-service --cluster itdev-test --service web

aws ecs create-service --generate-cli-skelenot


aws ecs delete-cluster --cluster <cluster_name>

### ECR 

aws ecr get-login 
aws ecr create-repository --repository-name itdev/nginx
aws ecr describe-repositories
aws ecr list-images --repository-name itdev/nginx
- tag an image with 
docker tag nginx:1.9 696327054069.dkr.ecr.us-west-2.amazonaws.com/itdev/nginx:1.9

### S3

aws s3api create-bucket --bucket ecs-itdev-test --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2

aws s3 rm s3://itdev-test --recursive
aws s3api delete-bucket --bucket itdev-test

### EC2

-- list

aws ec2 describe-images --owners amazon --filters 'Name=name,Values=amzn2-ami-hvm-2.0.????????-x86_64-gp2' 'Name=state,Values=available' --output json | jq -r '.Images | sort_by(.CreationDate) | last(.[]).ImageId'

-- init

aws ec2 run-instances --image-id ami-082b5a644766e0e6f --count 1 --instance-type t2.micro --iam-instance-profile Name=ecsInstanceRole --key aws-devops --security-group-ids sg-0c93d4f4835fd8cc3 --user-data file://copy-ecs-config-to-s3

aws ec2 run-instances --image-id ami-082b5a644766e0e6f --count 1 --instance-type t2.micro --iam-instance-profile Name=ecs_instanceRole --key aws-devops --security-group-ids sg-0c93d4f4835fd8cc3 --user-data file://copy-ecs-config-to-s3

-- status 

aws ec2  describe-instance-status --instance-id i-047e588f9c3d7fc37

### RDS

aws rds create-db-instance  --engine postgres --no-multi-az --no-publicly-accessible --vpc-security-group-ids sg-0c93d4f4835fd8cc3 --db-instance-class t2.micro --allocated-storage 20 --db-instance-identifier dockerzon-production --db-name dockerzon_production --master-username dockerzon --master-user-password victorvector

-- Update Password

aws rds modify-db-instance --db-instance-identifier dockerzon-production --master-user-password

-- Delete RDS

aws rds delete-db-instance --db-instance-dentifier <identiefier> --skip-final-snapshot 

### ElastiCache

aws elasticache create-cache-cluster --engine redis --security-group-ids sg-0c93d4f4835fd8cc3 --cache-node-type cache.t2.micro --num-cache-node 1 --cache-cluster-id dockerzon-production

aws elasticache describe-cache-clusters

aws elasticache describe-cache-clusters --show-cache-node-info 

### ELB 

aws elb create-load-balancer --load-balancer-name dockerzon-web --listeners "Protocol=HTTP, LoadBalancerPort=80,InstanceProtocol=HTTP,InstancePort=80" --subnets subnet-8c192ff5 subnet-1192934b subnet-ac1043e7 subnet-ac1043e7 --security-groups sg-0c93d4f4835fd8cc3

aws elb modify-load-balancer-attributes --load-balancer-name dockerzon-web --load-balancer-attributes "{\"ConnectionSettings\":{\"IdleTimeout\":5}}"

aws elb configure-health-check --load-balancer-name dockerzon-web --health-check "Target=HTTP:80/health_check,Timeout=5,Interval=30,UnhealthyThreshold=2,HealthyThreshold=10