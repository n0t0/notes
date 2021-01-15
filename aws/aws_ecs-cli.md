### Build and Deploy Containerized Apps with AWS ECS CLI

### Plan

- well architected
- production-ready
- multi-service
- multi-environement
- continuously delivered

### ecs-kudos

### Resources

#### Environment

1. VPC
-   2 public subnets
-   2 private busnets
-   2 route trables
-   1 internetagateway
2. ECS cluster
3. ECS services (2)
4. IAM roles (4)
5. ECR repository (2)
6. application load balancer
7. target groups (4)
8. ALB route rules (4)
9. security groups (2)
10. task definitions (4)
11. log groups (2)

#### + CD

12. AWS CodePipelihne
13. AWS CodeBuild project
14. S3 buckets
15. CMK KMS keys
16. x-account policies
17. x-region policies

### Releasing

1. Source
    - "master" branch
2. Build
    - AWS CodeBuild: Build and Push app image
3. Test
    - ECS: Deploy image to test env
4. Production
    - ECS: Deploy image to prod env

### ecs-preview

$ ecs-preview
