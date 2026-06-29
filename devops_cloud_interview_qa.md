# DevOps & Cloud Interview Questions and Answers (Fresher Level)

Covers: Linux | Git & GitHub | AWS (EC2, VPC, IAM, RDS, Auto Scaling, ELB, EFS, S3, DynamoDB, CloudWatch) | Docker | Terraform

---

## 1. Linux

**Q1. What is Linux and why is it widely used in DevOps?**
Linux is an open-source, Unix-like operating system kernel. It's used heavily in DevOps because it's free, stable, secure, highly customizable, and most cloud servers/containers run on Linux distributions like Ubuntu, CentOS, and Amazon Linux.

**Q2. What is the difference between a process and a thread?**
A process is an independent running instance of a program with its own memory space. A thread is a smaller unit of execution within a process that shares the same memory space as other threads in that process.

**Q3. What command would you use to check disk space usage?**
`df -h` shows disk space usage in human-readable format. `du -sh <folder>` shows the size of a specific folder.

**Q4. How do you check running processes in Linux?**
`ps -ef` or `ps aux` lists running processes. `top` or `htop` shows a live, interactive view of system processes and resource usage.

**Q5. What is the difference between a soft link and a hard link?**
A soft link (symbolic link) is a pointer/shortcut to another file and breaks if the original file is deleted. A hard link is a direct reference to the same inode/data on disk; the file still exists even if the original name is deleted.

**Q6. What does `chmod 755 file.sh` do?**
It sets permissions so the owner has read/write/execute (7), and group/others have read/execute (5). This is common for making a script executable.

**Q7. How do you find a specific text inside files in a directory?**
`grep -r "search_text" /path/to/directory` searches recursively for the text.

**Q8. What is the use of the `cron` utility?**
`cron` is a Linux job scheduler used to run scripts or commands automatically at specified times/intervals, configured via `crontab`.

**Q9. How do you check which ports are listening on a server?**
`netstat -tulnp` or the newer `ss -tulnp` shows listening ports and the processes using them.

**Q10. What is the difference between `systemctl` and `service` commands?**
Both manage services, but `systemctl` is part of `systemd` (used in modern distros like Ubuntu 16+, CentOS 7+) and offers more control (enable/disable on boot, status, logs), while `service` is the older SysV-style command.

---

## 2. Git

**Q1. What is Git and how is it different from GitHub?**
Git is a distributed version control system used to track changes in code locally. GitHub is a cloud-based hosting platform for Git repositories that adds collaboration features like pull requests, issues, and access control.

**Q2. What is the difference between `git pull` and `git fetch`?**
`git fetch` downloads changes from the remote repository but doesn't merge them into your local branch. `git pull` does a `fetch` followed by a `merge` automatically.

**Q3. What is a merge conflict and how do you resolve it?**
A merge conflict happens when Git can't automatically reconcile changes made to the same line(s) of a file in two branches. You resolve it by manually editing the conflicting file to keep the correct changes, then `git add` and `git commit`.

**Q4. What is the difference between `git merge` and `git rebase`?**
`git merge` combines branches and creates a new merge commit, preserving history as-is. `git rebase` moves/reapplies your commits on top of another branch, creating a cleaner, linear history.

**Q5. What does `git stash` do?**
It temporarily saves uncommitted changes so you can switch branches without committing incomplete work, and later restore them with `git stash pop`.

**Q6. What is the difference between `git reset` and `git revert`?**
`git reset` moves the branch pointer to a previous commit (can rewrite history). `git revert` creates a new commit that undoes the changes of a previous commit, keeping history intact — safer for shared branches.

**Q7. What is a `.gitignore` file used for?**
It tells Git which files/folders to ignore and not track (e.g., `node_modules/`, `.env`, log files, build artifacts).

**Q8. How do you create and switch to a new branch in one command?**
`git checkout -b new-branch-name` (or `git switch -c new-branch-name` in newer Git versions).

---

## 3. GitHub

**Q1. What is a Pull Request (PR)?**
A PR is a request to merge changes from one branch (often a fork or feature branch) into another, allowing team members to review code, discuss changes, and run automated checks before merging.

**Q2. What is the difference between forking and cloning a repository?**
Cloning copies a repo to your local machine while keeping the link to the original remote. Forking creates a copy of the repo under your own GitHub account, independent of the original, often used for contributing to others' projects.

**Q3. What are GitHub Actions?**
GitHub Actions is a CI/CD tool built into GitHub that lets you automate workflows (build, test, deploy) triggered by events like a push or pull request, defined in YAML files under `.github/workflows/`.

**Q4. What is branch protection in GitHub?**
A repository setting that enforces rules on a branch (e.g., `main`) such as requiring PR reviews, passing status checks, or preventing force pushes before code can be merged.

**Q5. What is the difference between a public and private repository?**
A public repo is visible to anyone on the internet. A private repo is accessible only to the owner and explicitly invited collaborators.

**Q6. How do you give someone access to your GitHub repository?**
Go to the repo → Settings → Collaborators and teams → Add people, then assign their role/permission level.

---

## 4. AWS — EC2 (Elastic Compute Cloud)

**Q1. What is EC2?**
EC2 is AWS's service for provisioning resizable virtual servers ("instances") in the cloud, where you choose CPU, memory, storage, and OS.

**Q2. What is an AMI?**
An Amazon Machine Image (AMI) is a template that contains the OS, application server, and software configuration used to launch an EC2 instance.

**Q3. What is the difference between Security Groups and NACLs?**
A Security Group is a stateful, instance-level virtual firewall (return traffic is automatically allowed). A Network ACL (NACL) is a stateless, subnet-level firewall where you must explicitly allow both inbound and outbound rules.

**Q4. What is the difference between On-Demand, Reserved, and Spot Instances?**
On-Demand: pay per hour/second with no commitment. Reserved: commit to 1 or 3 years for a significant discount. Spot: bid for unused AWS capacity at a much lower price, but the instance can be terminated by AWS with short notice.

**Q5. What is an Elastic IP?**
A static, public IPv4 address you can allocate and associate with an EC2 instance, which doesn't change even if you stop/start the instance (unlike the default public IP).

**Q6. What is the difference between EBS and instance store?**
EBS (Elastic Block Store) is persistent network-attached storage that survives instance stop/termination. Instance store is temporary storage physically attached to the host — data is lost when the instance stops or terminates.

**Q7. How do you connect to a Linux EC2 instance?**
Using SSH with the private key (`.pem` file): `ssh -i mykey.pem ec2-user@<public-ip>`.

**Q8. What is a key pair in EC2?**
A set of public/private keys AWS uses for secure SSH login — AWS stores the public key on the instance, and you keep the private key to authenticate.

---

## 5. AWS — VPC (Virtual Private Cloud)

**Q1. What is a VPC?**
A VPC is a logically isolated, private network within AWS where you launch resources like EC2 and RDS, with full control over IP ranges, subnets, route tables, and gateways.

**Q2. What is the difference between a public subnet and a private subnet?**
A public subnet has a route to an Internet Gateway, allowing direct internet access. A private subnet has no direct route to the internet (it may use a NAT Gateway for outbound-only access).

**Q3. What is an Internet Gateway (IGW)?**
A VPC component that allows resources in public subnets to communicate with the internet.

**Q4. What is a NAT Gateway used for?**
It allows instances in a private subnet to initiate outbound internet traffic (e.g., for updates) without being directly reachable from the internet.

**Q5. What is the purpose of a Route Table?**
It contains rules (routes) that determine where network traffic from a subnet is directed.

**Q6. What is VPC Peering?**
A networking connection between two VPCs that allows resources in each to communicate as if they were on the same network, without traversing the public internet.

**Q7. What is a CIDR block?**
A range of IP addresses (e.g., `10.0.0.0/16`) used to define the size of a VPC or subnet.

**Q8. What is the difference between Security Groups and Subnets in terms of scope?**
A subnet is a network segmentation concept tied to an Availability Zone. A Security Group is a firewall that controls traffic to/from resources (like EC2) regardless of which subnet they're in.

---

## 6. AWS — IAM (Identity and Access Management)

**Q1. What is IAM?**
IAM is AWS's service for securely managing access to AWS resources — controlling who (users, groups, roles) can do what (permissions) on which resources.

**Q2. What is the difference between an IAM User and an IAM Role?**
An IAM User represents a person or application with permanent credentials. An IAM Role is an identity with temporary permissions that can be assumed by users, applications, or AWS services (e.g., an EC2 instance assuming a role to access S3).

**Q3. What is an IAM Policy?**
A JSON document that defines permissions — specifying what actions are allowed or denied on which AWS resources.

**Q4. What is the principle of least privilege?**
A security best practice of granting only the minimum permissions necessary for a user or service to perform its required tasks — nothing more.

**Q5. What is MFA in IAM?**
Multi-Factor Authentication — an extra layer of security requiring a second verification factor (like a one-time code from a phone app) in addition to a password.

**Q6. What is the difference between an IAM Group and an IAM Role?**
A Group is a collection of IAM Users that share the same permissions (for easier management). A Role is not tied to a specific user — it's assumed temporarily by anyone/anything that needs it.

---

## 7. AWS — RDS (Relational Database Service)

**Q1. What is RDS?**
RDS is a managed relational database service supporting engines like MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server, where AWS handles patching, backups, and infrastructure management.

**Q2. What is the difference between Multi-AZ and Read Replicas in RDS?**
Multi-AZ creates a synchronous standby copy in another Availability Zone for high availability/failover (not for scaling reads). Read Replicas are asynchronous copies used to scale out read traffic and can be promoted to standalone databases.

**Q3. How does RDS handle backups?**
RDS supports automated daily backups with point-in-time recovery (within a retention window) and manual snapshots you can take anytime.

**Q4. What happens during an RDS failover in a Multi-AZ setup?**
AWS automatically detects the failure of the primary instance and switches to the standby instance, updating the DNS endpoint so applications reconnect with minimal downtime.

**Q5. Can you SSH into an RDS instance?**
No. RDS is a fully managed service, so AWS manages the underlying OS — you don't get shell access; you only connect via the database engine's port/protocol.

**Q6. What is the difference between RDS and DynamoDB?**
RDS is a managed relational (SQL) database service, while DynamoDB is a managed NoSQL key-value/document database designed for massive scalability and low-latency access.

---

## 8. AWS — Auto Scaling

**Q1. What is Auto Scaling in AWS?**
A service that automatically adjusts the number of EC2 instances in a group based on demand — scaling out (adding instances) under load and scaling in (removing instances) when demand drops, to maintain performance and save cost.

**Q2. What is an Auto Scaling Group (ASG)?**
A logical grouping of EC2 instances that are managed together, with defined minimum, maximum, and desired capacity.

**Q3. What are the types of scaling policies?**
Target tracking (maintain a metric like CPU at a target value), step scaling (scale based on alarm thresholds in steps), scheduled scaling (scale at predicted times), and predictive scaling (uses ML to forecast demand).

**Q4. What is a Launch Template/Launch Configuration?**
A blueprint specifying instance configuration (AMI, instance type, key pair, security groups) used by an Auto Scaling Group to launch new instances. Launch Templates are the newer, more flexible version of Launch Configurations.

**Q5. How does Auto Scaling decide when to add or remove instances?**
It uses CloudWatch alarms/metrics (like average CPU utilization or request count) tied to scaling policies to trigger scale-out or scale-in actions.

**Q6. What is a cooldown period in Auto Scaling?**
A configurable time after a scaling activity during which further scaling actions are paused, to let the system stabilize before reacting again.

---

## 9. AWS — Elastic Load Balancer (ELB)

**Q1. What is a Load Balancer and why is it used?**
A Load Balancer distributes incoming traffic across multiple targets (like EC2 instances) to improve availability, fault tolerance, and performance.

**Q2. What are the types of AWS Load Balancers?**
Application Load Balancer (ALB) — Layer 7, routes based on HTTP/HTTPS content. Network Load Balancer (NLB) — Layer 4, handles high-performance TCP/UDP traffic. Gateway Load Balancer — for third-party virtual appliances. Classic Load Balancer — legacy, rarely used now.

**Q3. What is a Target Group?**
A group of resources (EC2 instances, IPs, or Lambda functions) that a load balancer routes requests to, with its own health check configuration.

**Q4. What is a health check in a Load Balancer?**
A periodic check the load balancer performs on registered targets to determine if they're healthy; unhealthy targets are temporarily removed from receiving traffic.

**Q5. What is the difference between ALB and NLB?**
ALB operates at the application layer and supports content-based routing, path-based/host-based rules, and SSL termination. NLB operates at the transport layer, handles millions of requests per second with ultra-low latency, and preserves the client IP.

**Q6. How does a Load Balancer work with Auto Scaling?**
The Load Balancer distributes traffic to all healthy instances in the Auto Scaling Group, and as the ASG adds/removes instances, they're automatically registered/deregistered from the target group.

---

## 10. AWS — EFS (Elastic File System)

**Q1. What is EFS?**
EFS is a managed, scalable NFS (Network File System) storage service that can be mounted concurrently by multiple EC2 instances, automatically growing/shrinking as you add/remove files.

**Q2. What is the difference between EFS, EBS, and S3?**
EBS is block storage attached to a single EC2 instance at a time. EFS is file storage that multiple instances can mount simultaneously. S3 is object storage accessed via API/HTTP, not mounted as a traditional filesystem.

**Q3. What are the storage classes in EFS?**
Standard (frequently accessed data) and Infrequent Access (IA, for rarely accessed data at lower cost), with lifecycle management to move files between them automatically.

**Q4. When would you choose EFS over EBS?**
When multiple EC2 instances (e.g., a web server fleet) need to read/write the same shared files concurrently, such as shared content directories or application logs.

**Q5. Is EFS regional or zonal?**
EFS is a regional service — it can be mounted from instances across multiple Availability Zones within the same region for high availability.

---

## 11. AWS — S3 (Simple Storage Service)

**Q1. What is S3?**
S3 is a highly durable, scalable object storage service used to store and retrieve any amount of data (files, backups, images, logs) via a simple API, organized into buckets.

**Q2. What is the difference between S3 and EBS?**
S3 stores objects (files) accessed over HTTP/API and isn't tied to a specific instance. EBS is block storage that must be attached to a single EC2 instance like a virtual hard drive.

**Q3. What are S3 storage classes?**
Standard (frequent access), Intelligent-Tiering (auto-moves data based on access patterns), Standard-IA and One Zone-IA (infrequent access, cheaper), Glacier and Glacier Deep Archive (long-term archival, cheapest, slower retrieval).

**Q4. What is S3 bucket versioning?**
A feature that keeps multiple versions of an object in the same bucket, so you can retrieve or restore earlier versions if a file is overwritten or deleted.

**Q5. How do you control access to an S3 bucket?**
Through bucket policies (JSON-based resource policies), IAM policies (attached to users/roles), Access Control Lists (ACLs), and S3 Block Public Access settings.

**Q6. What is the difference between S3 and S3 Glacier?**
S3 (Standard) is for frequently accessed data with millisecond retrieval. S3 Glacier is a low-cost archival storage class meant for data accessed rarely, with retrieval times ranging from minutes to hours.

**Q7. Is data in S3 automatically replicated across Availability Zones?**
Yes, S3 Standard automatically stores data redundantly across multiple Availability Zones within a region for high durability (designed for 99.999999999% durability).

**Q8. What is a pre-signed URL in S3?**
A temporary URL that grants time-limited access to a private S3 object without requiring the requester to have AWS credentials.

---

## 12. AWS — DynamoDB

**Q1. What is DynamoDB?**
A fully managed, serverless NoSQL key-value and document database from AWS, designed for fast, predictable performance at any scale.

**Q2. What is a Partition Key vs. a Sort Key?**
The Partition Key (hash key) determines which partition stores the item and must be unique unless paired with a Sort Key. The Sort Key (range key) allows multiple items with the same partition key, sorted by that key's value.

**Q3. What is the difference between On-Demand and Provisioned capacity modes?**
Provisioned mode requires you to specify read/write capacity units in advance (predictable workloads, cheaper if usage is steady). On-Demand mode automatically scales capacity based on traffic, with pay-per-request pricing (good for unpredictable workloads).

**Q4. What is a Global Secondary Index (GSI)?**
An index with a partition key and sort key different from the base table, allowing you to query data using attributes other than the primary key.

**Q5. What is DynamoDB Streams?**
A feature that captures a time-ordered sequence of item-level changes (insert/update/delete) in a table, which can trigger AWS Lambda functions for event-driven processing.

**Q6. Is DynamoDB a SQL database?**
No, it's a NoSQL database — it doesn't use SQL or traditional joins; queries are based on keys and indexes.

---

## 13. AWS — CloudWatch

**Q1. What is CloudWatch?**
A monitoring and observability service for AWS resources and applications — it collects metrics, logs, and events, and can trigger alarms or automated actions.

**Q2. What is a CloudWatch Alarm?**
A watcher on a specific metric that triggers an action (like sending a notification via SNS or triggering Auto Scaling) when the metric crosses a defined threshold.

**Q3. What is the difference between CloudWatch Logs and CloudWatch Metrics?**
Logs store raw log data sent from applications/services (e.g., EC2, Lambda). Metrics are numerical data points (like CPUUtilization) tracked over time used for monitoring and alarms.

**Q4. What is a CloudWatch Dashboard?**
A customizable visual page where you can display multiple metrics/graphs from different AWS resources in one place for at-a-glance monitoring.

**Q5. What is the CloudWatch Agent used for?**
A software agent installed on EC2 instances or on-premises servers to collect additional system-level metrics (like memory and disk usage) and custom logs that aren't available by default.

**Q6. What is the difference between CloudWatch and CloudTrail?**
CloudWatch focuses on performance monitoring (metrics, logs, alarms). CloudTrail focuses on auditing — logging API calls and user activity across your AWS account for security and compliance.

---

## 14. Docker

**Q1. What is Docker and why is it used?**
Docker is a containerization platform that packages an application with all its dependencies into a lightweight, portable container, ensuring it runs consistently across different environments.

**Q2. What is the difference between a Docker Image and a Docker Container?**
An image is a read-only template/blueprint containing the application code and dependencies. A container is a running (or stopped) instance created from that image.

**Q3. What is a Dockerfile?**
A text file containing a set of instructions (like `FROM`, `RUN`, `COPY`, `CMD`) used to build a Docker image automatically.

**Q4. What is the difference between `CMD` and `ENTRYPOINT` in a Dockerfile?**
`CMD` specifies default arguments/command that can be easily overridden when running the container. `ENTRYPOINT` sets the main command that always runs, with `CMD` often used to supply default arguments to it.

**Q5. What is the difference between a Virtual Machine and a Docker Container?**
A VM virtualizes hardware and includes a full guest OS, making it heavier and slower to start. A container virtualizes at the OS level, sharing the host's kernel, making it lightweight and fast to start.

**Q6. What is Docker Compose?**
A tool for defining and running multi-container Docker applications using a single YAML file (`docker-compose.yml`), where you can configure multiple services, networks, and volumes together.

**Q7. What is a Docker Volume?**
A mechanism for persisting data generated by containers, stored outside the container's writable layer, so data survives even if the container is removed.

**Q8. How do you list running containers?**
`docker ps` lists running containers; `docker ps -a` lists all containers, including stopped ones.

**Q9. What is the difference between `docker stop` and `docker kill`?**
`docker stop` sends a graceful SIGTERM signal (with a timeout before forcing SIGKILL) allowing the app to shut down cleanly. `docker kill` immediately sends SIGKILL, force-stopping the container.

**Q10. What is Docker Hub?**
A public (and private) cloud registry for storing and sharing Docker images, similar to how GitHub hosts code repositories.

---

## 15. Terraform

**Q1. What is Terraform and what problem does it solve?**
Terraform is an open-source Infrastructure as Code (IaC) tool by HashiCorp that lets you define and provision cloud infrastructure (AWS, Azure, GCP, etc.) using declarative configuration files, instead of manually clicking through consoles.

**Q2. What is the difference between Terraform and CloudFormation?**
CloudFormation is AWS-specific IaC. Terraform is cloud-agnostic and can manage infrastructure across multiple providers (AWS, Azure, GCP) using a single, consistent workflow.

**Q3. What is the Terraform state file?**
A file (`terraform.tfstate`) that records the current state of your infrastructure as Terraform understands it, used to map real-world resources to your configuration and detect drift/changes.

**Q4. What is the purpose of `terraform plan`?**
It creates an execution plan, showing what actions (create, update, destroy) Terraform will take to reach the desired state defined in your configuration — without actually making changes.

**Q5. What is the purpose of `terraform apply`?**
It executes the changes proposed in the plan to actually create, update, or destroy real infrastructure resources.

**Q6. What is a Terraform provider?**
A plugin that lets Terraform interact with a specific platform's API (e.g., the AWS provider lets Terraform manage AWS resources).

**Q7. What is the difference between a Terraform module and a resource?**
A resource is a single infrastructure object (like one EC2 instance). A module is a reusable, organized collection of resources (and variables/outputs) that can be called multiple times with different inputs.

**Q8. What is `terraform destroy` used for?**
It removes all resources defined and tracked in the Terraform state, effectively tearing down the infrastructure that was created.

**Q9. What are Terraform variables and outputs used for?**
Variables (`variable` blocks) let you parameterize configurations so they're reusable with different values. Outputs (`output` blocks) expose specific values (like an instance's public IP) after `apply`, useful for chaining or display.

**Q10. What happens if two people run `terraform apply` at the same time without remote state locking?**
It can cause state file corruption or conflicting changes, since both could modify the same state simultaneously — this is why remote backends (like an S3 bucket with DynamoDB for state locking) are recommended for team environments.

---

### Quick Tips for the Interview
- For freshers, interviewers usually focus more on **concepts and "why"** rather than deep edge cases — be ready to explain things simply, with an example if possible.
- It's fine to say "I haven't used that in production, but I understand the concept as..." — honesty paired with solid fundamentals goes a long way.
- Practice explaining things out loud, not just reading — interviewers often ask quick follow-ups like "why would you use X over Y?"
