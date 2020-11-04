### Store Parameter

aws ssm get-parameters --names /evo-suite/dev/my-app/db-url /evo-suite/dev/my-app/db-pass --with-decryption
aws ssm get-parameters-by-path --path /evo-suite/dev/my-app/
aws ssm get-parameters-by-path --path /evo-suite/ --recursive

### S3 Pre-Signed URLs

$ aws s3 presign help
$ aws configure set default.s3.signature_version s3v4 --> compatible with KMS
$ aws s3 presign s3://<s3-bucket/path>/<file> --expires-in 300 --region us-west-2

### Amazon API Gateway

- enable API caching in Amazon API Gateway to cache your endpoint's response
- caching reduses the number of calls made to your endpoints and also improve the latency of the requests to your API
- API Gateway caches response from your endpoints for a specified time-to-live (TTL) period, in seconds
- throttle API Gateway to prevent attacks
- log results to CloudWatch
- if using multiple domains with API Gateway, ensure CORS on API Gateway is enabled
- CORS is enforced by the client

- Same Origin Policy
- Cross-Site Scripting (XSS)
- CORS (Cross origin resource sharing)
- Origin policy cannot be read at the remote resource --> enable CORS on API Gateway

- REST APIs (REpresentational State Transfer) --> JSON
- SOAP APIs (Simple Object Access Protocol) --> XML