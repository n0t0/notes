### Optimizing Lambda Performance for Your Serverless Applications

5. Compute Substrate - AWS managed
4. Lambda SErvice - AWS managed
3. Execution environment
2. Languange runtime
1. Your functiton

### Anatomy of Lambda Func

1. Handler () function
2. Event object
3. Context object

### Function Lifecycle - worker host

1. Download your code
2. Start code

### Measuring with AWS X-Ray

### Three Areas of Performance

1. Latency - overall user experience
2. Throughput - total number of transactions
3. Cost

### Cold Start

- service identified if warm execution is available

- you cannot target warm environment
- pinging functions to keep them warm is limited

- cold starts occur when enviornments is reaped, scaling up, updating code/config flushes. rebalancing across AZs

### Lambda + VPC - major performance improvement

### Cold Starts - Static Initialization

### Provisioned Concurrency on AWS Lambda

- pre-creates execution environments, running INIT code

- reduces the start time to <100ms
- can't configure for $LATEST

### Memory Usage and Profiling

1. more ram can be cheaper
2. aws-lambda-power-tuning

### Optimization Best Practices

1. Avoid monolithic funcitons
2. minify/uglify production code
3. optimize dependencies (and imports)

4. avoid idle/sleep - delegate to Step Functions
5. transform, not transport - minimize data transfer (S3 Select, advanced filtering, eventBridge input tranformer)
6. triger configuration (S3 prefix, SNS filter)
7. keep-alive

### Amazon RDS Proxy

### Comparing sync and async