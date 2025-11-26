# Cost Analysis (₹)

This document provides cost estimates for the **Network Function Virtualization** platform in **Indian Rupees (₹)**.

## Production Environment

At production scale (telecom-grade deployment), the architecture typically costs:

| Service | Monthly Cost (₹) | Notes |
|---------|------------------|-------|
| **EC2 (VNF hosts)** | ₹80,000–150,000 | c5n/c6i instances for NFV |
| **Network Firewall** | ₹40,000–70,000 | Managed firewall VNF |
| **Gateway Load Balancer** | ₹30,000–50,000 | VNF traffic distribution |
| **Transit Gateway** | ₹25,000–45,000 | Service chaining |
| **EBS (high IOPS)** | ₹15,000–30,000 | VNF storage |
| **CloudWatch** | ₹8,000–15,000 | Monitoring |
| **Total** | **₹200,000–360,000** | ~$2,500–4,500/month |

## Per-VNF Costs

| VNF Type | Monthly Cost (₹) | Notes |
|----------|------------------|-------|
| Virtual Firewall | ₹40,000–70,000 | HA pair |
| Load Balancer | ₹25,000–45,000 | Active-active |
| IDS/IPS | ₹35,000–60,000 | Inline inspection |
| DPI Engine | ₹50,000–90,000 | Deep packet inspection |
| NAT Gateway | ₹20,000–35,000 | High throughput |

## Scaling Costs

| Traffic Volume | Est. Monthly Cost (₹) |
|---------------|----------------------|
| 1 Gbps | ₹150,000–250,000 |
| 10 Gbps | ₹400,000–700,000 |
| 100 Gbps | ₹2,000,000–3,500,000 |

## Cost Optimization Strategies

- **Right-size VNF instances** – Match to actual throughput
- **Use Graviton instances** – 20% cost savings
- **Consolidate VNFs** – Multi-function appliances
- **Auto-scaling** – Scale down during low traffic
- **Reserved instances** – For baseline capacity
- **Spot for non-critical** – Test/dev environments

## Related Documentation

See `ARCHITECTURE.md` for service details and `DEPLOYMENT.md` for configuration options.
