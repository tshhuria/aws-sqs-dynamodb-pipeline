# 🧱 Optimizing WordPress Architecture on AWS

This project demonstrates how to transform and optimize a WordPress-based web application hosted on AWS using a combination of **scalability enhancements**, **auto-scaling strategies**, **performance monitoring**, and **cost-efficient practices**, aligning with the **AWS Well-Architected Framework**.

---

## 🚀 Overview

Retail and e-commerce applications, especially during peak events like Black Friday, demand **high availability**, **low latency**, and **dynamic scalability**. This project explores:

- Designing a robust WordPress deployment architecture on AWS
- Identifying and mitigating architectural pitfalls
- Implementing **dynamic auto-scaling policies** based on key metrics
- Using tools like **CloudWatch**, **Auto Scaling Groups**, **ALB**, and **RDS**
- Evaluating multiple **performance metrics** like CPU utilization, response time, and request rate
- Performing load testing with **Loader.io** and **AF WP StressKit**

---

## 🛠️ Tech Stack & AWS Services Used

- **Amazon EC2 (Elastic Compute Cloud)**
- **Amazon RDS (Relational Database Service)**
- **Amazon CloudWatch**
- **Amazon VPC, Security Groups, Internet Gateway**
- **Application Load Balancer (ALB)**
- **Auto Scaling Groups & Warm Pools**
- **Bitnami WordPress AMI**
- **Loader.io for Load Testing**

---

## 📈 Architecture Evolution

### 🧱 Initial Architecture


![CurrentArchitectureFinal](https://github.com/user-attachments/assets/d77a2c0e-4750-4cf1-9022-bbf83eb83f26)

- Single EC2 instance (t2.micro)
- Bitnami WordPress stack
- Loader.io for basic load testing
- VPC, Security Group, and Internet Gateway for network configuration

**✅ Pros:**
- Easy setup
- Low cost
- Basic security in place

**❌ Cons:**
- Single point of failure
- No load balancing or scaling
- Data loss risks
- Poor performance under high traffic

---

### ⚙️ Optimized Architecture

![OptimisedDiagram](https://github.com/user-attachments/assets/091692f6-7e42-4140-a2ba-223f45d5cc23)

- Multi-AZ deployment with **Application Load Balancer**
- **Auto Scaling Group** (Min: 1, Max: 3) with pre-warmed instances
- Integrated with **Amazon RDS** for shared storage
- **CloudWatch** used for real-time monitoring and dynamic scaling

> 📌 Designed to align with AWS Well-Architected Framework pillars: *Security, Reliability, Operational Excellence, Performance Efficiency, and Cost Optimization*

---

## 📊 Auto-Scaling Strategy

### ✅ Metrics Considered

| Metric              | Observations |
|---------------------|--------------|
| **CPU Utilization** | Unreliable due to backend bottlenecks |
| **Target Response Time** | Good for scaling out, weak for scale-in |
| **Number of Requests** | Best performance for both scale-out & scale-in |

### 🔁 Final Auto-Scaling Policy

- **Scale-Out:**  
  Triggered when request count > 20 (for 5 × 10s periods)  
  → Launch up to 3 instances (from warm pool)

- **Scale-In:**  
  Triggered when request count ≤ 20 (for 3 × 10s periods)  
  → Reduce to 2 or 1 instance based on thresholds

- Warm pool enabled for faster instance readiness
- Combined policy (CPU + Requests) further optimized latency

---

## 🧪 Load Testing Results

| Clients | Avg Response Time | Timeouts | Scaling Behavior |
|--------:|------------------:|----------|------------------|
| 250     | 435 ms            | 0        | Smooth scale-out |
| 350     | 503 ms            | 0        | Efficient scaling |
| 500     | 643 ms            | 0        | Optimized latency |

> ⚡ Initial latency spikes were resolved using warm pool and metric tuning.

---

## 🔐 Security Measures

- **VPC** for isolated environment
- **Security Groups** allow HTTP/SSH only
- Proposed **IAM roles**, **CloudTrail**, and **Backup**
- AWS-managed **snapshots** and **automated backups**

---

## ❌ Pitfalls in Initial Setup

- 🔻 Single EC2 instance (no high availability)
- 🚫 No shared storage or RDS
- 📉 No logging, monitoring, or backup strategy
- 🌐 Open traffic from any IP (security risk)
- ⚠️ No disaster recovery plan

---

## 🔧 Suggested Improvements

- ✅ Integrate Amazon **RDS** for shared database
- ✅ Use **EFS** for WordPress content sync across instances
- ✅ Enable **Multi-AZ** backups for RDS
- ✅ Add centralized monitoring with **CloudWatch Dashboards**
- ✅ Future plan: Incorporate **AWS Lambda** or **ECS**

---

## 📚 Key References

- [Bitnami WordPress Stack](https://bitnami.com/stack/wordpress)
- [Amazon EC2](https://aws.amazon.com/ec2/)
- [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
- [AWS Auto Scaling](https://aws.amazon.com/autoscaling/)
- [Amazon RDS](https://aws.amazon.com/rds/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Loader.io Load Testing Tool](https://loader.io/)

---

## 📌 Notes

- This project was created as part of a **cloud architecture optimization lab**.
- All AWS credentials and access information have been **removed** for security.
- No confidential or personal data has been shared in this repository.

---

## 📩 Contact

For questions or collaboration, feel free to raise an issue or reach out on [LinkedIn](#).

---
