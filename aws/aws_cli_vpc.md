### Create a VPC
aws ec2 create-vpc \
--cidr-block 10.0.0.0/16

### Grab the VPC ID and create two subnets inside this:
aws ec2 create-subnet \
--vpc-id <VPC_ID> \
--cidr-block 10.0.1.0/24 \
--availability-zone us-east-1a

aws ec2 create-subnet \
--vpc-id <VPC_ID> \
--cidr-block 10.0.0.0/24 \
--availability-zone us-east-1b

### Get the IDs of these two subnets and record them:
aws ec2 describe-subnets \
--filters "Name=vpc-id,Values=<VPC_ID>" \
--query "Subnets[*].{SubnetId:SubnetId,AvailabilityZone:AvailabilityZone}"

### Create an Internet Gateway:
### Make sure to record the InternetGatewayID
aws ec2 create-internet-gateway

### Attach the internet Gateway to the VPC:
aws ec2 attach-internet-gateway \
--vpc-id <VPC_ID> \
--internet-gateway-id <INTERNET_GATEWAY_ID>

### Create a custom route table:
### Make sure to note the RouteTableId
aws ec2 create-route-table \
--vpc-id <VPC_ID>

### Create a route in the table pointing all
### traffic to the internet gateway:
aws ec2 create-route \
--route-table-id <ROUTE_TABLE_ID> \
--destination-cidr-block 0.0.0.0/0 \
--gateway-id <INTERNET_GATEWAY_ID>

### Associate the route table with your Subnets:
### Once for each subnet
### Subnet 1A
aws ec2 associate-route-table \
--subnet-id <US_EAST_1A_SUBNET> \
--route-table-id <ROUTE_TABLE_ID>

### Subnet 1B:
aws ec2 associate-route-table \
--subnet-id <US_EAST_1B_SUBNET> \
--route-table-id <ROUTE_TABLE_ID>

### Make sure that instances in these subnets get public IPs
### Run the same command for each subnet
### For subnet 1A:
aws ec2 modify-subnet-attribute \
--subnet-id <US_EAST_1A_SUBNET> \
--map-public-ip-on-launch

### Then run the same command for Subnet 1B:
aws ec2 modify-subnet-attribute \
--subnet-id <US_EAST_1B_SUBNET> \
--map-public-ip-on-launch


### Create a security group for the VPC
### Make sure to copy down the GroupId!
aws ec2 create-security-group \
--description "ECS Security Group" \
--group-name "ecs-demo-sg" \
--vpc-id <VPC_ID>

### Add rules allowing inbound HTTPS traffic:
aws ec2 authorize-security-group-ingress \
--group-id <SECURITY_GROUP_ID> \
--protocol tcp \
--port 443 \
--cidr 0.0.0.0/0

### Add rule allowing inbound HTTP traffic:
aws ec2 authorize-security-group-ingress \
--group-id <SECURITY_GROUP_ID> \
--protocol tcp \
--port 80 \
--cidr 0.0.0.0/0

### Create the application load balancer:
aws elbv2 create-load-balancer \
--name bluegreen-alb \
--subnets <US_EAST_1A_SUBNET> <US_EAST_1B_SUBNET> \
--security-groups <SECURITY_GROUP_ID> \
--region us-east-1

### Make sure to copy down the resulting LoadBalancerArn
### for the ALB, it should look something like this:
arn:aws:elasticloadbalancing:region:aws_account_id:loadbalancer/app/bluegreen-alb/e5ba62739c16e642
