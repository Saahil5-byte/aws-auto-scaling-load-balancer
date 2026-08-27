# 🚀 Auto-Scaling Web Infrastructure for High-Traffic Events (AWS)

## 📌 Problem Statement / Use Case
E-commerce platforms face massive, unpredictable traffic spikes during sale
events like "Big Billion Days." Manually provisioning servers for such
events is slow, error-prone, and costly. This project simulates that exact
scenario — building a **self-healing, auto-scaling infrastructure** that
automatically launches additional servers when traffic rises, and scales
back down when demand drops, with zero manual intervention.

## 🎯 Scenario
> During a flash sale event, traffic can spike 4x within minutes.
> The infrastructure needs to detect this rise and scale automatically —
> without an engineer manually launching instances.

## 🛠️ Tech Stack
`AWS EC2` `Launch Templates` `Auto Scaling Groups (ASG)` `Elastic Load Balancer (ELB)`
`Target Groups` `Apache Web Server` `CRON Scaling Policies` `CloudWatch`
`High Availability` `Auto Scaling` `Cloud Cost Optimization`

## ⚙️ Scaling Configuration
| Setting | Value |
|---|---|
| Minimum Instances | 1 |
| Desired (Dedicated) Instances | 2 |
| Maximum Instances | 4 |
| Trigger | Traffic-based scaling policy (CRON) |
| Web Server | Apache (HTTPD) |

## 📋 Step-by-Step Implementation

### 1️⃣ Launch Templates
- Created a Launch Template with Apache pre-installed via user-data script
- Standardized AMI, instance type, and security group config for consistency

### 2️⃣ Auto Scaling Group (ASG)
- Configured ASG with **Min: 1, Desired: 2, Max: 4**
- Ensures 2 dedicated instances always run, with headroom to scale to 4
  under load

### 3️⃣ CRON-based Scaling Policy
- Set scaling policies to simulate traffic surge conditions
- When traffic crosses threshold → ASG automatically launches up to 4 instances
- When traffic normalizes → scales back down to reduce cost

### 4️⃣ Target Groups
- Registered all ASG instances to a Target Group
- Configured health checks so traffic only routes to healthy Apache servers

### 5️⃣ Load Balancer
- Deployed 1 Application Load Balancer (ALB) in front of the Target Group
- Distributes incoming traffic evenly across all active instances
- Single DNS endpoint regardless of how many instances are running behind it

## ✅ Result
Successfully tested the ALB DNS endpoint in a browser and confirmed live
traffic routing to the Apache web server through the auto-scaled instances —
verifying the entire pipeline worked end-to-end, from launch template to
load balancer, exactly as designed.

## 💰 Cost Optimization
All resources — instances, ASG, Target Groups, and Load Balancer — were
deprovisioned immediately after testing to stay within AWS Free Tier limits,
reflecting real-world cost discipline used in production cloud environments.

## 🔮 What I'd Improve at Scale
- Trigger scaling via **CloudWatch CPU/Network metrics** instead of only CRON, for real-time reactive scaling
- Convert manual console setup into **Terraform/CloudFormation** for repeatable, version-controlled infrastructure

![Alt text](./screenshots/214943.png)
- 
