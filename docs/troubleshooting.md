# Troubleshooting

Common issues and resolutions for the **Network Function Virtualization** platform.

## VNF Issues

### 1. VNF Instance Unhealthy

**Symptom:** VNF failing health checks.

**Resolution:**
- Check instance status in EC2 console
- Review CloudWatch metrics (CPU, memory)
- Check VNF application logs
- Verify network connectivity
- Restart VNF if necessary

### 2. VNF Performance Degradation

**Symptom:** High latency or packet drops.

**Resolution:**
- Check CPU utilization – scale up if needed
- Review network throughput limits
- Check for traffic spikes
- Verify EBS IOPS not exhausted
- Consider enhanced networking

### 3. VNF Failover Not Working

**Symptom:** Traffic not shifting to standby VNF.

**Resolution:**
- Verify health check configuration
- Check target group settings
- Review route table failover
- Test manual failover
- Check VNF state synchronization

## Service Chain Issues

### 4. Traffic Not Reaching VNF

**Symptom:** Packets bypassing VNF in chain.

**Resolution:**
- Verify route table configuration
- Check GWLB endpoint association
- Review Transit Gateway routes
- Verify VPC attachments
- Check security group rules

### 5. Service Chain Loop

**Symptom:** Traffic looping between VNFs.

**Resolution:**
- Review route table entries
- Check for asymmetric routing
- Verify return path configuration
- Review GWLB target settings

### 6. Inter-VNF Communication Failure

**Symptom:** VNFs cannot communicate.

**Resolution:**
- Check security groups allow traffic
- Verify VPC peering/Transit Gateway
- Review network ACLs
- Check VNF interface configuration

## Gateway Load Balancer Issues

### 7. GWLB Health Check Failures

**Symptom:** Targets showing unhealthy.

**Resolution:**
- Verify health check port/protocol
- Check VNF is responding to health checks
- Review security group for health check traffic
- Check VNF application status

### 8. GWLB Asymmetric Flow

**Symptom:** Return traffic not going through GWLB.

**Resolution:**
- Verify GENEVE encapsulation
- Check flow stickiness settings
- Review VNF return routing
- Verify endpoint associations

## Security VNF Issues

### 9. Firewall Blocking Legitimate Traffic

**Symptom:** Valid traffic being dropped.

**Resolution:**
- Review firewall rules
- Check rule order/priority
- Review logs for drop reason
- Add exception rules if needed
- Verify stateful tracking

### 10. IDS/IPS False Positives

**Symptom:** Too many alerts for normal traffic.

**Resolution:**
- Tune detection signatures
- Add whitelist rules
- Adjust sensitivity thresholds
- Review baseline traffic patterns

> For architecture details, see the project README.
