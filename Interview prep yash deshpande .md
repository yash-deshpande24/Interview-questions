# Interview Preparation Guide — Yash Deshpande (Cloud Engineer)

This guide is built from your resume and organized into sections: Work Experience, Projects, Cloud Services (concepts + Q&A), and DevOps Tools (concepts + Q&A). Backend-specific deep-dive questions are intentionally kept light, with guidance on how to redirect if asked.

---

## Section 1: Work Experience — Likely Questions & Answers

### Q1: Walk me through your role as a Cloud Engineer at Aisyntelligence LLP.
**A:** I joined Aisyntelligence in July 2025 as a Cloud Engineer. My main responsibility is designing and maintaining AWS infrastructure for production microservices that serve over 50,000 daily requests. I work primarily with EC2, ECS Fargate, Application Load Balancer, and VPC. I also lead our Infrastructure-as-Code efforts using Terraform, and I manage security, cost optimization, and serverless components like Lambda.

### Q2: You mentioned reducing infrastructure provisioning time from 2 days to under 2 hours. How did you achieve that?
**A:** Previously, infrastructure was set up manually — creating VPCs, subnets, security groups, and EC2/ECS resources by hand through the AWS console. I rewrote this as modular Terraform code, so the same environment could be provisioned repeatedly with a single `terraform apply`. This removed manual steps, human error, and approval delays, cutting the process from about 2 days to under 2 hours.

### Q3: How did you reduce API latency by 35% using Lambda and CloudFront?
**A:** I moved certain lightweight, event-driven operations to Lambda functions instead of routing them through the main backend service, which reduced processing overhead. I also used CloudFront to cache and serve content closer to users geographically, cutting round-trip time. Together, these changes reduced average response latency by about 35%.

### Q4: Tell me about the IAM and security work you did.
**A:** I audited existing IAM policies and found many were overly permissive. I rewrote them following the principle of least privilege — giving each role or service only the permissions it actually needed. I also set up automated access reviews so unused or excessive permissions get flagged periodically. This reduced our security audit findings by 40%.

### Q5: How did you cut monthly cloud spend by 22%?
**A:** I analyzed usage patterns with CloudWatch and Cost Explorer, identified over-provisioned EC2/ECS resources, and right-sized them to match actual load. I also moved predictable, steady workloads to Reserved Instances instead of On-Demand pricing, since Reserved Instances are cheaper for long-running workloads. Combined, this reduced our monthly bill by 22%.

### Q6: What did you do at Dream Filler Software Solutions before this role?
**A:** That was a Backend Engineering role from June 2024 to February 2025. I built and shipped over 10 RESTful API endpoints using Node.js and Express, designed both relational (PostgreSQL) and non-relational (MongoDB) schemas for multi-tenant applications, wrote Postman test suites covering 90%+ of endpoints, and worked closely with frontend engineers to reduce integration issues.

### Q7: Why did you move from a backend-focused role to cloud engineering?
**A:** During the backend role, I was already handling deployment and infrastructure setup for the APIs I built, and I found I enjoyed that side more — the infrastructure, automation, and reliability engineering. That interest led me to focus fully on cloud engineering, where I now specialize in AWS, Terraform, and CI/CD.

---

## Section 2: Projects — Likely Questions & Answers

### Project 1: Auto-Healing ECS Platform with Chaos Engineering

**Q1: What was the goal of this project?**
**A:** The goal was to build a self-healing container platform on AWS ECS Fargate that could automatically detect and recover from failures without manual intervention, and to prove its resilience using chaos engineering.

**Q2: How does the auto-healing mechanism work?**
**A:** I set up CloudWatch Alarms to monitor the health of ECS tasks. When a task becomes unhealthy, the alarm triggers an event-driven remediation flow that automatically stops the unhealthy task and replaces it with a new one — all within seconds, without anyone needing to intervene.

**Q3: What is chaos engineering, and how did you apply it here?**
**A:** Chaos engineering means deliberately injecting failures into a system to test how well it recovers. I built a framework using Lambda functions to simulate over 10 failure scenarios — like killing a task, simulating high CPU load, or network failures — to validate that the auto-healing system responded correctly every time.

**Q4: What result did you achieve?**
**A:** I cut Mean Time to Recovery (MTTR) from around 15 minutes (when handled manually) to under 90 seconds with the automated system.

**Q5: Why did you use Terraform for this project?**
**A:** I provisioned the entire stack — VPC, ECS, ALB, IAM, and Lambda — as reusable Terraform modules. This meant a new environment (staging, testing, or production) could be spun up quickly and consistently, which reduced environment setup time by 80%.

---

### Project 2: CloudTask Manager — Full-Stack SaaS Task Platform

**Q1: What is CloudTask Manager?**
**A:** It's a full-stack SaaS task management application built with React on the frontend and Node.js on the backend, supporting over 500 concurrent users with JWT-based authentication and role-based access control (RBAC).

**Q2: How did you improve database performance?**
**A:** I designed the PostgreSQL schema carefully and added indexes on frequently queried columns, which reduced average query response time by about 40%.

**Q3: How did Docker help in this project?**
**A:** I containerized both the frontend and backend using Docker Compose. This meant any developer could spin up the full local environment with one command instead of manually installing and configuring dependencies, cutting local setup time from 3 hours to 15 minutes.

**Q4: What was your CI/CD setup?**
**A:** I used GitHub Actions to automate testing and deployment, combined with Terraform-provisioned AWS infrastructure. Every code push triggered automated builds, tests, and deployment, which reduced the overall release cycle time by 60%.

**Q5: What is RBAC and why did you implement it?**
**A:** RBAC stands for Role-Based Access Control. It restricts what actions a user can perform based on their assigned role (e.g., admin vs. regular user). I implemented it so that sensitive actions, like deleting tasks or managing users, are only available to authorized roles — important for a multi-user SaaS product.

---

## Section 3: Cloud Services — Concepts + Likely Q&A

### Quick explanations of the AWS services on your resume:

- **EC2 (Elastic Compute Cloud):** Virtual servers in the cloud. You rent computing capacity to run applications.
- **ECS/Fargate:** ECS is AWS's container orchestration service; Fargate is the serverless mode where you don't manage the underlying servers — AWS handles that for you.
- **ECR (Elastic Container Registry):** A storage service for Docker container images, used alongside ECS.
- **Lambda:** A serverless compute service — you upload code, and AWS runs it in response to events without you managing any servers.
- **ALB (Application Load Balancer):** Distributes incoming traffic across multiple servers/containers to balance load and increase availability.
- **VPC (Virtual Private Cloud):** Your own isolated network within AWS, where you control IP ranges, subnets, and routing.
- **RDS (Relational Database Service):** A managed relational database service (supports PostgreSQL, MySQL, etc.) — AWS handles backups, patching, and scaling.
- **S3 (Simple Storage Service):** Object storage for files, backups, and static assets.
- **IAM (Identity and Access Management):** Controls who (users, services) can access what resources, and what actions they can perform.
- **CloudFront:** A Content Delivery Network (CDN) that caches content at edge locations closer to users for faster delivery.
- **Route 53:** AWS's DNS (Domain Name System) service, used to route users to applications by domain name.
- **SNS (Simple Notification Service):** A pub/sub messaging service for sending notifications between distributed system components.
- **SQS (Simple Queue Service):** A message queuing service that lets components communicate asynchronously and reliably.
- **CloudWatch (CW):** AWS's monitoring and observability service — collects logs, metrics, and can trigger alarms/automation.

### Likely Interview Questions & Answers

**Q1: What's the difference between EC2 and Lambda?**
**A:** EC2 gives you a full virtual server that you manage and pay for continuously, even when idle. Lambda is serverless — you only pay for the time your code actually runs, and AWS manages the underlying infrastructure. I use EC2/ECS for long-running services and Lambda for short, event-driven tasks.

**Q2: What's the difference between ECS and Fargate?**
**A:** ECS is the container orchestration service itself. You can run ECS on EC2 instances (where you manage the servers) or on Fargate (serverless, where AWS manages the compute). In my projects, I used Fargate to avoid managing underlying EC2 instances.

**Q3: Why use a VPC?**
**A:** A VPC isolates your resources in a private network, giving you control over IP addressing, subnets (public/private), and security. It's essential for controlling what's exposed to the internet versus what stays internal.

**Q4: What's the difference between SNS and SQS?**
**A:** SNS is a publish/subscribe service — one message can go out to multiple subscribers (fan-out). SQS is a queue — messages wait in the queue until a consumer processes them, and typically only one consumer processes each message. I'd use SNS for broadcasting events and SQS for reliable task processing.

**Q5: How do you monitor your infrastructure?**
**A:** I use CloudWatch for metrics, logs, and alarms. For example, in my Auto-Healing ECS project, CloudWatch Alarms detect unhealthy tasks and trigger automated remediation.

**Q6: How does IAM enforce least privilege?**
**A:** By granting only the specific permissions a user or service needs to do its job — nothing more. I write granular IAM policies scoped to specific resources and actions rather than broad wildcard permissions, and I review them periodically to remove unused access.

**Q7: What's the role of Route 53 and CloudFront together?**
**A:** Route 53 handles DNS resolution — pointing a domain name to the right resource. CloudFront then caches and delivers content from edge locations close to the user, reducing latency. Together they help route users efficiently and serve content faster.

---

## Section 4: DevOps Tools — Concepts + Likely Q&A

### Quick explanations:

- **Docker:** A tool that packages an application and all its dependencies into a "container" — a lightweight, portable unit that runs the same way on any machine.
- **Terraform:** An Infrastructure-as-Code (IaC) tool. Instead of manually clicking through the AWS console, you write code that defines your infrastructure, and Terraform creates/updates/destroys it consistently.
- **Jenkins:** An automation server used for CI/CD (Continuous Integration/Continuous Deployment) — it automatically builds, tests, and deploys code when changes are pushed.

### Likely Interview Questions & Answers

**Q1: Why use Docker instead of just running the app directly on a machine?**
**A:** Docker ensures consistency — "it works on my machine" problems go away because the container includes the app and all its dependencies in one package. It also makes local setup much faster, which I demonstrated in CloudTask Manager, cutting setup time from 3 hours to 15 minutes.

**Q2: What is Infrastructure as Code, and why is Terraform useful?**
**A:** Infrastructure as Code means defining your cloud infrastructure in code files rather than manually configuring it. Terraform reads these files and creates matching resources on AWS. Benefits include repeatability, version control (you can track infrastructure changes in Git), and faster provisioning — I used this to cut provisioning time from 2 days to under 2 hours.

**Q3: What's the difference between Terraform and manually configuring AWS console?**
**A:** Manual configuration is error-prone, not repeatable, and hard to track changes. Terraform code can be reviewed, versioned, and reused — so the same environment can be recreated identically in seconds, and changes are auditable through version history.

**Q4: How does Jenkins fit into your CI/CD pipeline?**
**A:** Jenkins automates the build-test-deploy pipeline — when code is pushed, Jenkins can automatically run tests, build artifacts, and trigger deployment, removing manual steps and reducing release time.

**Q5: What's a Terraform module, and why did you use them?**
**A:** A module is a reusable, self-contained group of Terraform configuration files (e.g., for VPC, ECS, IAM). In my Auto-Healing ECS project, I built reusable modules for the full stack, which reduced environment setup time by 80% since I could reuse the same modules across environments.

**Q6: What happens if a Terraform apply fails halfway?**
**A:** Terraform tracks state, so it knows what has and hasn't been created. On the next `terraform apply`, it compares the desired state with the current state and only makes the necessary changes to reach the desired configuration, rather than starting over.

**Q7: Have you used Docker Compose? What's it for?**
**A:** Yes, in CloudTask Manager. Docker Compose lets you define and run multiple containers together (e.g., frontend, backend, database) using a single configuration file, so the whole application stack starts with one command.

---

## Section 5: Backend Questions — How to Handle

Since your current focus is cloud engineering and not backend development, you don't need to go deep into backend architecture questions. If asked:

**Suggested response if asked a deep backend question (e.g., "how would you optimize this SQL query" or "explain Node.js event loop internals"):**
> "My current role is focused on cloud infrastructure and DevOps — I did work on backend APIs in my previous role at Dream Filler, where I built REST endpoints with Node.js and designed PostgreSQL/MongoDB schemas, but I haven't gone deep into backend internals recently since my focus has shifted to AWS, Terraform, and CI/CD. I'd be happy to discuss the infrastructure and deployment side of backend systems instead."

This is an honest, professional way to redirect without pretending to have expertise you're not focusing on. You can still mention the basic facts on your resume (10+ REST endpoints, PostgreSQL/MongoDB, Postman tests) if asked about your experience — just avoid volunteering for or being drawn into deep backend technical questions.

---
- Practice saying the numbers (35%, 22%, 40%, 80%, 60%) naturally — interviewers often probe on "how did you measure that?"
- Be ready to explain **why** you made a choice (e.g., why Fargate over EC2), not just what you did.
- For every project, know the "before vs after" clearly — that's your strongest talking point.
