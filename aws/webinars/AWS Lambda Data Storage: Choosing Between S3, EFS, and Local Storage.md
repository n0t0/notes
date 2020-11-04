### When your Lambda function is invoked

### Stores its code in

- Memory (128-3008MB)
- /tmp space (512MB)
- Deployment package (<250MB)

### S3 - Object Storage

- AWS SAM

### When to Use S3 for Lambda Data Storage

- High durability
- Binary data - e.g. media
- Object tagging and metadata
- AWS Glue
- Amazon QuickSight

### Local Storage Options

1. /tmp

- always available
- access /tmp as any other file system
- not shared across function envs
- contents not wiped between warm invocations
- 512MB limit

2. Lambda Layer

- up to 5 layers per function
- part of 50MB/250MB overall
- available in /opt during invocation
- immutable veresion
- by default layers are private but sharable with other accounts/public
- improves developer experience and deployment speed

### EFS Throughout Modes

1. Bursting

- throughput scales with storage
- burst to 100MiB/s per TiB
- uses a credit system
- recommended for most workloads

2. Provisioning

- you choose the throughput
- for workloads with high throughout-to-storage ratios
- additional cost for this mode

### EFS Mounting to Lambda

- supports up to 25,000 connections