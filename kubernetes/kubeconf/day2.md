https://nirmata.com/?_ga=2.43852453.1226136675.1605725032-1405637306.1605725032

### Hands-On Stateful Serverless Applications with K8s and Stateful Functions

Serverless

Stateful Serverless

### Safely Deploying a 100K line Envoy YAML Configuration to Production

https://www.gitpod.io/

### Service Mesh Specifications and Why They Matter in Your Deployment

https://meshery.io/
https://layer5.io/landscape
https://thenewstack.io/history-service-mesh/
https://www.nomadproject.io/
https://play.tetrate.io/
https://www.beautiful.ai/
https://epsagon.com/



{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPushPull",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::974397503065:root"
            },
            "Action": [
                "ecr:GetDownloadUrlForLayer",
                "ecr:BatchGetImage",
                "ecr:BatchCheckLayerAvailability",
                "ecr:PutImage",
                "ecr:InitiateLayerUpload",
                "ecr:UploadLayerPart",
                "ecr:CompleteLayerUpload"
            ]
        }
    ]
}