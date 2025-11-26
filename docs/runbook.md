# Runbook

Operational guide for deploying and managing the **Network Function Virtualization** platform.

## 1. Deployment

### Prerequisites

- AWS CLI configured with appropriate credentials
- Node.js 18+ and npm installed
- AWS CDK CLI installed
- VNF images available in AMI or container format

### Deploy Steps

```bash
# Install dependencies
npm install

# Bootstrap CDK
cdk bootstrap

# Deploy NFV infrastructure
cdk deploy --context environment=prod
```

## 2. VNF Deployment

### Deploy Virtual Firewall

```bash
# Deploy firewall VNF
cdk deploy FirewallStack --context vnf=firewall

# Configure firewall rules
aws ec2 create-network-firewall-rule-group ...
```

### Deploy IDS/IPS

```bash
# Deploy IDS VNF
cdk deploy IDSStack --context vnf=ids

# Enable inline mode
aws ec2 modify-traffic-mirror-session ...
```

## 3. Service Chaining

### Configure Service Chain

```hcl
# Example: Internet → Firewall → IDS → Application
resource "aws_ec2_transit_gateway_route" "chain" {
  destination_cidr_block = "0.0.0.0/0"
  transit_gateway_attachment_id = aws_ec2_transit_gateway_vpc_attachment.firewall.id
  transit_gateway_route_table_id = aws_ec2_transit_gateway_route_table.main.id
}
```

### Gateway Load Balancer Setup

1. Create GWLB in VNF VPC
2. Create GWLB endpoint in application VPC
3. Update route tables
4. Verify traffic flow

## 4. Monitoring

### Key Metrics to Watch

- **VNF health**: CPU, memory, network
- **Throughput**: Packets/bytes per second
- **Latency**: Per-VNF processing time
- **Drops**: Packet loss indicators
- **Security events**: Alerts and blocks

### Dashboards

Pre-configured dashboards for:

- VNF fleet health
- Service chain performance
- Security event summary
- Capacity planning

## 5. Scaling

### Horizontal Scaling

```bash
# Add VNF instance to target group
aws elbv2 register-targets \
  --target-group-arn arn:aws:elasticloadbalancing:... \
  --targets Id=i-xxx
```

### Auto-Scaling Configuration

- Scale on CPU utilization
- Scale on network throughput
- Minimum instances for HA
- Maximum for cost control

## 6. Maintenance

### Regular Tasks

- Update VNF images monthly
- Review security policies weekly
- Test failover quarterly
- Capacity review monthly

### VNF Update Process

1. Deploy new VNF version
2. Add to load balancer
3. Drain old instance
4. Verify functionality
5. Remove old instance

### Teardown

```bash
cdk destroy --context environment=dev
```

> For troubleshooting common issues, see `docs/troubleshooting.md`.
