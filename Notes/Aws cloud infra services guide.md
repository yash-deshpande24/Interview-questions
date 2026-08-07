# AWS Cloud & Infra Services — Full Forms, Explanation & Uses

This guide covers all the AWS services listed in your resume under "Cloud & Infra": EC2, ECS/Fargate, ECR, Lambda, ALB, VPC, RDS, S3, IAM, CloudFront, Route 53, SNS, SQS, and CW.

---

## 1. EC2 — Elastic Compute Cloud
**What it is:** A virtual server in the cloud. You rent computing power (CPU, RAM, storage) instead of buying physical hardware.

**Use:** To run applications, host websites, or run any workload that needs a full server. You control the operating system and everything installed on it.

---

## 2. ECS — Elastic Container Service
**What it is:** A service that runs and manages Docker containers at scale, without you having to manually start/stop each one.

**Use:** To deploy containerized applications (like microservices) reliably, with AWS handling scheduling, scaling, and health checks.

### Fargate
**What it is:** A serverless compute mode for ECS. "Fargate" is not an acronym — it's just a product name.

**Use:** Runs your containers without you managing the underlying EC2 servers — AWS handles the infrastructure completely. You just define CPU/memory needs and Fargate runs it.

---

## 3. ECR — Elastic Container Registry
**What it is:** A storage service for Docker container images (like a private Docker Hub, but on AWS).

**Use:** To store, version, and manage container images before deploying them to ECS or EKS.

---

## 4. Lambda
**What it is:** A serverless compute service. "Lambda" is a product name (not an acronym) — it runs your code only when triggered, without any server management.

**Use:** To run small pieces of code in response to events (e.g., a file upload, an API call, a scheduled time) without maintaining a server. You only pay for the time the code actually runs.

---

## 5. ALB — Application Load Balancer
**What it is:** A service that distributes incoming web traffic across multiple servers or containers.

**Use:** To balance load, increase availability, and route requests intelligently (e.g., based on URL path) so no single server gets overwhelmed.

---

## 6. VPC — Virtual Private Cloud
**What it is:** Your own isolated, private network inside AWS.

**Use:** To control networking — defining subnets, IP ranges, and routing rules — and to decide what's publicly accessible versus what stays private and secure.

---

## 7. RDS — Relational Database Service
**What it is:** A managed relational database service (supports engines like PostgreSQL, MySQL, etc.).

**Use:** To run a database without manually handling backups, patching, or scaling — AWS manages the database infrastructure for you.

---

## 8. S3 — Simple Storage Service
**What it is:** Object storage for files of any kind (images, backups, documents, static website files).

**Use:** To store and retrieve any amount of data reliably and cheaply. Commonly used for backups, file storage, hosting static websites, and data lakes.

---

## 9. IAM — Identity and Access Management
**What it is:** A service that controls who (users, applications, services) can access AWS resources, and what actions they're allowed to perform.

**Use:** To enforce security using the "least privilege" principle — giving only the exact permissions needed, nothing more. Used to create users, roles, and policies.

---

## 10. CloudFront
**What it is:** A Content Delivery Network (CDN). "CloudFront" is a product name (not an acronym).

**Use:** To cache and deliver content (images, videos, web pages) from servers located close to the user, reducing latency and speeding up load times.

---

## 11. Route 53
**What it is:** AWS's DNS (Domain Name System) service. Named "53" after the standard DNS port number (port 53).

**Use:** To route users to your application by domain name, manage domain registration, and perform health checks/failover routing.

---

## 12. SNS — Simple Notification Service
**What it is:** A publish/subscribe (pub/sub) messaging service.

**Use:** To send a single message out to multiple subscribers at once (e.g., email, SMS, or other services) — useful for broadcasting events or alerts.

---

## 13. SQS — Simple Queue Service
**What it is:** A message queuing service.

**Use:** To let different parts of a system communicate reliably and asynchronously — messages wait in a queue until a service is ready to process them, preventing data loss under heavy load.

---

## 14. CW — CloudWatch
**What it is:** AWS's monitoring and observability service. "CW" is simply the short form of CloudWatch.

**Use:** To collect logs, track metrics (CPU, memory, request counts), and set alarms that can trigger automated actions — like the auto-healing alarms you used in your ECS project.

---

## Quick Reference Table

| Service | Full Form | One-Line Use |
|---|---|---|
| EC2 | Elastic Compute Cloud | Virtual servers to run applications |
| ECS | Elastic Container Service | Runs and manages Docker containers |
| Fargate | (Product name) | Serverless compute for ECS containers |
| ECR | Elastic Container Registry | Stores Docker container images |
| Lambda | (Product name) | Runs code on events, serverless |
| ALB | Application Load Balancer | Distributes traffic across servers |
| VPC | Virtual Private Cloud | Your private network in AWS |
| RDS | Relational Database Service | Managed relational databases |
| S3 | Simple Storage Service | Object storage for files/backups |
| IAM | Identity and Access Management | Controls user/service access |
| CloudFront | (Product name) | CDN for fast content delivery |
| Route 53 | (Product name, "53" = DNS port) | DNS and domain routing |
| SNS | Simple Notification Service | Broadcasts messages to subscribers |
| SQS | Simple Queue Service | Queues messages between services |
| CW | CloudWatch | Monitoring, logging, and alarms |

---

## Simple Interview Answer

**Q: Can you explain the AWS services you've worked with?**

**A:** "I've worked with a mix of compute, networking, storage, and monitoring services on AWS. For compute, I use EC2 for virtual servers, ECS with Fargate to run containers without managing servers, and Lambda for serverless, event-driven code. For networking, I use VPC to control my private network, ALB to balance traffic, and Route 53 for DNS routing, with CloudFront as a CDN to speed up content delivery. For storage and databases, I use S3 for object storage and RDS for managed relational databases. For security, I use IAM to control access with least-privilege policies. And for messaging and monitoring, I use SNS and SQS to handle asynchronous communication between services, and CloudWatch to monitor logs, metrics, and trigger alarms — which I used to build the auto-healing system in one of my projects."
