# Designing a Highly Available Web Application Architecture on AWS

## Project Overview

This project demonstrates the deployment of a **highly available and scalable web application on AWS** using core cloud services such as EC2, Auto Scaling Groups, and an Application Load Balancer (ALB).

The architecture ensures that the application remains available even if individual EC2 instances fail by automatically replacing unhealthy instances and distributing traffic across multiple Availability Zones.

---

## Architecture Overview

- 1 VPC (10.0.0.0/16)
- 2 Public Subnets across 2 Availability Zones
- Internet-facing Application Load Balancer (ALB)
- Target Group with health checks
- Auto Scaling Group (Min: 2 | Desired: 2 | Max: 4)
- EC2 instances running NGINX web server

---

## 🔁 How It Works

1. Users access the application via the ALB DNS name.
2. The ALB distributes traffic across healthy EC2 instances.
3. EC2 instances run an NGINX web server deployed via Launch Template user data.
4. Auto Scaling Group ensures there are always 2 running instances.
5. If an instance fails or is terminated, AWS automatically launches a replacement.
6. The Target Group ensures only healthy instances receive traffic.

---

## AWS Services Used

| Service | Purpose |
|--------|---------|
| Amazon VPC | Isolated network environment |
| EC2 | Hosts the web application |
| Auto Scaling Group | Ensures high availability and self-healing |
| Application Load Balancer | Distributes traffic across instances |
| Target Group | Performs health checks |
| Launch Template | Defines EC2 configuration |
| CloudWatch | Monitoring and scaling triggers |
| Security Groups | Controls inbound/outbound traffic |

---

## Deployment Steps

### 1. VPC Setup
- I created a custom VPC (10.0.0.0/16)
- I configured 2 public subnets across 2 Availability Zones
- I attached the Internet Gateway
- I configured route tables for internet access

### 2. Security Groups
- ALB Security Group: Allows HTTP (80) from the internet
- EC2 Security Group: Allows HTTP only from ALB

### 3. Launch Template
- Amazon Linux 2 / Amazon Linux 2023
- I installed and configured NGINX using the user data script

### 4. Target Group
- I configured health checks on HTTP ("/")

### 5. Application Load Balancer
- Internet-facing ALB
- Listener on port 80
- Attached to Target Group

### 6. Auto Scaling Group
- Minimum capacity: 2
- Desired capacity: 2
- Maximum capacity: 4
- Spread across 2 Availability Zones

### 7. Monitoring
- Basic CloudWatch monitoring enabled
- Scaling policies configured based on CPU utilization

---

## Fault Tolerance Test

To validate self-healing behavior:

- I manually terminated one EC2 instance 
- Auto Scaling Group detected reduced capacity
- A new instance was automatically launched
- The replacement instance passed health checks
- Application remained fully available via ALB

---

## Key Outcomes

- Highly available architecture across multiple Availability Zones
- Automatic recovery from instance failure (self-healing)
- Load-balanced traffic distribution
- Scalable infrastructure based on demand
- Real-world cloud architecture design experience

---

## What I Learned

- How ALB distributes traffic across healthy instances
- How Auto Scaling Groups maintain desired capacity
- How health checks ensure system reliability
- How multi-AZ architecture improves fault tolerance
- How cloud infrastructure self-heals automatically

---

## 👤 Author

**Mabel Omolaja**  
Aspiring Cloud Engineer | AWS | Linux | Networking | DevOps
