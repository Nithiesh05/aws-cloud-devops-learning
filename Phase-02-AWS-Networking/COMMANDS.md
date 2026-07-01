# 💻 COMMANDS.md

# AWS Networking Commands Used in Phase 2

This document contains all the AWS CLI, Linux, and networking commands used throughout Phase 2 of my Cloud & DevOps learning journey.

Instead of simply listing commands, each section explains:

- What the command does
- Why I used it
- Example usage
- Expected output
- Real-world use case

---

# 1. aws sts get-caller-identity

## Purpose

Displays the AWS account and IAM identity currently configured in the AWS CLI.

---

## Syntax

```bash
aws sts get-caller-identity
```

---

## Example Output

```json
{
  "UserId": "AIDA***********",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/admin"
}
```

---

## Why I Used It

To verify that AWS CLI was configured correctly before performing AWS operations.

---

## Real-World Usage

Cloud Engineers commonly use this command before executing Terraform, AWS CLI, or deployment scripts to confirm they are working in the correct AWS account.

---

# 2. ip addr

## Purpose

Displays all network interfaces and IP addresses assigned to the Linux machine.

---

## Syntax

```bash
ip addr
```

---

## Why I Used It

To understand the difference between Public IP and Private IP inside an EC2 instance.

I learned that Linux only displays the Private IP because AWS performs Public IP translation through the Internet Gateway.

---

## Real-World Usage

Used while troubleshooting network connectivity and verifying interface configuration.

---

# 3. ip route

## Purpose

Displays the Linux routing table.

---

## Syntax

```bash
ip route
```

---

## Example Output

```text
default via 172.31.0.1 dev eth0
```

---

## Why I Used It

To understand how Linux determines the default gateway for outbound traffic.

---

## Real-World Usage

Useful while troubleshooting routing issues inside Linux servers.

---

# 4. ping

## Purpose

Checks network connectivity between two systems.

---

## Syntax

```bash
ping google.com
```

---

## Why I Used It

To verify internet connectivity from an EC2 instance.

---

## Real-World Usage

Commonly used to determine whether DNS resolution and network connectivity are working.

---

# 5. curl

## Purpose

Sends HTTP requests from the command line.

---

## Syntax

```bash
curl http://localhost
```

---

## Why I Used It

To determine whether an application was responding locally before investigating AWS networking components.

---

## Real-World Usage

Useful for verifying application availability from inside the server.

---

# 6. hostname -I

## Purpose

Displays all IP addresses assigned to the Linux system.

---

## Syntax

```bash
hostname -I
```

---

## Why I Used It

To verify the private IP assigned to the EC2 instance.

---

# 7. aws ec2 describe-vpcs

## Purpose

Lists all Virtual Private Clouds in the AWS account.

---

## Syntax

```bash
aws ec2 describe-vpcs
```

---

## Why I Used It

To verify available VPCs and understand their CIDR ranges.

---

## Real-World Usage

Useful while auditing AWS infrastructure or automating deployments.

---

# 8. aws ec2 describe-subnets

## Purpose

Lists all subnets inside a VPC.

---

## Syntax

```bash
aws ec2 describe-subnets
```

---

## Why I Used It

To verify subnet configuration and CIDR allocation.

---

# 9. aws ec2 describe-route-tables

## Purpose

Lists all Route Tables.

---

## Syntax

```bash
aws ec2 describe-route-tables
```

---

## Why I Used It

To understand how traffic is routed inside a VPC.

---

## Real-World Usage

Useful while troubleshooting internet connectivity issues.

---

# 10. aws ec2 describe-security-groups

## Purpose

Displays Security Groups and their inbound/outbound rules.

---

## Syntax

```bash
aws ec2 describe-security-groups
```

---

## Why I Used It

To verify whether required ports such as SSH (22) and HTTP (80) were allowed.

---

# 11. aws ec2 describe-instances

## Purpose

Displays EC2 instance information.

---

## Syntax

```bash
aws ec2 describe-instances
```

---

## Why I Used It

To verify instance state, networking information, and attached security groups.

---

# 12. aws ssm describe-instance-information

## Purpose

Lists EC2 instances managed by AWS Systems Manager.

---

## Syntax

```bash
aws ssm describe-instance-information
```

---

## Why I Used It

To verify whether an EC2 instance was successfully registered with Systems Manager.

---

## Real-World Usage

Useful while troubleshooting Session Manager connectivity.

---

# 13. systemctl status amazon-ssm-agent

## Purpose

Checks whether the Amazon SSM Agent service is running.

---

## Syntax

```bash
sudo systemctl status amazon-ssm-agent
```

---

## Why I Used It

To verify that the SSM Agent was running during Session Manager troubleshooting.

---

# 14. systemctl restart amazon-ssm-agent

## Purpose

Restarts the Systems Manager Agent.

---

## Syntax

```bash
sudo systemctl restart amazon-ssm-agent
```

---

## Why I Used It

To restart the agent after configuration changes or connectivity issues.

---

# 15. journalctl -u amazon-ssm-agent

## Purpose

Displays logs generated by the SSM Agent.

---

## Syntax

```bash
sudo journalctl -u amazon-ssm-agent
```

---

## Why I Used It

To investigate why Session Manager was unable to establish a connection.

---

# 16. ss -tulnp

## Purpose

Displays listening ports and active network sockets.

---

## Syntax

```bash
ss -tulnp
```

---

## Why I Used It

To verify that applications were listening on the expected ports during networking troubleshooting.

---

# 17. ps -ef

## Purpose

Displays all running processes.

---

## Syntax

```bash
ps -ef
```

---

## Why I Used It

To verify that important networking-related services such as the SSM Agent were running.

---

# Networking Troubleshooting Workflow

Whenever an EC2 instance was not reachable, I followed this sequence:

```text
1. Verify EC2 Instance State

↓

2. Verify Public or Private Subnet

↓

3. Verify Route Table Association

↓

4. Verify Internet Gateway

↓

5. Verify Security Group Rules

↓

6. Verify Network ACL Rules

↓

7. Verify Public IP / Elastic IP

↓

8. Verify IAM Role (SSM)

↓

9. Verify Amazon SSM Agent

↓

10. Review SSM Logs
```

---

# Key Commands to Remember

| Command | Why It Is Important |
|----------|---------------------|
| `ip addr` | View network interfaces |
| `ip route` | View routing table |
| `ping` | Verify connectivity |
| `curl` | Test application locally |
| `hostname -I` | View assigned IP addresses |
| `aws sts get-caller-identity` | Verify AWS CLI configuration |
| `aws ec2 describe-vpcs` | List VPCs |
| `aws ec2 describe-subnets` | Verify subnet configuration |
| `aws ec2 describe-route-tables` | Verify routing |
| `aws ec2 describe-security-groups` | Verify firewall rules |
| `systemctl status amazon-ssm-agent` | Verify SSM Agent |
| `journalctl -u amazon-ssm-agent` | View SSM logs |

---

# Final Notes

One of the biggest lessons from this phase was understanding that AWS networking issues should never be diagnosed by guessing.

Instead, every component should be verified in a logical sequence:

- Network Design
- Routing
- Security
- Connectivity
- Services

Following a structured troubleshooting methodology significantly reduces the time required to identify networking issues in production environments.