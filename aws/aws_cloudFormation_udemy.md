### Template Options

- tags
- permissions
- notification optios
- timeouts
- rollback on failure
- stack policy

### CF Building Block
#### Templates Components

- resources --> AWS resouces defined in the template
- parameters --> dynamic input for the template 
- mappings --> static variables for a template
- outputs --> reference to what have been created 
- conditionals --> list of conditions to perform resource creation 
- metadata 

#### Templates Helpers 

- references 
- functions 

### Deploying 
#### Manual 

- CF designer
- console input 

#### Automated 

- editing templates 
- AWS CLI

### Parameters 

- used to provide inputs to AWS CF template 
- reusable in templates 
- parameters are controlled, can prevent typos
- don't have to reupload template to change its content 

#### Parameters can be controles by 

- Type
    String
    Number
    CommaDelimitedList
    List<Type>
    AWS parameter 
- Description
- Constraints
- ConstraintDescription(String)
- Min/MaxLenght 
- Defaults
- AllowedValues (array)
- AllowedPattern (regexp)
- NoEcho (boolen)


### Reference a Parameter

- Fn::Ref 
- !Ref --> shorthand 

### Optional Attributes for Resources 

- DependsOn --> draw a dependency between two resources e.g. (only created 
ECS cluster after creating an ASG [auto scaling group])
- DeletionPolicy --> protect resources from being deleted even if the CF 
is deleted (RDS database)
- CreationPolicy
- Metadata 

### Mappings

- fixed variables within CF template 
- very handy to differentiate between different envs (dev vs. prod), regions, AMI types, etc
- all values are hardcoded within the templated 

### Fn::FindInMap (Accessing Mapping Values)

- !FindInMap [ mapName, TopLevelKey, SecondLevelKey ]

### Pseudo Parameters 

- AWS::AcountId, AWS::NotificationARNs, AWS:NoValue, AWS::Region, AWS::StackId, AWS::StackName

### Outputs

- optional outputs values
- useful when defininig network 
- cross stack collaboration 

### Cross Stack Reference Hands-On

- Fn::ImportValue

### Conditions

- environments 
- AWS Regions 
- any parameter value
- each condition can reference another condition, parameter value or mapping

 ### Fn::GetAtt

- logicalName.attributeName 

### metadata 

- AWS::CloudFormation::Designer 
- AWS::CloudFormation::Interface --> define grouping and ordering of input parameters when they are displayed in the AWS Console 
- AWS::CloudFormation::Init --> define configuration tasks for cfn-init

### CFN-Init and EC2-user data

- EC2 instances 
- AutoScaling Groups 

### Fn::Base64

### CloudFormation helper scripts

- cfn-init --> retrieve and interpret the resource metadata, installing packages, creating files and starting services
- cfn-signal --> simple wrapper to signal an AWS CloudFormation CreationPolicy or WaitCondition, enabling you to sunc other resources in the stack with the application being ready 
- cfn-get-metadata --> wrapper script making it easy to retrieve either all metadata defined for a resource or path to a specific key or subtree of the resource metadata
- cfn-hup --> a daemon to check for updates to metadata and execute custom hooks when the changes are detected 

### AWS::CloudFormation:Init

- config 
* packages 
* groups
* users
* sources
* files
* commands 
* services 
- can have multiple configs (configsets)

### Packages 

- apt, msi, python, rpm, rubygems, and yum 
- rpm, yum/apt, rubygems and python --> packages processing order 
- version or empty array for latest

### Groups and Users

- groups: {}
- groups: id '45'

### Sources

- donwload whole compressed archives from the web and unpack them on the instance directly 
- handy for set of standardized scripts for EC2 instances on S3
- or download a whole github project 

### Files 

- full control on any content 
- come fro URL or inline
- !Sub 

### Fn::Sub or !Sub

- String
- ${VariableName}

### Commands 

- run in alphabetical order 
- set a directory from which that command is run, env variables
- provide test to control wheter the command is executed or not 

### Services 

- httpd
- sendmail 

### CFN-Init and Signal 

- first cfn-init to launch the configuration 
- use cfn-signal to let CloudFormation know that the resource creation has been successful 
- used in conjunction of a CreationPolicy 

### cfn-hup 

- used to tell EC2 instance to look for M etadata changes every 15 minutes and apply the metadata configuration again 

### Logs

- /var/log/cloud-init-output.log --> ec2-user
- /var/log/cfn-init.log --> cfn-init

### Deletion Policy

- delete --> delete resource and its content
- retain --> delete the stack
- snapshot --> for resources that support snapshot (AWS:EC2::Volume, 
AWS::ElastiCache::CacheCluster, AWS::RDS::DBInstance...,etc.)

### Custom Resouces with AWS Lambda 

- include resources that aren't available as AWS CloudFormation 
- custom resource can be provision using and AWS lambda function 

### Best Practices

- layered architecture (horizontal layers) --> network, instance, application 
- service oriented architecture (vertical layers) --> for one service
- cross stacks references fro example to reference a VPC or Subnet 
- environment agnostic for dev/test/prod and across regions/accounts 
- use NoEcho or KMS

- specifif parameters types & constraints 
- CFN init (& latest version of helpers)
- validate templates 
- don't do manual 
- use delete policies 

### Cost Estimation 

- *