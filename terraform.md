### Add Terraform to $PATH

### Initialize Terraform

$ terraform init

### Start and Destroy and instance

$ terraform apply --> execute

$ terraform destroy

### Plan

$ terraform plan --> test/list what is going to be applid
$ terraform plan -out changes.terraform
$ terraform apply changes.terafform --> apply those changes only

$ terraform plan -out <file> ; terraform apply <file> ; rm <file>

### Variables

- vars.tf

### Output

- attributes

### Terraform  State

- terraform.tfstate
- terraform.tfstate.backup

### Commands

terraform init
terraform apply
destroy
fmt
get
graph
import [options] ADDRESS ID
output [options] [NAME]
plan
push
refresh
remote
show
state
taint
validate
untaint