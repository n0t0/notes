https://eksworkshop.com/020_prerequisites/


Event: CON205-R Deploying applications using Amazon EKS
Team Name: (Team Name Not Set Yet)
Event ID: 680a64c5cdbd4c48ac3e37619a8ac95e

Team ID: adb499b10599439fbf1fade9cac9ea87

export AWS_DEFAULT_REGION=us-west-2
export AWS_ACCESS_KEY_ID=ASIATDOGVQSKSPWXPP54
export AWS_SECRET_ACCESS_KEY=kE27QxOLPB9i7wyzmFOaiEE1l3BSEpVGkHERiJmR
export AWS_SESSION_TOKEN=FwoGZXIvYXdzEOT//////////wEaDKW1z4B8uv6unY+N1SKuAev9V0OidSpZFxL/oRtNkoXX3+QV/UIbpH0kuH1dUe3UMxJrTkLjsyUL4e/Atn0MoFMPD3o/53Iix/4qHZd6ulV2S2e77xz1/ZebxVhHVDnROZZvjSoFwP5g6kIR+hBvtvcnnezMkJ4GhIwLZzj7hf7iSlgn23krwnk9DRJN5QJMJvEA19iSn3a4zfM1e0gwGLp8hXCpShjB5xBUTLgSST2H3WMyNgBcWVU6Xn2TASjCuJXvBTItn2Ck5iZUXLqe+KA7MKC6uChM2Pn0godJrR/79h3fbqDjTiFATL8GvCUMS5s4


kubectl proxy --port=8080 --address='0.0.0.0' --disable-filter=true &

## Install Kubernetes Tools on Cloud9

### Install kubectl

sudo curl --silent --location -o /usr/local/bin/kubectl https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/kubectl


sudo chmod +x /usr/local/bin/kubectl

### Install jq, envsubst (from GNU gettext utilities) and bash-completion

sudo yum -y install jq gettext bash-completion

### Verify the binaries are in the path and executable

for command in kubectl jq envsubst
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done

### Enable kubectl bash_completion

kubectl completion bash >>  ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion

## Create an IAM role for your cluster

### Create and attach role

- create AdministratorAccess role and attach it to cloud9 instance

### Update Cloud9 environment

- update AWS Settings

### Ensure temp creds are not there

rm -vf ${HOME}/.aws/credentials

export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION= # for aws hosted event, set this to the region specified by your instructor

### Check the region

test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set

### Save to a bash profile

echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region

### Validate the IAM role

aws sts get-caller-identity

## Clone Project Repos

cd ~/environment
git clone https://github.com/brentley/ecsdemo-frontend.git
git clone https://github.com/brentley/ecsdemo-nodejs.git
git clone https://github.com/brentley/ecsdemo-crystal.git

## Create SSH key

### Gen a key

ssh-keygen
- press 'enter' 3 times

### Upload public key to EC2 region

aws ec2 import-key-pair --key-name "eksworkshop" --public-key-material file://~/.ssh/id_rsa.pub

## Launch Using eksctl

### Pre-Req

curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/latest_release/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp


sudo mv -v /tmp/eksctl /usr/local/bin

### Confirm it works

eksctl version

### Enable bash completion

eksctl completion bash >> ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion


## Launch EKS Cluster

### Create a cluster

eksctl create cluster --name=<eks-dev> --nodes=3 --managed --alb-ingress-access --region=${AWS_REGION}

- (it will take 15 minutes)

### Test the cluster

kubectl get nodes

### Export the worker role name for use throughout

STACK_NAME=$(eksctl get nodegroup --cluster <eks-dev> -o json | jq -r '.[].StackName')
ROLE_NAME=$(aws cloudformation describe-stack-resources --stack-name $STACK_NAME | jq -r '.StackResources[] | select(.ResourceType=="AWS::IAM::Role") | .PhysicalResourceId')
echo "export ROLE_NAME=${ROLE_NAME}" | tee -a ~/.bash_profile

