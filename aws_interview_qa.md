# AWS Interview Questions & Answers

Topics covered: EC2, ECS/Fargate, ECR, Lambda, ALB, VPC, RDS, S3, IAM, CloudFront, Route 53, SNS, SQS, EventBridge, CloudWatch
(50 Questions & Answers per topic)

---

## 1. EC2 (Elastic Compute Cloud)

**Q1. What is Amazon EC2?**
A: EC2 is a web service that provides resizable virtual servers (instances) in the AWS cloud, allowing users to run applications without owning physical hardware.

**Q2. What are EC2 instance types based on?**
A: They are based on the combination of CPU, memory, storage, and networking capacity, grouped into families like General Purpose, Compute Optimized, Memory Optimized, Storage Optimized, and Accelerated Computing.

**Q3. What is an AMI?**
A: Amazon Machine Image (AMI) is a template that contains the OS, application server, and applications needed to launch an EC2 instance.

**Q4. What is the difference between On-Demand, Reserved, and Spot Instances?**
A: On-Demand charges by the hour/second with no commitment; Reserved Instances offer discounts for 1 or 3-year commitments; Spot Instances offer unused capacity at a large discount but can be reclaimed by AWS.

**Q5. What is EC2 Auto Scaling?**
A: A service that automatically adjusts the number of EC2 instances in a group based on demand, health checks, or a defined schedule.

**Q6. What is a Launch Template?**
A: A reusable configuration (AMI, instance type, key pair, security groups, etc.) used to launch EC2 instances consistently, including with Auto Scaling.

**Q7. What is an EC2 instance's security group?**
A: A virtual firewall that controls inbound and outbound traffic at the instance level using allow rules.

**Q8. Can security groups have deny rules?**
A: No, security groups only support allow rules; they are stateful, meaning return traffic is automatically allowed.

**Q9. What is the difference between Security Groups and Network ACLs?**
A: Security Groups are stateful and operate at the instance level; Network ACLs are stateless and operate at the subnet level, supporting both allow and deny rules.

**Q10. What are EC2 instance store volumes?**
A: Temporary block-level storage physically attached to the host machine; data is lost when the instance stops or terminates.

**Q11. What is EBS?**
A: Elastic Block Store is persistent block storage that can be attached to EC2 instances and retains data independently of the instance lifecycle.

**Q12. What are the types of EBS volumes?**
A: gp3/gp2 (General Purpose SSD), io1/io2 (Provisioned IOPS SSD), st1 (Throughput Optimized HDD), and sc1 (Cold HDD).

**Q13. Can an EBS volume be attached to multiple instances?**
A: Only io1/io2 volumes support Multi-Attach, allowing attachment to multiple instances in the same Availability Zone simultaneously.

**Q14. What is an EC2 key pair used for?**
A: It is used for secure SSH (Linux) or RDP password decryption (Windows) login authentication to an instance.

**Q15. What is the difference between stopping and terminating an EC2 instance?**
A: Stopping preserves the instance and its EBS volumes for later restart; terminating permanently deletes the instance and, by default, its root EBS volume.

**Q16. What is an Elastic IP?**
A: A static, public IPv4 address that can be allocated to your account and associated with an EC2 instance, remaining fixed even if the instance restarts.

**Q17. What is EC2 placement group?**
A: A logical grouping of instances to influence their placement strategy: Cluster (low latency, same rack), Spread (across distinct hardware), or Partition (grouped across partitions for large distributed workloads).

**Q18. What is a Spot Instance interruption?**
A: When AWS reclaims a Spot Instance due to capacity needs, giving a two-minute warning before termination or stopping.

**Q19. What is an Instance Profile?**
A: A container that passes an IAM role to an EC2 instance, allowing applications on it to make authenticated AWS API calls.

**Q20. What is EC2 User Data?**
A: A script or set of commands that runs once at instance launch, commonly used for bootstrapping configuration.

**Q21. What is the difference between EC2 Metadata and User Data?**
A: Metadata provides information about the instance itself (accessible via 169.254.169.254), while User Data is custom data/scripts supplied at launch for initialization.

**Q22. What is IMDSv2?**
A: A more secure, session-oriented version of the Instance Metadata Service that requires token-based requests to prevent SSRF-based metadata theft.

**Q23. What is a Dedicated Host vs Dedicated Instance?**
A: A Dedicated Host is a physical server fully dedicated to your use with visibility into sockets/cores (useful for license needs); a Dedicated Instance runs on hardware dedicated to a single customer but shares the physical server with other instances of that same account.

**Q24. What is EC2 hibernation?**
A: A feature that saves the in-memory (RAM) state to the EBS root volume when stopping, allowing faster resume compared to a cold boot.

**Q25. What are EC2 tenancy options?**
A: Shared (default, multi-tenant hardware), Dedicated Instance, and Dedicated Host.

**Q26. What is an Elastic Network Interface (ENI)?**
A: A virtual network card that can be attached to an EC2 instance, allowing multiple IPs, security groups, and network interfaces per instance.

**Q27. How does EC2 Auto Scaling determine instance health?**
A: It uses EC2 status checks and, optionally, ELB health checks to determine if an instance is unhealthy and needs replacement.

**Q28. What is a Scaling Policy in Auto Scaling?**
A: Rules that define how Auto Scaling should scale, such as Target Tracking, Step Scaling, or Simple Scaling based on CloudWatch metrics.

**Q29. What is the default termination policy in an Auto Scaling Group?**
A: It terminates instances based on factors like the oldest launch configuration, closest to the next billing hour, and balancing across Availability Zones.

**Q30. What is an EC2 Reserved Instance's "Convertible" type?**
A: A Reserved Instance type that allows changing instance family, OS, or tenancy during the term in exchange for a different discount level than Standard RIs.

**Q31. What is a Savings Plan?**
A: A flexible pricing model offering lower rates in exchange for a committed usage amount (in $/hour) over 1 or 3 years, applicable across EC2, Fargate, and Lambda.

**Q32. How do you resize an EC2 instance?**
A: Stop the instance, change the instance type via the console/CLI, and start it again (note: instance store data is lost on stop).

**Q33. What is EC2 instance status check?**
A: AWS-performed checks including System Status Check (underlying hardware/host) and Instance Status Check (software/network config of the instance itself).

**Q34. What is a Bastion Host?**
A: An EC2 instance placed in a public subnet used as a secure gateway to access instances in private subnets.

**Q35. What is the difference between gp2 and gp3 EBS volumes?**
A: gp3 allows provisioning IOPS and throughput independently of volume size, generally at a lower cost than gp2, which ties performance to volume size.

**Q36. What is EBS snapshot?**
A: A point-in-time, incremental backup of an EBS volume stored in S3, usable to create new volumes or restore data.

**Q37. Are EBS snapshots incremental?**
A: Yes, after the first full snapshot, subsequent snapshots only save the changed blocks.

**Q38. What is the purpose of an EC2 Capacity Reservation?**
A: It reserves compute capacity for a specific AZ and instance type for any duration, without requiring a long-term commitment like RIs.

**Q39. What is a Spot Fleet?**
A: A collection of Spot (and optionally On-Demand) Instances launched based on criteria you specify, aiming to meet a target capacity at the lowest cost.

**Q40. What is EC2 instance metadata used for commonly?**
A: Retrieving instance ID, AMI ID, IAM role credentials, public/private IPs, and other launch details programmatically from within the instance.

**Q41. What is a warm pool in Auto Scaling?**
A: A pool of pre-initialized EC2 instances kept in a stopped or running state to reduce launch latency when scaling out.

**Q42. What are EC2 On-Demand Capacity Reservations combined with Savings Plans used for?**
A: To guarantee capacity in a specific AZ while still benefiting from discounted Savings Plan pricing.

**Q43. What is the maximum number of Elastic IPs per account by default?**
A: 5 per region by default, though this limit can be increased via a support request.

**Q44. How do you achieve high availability with EC2?**
A: By deploying instances across multiple Availability Zones behind a load balancer, combined with Auto Scaling.

**Q45. What is the difference between an EBS-backed and Instance Store-backed AMI?**
A: EBS-backed AMIs use EBS volumes as the root device (persistent, can stop/start), while Instance Store-backed AMIs use ephemeral local storage (cannot be stopped, only terminated).

**Q46. What is EC2 Image Builder?**
A: A service that automates the creation, testing, and maintenance of golden AMIs.

**Q47. What is Nitro System?**
A: AWS's underlying platform for modern EC2 instances that offloads virtualization functions to dedicated hardware, improving performance and security.

**Q48. What happens to data on an attached EBS volume when an EC2 instance is terminated?**
A: By default, the root EBS volume is deleted on termination, but additional attached EBS volumes are preserved unless configured otherwise ("Delete on Termination" flag).

**Q49. What is the purpose of an EC2 Elastic Network Adapter (ENA)?**
A: It provides enhanced networking capabilities delivering higher bandwidth and lower latency compared to standard networking.

**Q50. How can you monitor EC2 instance performance?**
A: Using Amazon CloudWatch metrics (CPU, network, disk), CloudWatch Agent for custom/OS-level metrics, and status checks.

---

## 2. ECS / Fargate (Elastic Container Service)

**Q1. What is Amazon ECS?**
A: A fully managed container orchestration service that lets you run, stop, and manage Docker containers on a cluster.

**Q2. What is a Task Definition in ECS?**
A: A JSON blueprint describing one or more containers, their images, CPU/memory, networking, and IAM roles needed to run a task.

**Q3. What is an ECS Task?**
A: An instantiation of a Task Definition, representing one or more running containers.

**Q4. What is an ECS Service?**
A: A construct that maintains a specified number of running tasks, handles load balancer registration, and replaces failed tasks automatically.

**Q5. What is the difference between EC2 launch type and Fargate launch type in ECS?**
A: EC2 launch type runs containers on self-managed EC2 instances registered to the cluster; Fargate is serverless, and AWS manages the underlying infrastructure.

**Q6. What is AWS Fargate?**
A: A serverless compute engine for containers that removes the need to provision or manage servers, letting you specify CPU/memory per task.

**Q7. What is an ECS Cluster?**
A: A logical grouping of tasks or services, which can run on EC2 instances or Fargate.

**Q8. What is the ECS Container Agent?**
A: Software that runs on each EC2 instance in an ECS cluster, allowing it to connect to the cluster and manage containers (not needed for Fargate).

**Q9. What is a Task Role vs Task Execution Role in ECS?**
A: Task Role grants permissions to the application code running inside the container; Task Execution Role grants ECS permissions to pull images and write logs on your behalf.

**Q10. What networking modes does ECS support?**
A: bridge, host, awsvpc, and none; Fargate requires awsvpc mode.

**Q11. What is awsvpc networking mode?**
A: A mode that gives each task its own Elastic Network Interface (ENI) with a private IP address, isolating networking per task.

**Q12. How does ECS Service Auto Scaling work?**
A: It uses Application Auto Scaling with CloudWatch metrics (like CPU/memory utilization or request count) to scale the desired task count up or down.

**Q13. What is a Capacity Provider in ECS?**
A: A mechanism that manages the infrastructure (EC2 Auto Scaling Group or Fargate) used by a cluster to run tasks, allowing mixed capacity strategies.

**Q14. What is the difference between ECS and EKS?**
A: ECS is AWS's proprietary container orchestrator, while EKS is a managed Kubernetes service; ECS is simpler, EKS offers Kubernetes-native tooling and portability.

**Q15. How does ECS handle service discovery?**
A: Through AWS Cloud Map integration, which creates DNS records allowing services to discover each other.

**Q16. What is a Sidecar container pattern in ECS?**
A: Running a helper container (e.g., logging agent, proxy) alongside the main application container within the same task.

**Q17. What is Fargate Spot?**
A: A pricing option that runs Fargate tasks on spare capacity at a discount, suitable for fault-tolerant workloads.

**Q18. How do you deploy updates to an ECS service with zero downtime?**
A: Using a rolling update deployment or blue/green deployment (via CodeDeploy) that gradually replaces old tasks with new ones behind a load balancer.

**Q19. What is the ECS deployment circuit breaker?**
A: A feature that automatically rolls back a service deployment if it fails to reach a steady state, preventing prolonged outages.

**Q20. How does ECS integrate with Application Load Balancer?**
A: ECS services register/deregister tasks as targets in an ALB target group dynamically as tasks start and stop.

**Q21. What is the purpose of health checks in an ECS service?**
A: To determine whether a task is healthy; unhealthy tasks are stopped and replaced automatically by the service scheduler.

**Q22. What is the maximum number of containers per ECS task?**
A: ECS supports up to 10 containers per task definition (soft limit, can be increased).

**Q23. What are ECS placement strategies?**
A: Rules like "binpack," "random," and "spread" that determine how tasks are placed across container instances (EC2 launch type).

**Q24. What is an ECS placement constraint?**
A: Rules that limit where tasks can be placed, such as on specific instance types or based on custom attributes.

**Q25. Can Fargate tasks access an on-premises network?**
A: Yes, through VPC connectivity, using PrivateLink, Direct Connect, or VPN configured on the VPC hosting the Fargate tasks.

**Q26. What log driver is commonly used with ECS/Fargate?**
A: The awslogs driver, which sends container logs to CloudWatch Logs.

**Q27. What is ECS Exec?**
A: A feature that allows running interactive commands or getting a shell inside a running ECS container for debugging purposes.

**Q28. How is persistent storage handled in Fargate tasks?**
A: Through Amazon EFS integration, which allows Fargate tasks to mount durable, shared file storage.

**Q29. What is the difference between "desired count" and "running count" in an ECS service?**
A: Desired count is the target number of tasks configured; running count is the actual number of tasks currently running.

**Q30. How do you pass secrets to ECS containers securely?**
A: By referencing AWS Secrets Manager or SSM Parameter Store values in the task definition, which are injected as environment variables at runtime.

**Q31. What is Fargate task sizing based on?**
A: Predefined combinations of vCPU and memory selected per task, since Fargate does not use underlying EC2 instance types.

**Q32. What happens if an ECS task fails a health check?**
A: The scheduler stops the unhealthy task and launches a replacement to maintain the desired count.

**Q33. What is the difference between "REPLICA" and "DAEMON" scheduling strategy in ECS?**
A: REPLICA runs and maintains a specified number of tasks across the cluster; DAEMON runs exactly one task on each active container instance (EC2 launch type only).

**Q34. Can you run ECS tasks on a schedule?**
A: Yes, using EventBridge Scheduled Rules to trigger ECS RunTask at defined intervals.

**Q35. What is the role of the ECS Scheduler?**
A: It places tasks onto container instances based on placement strategies/constraints and maintains the desired service state.

**Q36. What is Amazon ECS Anywhere?**
A: A feature that allows running ECS tasks on customer-managed infrastructure outside of AWS, such as on-premises servers.

**Q37. How is scaling different between Fargate and EC2 launch type?**
A: Fargate scales tasks without concern for underlying instance capacity, whereas EC2 launch type requires the underlying Auto Scaling Group to have sufficient instance capacity.

**Q38. What is a target group's deregistration delay used for in ECS deployments?**
A: It allows in-flight requests to complete before a task is deregistered and stopped during deployment or scale-in.

**Q39. What IAM entity does Fargate use to pull images from ECR?**
A: The Task Execution Role, which must have permissions like ecr:GetDownloadUrlForLayer and ecr:BatchGetImage.

**Q40. How can you control the number of tasks per Availability Zone?**
A: By configuring placement strategies (spread by AZ) or relying on awsvpc mode with subnets across multiple AZs.

**Q41. What is Blue/Green deployment via CodeDeploy for ECS?**
A: A deployment strategy where a new task set is created alongside the old one, traffic is shifted gradually or all at once, and the old set is terminated after validation.

**Q42. What is the purpose of "essential" flag in a container definition?**
A: If an essential container stops or fails, the entire task is stopped; non-essential containers can fail without stopping the task.

**Q43. How does ECS support GPU workloads?**
A: By using EC2 launch type with GPU-enabled instances (like p3/g4) and configuring resource requirements in the task definition (not supported on Fargate for GPU, except specific configurations).

**Q44. What is the significance of task definition revisions?**
A: Each update to a task definition creates a new immutable revision, allowing rollback to previous versions if needed.

**Q45. How do ECS services integrate with CloudWatch Container Insights?**
A: Container Insights collects and aggregates metrics and logs from ECS clusters, tasks, and containers for monitoring and troubleshooting.

**Q46. What is the minimum billing granularity for Fargate?**
A: Fargate bills per second, with a one-minute minimum charge, based on vCPU and memory resources requested.

**Q47. Can an ECS Service span multiple subnets and AZs?**
A: Yes, tasks can be distributed across multiple subnets/AZs specified in the service's network configuration for high availability.

**Q48. What is a task's "stopped reason" used for?**
A: It provides diagnostic information explaining why an ECS task stopped, useful for troubleshooting deployment or runtime failures.

**Q49. How do you restrict outbound internet access for Fargate tasks?**
A: By placing tasks in private subnets with no route to an Internet Gateway, and using a NAT Gateway or VPC endpoints for necessary outbound access.

**Q50. What is the benefit of using Fargate over EC2 launch type?**
A: No server management, automatic scaling of infrastructure, and billing based only on resources consumed by tasks rather than provisioned instances.

---

## 3. ECR (Elastic Container Registry)

**Q1. What is Amazon ECR?**
A: A fully managed Docker container registry service that lets you store, manage, and deploy container images.

**Q2. What are the two types of repositories in ECR?**
A: Private repositories (access controlled via IAM) and Public repositories (via ECR Public Gallery, accessible to anyone).

**Q3. How does authentication work with ECR?**
A: Using the AWS CLI command `aws ecr get-login-password`, which returns a temporary token used to authenticate Docker to the registry.

**Q4. What is image scanning in ECR?**
A: A feature that scans container images for software vulnerabilities using Basic scanning (Clair-based) or Enhanced scanning (via Amazon Inspector).

**Q5. What is ECR lifecycle policy?**
A: A set of rules that automatically expire/clean up old or untagged images based on age or count, to manage storage costs.

**Q6. Is ECR data encrypted?**
A: Yes, images are encrypted at rest by default using AES-256 (SSE-S3) or optionally with SSE-KMS.

**Q7. How do you push an image to ECR?**
A: Authenticate Docker to ECR, tag the local image with the repository URI, then run `docker push <repository-uri>:<tag>`.

**Q8. What is image tag immutability in ECR?**
A: A repository setting that prevents overwriting an existing image tag, ensuring a tag always refers to the same image.

**Q9. Can ECR replicate images across regions?**
A: Yes, using ECR Cross-Region and Cross-Account Replication, images can automatically be copied to other regions/accounts.

**Q10. What is the pricing model for ECR?**
A: Charges are based on the amount of data stored per month and data transfer, with a free tier available.

**Q11. How does IAM control access to ECR repositories?**
A: Through IAM policies and repository policies specifying who can push, pull, or manage specific repositories.

**Q12. What is the difference between ECR Public and Docker Hub?**
A: ECR Public is AWS-managed with integration into AWS IAM and no pull-rate throttling for AWS-authenticated pulls, while Docker Hub is a third-party registry with its own rate limits.

**Q13. How does ECS/EKS pull images from ECR?**
A: Via the Task Execution Role (ECS) or node IAM role (EKS) that has permissions to authenticate and pull from the ECR repository.

**Q14. What is a repository policy in ECR?**
A: A resource-based JSON policy attached to a specific repository controlling cross-account or specific principal access.

**Q15. Can you use ECR with Docker Compose?**
A: Yes, by referencing the full ECR image URI in the Compose file after authenticating Docker to the registry.

**Q16. What is "Enhanced scanning" in ECR?**
A: Continuous vulnerability scanning powered by Amazon Inspector that automatically rescans images when new CVEs are published.

**Q17. What image formats does ECR support?**
A: Docker images and OCI (Open Container Initiative) compliant images and artifacts.

**Q18. How can you automate ECR image builds and pushes?**
A: Using CI/CD pipelines like CodePipeline/CodeBuild, GitHub Actions, or Jenkins that build and push images programmatically.

**Q19. What happens if you exceed storage limits in ECR?**
A: There is no hard storage limit; you are billed per GB stored, so cost increases but pushes are not blocked (unless account-level quotas are hit).

**Q20. What is the significance of the image digest in ECR?**
A: A unique SHA256 hash that identifies an image's content precisely, useful for immutable references beyond mutable tags.

**Q21. Can ECR repositories be private within a VPC only?**
A: Yes, using VPC Endpoints (Interface endpoints) for ECR API and Docker registry (ecr.api, ecr.dkr) to keep traffic within AWS's network.

**Q22. What is the maximum image size supported by ECR?**
A: Individual image layers can be up to 10 GB, sufficient for most container use cases.

**Q23. How do you delete an image from ECR?**
A: Using `aws ecr batch-delete-image` specifying the repository and image tag/digest, or through the console.

**Q24. What is a "manifest list" in ECR?**
A: A multi-architecture image manifest that allows one tag to reference multiple platform-specific images (e.g., amd64, arm64).

**Q25. Does ECR support Helm charts?**
A: Yes, ECR can act as an OCI-compliant registry for storing Helm charts.

**Q26. What is the benefit of ECR's integration with IAM over managing separate registry credentials?**
A: It eliminates the need for separate registry usernames/passwords, using short-lived IAM-based tokens for secure, auditable access.

**Q27. How can you monitor ECR usage?**
A: Using CloudWatch metrics for repository size/count and CloudTrail for API call auditing.

**Q28. What is the "untagged image" cleanup strategy commonly used?**
A: Lifecycle policies that expire untagged images after a certain number of days to prevent storage bloat from CI/CD pipeline pushes.

**Q29. Can you scan images on push automatically?**
A: Yes, by enabling "Scan on Push" configuration on the repository.

**Q30. What's the maximum number of repositories per account in ECR?**
A: There's a default soft limit (e.g., 10,000 repositories), which can be increased via a service quota request.

**Q31. What is ECR Pull Through Cache?**
A: A feature that automatically caches images from upstream public registries (like Docker Hub, Quay) into your private ECR repository on first pull.

**Q32. How does cross-account access to ECR work?**
A: By adding a repository policy granting specific AWS account principals permission to pull or push images.

**Q33. What CLI command lists images in a repository?**
A: `aws ecr list-images --repository-name <name>`.

**Q34. Can Lambda use container images stored in ECR?**
A: Yes, Lambda supports deploying functions as container images (up to 10GB) pulled directly from ECR.

**Q35. What is the "KMS encryption" option in ECR used for?**
A: It allows using a customer-managed KMS key instead of the default AWS-managed key to encrypt image data at rest.

**Q36. How do you tag an image for ECR before pushing?**
A: `docker tag local-image:tag aws_account_id.dkr.ecr.region.amazonaws.com/repo-name:tag`.

**Q37. What's the difference between a repository and a registry in ECR?**
A: A registry is the top-level account-specific endpoint hosting all repositories; a repository is a specific collection of related container images.

**Q38. Does ECR support image signing?**
A: Yes, through integration with tools like Notation and AWS Signer for content trust and supply chain security.

**Q39. What is the typical workflow to deploy an updated image to ECS via ECR?**
A: Build → tag → push to ECR → update ECS task definition with new image URI/tag → update the ECS service to trigger a new deployment.

**Q40. Can you restrict which IAM roles can pull images from a specific ECR repository?**
A: Yes, using a combination of IAM policies and repository resource policies scoped to specific roles or accounts.

**Q41. What happens to replicated images if the source image is deleted?**
A: Replicated images in destination repositories remain independent; deleting the source does not automatically delete replicas.

**Q42. What is the benefit of using immutable tags in production repositories?**
A: It prevents accidental overwrites of a deployed image version, improving deployment traceability and rollback reliability.

**Q43. How does ECR handle multi-architecture images for ARM and x86?**
A: Through manifest lists/OCI image indexes that let a single tag resolve to the correct architecture-specific image at pull time.

**Q44. What logging service captures ECR API activity?**
A: AWS CloudTrail logs all ECR API calls for auditing and compliance purposes.

**Q45. Can you set a default lifecycle policy across multiple new repositories?**
A: Yes, using a Registry-level lifecycle policy template that applies to newly created repositories matching a pattern.

**Q46. What is the significance of "least privilege" for ECR IAM policies?**
A: Restricting permissions (e.g., only allow pull, not push/delete) to service roles reduces the risk of unauthorized image tampering.

**Q47. Can EKS pods authenticate to ECR without static credentials?**
A: Yes, using IAM Roles for Service Accounts (IRSA) which grants pods temporary credentials to pull images.

**Q48. What is the typical retention strategy for CI-built images?**
A: Keep a limited number of recent tagged images (e.g., last 10) and expire untagged/old images automatically via lifecycle rules.

**Q49. How can you reduce ECR storage costs?**
A: By using multi-stage Docker builds to reduce image size, applying lifecycle policies, and removing unused repositories.

**Q50. Is ECR available in all AWS Regions?**
A: ECR is available in most AWS commercial regions, with ECR Public hosted primarily in us-east-1 but accessible globally.

---

## 4. Lambda

**Q1. What is AWS Lambda?**
A: A serverless compute service that runs code in response to events without provisioning or managing servers, charging only for actual execution time.

**Q2. What programming languages does Lambda support?**
A: Node.js, Python, Java, Go, .NET (C#), Ruby, and custom runtimes via the Lambda Runtime API, plus container images.

**Q3. What is a Lambda handler?**
A: The function entry point that AWS Lambda invokes to start execution, receiving event and context objects as parameters.

**Q4. What is the maximum execution timeout for a Lambda function?**
A: 15 minutes (900 seconds).

**Q5. What is Lambda cold start?**
A: The latency incurred when a new execution environment is initialized to handle a request, as opposed to reusing a "warm" environment.

**Q6. How can you reduce Lambda cold start latency?**
A: By using Provisioned Concurrency, minimizing package size, choosing lighter runtimes, and reducing initialization code outside the handler.

**Q7. What is Provisioned Concurrency?**
A: A feature that keeps a specified number of execution environments initialized and ready to respond immediately, avoiding cold starts.

**Q8. What is the maximum memory allocation for a Lambda function?**
A: Up to 10,240 MB (10 GB), with CPU power scaling proportionally to memory allocated.

**Q9. What is a Lambda Layer?**
A: A ZIP archive containing shared code or dependencies that can be attached to multiple Lambda functions to avoid duplication.

**Q10. What is the difference between synchronous and asynchronous Lambda invocation?**
A: Synchronous invocation waits for a response (e.g., API Gateway); asynchronous invocation queues the event and returns immediately, with Lambda processing it separately (e.g., S3 events, SNS).

**Q11. What happens when an asynchronous Lambda invocation fails?**
A: Lambda retries automatically (default up to 2 times) and can route failed events to a Dead Letter Queue (DLQ) or Lambda Destinations.

**Q12. What are Lambda Destinations?**
A: A feature that routes the result of an asynchronous invocation (success or failure) to a target like SQS, SNS, another Lambda, or EventBridge.

**Q13. What is a Dead Letter Queue (DLQ) in the context of Lambda?**
A: An SQS queue or SNS topic that captures events that fail processing after all retry attempts, for later analysis.

**Q14. What is the maximum deployment package size for Lambda?**
A: 50 MB (zipped, direct upload), 250 MB (unzipped, including layers), or up to 10 GB for container images.

**Q15. How does Lambda scale?**
A: Automatically, by creating new execution environments in parallel to handle concurrent invocations, up to the account/function concurrency limit.

**Q16. What is Reserved Concurrency in Lambda?**
A: A setting that reserves a specific portion of the account's concurrency limit exclusively for a function, also capping its maximum concurrent executions.

**Q17. What is the default concurrency limit per AWS account for Lambda?**
A: 1,000 concurrent executions per region by default (can be increased via a support request).

**Q18. What is an execution context in Lambda?**
A: The runtime environment that manages resources like temp storage and network connections, which can be reused across invocations for performance benefits.

**Q19. How can Lambda functions access resources inside a VPC?**
A: By configuring the function with VPC settings (subnets, security groups), which attaches an ENI to allow access to private VPC resources.

**Q20. What is a common downside of placing Lambda in a VPC?**
A: Potentially increased cold start latency historically (largely mitigated by Hyperplane ENIs now) and the need for NAT Gateway for internet access.

**Q21. What is the /tmp directory in Lambda used for?**
A: Ephemeral storage (up to 10 GB configurable) available during a single execution environment's lifetime for temporary file operations.

**Q22. What is Lambda@Edge?**
A: A feature that lets you run Lambda functions at CloudFront edge locations to customize content closer to users with low latency.

**Q23. What triggers can invoke a Lambda function?**
A: S3 events, API Gateway, DynamoDB Streams, SNS, SQS, EventBridge, Kinesis, CloudWatch Events/Alarms, ALB, and many more.

**Q24. How does Lambda integrate with API Gateway?**
A: API Gateway can trigger Lambda synchronously via Lambda Proxy Integration, passing the HTTP request as an event and returning the Lambda's response as the HTTP response.

**Q25. What is the purpose of environment variables in Lambda?**
A: To pass configuration data to the function code without hardcoding values, optionally encrypted with KMS.

**Q26. What IAM role is required for a Lambda function?**
A: An execution role that grants the function permissions to interact with other AWS services and write logs to CloudWatch.

**Q27. How does Lambda handle concurrency with SQS as a trigger?**
A: Lambda polls the SQS queue and scales the number of concurrent pollers based on queue depth, up to the function's concurrency limit.

**Q28. What is the difference between Lambda versions and aliases?**
A: A version is an immutable snapshot of function code/config; an alias is a pointer to a specific version (or split traffic between versions) allowing flexible deployment strategies.

**Q29. What is Lambda's traffic shifting / canary deployment feature?**
A: Using weighted aliases (or with CodeDeploy) to gradually shift a percentage of traffic from an old version to a new version.

**Q30. What is X-Ray used for with Lambda?**
A: AWS X-Ray provides distributed tracing to visualize and debug the performance and behavior of Lambda functions within a request flow.

**Q31. How does Lambda pricing work?**
A: Billed based on the number of requests and the duration of execution (GB-seconds), with a generous free tier.

**Q32. What is the difference between event source mapping and direct invocation?**
A: Event source mapping is a Lambda-managed poller (used for streams like DynamoDB/Kinesis/SQS) that reads from the source and invokes the function; direct invocation is triggered directly by another service or API call.

**Q33. Can Lambda functions be deployed as container images?**
A: Yes, Lambda supports packaging functions as container images (up to 10 GB) stored in ECR, using the Lambda Runtime API.

**Q34. What is the maximum number of layers a Lambda function can use?**
A: Up to 5 layers per function.

**Q35. How do you handle secrets securely in Lambda?**
A: By retrieving them at runtime from AWS Secrets Manager or SSM Parameter Store rather than storing them as plain environment variables.

**Q36. What is the purpose of the "context" object passed to a handler?**
A: It provides runtime information such as remaining execution time, function name, memory limit, and request ID.

**Q37. What happens if a Lambda function exceeds its memory limit?**
A: The function is terminated with an "Out of Memory" error.

**Q38. How does Lambda integrate with Step Functions?**
A: Step Functions can orchestrate multiple Lambda functions as states in a workflow, handling retries, error handling, and parallel execution.

**Q39. What is the significance of idempotency in Lambda functions?**
A: Since events may be retried (especially async or stream-based), functions should be designed to safely process the same event multiple times without unintended side effects.

**Q40. What is the batch size parameter in event source mappings?**
A: It controls how many records (e.g., from SQS, Kinesis, DynamoDB Streams) are sent to a single Lambda invocation.

**Q41. How can you monitor Lambda function errors and performance?**
A: Using CloudWatch Logs for execution logs, CloudWatch Metrics (Invocations, Errors, Duration, Throttles), and CloudWatch Alarms.

**Q42. What causes a Lambda "Throttle" error?**
A: When the number of concurrent invocations exceeds the account or function's concurrency limit.

**Q43. What is Graviton support in Lambda?**
A: Lambda supports ARM-based AWS Graviton2 processors, which can offer better price-performance for many workloads compared to x86.

**Q44. Can Lambda functions call other Lambda functions?**
A: Yes, using the AWS SDK to invoke another function synchronously or asynchronously, though tight coupling like this is often discouraged in favor of Step Functions or events.

**Q45. What is a Function URL in Lambda?**
A: A built-in HTTPS endpoint directly on a Lambda function, allowing invocation without needing API Gateway.

**Q46. How does Lambda ensure high availability?**
A: By automatically running across multiple Availability Zones within a region without requiring manual configuration.

**Q47. What is the /var/task directory in a Lambda execution environment?**
A: The read-only directory where the deployment package (function code) is extracted and available during execution.

**Q48. How do you optimize Lambda function performance for cost?**
A: Right-sizing memory allocation (which also scales CPU), minimizing execution duration, using Provisioned Concurrency judiciously, and avoiding unnecessary VPC attachment.

**Q49. What is a "poison pill" message in the context of Lambda and streams?**
A: A malformed or persistently failing record in a stream (like Kinesis/DynamoDB) that repeatedly causes processing failures and can block the shard iterator if not handled with bisecting/retry limits.

**Q50. Can Lambda functions have multiple triggers?**
A: Yes, a single Lambda function can be configured with multiple event sources/triggers simultaneously.

---

## 5. ALB (Application Load Balancer)

**Q1. What is an Application Load Balancer?**
A: A Layer 7 (HTTP/HTTPS) load balancer that routes traffic to targets based on the content of the request, such as path, host, or headers.

**Q2. What are the types of AWS Elastic Load Balancers?**
A: Application Load Balancer (ALB), Network Load Balancer (NLB), Gateway Load Balancer (GWLB), and the legacy Classic Load Balancer (CLB).

**Q3. What is a Target Group in ALB?**
A: A logical grouping of registered targets (EC2 instances, IPs, Lambda functions, or containers) that the ALB routes requests to.

**Q4. What routing capabilities does ALB support?**
A: Path-based routing, host-based routing, HTTP header/method-based routing, query string routing, and source IP-based routing.

**Q5. What target types are supported by ALB target groups?**
A: Instance (EC2 instance ID), IP (private IP address), and Lambda function.

**Q6. What is a Listener in ALB?**
A: A process that checks for connection requests on a configured protocol and port (e.g., HTTP:80, HTTPS:443) and forwards them based on rules.

**Q7. What is a Listener Rule?**
A: A rule attached to a listener that defines conditions (path, host, etc.) and an action (forward, redirect, fixed-response) for matching requests.

**Q8. How does ALB perform health checks?**
A: It periodically sends requests (HTTP/HTTPS) to targets on a specified path and port, marking targets healthy or unhealthy based on the response.

**Q9. What is Sticky Sessions (session affinity) in ALB?**
A: A feature that binds a user's session to a specific target using cookies, ensuring subsequent requests go to the same backend instance.

**Q10. Does ALB support WebSocket connections?**
A: Yes, ALB natively supports WebSocket and HTTP/2 protocols.

**Q11. How does ALB handle SSL/TLS termination?**
A: ALB can terminate SSL/TLS at the load balancer using an ACM certificate, then optionally re-encrypt traffic to targets or forward it as plain HTTP.

**Q12. What is SNI (Server Name Indication) support in ALB?**
A: It allows an ALB listener to host multiple SSL certificates for different domains on the same HTTPS listener/port.

**Q13. Can ALB route traffic to multiple target groups from a single listener?**
A: Yes, using content-based routing rules to forward requests to different target groups based on conditions.

**Q14. What is the difference between ALB and NLB in terms of layer?**
A: ALB operates at Layer 7 (application layer) understanding HTTP/HTTPS content; NLB operates at Layer 4 (transport layer) handling TCP/UDP with ultra-low latency.

**Q15. Does ALB have a static IP address?**
A: No, ALB uses DNS names and its IP addresses can change; for static IP requirements, NLB or an Elastic IP behind NLB is used.

**Q16. What is cross-zone load balancing in ALB?**
A: A feature (enabled by default in ALB) that distributes traffic evenly across all registered targets in all enabled Availability Zones, regardless of which AZ the load balancer node received the request in.

**Q17. What is the purpose of an ALB security group?**
A: It controls which inbound traffic (e.g., from the internet) is allowed to reach the load balancer, which then forwards allowed traffic to targets.

**Q18. How does ALB integrate with AWS WAF?**
A: AWS WAF can be attached directly to an ALB to filter malicious traffic (SQL injection, XSS, rate limiting) before it reaches targets.

**Q19. What is a Fixed-response action in ALB?**
A: A listener rule action that returns a custom HTTP response (status code, body, content type) directly from the load balancer without forwarding to a target.

**Q20. What is a Redirect action in ALB?**
A: A listener rule action that redirects the client to another URL, commonly used to redirect HTTP to HTTPS.

**Q21. How does ALB support containerized applications?**
A: By using dynamic port mapping with ECS, where target groups can register tasks on dynamically assigned ports.

**Q22. What is deregistration delay (connection draining) in ALB?**
A: A configurable time period during which the load balancer allows in-flight requests to a target to complete before fully deregistering it.

**Q23. What HTTP status codes indicate a healthy target by default?**
A: HTTP 200 (OK), though custom success codes can be configured for health checks.

**Q24. Can an ALB be internal (private)?**
A: Yes, an ALB can be configured as internal, only accessible within the VPC or connected networks, with no public IP.

**Q25. What is the purpose of Access Logs in ALB?**
A: They capture detailed information about requests sent to the load balancer, stored in S3, useful for analysis and troubleshooting.

**Q26. How many Availability Zones must an ALB span?**
A: At least two Availability Zones are required for an ALB to operate.

**Q27. What is the maximum idle timeout for ALB connections?**
A: Default is 60 seconds, configurable up to 4000 seconds.

**Q28. What is Slow Start Mode in ALB target groups?**
A: A feature that gradually increases the proportion of traffic sent to a newly registered target over a configured warm-up period.

**Q29. How does ALB support gRPC?**
A: ALB natively supports routing gRPC traffic using HTTP/2, with the ability to route based on gRPC method.

**Q30. What is a Weighted Target Group in ALB?**
A: A forward action that splits traffic across multiple target groups based on assigned weights, useful for blue/green or canary deployments.

**Q31. What authentication feature does ALB provide?**
A: Built-in integration with Amazon Cognito or OIDC-compliant identity providers to authenticate users before forwarding requests.

**Q32. Can ALB target an on-premises server?**
A: Yes, if using IP-based target groups and the on-premises server is reachable via VPN/Direct Connect within the VPC's routing.

**Q33. What is the difference between "unhealthy threshold" and "healthy threshold" in health checks?**
A: Unhealthy threshold is the number of consecutive failed checks before marking a target unhealthy; healthy threshold is the number of consecutive successful checks before marking it healthy again.

**Q34. How does ALB scale to handle traffic spikes?**
A: ALB automatically scales its capacity (load balancer nodes) based on incoming traffic; it's a managed, elastic service.

**Q35. What is the purpose of the X-Forwarded-For header in ALB?**
A: It preserves the original client IP address in the HTTP header since ALB terminates the client connection before forwarding to targets.

**Q36. Can multiple listeners be configured on a single ALB?**
A: Yes, an ALB can have multiple listeners (e.g., HTTP:80 and HTTPS:443) each with their own rules.

**Q37. What is the purpose of a default rule in ALB listener rules?**
A: It defines the action taken when no other rule conditions match the incoming request.

**Q38. How is ALB priced?**
A: Based on the number of hours the load balancer runs and Load Balancer Capacity Units (LCUs) consumed, which factor in new connections, active connections, bandwidth, and rule evaluations.

**Q39. What is target group "target type: lambda" used for?**
A: It allows an ALB to directly invoke a Lambda function to process HTTP requests, useful for serverless web applications.

**Q40. How can ALB improve application security?**
A: By integrating AWS WAF, enforcing HTTPS via redirect rules, using security groups to restrict access, and enabling access logging for auditing.

**Q41. What is the difference between Target Group deregistration and target group draining?**
A: They refer to the same concept — allowing existing connections to complete gracefully before a target is fully removed from service.

**Q42. Can an ALB route based on custom HTTP headers?**
A: Yes, ALB supports routing rules based on HTTP header presence or value.

**Q43. What is required to enable HTTPS on an ALB listener?**
A: An SSL/TLS certificate (commonly from AWS Certificate Manager) attached to the HTTPS listener.

**Q44. How does ALB handle unhealthy targets during routing?**
A: It stops sending new traffic to unhealthy targets, only routing requests to targets currently marked healthy.

**Q45. What is the maximum number of certificates an ALB HTTPS listener can support?**
A: Multiple certificates can be added using SNI, with a default limit (e.g., 25) that can be increased via quota request.

**Q46. What is Target Group Stickiness duration configurable range?**
A: From 1 second up to 7 days, defining how long a session remains "sticky" to a target.

**Q47. How does ALB differ in cost model from NLB?**
A: Both charge based on hours running plus capacity units, but ALB uses LCUs based on connections/bandwidth/rule evaluations while NLB uses NLCUs based on connections/bandwidth/flows.

**Q48. What are Application Load Balancer's supported protocols for listeners?**
A: HTTP and HTTPS.

**Q49. How does ALB integrate with Auto Scaling Groups?**
A: The Auto Scaling Group can be attached to a target group, and ALB automatically registers/deregisters instances as the group scales in or out.

**Q50. What is the purpose of "Rule Priority" in ALB listener rules?**
A: It determines the order in which rules are evaluated; the first matching rule (lowest priority number) is applied to the request.

---

## 6. VPC (Virtual Private Cloud)

**Q1. What is Amazon VPC?**
A: A logically isolated virtual network within AWS where you can launch resources with full control over IP addressing, subnets, routing, and security.

**Q2. What is a CIDR block?**
A: Classless Inter-Domain Routing notation defining an IP address range for a VPC or subnet (e.g., 10.0.0.0/16).

**Q3. What is a subnet?**
A: A range of IP addresses within a VPC, tied to a specific Availability Zone, used to organize resources (public or private).

**Q4. What is the difference between a public and private subnet?**
A: A public subnet has a route to an Internet Gateway, allowing direct internet access; a private subnet does not have such a route.

**Q5. What is an Internet Gateway (IGW)?**
A: A horizontally scaled, redundant VPC component that allows communication between instances in a VPC and the internet.

**Q6. What is a NAT Gateway?**
A: A managed service that allows instances in a private subnet to initiate outbound internet traffic while preventing unsolicited inbound connections.

**Q7. What is the difference between NAT Gateway and NAT Instance?**
A: NAT Gateway is a fully managed, highly available AWS service; a NAT Instance is a self-managed EC2 instance configured to perform NAT, requiring manual scaling and patching.

**Q8. What is a Route Table?**
A: A set of rules (routes) that determine where network traffic from a subnet is directed.

**Q9. What is a Network ACL (NACL)?**
A: A stateless firewall at the subnet level that controls inbound and outbound traffic using numbered allow/deny rules.

**Q10. What is the default NACL behavior?**
A: The default NACL allows all inbound and outbound traffic; custom NACLs deny all traffic until rules are explicitly added.

**Q11. What is VPC Peering?**
A: A networking connection between two VPCs that enables routing traffic between them using private IP addresses, as if they were on the same network.

**Q12. Does VPC Peering support transitive routing?**
A: No, VPC Peering is non-transitive; traffic cannot route through an intermediate peered VPC to reach a third VPC.

**Q13. What is a Transit Gateway?**
A: A hub-and-spoke networking service that simplifies connecting multiple VPCs and on-premises networks through a single gateway, supporting transitive routing.

**Q14. What is VPC Endpoint?**
A: A feature that enables private connectivity between a VPC and supported AWS services without needing an Internet Gateway, NAT device, or public IP.

**Q15. What are the two types of VPC Endpoints?**
A: Interface Endpoints (powered by AWS PrivateLink, uses an ENI) and Gateway Endpoints (used only for S3 and DynamoDB, added as a route table entry).

**Q16. What is AWS Direct Connect?**
A: A dedicated, private network connection from an on-premises data center to AWS, offering more consistent bandwidth and lower latency than internet-based VPN.

**Q17. What is a Site-to-Site VPN?**
A: An encrypted connection over the public internet between an on-premises network and a VPC, using a Virtual Private Gateway or Transit Gateway.

**Q18. What is a Virtual Private Gateway (VGW)?**
A: The VPN concentrator on the AWS side of a Site-to-Site VPN connection, attached to a VPC.

**Q19. What is the maximum number of Availability Zones a VPC can span?**
A: A VPC can span all Availability Zones within a single AWS Region (a VPC does not cross regions).

**Q20. What is a Security Group's default behavior?**
A: By default, a new security group denies all inbound traffic and allows all outbound traffic.

**Q21. What is an Elastic Network Interface (ENI)?**
A: A virtual network card that can be attached to instances, enabling multiple IP addresses and network interfaces per instance.

**Q22. What is VPC Flow Logs?**
A: A feature that captures information about IP traffic going to and from network interfaces in a VPC, useful for troubleshooting and security analysis.

**Q23. What is the smallest and largest CIDR block size allowed for a VPC?**
A: Smallest is /28 (16 IP addresses), largest is /16 (65,536 IP addresses).

**Q24. How many IP addresses does AWS reserve in each subnet?**
A: 5 IP addresses are reserved (network address, VPC router, DNS, future use, and broadcast address, though broadcast isn't used).

**Q25. What is a Bastion Host used for in VPC architecture?**
A: A secure jump box placed in a public subnet to allow SSH/RDP access to instances in private subnets.

**Q26. What is the difference between Security Groups and NACLs regarding statefulness?**
A: Security Groups are stateful (return traffic automatically allowed); NACLs are stateless (return traffic must be explicitly allowed by a rule).

**Q27. What is a VPC's default tenancy?**
A: "Default," meaning instances run on shared hardware unless explicitly launched with dedicated tenancy.

**Q28. Can a subnet span multiple Availability Zones?**
A: No, each subnet is mapped to exactly one Availability Zone.

**Q29. What is AWS PrivateLink?**
A: A service that enables private connectivity between VPCs, AWS services, and on-premises applications without exposing traffic to the public internet.

**Q30. What is a VPC's default VPC used for?**
A: A pre-configured VPC created automatically in each region with public subnets, an Internet Gateway, and default route table for quick instance launches.

**Q31. What is Route Propagation in a route table?**
A: A feature that automatically adds routes learned via VPN or Direct Connect (through a gateway) into the route table.

**Q32. What is the purpose of an Egress-Only Internet Gateway?**
A: It allows outbound-only IPv6 traffic from instances in a VPC to the internet while preventing inbound IPv6 connections.

**Q33. What is a VPC's local route used for?**
A: An implicit route automatically present in every route table that allows communication between all resources within the VPC's CIDR range.

**Q34. How does DNS resolution work within a VPC?**
A: Via the Amazon-provided DNS server (VPC+2 address) when `enableDnsSupport` and `enableDnsHostnames` attributes are enabled.

**Q35. What is a Transit Gateway Attachment?**
A: A connection point that attaches a VPC, VPN, Direct Connect gateway, or peering connection to a Transit Gateway.

**Q36. Can you peer VPCs across different AWS accounts and regions?**
A: Yes, VPC Peering supports both cross-account and cross-region connections.

**Q37. What is a "/32" CIDR block used for?**
A: It represents a single specific IP address, often used in security group or NACL rules to allow/deny a single host.

**Q38. What is the purpose of Elastic IP in a VPC context?**
A: A static public IPv4 address that can be remapped between instances or network interfaces within a VPC.

**Q39. What is VPC Sharing?**
A: A feature using AWS Resource Access Manager (RAM) that allows multiple AWS accounts to create resources in shared, centrally managed VPC subnets.

**Q40. How does a Gateway Endpoint differ from an Interface Endpoint in cost?**
A: Gateway Endpoints (S3, DynamoDB) are free of charge; Interface Endpoints incur hourly and data processing charges.

**Q41. What is a "jumbo frame" in VPC networking?**
A: An Ethernet frame with a payload larger than the standard 1500 MTU (up to 9001 MTU), supported within VPC and via Direct Connect/VPC Peering for improved throughput.

**Q42. What are the main components required to make a subnet "public"?**
A: An Internet Gateway attached to the VPC and a route table entry directing 0.0.0.0/0 traffic to that gateway, plus instances with public IPs.

**Q43. What is the purpose of a NAT Gateway's Elastic IP?**
A: It provides a consistent public IP address used for all outbound traffic originating from the NAT Gateway.

**Q44. Can Security Groups reference other Security Groups as a source?**
A: Yes, allowing traffic based on membership in another security group rather than a fixed IP range, useful for dynamic environments.

**Q45. What is the maximum number of VPCs per region by default?**
A: 5 per region by default (a soft limit that can be increased via a service quota request).

**Q46. What is a Carrier Gateway used for?**
A: It enables connectivity between a VPC and a telecommunications carrier network, used with AWS Wavelength for mobile edge applications.

**Q47. What is VPC Reachability Analyzer?**
A: A tool that performs static analysis of network configurations to verify connectivity between resources without sending live traffic.

**Q48. What is the difference between a Transit Gateway and VPC Peering for connecting many VPCs?**
A: Transit Gateway scales more efficiently for many-to-many connections (hub-and-spoke, transitive routing) whereas VPC Peering requires a full mesh of point-to-point connections that grows complex at scale.

**Q49. What is Multi-Region VPC connectivity typically achieved with?**
A: Inter-Region VPC Peering, Transit Gateway peering across regions, or Direct Connect/VPN combined with routing.

**Q50. What is the purpose of DHCP Option Sets in a VPC?**
A: They configure settings like domain name and DNS servers that are automatically assigned to instances launched within the VPC.

---

## 7. RDS (Relational Database Service)

**Q1. What is Amazon RDS?**
A: A managed relational database service that automates provisioning, patching, backup, and scaling for database engines like MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora.

**Q2. What database engines does RDS support?**
A: MySQL, PostgreSQL, MariaDB, Oracle, Microsoft SQL Server, and Amazon Aurora (MySQL/PostgreSQL compatible).

**Q3. What is Multi-AZ deployment in RDS?**
A: A high-availability feature that synchronously replicates data to a standby instance in a different Availability Zone, with automatic failover during outages.

**Q4. What is a Read Replica in RDS?**
A: An asynchronously replicated, read-only copy of a database used to offload read traffic and improve scalability.

**Q5. What is the difference between Multi-AZ and Read Replicas?**
A: Multi-AZ is for high availability/disaster recovery with synchronous replication and automatic failover; Read Replicas are for read scalability with asynchronous replication and are not automatic failover targets by default (though can be manually promoted).

**Q6. What is Amazon Aurora?**
A: A MySQL and PostgreSQL-compatible relational database engine built for the cloud, offering higher performance, storage auto-scaling, and higher availability than standard RDS engines.

**Q7. What is Aurora Serverless?**
A: An on-demand, auto-scaling configuration of Aurora that automatically adjusts database capacity based on application demand, useful for unpredictable workloads.

**Q8. How does RDS handle automated backups?**
A: RDS takes daily automated snapshots and continuously archives transaction logs, allowing point-in-time recovery within the configured retention period.

**Q9. What is the maximum backup retention period for automated RDS backups?**
A: 35 days.

**Q10. What is a DB Snapshot?**
A: A user-initiated or automated backup of an RDS instance's storage volume that persists until explicitly deleted, usable to restore a new instance.

**Q11. What happens to automated backups when an RDS instance is deleted?**
A: Automated backups are deleted along with the instance by default unless you take a final manual snapshot or opt to retain automated backups.

**Q12. What is RDS Proxy?**
A: A fully managed database proxy that pools and shares database connections to improve scalability and resilience, especially useful for Lambda-based applications.

**Q13. How is encryption at rest handled in RDS?**
A: Using AWS KMS to encrypt the underlying storage, automated backups, snapshots, and replicas, configured at instance creation time.

**Q14. Can you enable encryption on an existing unencrypted RDS instance?**
A: Not directly; you must create a snapshot, copy it with encryption enabled, and restore a new encrypted instance from that snapshot.

**Q15. What is the difference between vertical and horizontal scaling in RDS?**
A: Vertical scaling increases instance size (CPU/RAM) or storage; horizontal scaling adds read replicas to distribute read traffic.

**Q16. What is Storage Auto Scaling in RDS?**
A: A feature that automatically increases allocated storage when RDS detects it's running low on free space, without manual intervention.

**Q17. What is the maintenance window in RDS used for?**
A: A configurable weekly time window during which AWS applies pending patches, upgrades, or modifications to the database.

**Q18. How does RDS handle failover in a Multi-AZ deployment?**
A: RDS automatically detects failure and switches the DNS endpoint (CNAME) to point to the standby instance, typically completing within 60-120 seconds.

**Q19. Can Read Replicas be created across regions?**
A: Yes, RDS supports Cross-Region Read Replicas for disaster recovery and reducing read latency for globally distributed applications.

**Q20. What is Aurora Global Database?**
A: A feature allowing an Aurora database to span multiple AWS regions, with fast replication (typically under 1 second) and disaster recovery capabilities.

**Q21. What is Performance Insights in RDS?**
A: A monitoring feature that visualizes database load and helps identify performance bottlenecks by analyzing wait events, SQL statements, and users/hosts.

**Q22. How do you connect an application to RDS securely?**
A: Using database credentials stored in Secrets Manager or SSM Parameter Store, over SSL/TLS connections, restricted by security groups.

**Q23. What is the purpose of Parameter Groups in RDS?**
A: A collection of engine configuration values (like max_connections) applied to a DB instance, allowing customization of database engine behavior.

**Q24. What is the purpose of Option Groups in RDS?**
A: Used to enable and configure additional features specific to certain database engines, such as Oracle's Advanced Security or SQL Server's Transparent Data Encryption.

**Q25. What is the difference between a DB Instance and a DB Cluster in RDS?**
A: A DB Instance is a standalone database environment (standard RDS engines); a DB Cluster (used by Aurora) consists of one or more instances sharing a distributed, auto-scaling storage volume.

**Q26. How does Aurora achieve high durability?**
A: By replicating data six ways across three Availability Zones using a distributed, self-healing storage system.

**Q27. What is RDS's approach to minor version upgrades?**
A: They can be applied automatically during the maintenance window if "Auto minor version upgrade" is enabled.

**Q28. Can you resize storage without downtime in RDS?**
A: Yes, for most engines, storage can be scaled while the database remains online (though performance may be briefly affected).

**Q29. What is a DB Subnet Group?**
A: A collection of subnets (in different AZs) designated for RDS instances within a VPC, used to determine where DB instances can be placed.

**Q30. What is the difference between Provisioned IOPS and General Purpose storage for RDS?**
A: Provisioned IOPS (io1/io2) offers consistent, high-performance I/O for demanding workloads; General Purpose SSD (gp2/gp3) offers balanced price/performance for most workloads.

**Q31. What is RDS event notification?**
A: A feature using SNS to notify users about RDS events such as backups, failovers, and configuration changes.

**Q32. What is the purpose of a final snapshot when deleting an RDS instance?**
A: It preserves a backup of the database state at deletion time, allowing future restoration if needed.

**Q33. Can Read Replicas have their own Read Replicas?**
A: Yes, for some engines, you can create a Read Replica of a Read Replica, though this adds replication lag.

**Q34. What is RDS's default behavior regarding public accessibility?**
A: By default, new RDS instances are not publicly accessible unless explicitly configured with a public IP and appropriate security group rules.

**Q35. What is the maximum storage size for RDS (non-Aurora)?**
A: Up to 64 TiB depending on the engine and storage type.

**Q36. What is Amazon RDS Custom?**
A: A managed database service that provides access to the underlying OS and database environment for customization while still offering automation for common admin tasks, mainly for legacy or custom applications (Oracle, SQL Server).

**Q37. How does RDS support disaster recovery across regions?**
A: Through Cross-Region Read Replicas or Aurora Global Database, which can be promoted to a standalone primary during a regional outage.

**Q38. What is the significance of the "Endpoint" in RDS?**
A: A DNS address used by applications to connect to the database, which remains constant even as underlying infrastructure changes (e.g., during failover).

**Q39. Can you change the database engine of an existing RDS instance (e.g., MySQL to PostgreSQL)?**
A: Not directly via a simple upgrade; a migration approach (e.g., using AWS DMS - Database Migration Service) is required.

**Q40. What is the purpose of RDS Enhanced Monitoring?**
A: It provides real-time OS-level metrics (CPU, memory, file system, disk I/O) for the DB instance, offering more granular visibility than standard CloudWatch metrics.

**Q41. What is the recommended way to rotate database credentials in RDS?**
A: Using AWS Secrets Manager's automatic rotation feature, which updates the password and stores the new secret securely.

**Q42. What is the difference between RDS snapshot copy and RDS snapshot share?**
A: Copying creates a duplicate snapshot (e.g., in another region); sharing grants another AWS account permission to use your existing snapshot directly.

**Q43. What is Amazon Aurora Serverless v2 designed for?**
A: Fine-grained, fast auto-scaling of database capacity in fractional ACUs (Aurora Capacity Units) suited for variable or unpredictable production workloads.

**Q44. How is RDS billed?**
A: Based on instance hours, storage provisioned, I/O requests (for some storage types), backup storage beyond free allowance, and data transfer.

**Q45. What is Blue/Green Deployments in RDS?**
A: A feature that creates a staging (green) environment mirroring production (blue) to safely test changes before switching over with minimal downtime.

**Q46. What is the significance of "Backtrack" in Aurora MySQL?**
A: A feature that allows rewinding a database cluster to a specific point in time without restoring from a backup, useful for quick recovery from user errors.

**Q47. What is the maximum number of Read Replicas supported per Aurora cluster?**
A: Up to 15 Aurora Replicas per cluster.

**Q48. How does RDS handle patching for security vulnerabilities?**
A: Through automated OS and database engine patching applied during defined maintenance windows, managed by AWS.

**Q49. What is a "reader endpoint" in Aurora?**
A: A single endpoint that automatically load-balances read connections across all available Aurora Replicas in the cluster.

**Q50. How can you migrate an on-premises database to RDS with minimal downtime?**
A: Using AWS Database Migration Service (DMS) with continuous data replication (CDC) to keep the target in sync until cutover.

---

## 8. S3 (Simple Storage Service)

**Q1. What is Amazon S3?**
A: A highly durable, scalable object storage service that stores data as objects within buckets, accessible via API, CLI, or console.

**Q2. What is the durability of S3 Standard storage?**
A: 99.999999999% (11 nines) durability, achieved by automatically replicating data across multiple Availability Zones.

**Q3. What are the S3 storage classes?**
A: S3 Standard, S3 Intelligent-Tiering, S3 Standard-IA, S3 One Zone-IA, S3 Glacier Instant Retrieval, S3 Glacier Flexible Retrieval, S3 Glacier Deep Archive, and S3 Express One Zone.

**Q4. What is S3 Intelligent-Tiering?**
A: A storage class that automatically moves objects between access tiers based on changing access patterns, without performance impact or retrieval fees for frequent/infrequent tiers.

**Q5. What is the difference between S3 Standard-IA and One Zone-IA?**
A: Standard-IA replicates data across multiple AZs; One Zone-IA stores data in only a single AZ at a lower cost but with less resilience.

**Q6. What is an S3 bucket policy?**
A: A resource-based JSON policy attached to a bucket that defines permissions for who can access the bucket and its objects.

**Q7. What is the difference between a bucket policy and an IAM policy for S3 access?**
A: A bucket policy is attached to the S3 resource itself and can grant cross-account access; an IAM policy is attached to a user/role and defines what that identity can do across resources.

**Q8. What is S3 Versioning?**
A: A feature that keeps multiple variants of an object in the same bucket, protecting against accidental overwrites or deletions.

**Q9. What is S3 Object Lock?**
A: A feature that enables WORM (Write Once Read Many) protection, preventing objects from being deleted or overwritten for a specified retention period.

**Q10. What are the two retention modes in S3 Object Lock?**
A: Governance mode (can be overridden by users with special permissions) and Compliance mode (cannot be overridden by any user, including root, until the retention period expires).

**Q11. What is S3 Lifecycle Policy?**
A: Rules that automatically transition objects between storage classes or expire (delete) them after a specified time period.

**Q12. How does S3 achieve high availability and durability?**
A: By automatically storing data redundantly across multiple devices and multiple Availability Zones within a region.

**Q13. What is Cross-Region Replication (CRR) in S3?**
A: A feature that automatically replicates objects from a bucket in one region to a bucket in a different region, useful for compliance, latency reduction, or DR.

**Q14. What is the difference between CRR and SRR?**
A: CRR replicates objects across different AWS regions; SRR (Same-Region Replication) replicates objects within the same region, often for log aggregation or account separation.

**Q15. What is S3 Transfer Acceleration?**
A: A feature that speeds up uploads to S3 by routing traffic through Amazon CloudFront's globally distributed edge locations.

**Q16. What encryption options does S3 support?**
A: SSE-S3 (S3-managed keys), SSE-KMS (AWS KMS-managed keys), SSE-C (customer-provided keys), and client-side encryption.

**Q17. What is the maximum size of a single object in S3?**
A: 5 TB.

**Q18. What is Multipart Upload in S3?**
A: A feature that splits large objects into smaller parts uploaded independently (and potentially in parallel), then reassembled, recommended for objects larger than 100 MB.

**Q19. What is a Pre-signed URL in S3?**
A: A temporary URL that grants time-limited access to a private S3 object without requiring the requester to have AWS credentials.

**Q20. What is S3 Static Website Hosting?**
A: A feature that allows an S3 bucket to serve static content (HTML, CSS, JS) directly as a website, with configurable index and error documents.

**Q21. Can an S3 bucket be used for both static website hosting and remain private?**
A: No, for website hosting, the bucket (or CloudFront distribution in front of it) content must be publicly accessible unless served exclusively via CloudFront with Origin Access Control.

**Q22. What is S3 Event Notifications?**
A: A feature that triggers notifications (to SNS, SQS, or Lambda) when specific events occur in a bucket, such as object creation or deletion.

**Q23. What is S3 Select?**
A: A feature that allows retrieving a subset of data from an object using simple SQL expressions, reducing the amount of data transferred and processed.

**Q24. What is the difference between S3 and EBS?**
A: S3 is object storage accessed via API/HTTP for storing files of any type at scale; EBS is block storage attached directly to a single EC2 instance for OS/application-level file systems.

**Q25. What is a "prefix" in S3?**
A: A string that objects' keys start with, used to logically organize objects (simulating folder structures) and to partition workload for performance.

**Q26. How does S3 ensure consistency?**
A: S3 provides strong read-after-write consistency for all GET, PUT, and LIST operations by default.

**Q27. What is the purpose of S3 Access Points?**
A: Named network endpoints attached to a bucket that simplify managing data access for shared datasets by defining specific permissions per application/use case.

**Q28. What is S3 Batch Operations?**
A: A feature that performs large-scale operations (like copy, tagging, or Object Lock) on billions of objects with a single request.

**Q29. What is S3 Glacier Deep Archive used for?**
A: The lowest-cost storage class for long-term archival data rarely accessed, with retrieval times of 12 hours or more.

**Q30. What is a "Requester Pays" bucket?**
A: A configuration where the requester (rather than the bucket owner) pays for data transfer and request costs when accessing objects.

**Q31. What is Object Ownership setting "Bucket owner enforced" used for?**
A: It disables ACLs so all objects in the bucket are automatically owned by the bucket owner, simplifying access management.

**Q32. What is the difference between S3 Standard and S3 Express One Zone?**
A: S3 Express One Zone is a high-performance, single-AZ storage class designed for latency-sensitive applications, offering significantly faster data access than S3 Standard.

**Q33. Can you host a custom domain with S3 static website hosting?**
A: Yes, by naming the bucket to match the domain and configuring Route 53 (often paired with CloudFront for HTTPS support).

**Q34. What is S3 Inventory?**
A: A feature that generates scheduled reports listing objects and their metadata within a bucket, useful for auditing and compliance.

**Q35. What is Server Access Logging in S3?**
A: A feature that records detailed records for requests made to a bucket, useful for security audits and access pattern analysis.

**Q36. How does S3 handle object tagging?**
A: Key-value pairs (up to 10 per object) that can be used for access control, lifecycle rule targeting, and cost allocation.

**Q37. What is the difference between "Block Public Access" settings at the account level vs. bucket level?**
A: Account-level settings apply as a blanket restriction across all buckets in the account; bucket-level settings apply only to that specific bucket, and both are enforced together (most restrictive wins).

**Q38. How is S3 pricing structured?**
A: Based on storage used (per GB/month by class), number and type of requests, data transfer out, and additional features like replication or Transfer Acceleration.

**Q39. What is Same-Region Replication commonly used for?**
A: Aggregating logs from multiple buckets, meeting data sovereignty requirements, or maintaining a live copy in another account.

**Q40. What is the purpose of S3 Access Analyzer?**
A: A tool (part of IAM Access Analyzer) that identifies S3 buckets that are shared with external entities, helping detect unintended public or cross-account access.

**Q41. Can you enable versioning and then disable it later?**
A: Versioning can be suspended (stopping new versions from being created) but not fully "disabled" once enabled; existing versions remain until explicitly deleted.

**Q42. What happens to old versions of an object with a lifecycle policy?**
A: You can configure lifecycle rules to transition or expire noncurrent (older) object versions separately from the current version.

**Q43. What is Amazon S3 Object Lambda?**
A: A feature that lets you add custom code to process data retrieved from S3 before returning it to the requesting application, without modifying the original object.

**Q44. What is the significance of ETag in S3?**
A: A hash (often MD5 for non-multipart uploads) representing an object's content, useful for verifying integrity or detecting changes.

**Q45. Can S3 buckets be renamed?**
A: No, bucket names are immutable after creation; you must create a new bucket and copy the objects if a rename is needed.

**Q46. What is the significance of bucket naming being globally unique?**
A: All S3 bucket names must be unique across all AWS accounts globally, since bucket names form part of the URL/DNS.

**Q47. What is S3 Replication Time Control (RTC)?**
A: An SLA-backed feature that replicates 99.99% of new objects within 15 minutes, useful for meeting strict compliance or DR requirements.

**Q48. How can you restrict access to an S3 bucket to only a specific VPC?**
A: Using a bucket policy with a condition on `aws:SourceVpce` (VPC endpoint) or `aws:SourceVpc`, combined with a Gateway VPC Endpoint.

**Q49. What is the minimum storage duration charge for S3 Glacier Deep Archive?**
A: 180 days; objects deleted before this incur a pro-rated early deletion charge.

**Q50. What is Cross-Origin Resource Sharing (CORS) in S3 used for?**
A: A configuration that allows web applications from one domain to access resources (like fonts, scripts) from an S3 bucket hosted on a different domain.

---

## 9. IAM (Identity and Access Management)

**Q1. What is AWS IAM?**
A: A service that enables you to securely manage access to AWS resources by controlling who is authenticated and authorized to use them.

**Q2. What are the main components of IAM?**
A: Users, Groups, Roles, and Policies.

**Q3. What is an IAM User?**
A: An entity representing a person or application with long-term credentials (password and/or access keys) used to interact with AWS.

**Q4. What is an IAM Role?**
A: An identity with specific permissions that can be assumed temporarily by trusted entities (users, services, or applications) without needing long-term credentials.

**Q5. What is the difference between an IAM User and an IAM Role?**
A: A User has permanent credentials tied to a specific identity; a Role provides temporary credentials that can be assumed by multiple different trusted entities as needed.

**Q6. What is an IAM Policy?**
A: A JSON document that defines permissions, specifying what actions are allowed or denied on which resources, under what conditions.

**Q7. What is the difference between Identity-based and Resource-based policies?**
A: Identity-based policies are attached to users, groups, or roles; resource-based policies are attached directly to a resource (e.g., S3 bucket policy) and can grant access to other accounts.

**Q8. What is the Principle of Least Privilege?**
A: A security best practice of granting only the minimum permissions necessary for a user or role to perform its required tasks.

**Q9. What is an IAM Group?**
A: A collection of IAM users to which you can attach policies, simplifying permission management for multiple users with similar access needs.

**Q10. What is Multi-Factor Authentication (MFA) in IAM?**
A: An extra layer of security requiring users to provide a second factor (e.g., a one-time code) in addition to their password when signing in.

**Q11. What is the root user in AWS?**
A: The initial account owner identity with full, unrestricted access to all resources and billing; AWS recommends securing it with MFA and not using it for daily tasks.

**Q12. What is the difference between an explicit deny and an implicit deny in IAM?**
A: An implicit deny is the default when no policy explicitly allows an action; an explicit deny is a statement that specifically denies an action and always overrides any allow.

**Q13. How is policy evaluation logic determined when multiple policies apply?**
A: Explicit deny always wins; if there's no explicit deny, an explicit allow grants access; otherwise, access is implicitly denied by default.

**Q14. What is an IAM Policy's "Condition" element used for?**
A: It restricts when a policy statement is in effect, based on context keys like source IP, time, MFA status, or tags.

**Q15. What is Cross-Account Access in IAM?**
A: A mechanism allowing users in one AWS account to assume a role in another account, granting temporary access without sharing credentials.

**Q16. What is an IAM Access Key?**
A: A pair of credentials (Access Key ID and Secret Access Key) used to make programmatic requests to AWS via CLI, SDK, or API.

**Q17. What is AWS STS (Security Token Service)?**
A: A service that issues temporary, limited-privilege security credentials for IAM users, federated users, or assumed roles.

**Q18. What is an Instance Profile in the context of IAM and EC2?**
A: A container that holds an IAM role and passes its permissions to an EC2 instance, allowing applications on it to make authenticated API calls.

**Q19. What is IAM Identity Federation?**
A: A mechanism allowing users to authenticate using an external identity provider (like Active Directory, Google, or SAML-based IdPs) and obtain temporary AWS credentials.

**Q20. What is the difference between AWS managed policies and customer managed policies?**
A: AWS managed policies are created and maintained by AWS for common use cases; customer managed policies are created and fully controlled by the account owner.

**Q21. What is an Inline Policy?**
A: A policy embedded directly within a single user, group, or role, existing in a strict one-to-one relationship (not reusable across identities).

**Q22. What is a Permissions Boundary?**
A: An advanced feature that sets the maximum permissions an IAM entity can have, regardless of what its attached policies allow.

**Q23. What is an IAM Policy ARN?**
A: The Amazon Resource Name uniquely identifying a specific policy resource within AWS.

**Q24. What is AWS Organizations Service Control Policy (SCP)?**
A: A policy applied at the AWS Organizations level that sets the maximum available permissions for accounts within an organization or organizational unit, but does not itself grant permissions.

**Q25. What is the difference between SCPs and IAM Policies?**
A: SCPs set guardrails/limits across accounts in an Organization and never grant permissions by themselves; IAM policies grant actual permissions to identities within an account.

**Q26. What is IAM Access Analyzer?**
A: A tool that analyzes resource policies to identify resources shared with external entities, helping detect unintended public or cross-account access.

**Q27. What is the purpose of tags in IAM policies (ABAC)?**
A: Attribute-Based Access Control uses resource/user tags in policy conditions to dynamically grant permissions, reducing the need for numerous individual policies.

**Q28. What is the AssumeRole API used for?**
A: It allows an IAM entity to obtain temporary security credentials to act as a specified IAM role, typically for cross-account access or service-to-service permission delegation.

**Q29. What is the trust policy of an IAM role?**
A: A resource-based policy attached to a role that specifies which principals (users, accounts, services) are allowed to assume that role.

**Q30. How does IAM support password policies?**
A: Administrators can enforce rules such as minimum length, complexity requirements, expiration, and reuse prevention for IAM user passwords.

**Q31. What is the maximum session duration for an assumed IAM role?**
A: Configurable up to a maximum of 12 hours (default is often 1 hour), depending on the role's settings.

**Q32. What is IAM Credential Report?**
A: A downloadable report listing all IAM users in an account and the status of their various credentials (passwords, access keys, MFA).

**Q33. What is a Service-Linked Role?**
A: A predefined IAM role linked to a specific AWS service that includes all permissions the service requires to perform actions on your behalf.

**Q34. What is the recommended way for applications running on EC2 to access AWS services?**
A: By attaching an IAM role via an instance profile rather than storing long-term access keys on the instance.

**Q35. What is the "NotAction" element in an IAM policy?**
A: It specifies an exception—matching all actions except those listed—often used with "Deny" effects for broad restrictions.

**Q36. Can IAM policies be versioned?**
A: Yes, customer managed policies support versioning, allowing rollback to previous policy versions, with a maximum of 5 versions retained.

**Q37. What is IAM Policy Simulator?**
A: A tool that lets you test and troubleshoot IAM policies to verify whether they would grant or deny specific actions before applying them.

**Q38. What is the difference between authentication and authorization in the context of IAM?**
A: Authentication verifies identity (who you are); authorization determines what actions the authenticated identity is permitted to perform.

**Q39. What is AWS IAM Identity Center (formerly AWS SSO)?**
A: A service that provides centralized access management for multiple AWS accounts and business applications using a single sign-on experience.

**Q40. What is a wildcard (*) used for in an IAM policy?**
A: It matches any value in place of the wildcard, such as allowing all actions (`"Action": "*"`) or all resources (`"Resource": "*"`) — generally discouraged for least privilege.

**Q41. How can you enforce MFA for sensitive actions using IAM?**
A: By adding a condition in the policy checking `aws:MultiFactorAuthPresent: true`, denying access to sensitive actions unless MFA was used.

**Q42. What happens if a user is a member of multiple IAM Groups with conflicting policies?**
A: All applicable policies from all groups are evaluated together; an explicit deny in any policy overrides any allow.

**Q43. What is the difference between IAM Roles for EC2 and IAM Roles for Lambda?**
A: Both grant temporary permissions to the respective compute service, but EC2 roles are delivered via an instance profile while Lambda roles are directly specified as the function's execution role.

**Q44. What is Cross-Account Role Chaining?**
A: The process of assuming a role in one account, then using those temporary credentials to assume another role in a different account, subject to session duration limits.

**Q45. Why is it best practice to avoid using the root account for daily operations?**
A: Because the root account has unrestricted access to everything including billing, and compromise or misuse can cause catastrophic damage; IAM users/roles with least privilege should be used instead.

**Q46. What is the "Principal" element used for in a resource-based policy?**
A: It specifies which AWS account, IAM user, role, or service the policy statement applies to.

**Q47. How does AWS recommend rotating IAM access keys?**
A: Regularly rotating keys (e.g., every 90 days) and using IAM Roles instead of long-lived access keys wherever possible.

**Q48. What is the purpose of AWS CloudTrail in relation to IAM?**
A: It logs all API calls made using IAM identities, providing an audit trail useful for security analysis and compliance.

**Q49. What is a "condition key" example commonly used in IAM policies?**
A: `aws:SourceIp` to restrict access based on the requester's IP address, or `aws:RequestedRegion` to restrict actions to specific AWS regions.

**Q50. Can an IAM Role be assumed by an AWS service like Lambda or ECS directly?**
A: Yes, services like Lambda and ECS tasks can assume an execution role automatically as defined in the trust policy, enabling them to call other AWS APIs securely.

---

## 10. CloudFront

**Q1. What is Amazon CloudFront?**
A: A content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to users globally with low latency via edge locations.

**Q2. What is an Origin in CloudFront?**
A: The source location from which CloudFront fetches content to cache and distribute, such as an S3 bucket, ALB, EC2 instance, or custom HTTP server.

**Q3. What is an Edge Location?**
A: A globally distributed data center where CloudFront caches copies of content close to end users to reduce latency.

**Q4. What is a CloudFront Distribution?**
A: The configuration entity that defines how CloudFront delivers content, including origins, cache behaviors, and settings.

**Q5. What is the difference between a Web Distribution and RTMP Distribution?**
A: Web Distribution is used for general web content delivery (HTTP/HTTPS); RTMP Distribution (deprecated) was used for streaming media using Adobe's RTMP protocol.

**Q6. What is Origin Access Control (OAC)?**
A: A feature that restricts direct public access to an S3 origin, ensuring content can only be accessed through CloudFront.

**Q7. What is a Cache Behavior in CloudFront?**
A: A set of rules defining how CloudFront handles requests for a specific URL path pattern, including caching policies, allowed methods, and origin routing.

**Q8. What is TTL (Time to Live) in CloudFront caching?**
A: The duration an object remains cached at an edge location before CloudFront checks the origin for an updated version.

**Q9. How can you invalidate cached content in CloudFront?**
A: By creating a cache invalidation request specifying the paths to remove, forcing CloudFront to fetch fresh content from the origin.

**Q10. What is a Signed URL in CloudFront?**
A: A URL that includes a signature granting time-limited, restricted access to a specific private object.

**Q11. What is a Signed Cookie in CloudFront?**
A: A mechanism for granting access to multiple restricted files (e.g., a whole application) without needing signed URLs for every file.

**Q12. What is the difference between Signed URLs and Signed Cookies?**
A: Signed URLs grant access to a single specific file; Signed Cookies grant access to multiple files matching a pattern, useful for subscription-based content.

**Q13. What is a CloudFront Origin Group?**
A: A configuration that provides failover by defining a primary and secondary origin; CloudFront automatically switches to the secondary if the primary fails.

**Q14. What is Lambda@Edge used for in CloudFront?**
A: Running custom code at CloudFront edge locations to modify requests/responses, such as header manipulation, A/B testing, or authentication.

**Q15. What is CloudFront Functions?**
A: A lightweight JavaScript-based compute feature for high-scale, latency-sensitive operations at the edge, simpler and faster than Lambda@Edge but with fewer capabilities.

**Q16. What is the difference between Lambda@Edge and CloudFront Functions?**
A: CloudFront Functions handle simpler, sub-millisecond tasks (like header manipulation) at all edge locations; Lambda@Edge supports more complex logic with longer execution times but higher latency and cost.

**Q17. How does CloudFront support HTTPS?**
A: By using SSL/TLS certificates (from ACM or custom certificates) for both viewer-to-CloudFront and CloudFront-to-origin connections.

**Q18. What is Field-Level Encryption in CloudFront?**
A: A feature that encrypts specific sensitive data fields (like credit card numbers) at the edge, ensuring only authorized systems downstream can decrypt them.

**Q19. What is Geo-Restriction in CloudFront?**
A: A feature that allows or blocks access to content based on the geographic location of the requester, using an allowlist or denylist of countries.

**Q20. How does CloudFront integrate with AWS WAF?**
A: WAF can be attached to a CloudFront distribution to filter malicious requests based on rules before they reach the origin.

**Q21. What is the purpose of CloudFront's Price Class setting?**
A: It controls which edge locations are used to serve content, allowing cost optimization by limiting distribution to specific regions.

**Q22. What HTTP methods does CloudFront support caching for?**
A: By default, GET and HEAD are cached; PUT, POST, PATCH, OPTIONS, and DELETE can be forwarded to the origin but are not cached.

**Q23. What is a Custom Error Response in CloudFront?**
A: A configuration that allows CloudFront to return a custom error page (and optionally cache it) when the origin returns specific error codes.

**Q24. What is the significance of Origin Shield in CloudFront?**
A: An additional caching layer that consolidates requests to the origin from multiple edge locations, reducing origin load and improving cache hit ratio.

**Q25. How does CloudFront handle dynamic content?**
A: It can pass dynamic requests through to the origin without caching, or use minimal caching combined with techniques like Lambda@Edge for personalization.

**Q26. What is the maximum file size CloudFront can serve from cache?**
A: Up to 30 GB per file.

**Q27. What protocols does CloudFront support for origin communication?**
A: HTTP and HTTPS to custom or S3 origins, with configurable minimum origin SSL protocol versions.

**Q28. What is Real-Time Logs in CloudFront?**
A: A feature that delivers request logs to Kinesis Data Streams in near real-time for immediate analysis, unlike standard logs which are delivered periodically to S3.

**Q29. How does CloudFront handle compression?**
A: It can automatically compress certain file types (e.g., text, CSS, JS) before serving them to reduce transfer size and improve load times.

**Q30. What is the relationship between CloudFront and Route 53 Alias records?**
A: Route 53 Alias records can point a custom domain directly to a CloudFront distribution's domain name without needing a CNAME.

**Q31. What is an Origin Request Policy in CloudFront?**
A: A policy that defines which headers, cookies, and query strings are forwarded to the origin for a given cache behavior.

**Q32. What is a Cache Policy in CloudFront?**
A: A policy specifying which values (headers, cookies, query strings) are included in the cache key, determining how CloudFront differentiates cached objects.

**Q33. Can CloudFront serve private content from a custom (non-S3) origin?**
A: Yes, using custom origin access restrictions such as requiring a custom header shared secret between CloudFront and the origin.

**Q34. What is the benefit of using CloudFront in front of an API Gateway or ALB?**
A: It reduces latency for global users, provides an additional layer of caching and DDoS protection (via AWS Shield), and can enable custom domain/SSL termination.

**Q35. How does CloudFront support WebSocket connections?**
A: CloudFront supports proxying WebSocket connections to origins that support them, such as ALB.

**Q36. What is the default CloudFront domain name format?**
A: `<distribution-id>.cloudfront.net`.

**Q37. How is CloudFront billed?**
A: Based on data transfer out, number of HTTP/HTTPS requests, and optional features like invalidations beyond the free tier or Lambda@Edge execution.

**Q38. What is Continuous Deployment in CloudFront?**
A: A feature allowing you to test a new distribution configuration by shifting a percentage of live traffic before fully promoting it.

**Q39. Can CloudFront distribute content over IPv6?**
A: Yes, IPv6 support can be enabled on a distribution.

**Q40. What is the purpose of a "default cache behavior" in CloudFront?**
A: It defines the fallback caching and routing rules applied when no other specific path pattern matches the request.

**Q41. How does AWS Shield integrate with CloudFront?**
A: AWS Shield Standard is automatically applied to all CloudFront distributions for DDoS protection at no extra cost; Shield Advanced offers enhanced protections for an additional fee.

**Q42. What is the difference between forwarding all cookies vs. no cookies to the origin?**
A: Forwarding all cookies allows origin-driven personalization but reduces cache efficiency; forwarding none maximizes cache hit ratio but limits per-user customization.

**Q43. Can you use multiple origins within a single CloudFront distribution?**
A: Yes, using cache behaviors with different path patterns, each routed to a different origin (e.g., /images/* to S3, /api/* to ALB).

**Q44. What is a "trusted key group" in CloudFront?**
A: A configuration used with signed URLs/cookies that specifies which public keys CloudFront trusts to validate the signatures.

**Q45. How can you restrict access to a CloudFront distribution to specific referring domains?**
A: By checking the Referer header at the origin or using AWS WAF rules, since CloudFront itself doesn't natively enforce Referer restrictions.

**Q46. What is the purpose of Origin Groups' failover criteria?**
A: They define which HTTP status codes from the primary origin (e.g., 500, 502, 503, 504) trigger failover to the secondary origin.

**Q47. How does CloudFront improve security posture for S3-hosted websites?**
A: By keeping the S3 bucket private (using OAC) and only allowing access through CloudFront, preventing users from bypassing the CDN and accessing S3 directly.

**Q48. What is the "minimum TTL," "default TTL," and "maximum TTL" in a cache behavior?**
A: They define the lower bound, default, and upper bound for how long an object can be cached, working alongside origin cache-control headers.

**Q49. Can CloudFront be used to accelerate S3 uploads similarly to Transfer Acceleration?**
A: Yes, indirectly, by proxying PUT/POST requests through CloudFront's edge network to origins, though S3 Transfer Acceleration is the dedicated feature for upload acceleration.

**Q50. What logging options does CloudFront provide?**
A: Standard access logs delivered to S3, and Real-Time Logs delivered to Kinesis Data Streams for near-instant analysis.

---

## 11. Route 53

**Q1. What is Amazon Route 53?**
A: A highly available and scalable Domain Name System (DNS) web service that also offers domain registration and health checking.

**Q2. What DNS record types does Route 53 support?**
A: A, AAAA, CNAME, MX, NS, PTR, SOA, SRV, TXT, CAA, and the AWS-specific Alias record.

**Q3. What is an Alias record in Route 53?**
A: A Route 53-specific extension that maps a domain name directly to an AWS resource (like CloudFront, ALB, or S3) without needing an IP address, and unlike CNAME, can be used at the zone apex.

**Q4. What is the difference between a CNAME and an Alias record?**
A: CNAME cannot be used for the root/apex domain and always incurs a DNS lookup; Alias records can be used at the zone apex and, for AWS targets, don't incur additional charges for the lookup.

**Q5. What are Route 53 Routing Policies?**
A: Simple, Weighted, Latency-based, Failover, Geolocation, Geoproximity, Multi-value Answer, and IP-based routing policies.

**Q6. What is Weighted Routing Policy?**
A: A policy that distributes traffic across multiple resources based on assigned weight values, useful for A/B testing or gradual rollouts.

**Q7. What is Latency-based Routing?**
A: A policy that routes users to the AWS region providing the lowest network latency for them.

**Q8. What is Geolocation Routing?**
A: A policy that routes traffic based on the geographic location of the user (continent, country, or state), useful for localization or compliance.

**Q9. What is Geoproximity Routing?**
A: A policy (requiring Route 53 Traffic Flow) that routes traffic based on the geographic location of resources and users, with the ability to shift traffic using a "bias" value.

**Q10. What is Failover Routing Policy?**
A: A policy that routes traffic to a primary resource when healthy, and automatically fails over to a secondary resource when the primary is deemed unhealthy.

**Q11. What is Multi-Value Answer Routing?**
A: A policy that returns multiple healthy IP addresses (up to 8) randomly selected, providing basic load balancing and improved availability without an actual load balancer.

**Q12. What is a Route 53 Health Check?**
A: A configuration that monitors the health/availability of an endpoint (via HTTP, HTTPS, or TCP) and can trigger failover or influence DNS responses.

**Q13. What is a Hosted Zone?**
A: A container for DNS records for a specific domain, defining how traffic is routed for that domain and its subdomains.

**Q14. What is the difference between a Public and Private Hosted Zone?**
A: A Public Hosted Zone manages DNS records for internet-visible domains; a Private Hosted Zone manages DNS records accessible only within specified VPCs.

**Q15. What is Domain Registration in Route 53?**
A: A feature allowing you to register new domain names directly through AWS, automatically creating a corresponding hosted zone.

**Q16. What is TTL in the context of Route 53 DNS records?**
A: Time to Live specifies how long resolvers should cache a DNS record's response before querying again.

**Q17. What is Route 53 Resolver?**
A: A service that enables DNS resolution between your VPC and on-premises networks (via Resolver endpoints), especially useful in hybrid cloud setups.

**Q18. What is a Route 53 Resolver Inbound Endpoint?**
A: An endpoint that allows DNS queries from on-premises networks to be resolved by Route 53 Resolver for a private hosted zone or VPC.

**Q19. What is a Route 53 Resolver Outbound Endpoint?**
A: An endpoint that forwards DNS queries from a VPC to DNS resolvers on an on-premises network or other locations.

**Q20. What is Route 53 Traffic Flow?**
A: A visual tool for creating complex routing configurations that combine multiple routing policies, saved as reusable traffic policies.

**Q21. What is a Route 53 Traffic Policy?**
A: A saved, reusable configuration created via Traffic Flow that defines how DNS queries are routed, which can be applied to multiple domains.

**Q22. What is the purpose of NS records in a hosted zone?**
A: They specify the authoritative name servers responsible for answering DNS queries for that domain.

**Q23. What is the purpose of SOA records?**
A: Start of Authority records contain administrative information about the domain, including the primary name server and refresh timers.

**Q24. Can Route 53 route traffic based on both latency and health checks combined?**
A: Yes, health checks can be associated with any routing policy, so unhealthy endpoints are automatically excluded from the DNS response regardless of the policy used.

**Q25. What is DNSSEC support in Route 53?**
A: A feature that allows enabling Domain Name System Security Extensions to cryptographically sign DNS records, protecting against certain spoofing attacks.

**Q26. What is a Calculated Health Check in Route 53?**
A: A health check that combines the status of multiple other health checks using logical operators (AND, OR, NOT) to determine overall health.

**Q27. How does Route 53 support hybrid cloud DNS resolution?**
A: Via Route 53 Resolver endpoints (inbound/outbound) that bridge DNS resolution between on-premises networks and VPCs over Direct Connect or VPN.

**Q28. What is the significance of the "Evaluate Target Health" setting on an Alias record?**
A: It determines whether Route 53 considers the health of the underlying AWS resource (like an ALB) when deciding whether to return that record in a query.

**Q29. What is a Route 53 Resolver DNS Firewall?**
A: A managed firewall that filters outbound DNS traffic from your VPC, blocking queries to known malicious domains.

**Q30. Can Route 53 be used purely for domain registration without hosting DNS there?**
A: Yes, you can register a domain via Route 53 and point its name servers to a different DNS provider if desired.

**Q31. What is the maximum TTL Route 53 supports for a record?**
A: There's no strict maximum enforced by Route 53 itself, though extremely large values are uncommon; it's practically limited to reasonable operational values (often set from 0 seconds up to many days).

**Q32. What is the significance of low TTL values before a migration?**
A: Lowering TTL before a DNS change ensures resolvers refresh their cache quickly, minimizing the time users are directed to old endpoints after cutover.

**Q33. How does Route 53 pricing work?**
A: Charges are based on the number of hosted zones, DNS queries, health checks, and optional features like domain registration or Resolver endpoints.

**Q34. What is a "Simple Routing Policy" typically used for?**
A: Routing traffic to a single resource, without health checks or complex routing logic, suitable for basic single-server setups.

**Q35. Can Route 53 route based on the client's specific IP address ranges?**
A: Yes, using IP-based Routing, which allows defining CIDR blocks mapped to specific endpoints.

**Q36. What is the relationship between Route 53 and ACM (Certificate Manager) for domain validation?**
A: Route 53 can automatically create the DNS CNAME validation records required by ACM to prove domain ownership when issuing a certificate.

**Q37. What is a "Private DNS for VPC" configuration used for?**
A: Associating a private hosted zone with one or more VPCs so that internal resources can resolve custom domain names privately, without exposing them publicly.

**Q38. How many name servers does Route 53 assign to each hosted zone?**
A: Four name servers, for redundancy across different top-level domains.

**Q39. What happens if all health-checked endpoints in a policy are unhealthy?**
A: Route 53 typically reverts to returning all records regardless of health status ("fail open"), depending on the specific policy and configuration, to avoid returning no answer at all.

**Q40. What is Route 53 Application Recovery Controller?**
A: A set of capabilities to help manage and automate failover for multi-region application architectures, including readiness checks and routing controls.

**Q41. Can you import/export DNS records in bulk in Route 53?**
A: Yes, using zone file import/export functionality in the console or via API/CLI with structured record sets.

**Q42. What is the difference between Route 53 Resolver and standard VPC DNS?**
A: Standard VPC DNS (Amazon-provided DNS) resolves standard queries within the VPC; Route 53 Resolver extends this with hybrid resolution capabilities and DNS Firewall for more complex/hybrid environments.

**Q43. What is a CAA record used for?**
A: Certificate Authority Authorization record specifies which certificate authorities are permitted to issue certificates for the domain.

**Q44. How does Route 53 support blue/green deployments?**
A: By using Weighted Routing Policy to gradually shift traffic percentage between old (blue) and new (green) environments.

**Q45. What is the primary use case for a Failover Routing Policy with an S3 static site as secondary?**
A: To provide a "sorry page" or static fallback content automatically served if the primary dynamic application becomes unhealthy.

**Q46. Is Route 53 a global or regional service?**
A: Route 53 is a global service; hosted zones and health checks aren't tied to a specific AWS region (though health checkers operate from various global locations).

**Q47. What is the purpose of a "latency resource record" alongside health checks?**
A: To ensure that even the lowest-latency region is excluded from responses if it becomes unhealthy, redirecting users to the next best healthy, low-latency option.

**Q48. Can Route 53 monitor endpoints outside of AWS?**
A: Yes, health checks can monitor any publicly accessible endpoint, whether hosted on AWS or elsewhere.

**Q49. What is the significance of "Alias Target" when pointing to an S3 static website?**
A: It allows the domain (including apex) to point directly to the S3 website endpoint without needing a separate IP address, though this requires the bucket name to match the domain.

**Q50. How can Route 53 help implement disaster recovery across AWS regions?**
A: By combining Failover Routing Policy with health checks to automatically redirect traffic from a primary region to a standby region during outages.

---

## 12. SNS (Simple Notification Service)

**Q1. What is Amazon SNS?**
A: A fully managed publish/subscribe (pub/sub) messaging service that enables message delivery from publishers to multiple subscribers.

**Q2. What is a Topic in SNS?**
A: A logical access point/channel that acts as a communication hub, allowing publishers to send messages that are broadcast to all subscribed endpoints.

**Q3. What subscriber (protocol) types does SNS support?**
A: HTTP/HTTPS, Email, Email-JSON, SMS, SQS, Lambda, and Mobile Push Notifications (APNS, FCM, etc.).

**Q4. What is the difference between Standard and FIFO topics in SNS?**
A: Standard topics offer high throughput with best-effort ordering and at-least-once delivery; FIFO topics guarantee strict message ordering and exactly-once delivery, but with lower throughput.

**Q5. What is Fan-Out pattern in SNS?**
A: A messaging pattern where a single message published to an SNS topic is delivered to multiple subscribed endpoints (e.g., multiple SQS queues) simultaneously.

**Q6. How does SNS integrate with SQS in the fan-out pattern?**
A: An SNS topic publishes a message once, and it's automatically delivered to multiple SQS queues subscribed to that topic, enabling parallel, decoupled processing.

**Q7. What is Message Filtering in SNS?**
A: A feature that allows subscribers to receive only a subset of messages published to a topic, based on filter policies matching message attributes.

**Q8. What is a Dead Letter Queue (DLQ) in the context of SNS?**
A: An SQS queue configured to capture messages that SNS failed to deliver to a subscriber after exhausting retry attempts.

**Q9. What is SNS message durability?**
A: SNS stores messages redundantly across multiple Availability Zones to ensure high availability and durability before delivery.

**Q10. What is the maximum message size for SNS?**
A: 256 KB per message (can use Extended Client Library with S3 for larger payloads).

**Q11. What is a Subscription Filter Policy?**
A: A JSON policy attached to a subscription that specifies conditions message attributes must meet for the message to be delivered to that particular subscriber.

**Q12. Can SNS deliver messages directly to mobile devices?**
A: Yes, via Mobile Push Notifications, integrating with services like Apple Push Notification Service (APNS) and Firebase Cloud Messaging (FCM).

**Q13. What is Message Attributes in SNS?**
A: Optional structured metadata (key-value pairs) attached to a message, often used for filtering without needing to parse the message body.

**Q14. How does SNS ensure message delivery reliability?**
A: Through automatic retries with exponential backoff for delivery failures, and optionally routing failed messages to a DLQ.

**Q15. What is the difference between SNS and SQS?**
A: SNS is a push-based pub/sub service delivering messages to multiple subscribers immediately; SQS is a pull-based queue service where consumers poll for and process messages at their own pace.

**Q16. Can you encrypt messages in SNS?**
A: Yes, using Server-Side Encryption (SSE) with AWS KMS to encrypt messages at rest within the topic.

**Q17. What is SNS's pricing model?**
A: Based on the number of API requests (publishes), notifications delivered, and delivery type (e.g., SMS has additional per-message charges).

**Q18. What is a Topic Policy in SNS?**
A: A resource-based policy attached to a topic controlling which AWS accounts/services can publish to or subscribe to the topic.

**Q19. What is the maximum number of subscriptions per SNS topic?**
A: Default limit is 12,500,000 subscriptions per topic (a very high soft limit, adjustable).

**Q20. How does SNS handle raw message delivery?**
A: An option that delivers the message payload directly to the subscriber (e.g., SQS) without wrapping it in the standard SNS JSON envelope.

**Q21. Can SNS trigger a Lambda function?**
A: Yes, Lambda can subscribe to an SNS topic, and SNS will invoke the function asynchronously with the message as the event payload.

**Q22. What is Message Deduplication in SNS FIFO topics?**
A: A mechanism to prevent duplicate messages, achieved via content-based deduplication or explicitly providing a deduplication ID.

**Q23. What is a Message Group ID used for in SNS FIFO?**
A: It groups messages so that FIFO ordering is guaranteed within each group, while messages across different groups can be processed independently.

**Q24. What happens if a subscriber endpoint is unreachable in SNS?**
A: SNS retries delivery based on a retry policy (with backoff), and if all retries fail, the message may be sent to a configured DLQ or dropped.

**Q25. What is Cross-Region delivery in SNS?**
A: SNS topics and subscriptions are region-specific, but you can publish cross-region by having a Lambda or application in another region call the SNS API, or use cross-region replication patterns.

**Q26. How can you secure an SNS topic from unauthorized publishing?**
A: By configuring a topic policy that restricts the `sns:Publish` action to specific IAM principals or AWS services.

**Q27. What is the use case for SNS + SQS fan-out over sending directly to multiple SQS queues?**
A: It decouples the publisher from needing to know about all consumers, allowing new subscribers to be added without changing the publisher's code.

**Q28. What is a "confirmation" step required for HTTP/HTTPS or Email subscriptions in SNS?**
A: The subscriber must confirm the subscription (e.g., by clicking a confirmation link) before it starts receiving actual notifications.

**Q29. Can SNS be used for application alerting alongside CloudWatch?**
A: Yes, CloudWatch Alarms commonly publish to an SNS topic to notify subscribers (email, SMS, Lambda) when a metric breaches a threshold.

**Q30. What is the difference between "SNS Standard" throughput and "SNS FIFO" throughput?**
A: Standard supports nearly unlimited throughput; FIFO is limited (e.g., up to 300 messages/second without batching, or higher with batching), trading throughput for strict ordering guarantees.

**Q31. Can an SNS topic have subscribers in multiple AWS accounts?**
A: Yes, cross-account subscriptions are supported when the topic policy grants the necessary permissions.

**Q32. What is the purpose of a "Redrive Policy" on an SNS subscription?**
A: It specifies the DLQ (SQS) that captures messages the subscription failed to process after all delivery attempts are exhausted.

**Q33. How does SNS support SMS notifications globally?**
A: SNS can send SMS text messages to phone numbers in many countries, with configurable sender ID, message type (transactional/promotional), and spending limits.

**Q34. What is the significance of message ordering in Standard SNS topics?**
A: Standard topics do not guarantee ordering; messages may be delivered out of order, unlike FIFO topics.

**Q35. What is a common architecture pattern using SNS for event-driven microservices?**
A: Publishing domain events to an SNS topic, with each interested microservice subscribing via its own SQS queue to process relevant events asynchronously.

**Q36. Can SNS deliver a single message to different protocols simultaneously (e.g., email and SQS)?**
A: Yes, a topic can have subscribers using multiple different protocols, and all receive the published message.

**Q37. What is the maximum SMS message length via SNS?**
A: Approximately 140 bytes per message part (longer messages may be split into multiple parts depending on carrier and language encoding).

**Q38. How can you test SNS message delivery during development?**
A: By subscribing an email endpoint or an SQS queue and publishing test messages to observe expected delivery behavior.

**Q39. What is the "Effective Delivery Policy" in SNS?**
A: The resolved policy combining default and custom retry/backoff settings that determines how SNS retries failed HTTP/HTTPS deliveries.

**Q40. How does SNS charge for SMS messages differently from other protocols?**
A: SMS messages incur a per-message cost based on destination country and message type, unlike email or SQS/Lambda deliveries which are typically included in the request pricing.

**Q41. What is the maximum number of topics per AWS account in SNS?**
A: Default limit is 100,000 topics per account per region (adjustable soft limit).

**Q42. What is required to enable a Lambda function to be invoked by SNS?**
A: The Lambda function's resource policy must grant SNS permission to invoke it, and the function must be subscribed to the topic.

**Q43. Can SNS integrate with AWS Chatbot or Slack for alerts?**
A: Yes, SNS notifications can be routed to AWS Chatbot, which posts formatted alerts to Slack or Amazon Chime channels.

**Q44. What is the benefit of using message attributes over parsing the message body for filtering?**
A: It allows SNS to filter messages server-side before delivery, reducing unnecessary processing and cost on the subscriber side.

**Q45. Can an SQS queue be subscribed to multiple SNS topics?**
A: Yes, a single SQS queue can subscribe to multiple SNS topics, aggregating events from different sources into one queue.

**Q46. What happens during an SNS topic deletion?**
A: All subscriptions associated with the topic are also deleted, and any pending message deliveries in progress may fail.

**Q47. What is Amazon SNS's delivery status logging feature?**
A: A feature that logs delivery success/failure details to CloudWatch Logs for supported protocols (e.g., HTTP, Lambda, SQS), useful for troubleshooting.

**Q48. What is the typical use case for combining SNS with Step Functions?**
A: Sending notifications about workflow state changes or triggering human approval flows via email/SMS during a Step Functions execution.

**Q49. How does SNS support mobile app push notification "platform applications"?**
A: By creating platform application objects representing specific mobile push services (like FCM or APNS), and platform endpoints representing individual device tokens.

**Q50. What is the key architectural benefit of using SNS in a decoupled system?**
A: It allows producers and consumers to operate independently, enabling scalability, flexibility to add/remove subscribers, and resilience against tight coupling failures.

---

## 13. SQS (Simple Queue Service)

**Q1. What is Amazon SQS?**
A: A fully managed message queuing service that enables decoupling and scaling of microservices, distributed systems, and serverless applications.

**Q2. What are the two types of SQS queues?**
A: Standard Queues (high throughput, best-effort ordering, at-least-once delivery) and FIFO Queues (First-In-First-Out, exactly-once processing, strict ordering).

**Q3. What is the maximum message size in SQS?**
A: 256 KB (larger payloads can be handled using the Extended Client Library, which stores the payload in S3 and passes a reference).

**Q4. What is Visibility Timeout in SQS?**
A: The period during which a message, after being received by a consumer, is hidden from other consumers to prevent duplicate processing.

**Q5. What happens if a consumer doesn't delete a message before the visibility timeout expires?**
A: The message becomes visible again in the queue and can be received and processed by another consumer.

**Q6. What is a Dead Letter Queue (DLQ) in SQS?**
A: A separate queue that receives messages which have failed processing after exceeding the configured maximum receive count, isolating problematic messages for analysis.

**Q7. What is the Redrive Policy in SQS?**
A: A configuration on a source queue that specifies the DLQ and the maximum number of receives before a message is moved to that DLQ.

**Q8. What is Long Polling in SQS?**
A: A polling mechanism where the ReceiveMessage call waits (up to 20 seconds) for a message to arrive before returning, reducing empty responses and cost compared to short polling.

**Q9. What is the difference between Short Polling and Long Polling?**
A: Short polling returns immediately, potentially with an empty response even if messages are queued (querying only a subset of servers); long polling waits and queries all servers, more efficiently retrieving all available messages.

**Q10. What is the maximum message retention period in SQS?**
A: 14 days (default is 4 days, configurable from 1 minute to 14 days).

**Q11. What is a FIFO queue's Message Group ID?**
A: An identifier that groups related messages; ordering is preserved within a group, while messages from different groups can be processed in parallel.

**Q12. What is Message Deduplication ID in SQS FIFO queues?**
A: An identifier used to detect and eliminate duplicate messages sent within a 5-minute deduplication interval.

**Q13. What is Content-Based Deduplication?**
A: A FIFO queue feature that automatically generates a deduplication ID based on a SHA-256 hash of the message body, rather than requiring an explicit ID.

**Q14. What is the maximum throughput for a FIFO queue?**
A: Up to 3,000 messages per second with batching, or 300 messages per second without batching (per API action).

**Q15. What is Delay Queue in SQS?**
A: A queue configuration that postpones the delivery of new messages for a specified period (up to 15 minutes) before they become available for consumers.

**Q16. What is the difference between a Delay Queue and setting a per-message DelaySeconds?**
A: A Delay Queue applies the delay to all messages sent to the queue; DelaySeconds can be set individually per message (Standard queues only, up to 15 minutes).

**Q17. What is Server-Side Encryption (SSE) in SQS?**
A: A feature that encrypts messages at rest using either SQS-managed keys (SSE-SQS) or AWS KMS customer-managed keys (SSE-KMS).

**Q18. What is Batch operations in SQS?**
A: APIs like SendMessageBatch, DeleteMessageBatch, and ChangeMessageVisibilityBatch that allow processing up to 10 messages in a single API call for efficiency.

**Q19. How does SQS achieve high availability?**
A: By storing messages redundantly across multiple servers and Availability Zones within a region.

**Q20. What is a Dead Letter Queue's "maxReceiveCount" used for?**
A: It defines the number of times a message can be received before it's automatically moved to the associated DLQ.

**Q21. Can Lambda consume messages from an SQS queue?**
A: Yes, using an event source mapping, Lambda polls the queue and invokes the function with a batch of messages.

**Q22. What is the difference between SQS and Kinesis Data Streams?**
A: SQS is a simple queue for decoupling with a "pull once, delete" model per message; Kinesis is a stream that retains records for replay and allows multiple independent consumers to read the same data.

**Q23. What is a Message Attribute in SQS?**
A: Optional structured metadata (up to 10 per message) attached to a message, separate from the body, useful for routing or filtering logic in consumers.

**Q24. How is SQS priced?**
A: Based on the number of requests (API calls) beyond the free tier, with additional costs for data transfer.

**Q25. What is the maximum number of in-flight messages for a Standard queue?**
A: Approximately 120,000 messages (varies), while FIFO queues support up to 20,000 in-flight messages.

**Q26. What is Queue Purge in SQS?**
A: An action that deletes all messages in a queue immediately, useful for clearing out stale or test data.

**Q27. What is the difference between Standard and FIFO queue naming conventions?**
A: FIFO queue names must end with the ".fifo" suffix; Standard queues have no such requirement.

**Q28. Can you change a Standard queue to a FIFO queue?**
A: No, the queue type cannot be changed after creation; you must create a new queue of the desired type and migrate.

**Q29. What is the significance of "exactly-once processing" in FIFO queues?**
A: FIFO queues ensure a message is delivered and processed exactly once, without duplicates, as long as deduplication is properly configured and consumers use the API correctly.

**Q30. What is a Queue Policy in SQS?**
A: A resource-based, JSON-formatted policy attached to a queue that controls which principals can send or receive messages, similar to an S3 bucket policy.

**Q31. What happens to a message if it's successfully processed but not explicitly deleted?**
A: It remains in the queue and becomes visible again after the visibility timeout expires, potentially causing duplicate processing.

**Q32. What is the recommended way to handle "poison pill" messages in SQS?**
A: Configure a DLQ with an appropriate maxReceiveCount so persistently failing messages are automatically isolated rather than blocking the queue indefinitely.

**Q33. What is the ApproximateNumberOfMessages attribute used for?**
A: A queue attribute (visible via CloudWatch/GetQueueAttributes) indicating roughly how many messages are available for retrieval, useful for scaling decisions.

**Q34. How does SQS support scaling of consumers?**
A: Since SQS is a pull-based, distributed queue, multiple consumers (e.g., EC2 instances, Lambda functions) can poll concurrently to process messages in parallel, and consumer count can scale based on queue depth.

**Q35. What is Extended Client Library used for with SQS?**
A: A library that automatically stores large message payloads (over 256 KB) in S3 and sends only a reference/pointer via SQS.

**Q36. What is the ChangeMessageVisibility API used for?**
A: It allows a consumer to extend (or reduce) the visibility timeout of a specific in-flight message, useful when processing takes longer than expected.

**Q37. What is the difference between SQS and SNS regarding message consumption?**
A: SQS messages are consumed (pulled) by one consumer per message (within a queue) and removed after processing; SNS pushes messages to all subscribers simultaneously.

**Q38. Can an SQS queue be encrypted with a customer-managed KMS key and still be used efficiently at scale?**
A: Yes, though SSE-KMS incurs additional API call charges to KMS compared to SSE-SQS, which uses AWS-owned keys at no extra cost.

**Q39. What is the maximum delay a Standard SQS queue supports?**
A: 15 minutes (900 seconds) maximum delay, either at the queue level or per message.

**Q40. What is a common pattern for using SQS with Auto Scaling?**
A: Scaling the number of EC2 instances (consumers) based on the ApproximateNumberOfMessagesVisible CloudWatch metric to match processing capacity with queue depth.

**Q41. What happens to unprocessed messages when an SQS queue is deleted?**
A: All messages within the queue are permanently lost upon deletion.

**Q42. What is the FIFO queue's default throughput mode versus high throughput mode?**
A: Default mode processes up to 300 (or 3,000 batched) messages/second per queue; High Throughput Mode partitions messages by group ID to significantly increase throughput beyond these limits.

**Q43. Can SQS trigger other AWS services directly like S3 can trigger Lambda?**
A: SQS itself doesn't push events like S3 does; instead, consumers (like Lambda via event source mapping) actively poll SQS for new messages.

**Q44. What is the purpose of setting a minimal ReceiveMessageWaitTimeSeconds?**
A: Configuring long polling wait time reduces the number of empty responses and API calls, lowering cost and latency in message retrieval.

**Q45. How do you ensure idempotent processing when using Standard SQS queues (which allow duplicates)?**
A: By designing consumers to check/store processed message IDs or using idempotency keys within business logic, since Standard queues offer at-least-once (not exactly-once) delivery.

**Q46. What is the significance of message order across multiple Message Group IDs in FIFO?**
A: Order is guaranteed only within a single group; different groups can be processed independently and concurrently without a strict cross-group order.

**Q47. What CloudWatch metrics are commonly monitored for SQS queues?**
A: ApproximateNumberOfMessagesVisible, ApproximateAgeOfOldestMessage, NumberOfMessagesSent, and NumberOfMessagesDeleted.

**Q48. What is a "fan-out" architecture using SQS and SNS combined?**
A: Publishing a single message to an SNS topic, which then distributes copies to multiple subscribed SQS queues for independent, parallel consumer processing.

**Q49. Can an SQS queue span multiple AWS regions?**
A: No, an SQS queue exists within a single AWS region; cross-region messaging requires custom application logic or other services.

**Q50. What is the primary architectural benefit of using SQS in a distributed system?**
A: It decouples producers and consumers, buffers load spikes, and increases fault tolerance since messages persist in the queue until successfully processed.

---

## 14. EventBridge

**Q1. What is Amazon EventBridge?**
A: A serverless event bus service that enables building event-driven applications by routing events from AWS services, SaaS applications, and custom applications to targets.

**Q2. What is an Event Bus in EventBridge?**
A: A pipeline that receives events and routes them to matching rules and their targets; types include the default bus, custom event buses, and partner event buses.

**Q3. What is a Rule in EventBridge?**
A: A configuration that matches incoming events against a defined event pattern and routes matching events to one or more specified targets.

**Q4. What is an Event Pattern in EventBridge?**
A: A JSON structure that defines the criteria (fields and values) an event must match for a rule to trigger and forward it to a target.

**Q5. What is the difference between EventBridge and SNS?**
A: EventBridge offers advanced content-based filtering, integrates with many AWS/SaaS event sources, and supports schema registry; SNS is a simpler pub/sub system focused on straightforward message fan-out.

**Q6. What targets can EventBridge route events to?**
A: Lambda, SQS, SNS, Step Functions, Kinesis, ECS tasks, API destinations (external HTTP endpoints), and many others (over 20 target types).

**Q7. What is a Custom Event Bus?**
A: A dedicated event bus (separate from the AWS default bus) created for a specific application or team, allowing custom events to be published and routed independently.

**Q8. What is a Partner Event Bus?**
A: An event bus that receives events directly from supported third-party SaaS providers (like Zendesk, Datadog) integrated with EventBridge.

**Q9. What is Schema Registry in EventBridge?**
A: A feature that stores and manages event structure schemas, enabling code generation and validation for events flowing through EventBridge.

**Q10. What is EventBridge Scheduler?**
A: A feature (separate from Rules with cron/rate expressions) that allows creating and managing millions of schedules to invoke targets at specific times or recurring intervals, at scale.

**Q11. What is the difference between a scheduled Rule and EventBridge Scheduler?**
A: Scheduled Rules on an event bus support cron/rate expressions but have practical scale limits; EventBridge Scheduler is purpose-built for high-scale, flexible one-time and recurring schedules with more features like time zones and flexible time windows.

**Q12. What is an API Destination in EventBridge?**
A: A configured HTTPS endpoint outside of AWS that EventBridge can invoke as a target, with built-in connection management (including authentication).

**Q13. What is EventBridge Pipes?**
A: A feature that creates point-to-point integrations between event sources (like SQS, Kinesis, DynamoDB Streams) and targets, with optional filtering, enrichment, and transformation.

**Q14. What is the maximum event size in EventBridge?**
A: 256 KB per event.

**Q15. How does EventBridge handle event delivery failures to a target?**
A: It retries delivery based on a configurable retry policy, and can route persistently failed events to a Dead Letter Queue (SQS) if configured.

**Q16. What is Input Transformer in EventBridge?**
A: A feature that customizes the event data sent to a target by extracting specific fields and reformatting them before delivery.

**Q17. What is the difference between EventBridge and CloudWatch Events?**
A: EventBridge is the evolution/rebrand of CloudWatch Events with expanded capabilities (custom buses, SaaS integrations, schema registry); the core rule-matching engine originated from CloudWatch Events.

**Q18. What are AWS service events commonly routed through EventBridge?**
A: Events like EC2 instance state changes, S3 object creation, CodePipeline state changes, and many other AWS service-generated events.

**Q19. What is Content Filtering in EventBridge rules?**
A: The ability to match events based on specific field values, numeric ranges, prefixes, or existence checks within the event pattern, enabling more granular routing than simple type matching.

**Q20. Can EventBridge trigger cross-account event delivery?**
A: Yes, using resource-based policies on event buses, events can be sent from one AWS account and received/processed in another.

**Q21. What is the default retry behavior for EventBridge rule targets?**
A: EventBridge retries for up to 24 hours (185 attempts by default, though configurable), with exponential backoff, before giving up or sending to a DLQ if configured.

**Q22. What is Event Replay in EventBridge?**
A: A feature (used with Archive) that allows replaying previously archived events through the event bus again, useful for testing or recovery.

**Q23. What is Event Archive in EventBridge?**
A: A feature that stores events matching specified criteria for a configurable retention period, enabling later replay.

**Q24. How does EventBridge support event-driven microservices architecture?**
A: By allowing services to publish domain events to a shared or custom event bus, with other services subscribing via rules without direct coupling between producer and consumer.

**Q25. What is the difference between EventBridge and Step Functions?**
A: EventBridge routes discrete events based on patterns to targets; Step Functions orchestrates a defined sequence/workflow of steps, often including error handling, retries, and state management across multiple actions.

**Q26. What is an EventBridge Connection used for with API Destinations?**
A: It stores the authorization details (API key, OAuth, basic auth) required to securely invoke an external HTTP endpoint as an API Destination target.

**Q27. Can EventBridge invoke multiple targets from a single rule?**
A: Yes, a single rule can specify up to 5 targets (default limit, can request increase), and the matching event is sent to all of them.

**Q28. What is the "detail-type" field in an EventBridge event?**
A: A field that identifies the specific type of event within a source, used commonly in event patterns for precise matching.

**Q29. How does EventBridge Pipes differ from standard EventBridge Rules?**
A: Pipes provide a dedicated point-to-point integration (source to target) with built-in enrichment and filtering, ideal for stream-based sources like SQS/Kinesis/DynamoDB Streams, whereas Rules match events flowing through an event bus more broadly.

**Q30. What is the purpose of the "source" field in an EventBridge event pattern?**
A: It identifies which service or application generated the event (e.g., "aws.ec2" or a custom application name), used as a primary filtering criterion.

**Q31. Can EventBridge be used to build a Software-as-a-Service (SaaS) integration hub?**
A: Yes, through Partner Event Sources, allowing SaaS providers' events to flow directly into a customer's AWS account for processing.

**Q32. What is the significance of "Enrichment" in EventBridge Pipes?**
A: It allows calling a Lambda function, Step Functions, or API Destination to transform or add data to an event before it reaches the final target.

**Q33. How is EventBridge priced?**
A: Based on the number of events published to custom/partner event buses (default bus AWS events are free), with additional charges for schema discovery and archive/replay usage.

**Q34. What is the "PutEvents" API used for in EventBridge?**
A: It's used to publish custom events to an event bus programmatically from applications.

**Q35. What is a "managed rule" in EventBridge?**
A: A rule automatically created and managed by another AWS service (like AWS Config or Systems Manager) to integrate with EventBridge without manual setup.

**Q36. Can EventBridge route events based on nested JSON fields?**
A: Yes, event patterns can match against nested fields within the event's "detail" object.

**Q37. What is the benefit of using a Dead Letter Queue with an EventBridge rule target?**
A: It captures events that failed all delivery retry attempts to that target, preventing silent data loss and enabling later analysis/reprocessing.

**Q38. What is EventBridge's role in decoupling microservices from direct API calls?**
A: It allows services to publish events without knowing which (or how many) other services consume them, promoting loose coupling and independent scalability.

**Q39. What is a "wildcard" or "prefix" match used for in EventBridge patterns?**
A: It allows matching events where a field starts with a specific string, useful for grouping related event types or resource ARNs.

**Q40. Can Lambda functions publish custom events to EventBridge?**
A: Yes, using the AWS SDK's PutEvents call within the function code to publish application-specific events to a bus.

**Q41. What is the significance of ordering guarantees in EventBridge?**
A: EventBridge does not guarantee strict delivery ordering of events to targets; applications requiring strict ordering should consider Kinesis or SQS FIFO instead.

**Q42. How does EventBridge Scheduler support time zones?**
A: It allows specifying a time zone for each schedule, ensuring the invocation time aligns correctly with local time regardless of daylight saving changes.

**Q43. What AWS service is commonly used alongside EventBridge for orchestrating multi-step responses to an event?**
A: AWS Step Functions, often triggered as a target to manage complex workflows resulting from an event.

**Q44. What is a "global endpoint" in EventBridge?**
A: A feature that improves the availability of event ingestion by automatically routing events to a secondary region if the primary region's event bus is unavailable.

**Q45. What is the maximum number of custom event buses per account?**
A: A default soft limit (e.g., 100) exists per account, which can be increased via a service quota request.

**Q46. Can EventBridge be used to trigger AWS Batch jobs?**
A: Yes, AWS Batch job queues can be configured as EventBridge rule targets to launch jobs in response to matching events.

**Q47. What is the "Resource" field commonly present in AWS-generated EventBridge events?**
A: It typically contains the ARN(s) of the AWS resource(s) involved in the event, useful for filtering or downstream processing.

**Q48. How does EventBridge support hybrid/on-premises event sources?**
A: Through the PutEvents API called from any application (including on-premises systems with network connectivity to AWS), allowing custom events to flow into EventBridge.

**Q49. What is a common use case for combining S3 Event Notifications with EventBridge instead of direct Lambda triggers?**
A: To enable advanced filtering, multiple/parallel target routing, and combining S3 events with other event sources in a unified event-driven architecture.

**Q50. What is the key architectural value proposition of EventBridge?**
A: It provides a centralized, scalable, serverless event bus that simplifies building loosely coupled, event-driven architectures across AWS services, SaaS apps, and custom applications.

---

## 15. CloudWatch

**Q1. What is Amazon CloudWatch?**
A: A monitoring and observability service that collects metrics, logs, and events from AWS resources and applications, enabling visibility into system performance and health.

**Q2. What is a CloudWatch Metric?**
A: A time-ordered set of data points representing a specific variable being monitored, such as CPUUtilization or NetworkIn.

**Q3. What is a CloudWatch Namespace?**
A: A container that isolates metrics from different applications or AWS services to prevent naming collisions (e.g., AWS/EC2).

**Q4. What is a CloudWatch Alarm?**
A: A watcher on a metric that triggers a specified action (like an SNS notification or Auto Scaling action) when the metric breaches a defined threshold over a set evaluation period.

**Q5. What are the states of a CloudWatch Alarm?**
A: OK (within threshold), ALARM (breaching threshold), and INSUFFICIENT_DATA (not enough data to determine state).

**Q6. What is the difference between Standard and Detailed (High-Resolution) Monitoring?**
A: Standard monitoring provides metrics at 5-minute intervals (1-minute for some services); Detailed monitoring provides metrics at 1-minute intervals (or down to 1-second for custom high-resolution metrics), for an additional cost.

**Q7. What is CloudWatch Logs?**
A: A service that centralizes log data from EC2 instances, Lambda, and other sources, enabling storage, search, and analysis.

**Q8. What is a Log Group and Log Stream in CloudWatch Logs?**
A: A Log Group is a container for log streams sharing the same retention/permission settings; a Log Stream is a sequence of log events from a single source (e.g., a specific instance or Lambda invocation).

**Q9. What is the CloudWatch Agent used for?**
A: Software installed on EC2 instances or on-premises servers to collect system-level metrics (like memory, disk usage) and custom application logs not available by default.

**Q10. What is CloudWatch Logs Insights?**
A: A feature that allows querying and analyzing log data in CloudWatch Logs using a purpose-built query language.

**Q11. What is a CloudWatch Dashboard?**
A: A customizable, visual home page in the CloudWatch console displaying graphs and metrics for chosen resources across regions.

**Q12. What is a Composite Alarm in CloudWatch?**
A: An alarm that combines the states of multiple other alarms using logical operators (AND, OR, NOT) to reduce alarm noise and reflect complex conditions.

**Q13. What is CloudWatch Events (now largely replaced by EventBridge)?**
A: The original service (whose engine now powers EventBridge's default bus) that delivers near real-time system events describing changes in AWS resources, triggering targets based on rules.

**Q14. What is a CloudWatch Metric Filter?**
A: A pattern applied to CloudWatch Logs that extracts specific terms or values from log events and converts them into a numerical CloudWatch metric.

**Q15. What is Log Retention in CloudWatch?**
A: A configurable setting (from 1 day to indefinite) that determines how long log events are kept in a log group before automatic expiration.

**Q16. What is a Custom Metric in CloudWatch?**
A: A metric published by an application or user (via PutMetricData API) rather than being automatically generated by an AWS service.

**Q17. What is the difference between CloudWatch Metrics and CloudWatch Logs?**
A: Metrics are numerical time-series data used for monitoring trends and triggering alarms; Logs are raw text-based event records used for detailed troubleshooting and analysis.

**Q18. What is CloudWatch Container Insights?**
A: A feature that collects, aggregates, and summarizes metrics and logs from containerized applications running on ECS, EKS, and Kubernetes.

**Q19. What is CloudWatch Application Insights?**
A: A feature that automatically detects potential application problems by analyzing metrics, logs, and correlating data for common technology stacks.

**Q20. What is a CloudWatch Synthetics Canary?**
A: A configurable script that runs on a schedule to monitor endpoints and APIs, simulating user traffic to detect availability or performance issues proactively.

**Q21. What is CloudWatch Anomaly Detection?**
A: A machine-learning-based feature that analyzes a metric's historical data to establish a baseline, flagging deviations as anomalies for alarm triggering.

**Q22. What is the purpose of "evaluation periods" and "datapoints to alarm" in a CloudWatch Alarm?**
A: They define how many consecutive (or out of how many total) periods a metric must breach the threshold before the alarm state changes, reducing false positives from brief spikes.

**Q23. What is CloudWatch Logs Subscription Filter?**
A: A configuration that streams log data in near real-time from a log group to a destination like Lambda, Kinesis, or Kinesis Firehose for further processing.

**Q24. What is a Cross-Account Dashboard in CloudWatch?**
A: A dashboard configuration that allows viewing and monitoring metrics from multiple AWS accounts in a single unified view.

**Q25. What is the maximum retention for CloudWatch Metrics data?**
A: Data is retained at varying resolutions for up to 15 months, with older data automatically aggregated to lower resolution (e.g., 1-minute data is kept for 15 days, 5-minute for 63 days, 1-hour for 15 months).

**Q26. What is a CloudWatch Alarm Action?**
A: The response triggered when an alarm changes state, such as sending an SNS notification, executing an Auto Scaling policy, or stopping/rebooting an EC2 instance.

**Q27. What is the difference between CloudWatch and AWS X-Ray?**
A: CloudWatch focuses on metrics, logs, and alarms for overall system health; X-Ray provides distributed tracing to analyze and debug requests as they travel through multiple services.

**Q28. What is CloudWatch RUM (Real User Monitoring)?**
A: A feature that collects and analyzes client-side performance data from real users interacting with a web application, such as page load times.

**Q29. What is CloudWatch ServiceLens?**
A: A feature that integrates CloudWatch metrics/logs with X-Ray traces to provide an end-to-end view of application health and performance.

**Q30. What is the purpose of CloudWatch Contributor Insights?**
A: A feature that analyzes log data to identify top contributors (e.g., top talkers, error sources) impacting system performance.

**Q31. What is a Log Group's "Export to S3" feature used for?**
A: Exporting historical log data from CloudWatch Logs to an S3 bucket for long-term archival or further offline analysis.

**Q32. How can CloudWatch Alarms trigger Auto Scaling actions?**
A: By configuring the alarm to invoke a Scaling Policy (e.g., increase desired capacity) when a metric like CPUUtilization crosses a threshold.

**Q33. What is the significance of the "Missing Data Treatment" setting in an Alarm?**
A: It determines how the alarm behaves when data points are missing—treating them as missing (default), as breaching, as not breaching, or maintaining the current alarm state.

**Q34. What is CloudWatch's role in observability for Lambda functions?**
A: It automatically captures invocation metrics (Duration, Errors, Throttles, Invocations) and logs, enabling monitoring and alerting on serverless function behavior.

**Q35. What is a "metric math" expression in CloudWatch?**
A: A feature that allows performing mathematical operations across one or more metrics to create derived metrics for more insightful monitoring (e.g., calculating error rate as a percentage).

**Q36. What is the CloudWatch Unified Agent's advantage over the older CloudWatch Logs Agent?**
A: It collects both metrics and logs in a single agent, works across Linux and Windows, and supports more granular OS-level metrics like memory and disk usage.

**Q37. What is the purpose of CloudWatch Events/EventBridge rule triggered by an EC2 state change, combined with an alarm?**
A: To automate operational responses, such as notifying teams or triggering remediation workflows when instances stop unexpectedly.

**Q38. What is a Percentile statistic in CloudWatch (e.g., p99)?**
A: A statistic showing the value below which a given percentage of data points fall, useful for understanding tail latency/performance beyond simple averages.

**Q39. What is the difference between "Sum," "Average," "Minimum," "Maximum," and "SampleCount" statistics in CloudWatch?**
A: They represent different aggregations of data points within a period: total, mean, lowest, highest, and count of data points respectively.

**Q40. How does CloudWatch support billing and cost monitoring?**
A: Through the AWS/Billing namespace metrics (like EstimatedCharges) and integration with Cost Anomaly Detection and Budgets for proactive cost alerts.

**Q41. What is the purpose of CloudWatch cross-region metric aggregation?**
A: It allows viewing and analyzing metrics from resources across multiple AWS regions in unified dashboards or queries.

**Q42. What is a "stat" period in a CloudWatch metric query?**
A: The time interval (e.g., 60 seconds, 5 minutes) over which raw data points are aggregated into a single statistical value.

**Q43. How can CloudWatch Logs Insights help troubleshoot Lambda errors?**
A: By running structured queries against Lambda's CloudWatch Logs to filter, aggregate, and analyze error patterns or execution details across many invocations quickly.

**Q44. What is the significance of encrypting CloudWatch Logs with KMS?**
A: It ensures log data at rest is protected using a customer-managed key, supporting compliance and data protection requirements.

**Q45. What is CloudWatch's integration with AWS Systems Manager used for?**
A: Systems Manager can use CloudWatch metrics/alarms and logs to inform automation runbooks, patch compliance tracking, and operational insights (OpsCenter).

**Q46. What is a "high-resolution" custom metric in CloudWatch?**
A: A metric published with a granularity of 1 second (instead of the standard 1-minute minimum), useful for applications needing very fine-grained monitoring.

**Q47. What is CloudWatch's pricing model based on?**
A: Charges based on number of metrics (custom and detailed monitoring), API requests, log ingestion/storage volume, dashboards, alarms, and features like Contributor Insights or Synthetics.

**Q48. How does CloudWatch support multi-account observability at scale?**
A: Through CloudWatch cross-account observability, which links a monitoring account to multiple source accounts for centralized metrics, logs, and traces visibility.

**Q49. What is the purpose of a CloudWatch Alarm's "Treat missing data as breaching" option in the context of a health check pattern?**
A: It ensures that if metric data stops arriving entirely (e.g., due to a crashed instance not reporting), the alarm still triggers rather than staying in an inconclusive state.

**Q50. What is the overall role of CloudWatch in an AWS observability strategy?**
A: It serves as the central hub for collecting metrics, logs, traces (via ServiceLens/X-Ray integration), and events, enabling monitoring, alerting, automated response, and troubleshooting across the entire AWS environment.

---

*End of document — 15 topics × 50 Q&A = 750 questions and answers.*
