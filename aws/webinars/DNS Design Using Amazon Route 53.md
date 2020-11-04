### DNS Design Using Amazon Route 53

### Public vs Private Hosted Zones

1. Public Hosted Zones
- dmain name registration
- health checks
- advanced requests routing

2. Private Hosted Zones
- VPC Route 53 Resolver
- health checks (non-public)
- hybrid integration using forwarding rules and endpoints

### DNS Options

1. DNS resolution
2. DNS hostnames
3. DHCP Option Sets

### Split Horizon DNS

- some requests are resolved publicly and some privetly

### VPC DNS - considerations

- private zones take precedence over public
- when multiple overlapping private hosted zones exists Resolver matches the more specific zone
- each EC2 instance can send 1024 requests per second to Route 53 Resolver
- private hosted zones do not support delegation

### VPC Endpoints

### EFS

### Elastic Map Reduce

- it is a best practice with Hadoop and related applications to ensure resolution of the fully qualified domain name (FQDN) for nodes

### Route 53 health checks and routing rules

- the health of a speific resource
- the health of other health check
- a CloudWatch alarm

### Request Routing for Private Hosted Zones

1. Simple Routing
2. Failover Routing
3. Weighed Answer

### Traffic Policy

### Amazon Route 53 Resolver Rules & Endpoints

1. Managed DNS Resolver service from Route 53
2. Enables hybrid DNS
3. Conditional DNS