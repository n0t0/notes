### Store Parameter

aws ssm get-parameters --names /evo-suite/dev/my-app/db-url /evo-suite/dev/my-app/db-pass --with-decryption
aws ssm get-parameters-by-path --path /evo-suite/dev/my-app/
aws ssm get-parameters-by-path --path /evo-suite/ --recursive 

### S3 Pre-Signed URLs

$ aws s3 presign help
$ aws configure set default.s3.signature_version s3v4 --> compatible with KMS
$ aws s3 presign s3://<s3-bucket/path>/<file> --expires-in 300 --region us-west-2
