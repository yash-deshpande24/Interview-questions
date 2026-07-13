# Interview Q&A — Part 1: EC2, ECS/Fargate/ECR, Lambda (50 each)

---

# TOPIC 1: EC2 (50 Questions)

**Q1. EC2 म्हणजे काय?**
A: Elastic Compute Cloud — AWS ची resizable virtual server (compute) service, on-demand instances launch/stop/terminate करता येतात.

**Q2. Instance types (family) कोणते आहेत?**
A: General Purpose (T, M series), Compute Optimized (C series), Memory Optimized (R, X series), Storage Optimized (I, D series), Accelerated Computing (P, G series - GPU).

**Q3. On-Demand vs Reserved vs Spot vs Savings Plan?**
A: On-Demand = flexible, महाग. Reserved = 1-3yr commitment, discount. Spot = unused capacity स्वस्त, interruption शक्य. Savings Plans = usage-based commitment, flexible instance family.

**Q4. AMI म्हणजे काय?**
A: Amazon Machine Image — OS + software + config चा template, नवीन instance launch साठी वापरतात.

**Q5. Custom AMI कसा बनवाल?**
A: Running instance configure करून `Create Image` action (Console/CLI: `aws ec2 create-image`) वापरून snapshot घेतात.

**Q6. Instance Store vs EBS?**
A: Instance store = ephemeral (temporary), EBS = persistent block storage, stop/terminate नंतरही data राहतो.

**Q7. EBS volume types कोणते?**
A: gp3/gp2 (general purpose SSD), io1/io2 (provisioned IOPS SSD), st1 (throughput HDD), sc1 (cold HDD).

**Q8. EBS snapshot म्हणजे काय?**
A: EBS volume चा point-in-time backup, S3 मध्ये incrementally store होतो, नवीन volume create करण्यासाठी वापरतात.

**Q9. Elastic IP म्हणजे काय आणि कधी वापराल?**
A: Static public IP address जो account शी बांधलेला असतो. Instance restart झाल्यावरही IP बदलत नाही — production services साठी उपयुक्त.

**Q10. Security Group stateful का असतो?**
A: Inbound traffic allow केला की त्याचा return (outbound) traffic automatically allow होतो, वेगळा outbound rule लागत नाही.

**Q11. SSH connect होत नाहीये — troubleshooting steps सांगा.**
A: Security Group port 22, Key pair correct, instance running+status checks pass, route table मध्ये IGW route, public IP असणे — हे सगळं check करा.

**Q12. User Data script म्हणजे काय?**
A: Instance पहिल्यांदा boot होताना automatically चालणारा script (bootstrap actions, software install) — launch करताना पास करतात.

**Q13. Instance Metadata Service (IMDS) म्हणजे काय?**
A: `169.254.169.254` वरून instance ला स्वतःची info (instance-id, IAM role credentials इ.) मिळते. IMDSv2 (token-based) जास्त secure आहे SSRF attacks पासून.

**Q14. Placement Groups कोणते प्रकार आहेत?**
A: Cluster (low latency, same AZ), Spread (max 7 instances, वेगवेगळ्या hardware वर - HA साठी), Partition (मोठ्या distributed apps साठी, Hadoop/Cassandra).

**Q15. Auto Scaling Group (ASG) म्हणजे काय?**
A: Demand नुसार automatically instances add/remove करणारी service — min/max/desired capacity, scaling policies (target tracking, step scaling) वापरून.

**Q16. Launch Template vs Launch Configuration?**
A: Launch Configuration जुना/immutable आहे (edit करता येत नाही, नवीन बनवावं लागतं). Launch Template नवीन, versioning support करतो, जास्त features (mixed instance types, Spot+On-Demand combo).

**Q17. EC2 instance stop आणि terminate मध्ये फरक काय?**
A: Stop = instance shutdown पण EBS volumes राहतात, नंतर restart करता येतं (billing फक्त EBS साठी). Terminate = instance permanently delete, root EBS (default) पण delete होतो.

**Q18. Instance ला IAM role का लावतात, access keys का नाही?**
A: IAM Role temporary, auto-rotating credentials देते — hardcoded keys पेक्षा जास्त secure, key leak होण्याचा धोका नाही.

**Q19. EC2 instance चा CPU credit (T-series burstable) म्हणजे काय?**
A: T-series instances (t2/t3) baseline पेक्षा जास्त CPU वापरण्यासाठी credits जमा/खर्च करतात. Credits संपले की performance throttle होते (unless unlimited mode).

**Q20. Elastic Network Interface (ENI) म्हणजे काय?**
A: Virtual network card जी instance ला attach होते — private IP, security groups, MAC address असते. एक instance ला multiple ENIs attach करता येतात.

**Q21. EC2 instance मध्ये disk जागा संपली, कसं handle कराल?**
A: EBS volume resize करा (`modify-volume`), नंतर OS मध्ये filesystem extend करा (`growpart` + `resize2fs`/`xfs_growfs`) — downtime शिवाय शक्य.

**Q22. Dedicated Host vs Dedicated Instance?**
A: Dedicated Host = entire physical server तुमच्यासाठी allocate, licensing (BYOL) साठी उपयुक्त. Dedicated Instance = hardware dedicated पण host-level control नाही.

**Q23. EC2 instance खूप वेळा crash/reboot होतोय, कसं debug कराल?**
A: System log check करा (Console > Get System Log), CloudWatch metrics (CPU, memory, StatusCheckFailed), OOM killer logs, underlying hardware issue असल्यास AWS support case.

**Q24. Hibernate feature म्हणजे काय?**
A: Instance stop करताना RAM चा content EBS root volume वर save होतो, restart केल्यावर RAM state restore होते (faster boot, in-memory data टिकतं).

**Q25. EC2 Auto Recovery म्हणजे काय?**
A: CloudWatch alarm (StatusCheckFailed_System) trigger झाल्यावर instance त्याच configuration सह automatically दुसऱ्या hardware वर recover होतो.

**Q26. Security patching EC2 fleet वर कसं manage कराल?**
A: AWS Systems Manager (SSM) Patch Manager वापरून scheduled patching, Golden AMI approach (नवीन patched AMI बनवून rolling replace).

**Q27. Instance ला outbound internet हवं आहे पण inbound नको, कसं कराल?**
A: Private subnet मध्ये instance ठेवा, NAT Gateway मार्फत outbound traffic द्या, कोणताही public IP/inbound rule देऊ नका.

**Q28. EC2 pricing model मध्ये "Convertible" Reserved Instance म्हणजे काय?**
A: Instance family/OS/tenancy बदलण्याची flexibility देणारा RI प्रकार (Standard RI पेक्षा कमी discount पण जास्त flexible).

**Q29. Termination Protection म्हणजे काय?**
A: Accidental terminate होऊ नये म्हणून instance वर लावलेला flag — enable असल्यास console/CLI मधून directly terminate करता येत नाही, आधी disable करावं लागतं.

**Q30. EC2 instance खूप वेळा CPU 100% दाखवतोय, root cause कसं शोधाल?**
A: `top`/`htop` ने process ओळखा, CloudWatch detailed monitoring enable करा, application logs/APM (Datadog) मध्ये slow queries/loops check करा, right-sizing गरज आहे का बघा.

**Q31. Golden AMI pipeline म्हणजे काय?**
A: Packer सारखं tool वापरून automated, tested, hardened AMI तयार करणं आणि CI/CD मध्ये त्याच AMI ला version करून deploy करणं — consistency साठी.

**Q32. EC2 instance च्या root volume चा encryption कसा लावाल?**
A: AMI/launch वेळी "Encrypt this volume" option, किंवा account-level default encryption enable करा (`EnableEbsEncryptionByDefault`), KMS key वापरून.

**Q33. Tenancy options कोणते आहेत (Shared, Dedicated, Host)?**
A: Shared (default, multiple customers same hardware), Dedicated Instance (hardware dedicated to account), Dedicated Host (specific physical server, licensing control).

**Q34. Spot Instance interruption कसं handle कराल application मध्ये?**
A: Spot interruption notice (2 min आधी) CloudWatch Events/metadata द्वारे मिळतो — graceful shutdown logic लावा, stateless design ठेवा, checkpoint save करा.

**Q35. EC2 Instance Connect म्हणजे काय?**
A: Browser-based SSH access, temporary key push करून — permanent key pair शिवाय secure access देतो (IAM permission based).

**Q36. Multiple AZ मध्ये instances का ठेवतात?**
A: High Availability साठी — एक AZ down झाला तरी दुसऱ्या AZ मधले instances traffic serve करत राहतात.

**Q37. EC2 Fleet म्हणजे काय?**
A: एकाच वेळी multiple instance types/purchase options (On-Demand+Spot mix) मधून desired capacity launch करणारी feature.

**Q38. Enhanced Networking म्हणजे काय?**
A: SR-IOV वापरून higher bandwidth, lower latency, lower CPU utilization — specific instance types + drivers (ENA) आवश्यक.

**Q39. EC2 instance ला attach केलेला EBS volume "stuck" (busy) दाखवतोय detach करताना, काय कराल?**
A: आधी instance वरून unmount करा (`umount`), volume ला I/O operations चालू नाहीयेत ना confirm करा, force detach (शेवटचा उपाय, data corruption risk).

**Q40. Cross-account AMI share कसं कराल?**
A: AMI च्या permissions मध्ये target account ID add करा (`modify-image-attribute`), जर encrypted असेल तर KMS key policy मध्येही access द्यावा लागतो.

**Q41. EC2 instance boot वेळ जास्त लागतोय, कसं optimize कराल?**
A: Smaller/optimized AMI वापरा, User Data script मध्ये heavy operations कमी करा, EBS-optimized instance वापरा, gp3 volume (better baseline IOPS).

**Q42. Nitro-based instances चं वैशिष्ट्य काय?**
A: Dedicated hardware/software (Nitro hypervisor) मुळे better performance, security isolation, higher network/storage throughput.

**Q43. EC2 instance खर्च कमी करण्यासाठी काय कराल (cost optimization)?**
A: Right-sizing, Reserved/Savings Plans, unused/stopped instances identify करा, Auto Scaling (idle वेळेस scale down), Spot for non-critical workloads.

**Q44. Instance launch fail होतोय "InsufficientInstanceCapacity" error, काय कराल?**
A: वेगळा AZ try करा, वेगळा instance type/size try करा, On-Demand Capacity Reservation वापरा critical workload साठी.

**Q45. EC2 वर license-included vs BYOL (Bring Your Own License) म्हणजे काय?**
A: License-included = AWS software license cost instance price मध्ये समाविष्ट (उदा. Windows AMI). BYOL = तुमचा स्वतःचा license वापरता, Dedicated Host आवश्यक असू शकतो compliance साठी.

**Q46. Instance च्या Security Group मध्ये बदल केला, तो live instances वर लगेच apply होतो का?**
A: हो, Security Group changes immediately effective होतात — instance restart करावं लागत नाही.

**Q47. EC2 Instance वर Systems Manager Session Manager कसा वापराल (SSH शिवाय)?**
A: SSM Agent installed + IAM role (AmazonSSMManagedInstanceCore) attach केल्यावर, Console/CLI मधून browser-based shell मिळतो — port 22 open करण्याची गरज नाही.

**Q48. Capacity Reservation म्हणजे काय?**
A: विशिष्ट AZ मध्ये ठराविक instance capacity reserve करणं (billing चालू राहतं वापरा किंवा नाही), guaranteed availability हवं असल्यास वापरतात.

**Q49. EC2 fleet मध्ये rolling AMI update (patch/upgrade) कसं कराल zero downtime सह?**
A: नवीन Launch Template version (नवीन AMI सह) बनवा, ASG instance refresh (`start-instance-refresh`) वापरा — batch by batch old instances replace होतात, ALB health check pass झाल्यावरच पुढे जातं.

**Q50. EC2 चं billing कसं calculate होतं (per-second)?**
A: Linux instances per-second billing (minimum 60 seconds), Windows/other OS per-hour. Stopped instance फक्त attached EBS/EIP साठी charge होतो, compute साठी नाही.

---

# TOPIC 2: ECS / Fargate / ECR (50 Questions)

**Q1. ECS म्हणजे काय?**
A: Elastic Container Service — AWS ची fully managed container orchestration service, Docker containers चालवण्यासाठी/manage करण्यासाठी.

**Q2. EC2 launch type vs Fargate launch type?**
A: EC2 = तुम्ही cluster infra (instances) manage करता. Fargate = serverless, AWS underlying infra manage करतं, तुम्ही फक्त CPU/memory define करता.

**Q3. Task Definition म्हणजे काय?**
A: Container(s) साठी blueprint — image, CPU/memory, port mappings, environment variables, IAM roles, logging config यांचं JSON definition.

**Q4. Task आणि Service मध्ये फरक?**
A: Task = task definition चं एक running instance. Service = specified count of tasks सतत healthy ठेवते, ALB integration, auto-restart करते.

**Q5. ECS Cluster म्हणजे काय?**
A: Logical grouping of tasks/services — EC2 instances (capacity) किंवा Fargate capacity provider वापरून तयार होतं.

**Q6. Task Role vs Execution Role?**
A: Execution Role = ECS agent ला ECR image pull, CloudWatch logs create करण्यासाठी permissions. Task Role = container च्या आतल्या application कोड ला AWS API calls (S3, DynamoDB इ.) करण्यासाठी permissions.

**Q7. ECS Service मधलं rolling deployment कसं होतं?**
A: `minimumHealthyPercent` आणि `maximumPercent` वापरून control होतं — जुने tasks टप्प्याटप्प्याने नवीन tasks ने replace होतात, health check pass झाल्यावरच पुढचा टप्पा.

**Q8. Capacity Provider म्हणजे काय?**
A: Cluster ला कोणत्या infra वर (EC2 ASG किंवा Fargate/Fargate Spot) tasks run करायचे ते ठरवणारी strategy — capacity provider strategy द्वारे weight/base सेट करता येतो.

**Q9. Fargate Spot म्हणजे काय?**
A: Fargate चा discounted (up to 70% स्वस्त) पर्याय, unused capacity वापरतो — interruption शक्य, fault-tolerant/batch workloads साठी उपयुक्त.

**Q10. ECR म्हणजे काय?**
A: Elastic Container Registry — AWS ची private/public Docker image registry, IAM integrated.

**Q11. ECR ला image push करण्याचे steps सांगा.**
A: `aws ecr get-login-password | docker login`, नंतर `docker tag`, नंतर `docker push` — repository आधी create केलेली असावी लागते.

**Q12. ECR Lifecycle Policy म्हणजे काय?**
A: जुन्या/untagged images automatically delete करण्यासाठी rule (उदा. "keep last 10 images") — storage cost control साठी.

**Q13. ECS task स्टार्ट होत नाहीये, कसं debug कराल?**
A: `describe-tasks` मधून `stoppedReason` बघा, CloudWatch Logs check करा, execution role permissions (ECR pull) confirm करा, task CPU/memory पुरेसं आहे का बघा.

**Q14. "CannotPullContainerError" चा अर्थ काय आणि कारणं?**
A: Image pull fail झाला — चुकीचा image URI, execution role ला ECR permission नाही, VPC मध्ये internet/VPC endpoint access नाही.

**Q15. ECS Service Auto Scaling कसं configure कराल?**
A: Application Auto Scaling वापरून target tracking policy (उदा. CPUUtilization 50%) किंवा step scaling लावतात — desired count त्यानुसार वाढतो/कमी होतो.

**Q16. Fargate मध्ये persistent storage कशी वापराल?**
A: EFS (Elastic File System) mount करता येतं task definition मध्ये — ephemeral container storage पेक्षा persistent, shared storage हवं असल्यास.

**Q17. ECS मध्ये Service Discovery कसं काम करतं?**
A: AWS Cloud Map सोबत integrate होऊन प्रत्येक service ला DNS name मिळतो (उदा. `myservice.local`) — microservices मध्ये एकमेकांना शोधण्यासाठी.

**Q18. ECS Task मध्ये multiple containers (sidecar pattern) का वापरतात?**
A: Main app container सोबत logging agent, proxy (Envoy), किंवa monitoring agent एकत्र run करण्यासाठी — त्याच network namespace/task मध्ये.

**Q19. awsvpc network mode म्हणजे काय?**
A: प्रत्येक task ला स्वतःचा ENI आणि private IP मिळतो — Security Groups task-level लावता येतात, Fargate साठी mandatory mode आहे.

**Q20. ECS Deployment Circuit Breaker म्हणजे काय?**
A: Deployment fail झाल्यास (tasks सतत crash होत असतील) automatically rollback करणारी feature — manual intervention शिवाय.

**Q21. ECS मध्ये Blue/Green deployment कसं कराल?**
A: AWS CodeDeploy integration वापरून — नवीन task set वेगळ्या target group वर deploy, traffic shift (all-at-once/canary/linear), जुना task set terminate.

**Q22. Task Definition मध्ये environment variables आणि secrets कसे pass कराल?**
A: Plain env vars `environment` field मध्ये, sensitive data साठी `secrets` field वापरून Secrets Manager/SSM Parameter Store मधून inject करतात.

**Q23. ECS मध्ये container health check कसं define कराल?**
A: Task definition मध्ये `healthCheck` field (command, interval, timeout, retries) — container-level health tracking, ALB target group health check पेक्षा वेगळं.

**Q24. Fargate task ला किती CPU/Memory combinations allowed आहेत?**
A: Fixed combinations आहेत (उदा. 0.25 vCPU with 0.5-2GB, 1 vCPU with 2-8GB इ.) — AWS docs मध्ये specific supported values आहेत.

**Q25. ECS EC2 launch type मध्ये "bin packing" म्हणजे काय?**
A: Placement strategy जी cluster च्या instances वर tasks efficiently pack करते (जागा वाया न घालवता) — cost optimization साठी.

**Q26. ECS Task placement strategies कोणते?**
A: `binpack` (resource efficient), `random`, `spread` (AZ/instance वर evenly distribute — HA साठी).

**Q27. ECS Service ला ALB शी कसं जोडाल?**
A: Service create करताना target group specify करा, container port map करा — ECS automatically tasks register/deregister करतं target group मध्ये.

**Q28. ECS Exec म्हणजे काय?**
A: Running container च्या आत directly shell access (`aws ecs execute-command`) देणारी feature — SSH शिवाय debugging साठी.

**Q29. ECS मध्ये logging कसं configure कराल?**
A: `awslogs` log driver वापरून task definition मध्ये log group/region/stream-prefix द्या — logs automatically CloudWatch Logs कडे जातात.

**Q30. ECS task memory limit ओलांडली तर काय होतं?**
A: Container OOM (Out Of Memory) होऊन kill होतो, task restart होतो (जर service मध्ये असेल तर) — logs मध्ये "OutOfMemoryError" दिसतं.

**Q31. Fargate vs EC2 launch type — cost comparison कधी कोणतं स्वस्त पडतं?**
A: Steady, predictable, high-utilization workload साठी EC2 (with Reserved/Savings) स्वस्त पडतं. Variable/spiky/low-ops-overhead workload साठी Fargate फायदेशीर (जरी per-unit महाग असलं तरी).

**Q32. ECS Cluster मध्ये EC2 instances "draining" state म्हणजे काय?**
A: Instance ला cluster मधून काढण्याआधी त्यावरचे tasks gracefully दुसरीकडे move करण्यासाठी वापरतात — जेणेकरून abrupt task termination होत नाही.

**Q33. ECR मध्ये vulnerability scanning कसं करता?**
A: Enhanced/Basic image scanning enable करा (push वर automatic scan किंवा on-demand) — CVE वगैरे findings ECR console मध्ये दिसतात.

**Q34. ECS Task मध्ये "essential" container फील्ड म्हणजे काय?**
A: जर essential=true असलेला container stop/fail झाला तर संपूर्ण task stop होतो. Non-essential (sidecar) container fail झाल्यास task चालू राहू शकतो.

**Q35. Cross-account ECR image pull कसं कराल?**
A: ECR repository policy मध्ये target account ला `GetDownloadUrlForLayer`, `BatchGetImage` permissions द्या, target account च्या task execution role ला त्या ECR वर access हवा.

**Q36. ECS मध्ये "Reservation" vs "Limit" (CPU/Memory) म्हणजे काय (EC2 launch type)?**
A: Reservation = guaranteed minimum resources container साठी. Limit = maximum वापरता येईल इतकं (hard cap) — Reservation पेक्षा जास्त असू शकतं (burst).

**Q37. ECS Service Connect म्हणजे काय?**
A: Cloud Map पेक्षा advanced service-to-service communication feature — built-in traffic management, observability (metrics) सह.

**Q38. Fargate task launch वेळ जास्त लागतोय, कसं optimize कराल?**
A: Smaller image size (multi-stage build), fewer layers, ECR मध्येच image ठेवा (VPC endpoint वापरून faster pull), unnecessary sidecars कमी करा.

**Q39. ECS Cluster Auto Scaling (EC2 launch type) कसं काम करतं?**
A: ASG + Capacity Provider managed scaling — tasks साठी पुरेशी capacity नसेल तर नवीन EC2 instances automatically launch होतात.

**Q40. ECR image immutability म्हणजे काय?**
A: Tag immutability enable केलं की एकदा push केलेला tag (उदा. `v1.0`) परत overwrite करता येत नाही — accidental overwrite रोखण्यासाठी.

**Q41. ECS task मध्ये ulimits कसे set कराल?**
A: Task definition मध्ये `ulimits` field (उदा. nofile, nproc) container-level resource limits साठी वापरतात.

**Q42. ECS Deployment मध्ये "Canary" strategy कशी implement कराल?**
A: CodeDeploy मार्फत ठराविक % traffic नवीन version कडे पाठवून (उदा. 10%), काही वेळ monitor करून, बाकी सगळं traffic shift करतात जर सगळं ठीक असेल.

**Q43. ECS Fargate मध्ये VPC networking कसं काम करतं (subnet placement)?**
A: Private subnet मध्ये tasks ठेवून NAT Gateway मार्फत outbound द्या (ECR pull साठी) किंवा VPC Endpoints (ECR, S3, CloudWatch Logs) वापरून NAT शिवायच काम भागवा.

**Q44. ECS Task Definition revisions म्हणजे काय?**
A: प्रत्येक वेळी task definition update केली की नवीन revision (version number) तयार होतो — जुन्या revisions rollback साठी वापरता येतात.

**Q45. ECS मध्ये Container Insights म्हणजे काय?**
A: CloudWatch Container Insights enable केल्यावर cluster/service/task level detailed metrics (CPU, memory, network) आणि dashboards मिळतात.

**Q46. ECS Fargate platform version म्हणजे काय?**
A: Fargate च्या underlying infra चं version (उदा. 1.4.0) — नवीन features/security patches त्यासोबत येतात, task definition मध्ये specify करता येतं.

**Q47. Multiple environments (dev/staging/prod) साठी ECS setup कसं design कराल?**
A: वेगवेगळे clusters (किंवा namespace/tags वापरून एकाच cluster मध्ये separate services), वेगवेगळे task definitions/parameter values, Terraform modules वापरून consistency ठेवा.

**Q48. ECS Task ला SSM Parameter Store मधून secret कसा inject कराल?**
A: Task definition च्या `secrets` array मध्ये parameter ARN द्या, execution role ला `ssm:GetParameters` permission द्या.

**Q49. ECS Service update करताना "desired count" 0 केलं तर काय होतं?**
A: सगळे running tasks gracefully stop होतात (service मात्र exist करत राहते, फक्त 0 tasks running) — temporary shutdown साठी उपयुक्त, delete करण्याची गरज नाही.

**Q50. ECS troubleshooting साठी कोणते logs/tools सर्वात आधी बघाल?**
A: `aws ecs describe-tasks` (stoppedReason), CloudWatch Logs (application logs), Container Insights metrics, ALB target group health, ECR pull errors — या क्रमाने.

---

# TOPIC 3: Lambda (50 Questions)

**Q1. AWS Lambda म्हणजे काय?**
A: Serverless compute service — server provision/manage न करता code run करता येतो, event-driven, automatically scale होतो.

**Q2. Lambda cold start म्हणजे काय?**
A: नवीन execution environment initialize होताना (container spin-up + runtime + code load) लागणारा extra latency.

**Q3. Cold start कसा कमी कराल?**
A: Provisioned Concurrency, smaller package size, unnecessary dependencies काढा, language choice (Python/Node faster than Java for cold start).

**Q4. Lambda max timeout आणि memory limit काय आहे?**
A: Max timeout 15 minutes, memory 128MB ते 10,240MB (proportionally CPU सुद्धा वाढतं).

**Q5. Lambda function ला कोणकोणते triggers असू शकतात?**
A: S3 events, API Gateway, EventBridge (schedule/event pattern), SQS, SNS, DynamoDB Streams, Kinesis, ALB.

**Q6. Lambda Layers म्हणजे काय?**
A: Common code/dependencies (libraries) वेगळ्या ZIP मध्ये package करून multiple functions मध्ये reuse करण्याची feature.

**Q7. Lambda execution role म्हणजे काय?**
A: IAM role जी function ला इतर AWS services access करण्यासाठी permissions देते (उदा. S3 read, DynamoDB write).

**Q8. Synchronous vs Asynchronous invocation?**
A: Synchronous (API Gateway) = caller response ची वाट बघतो. Asynchronous (S3, SNS) = event queue होतो, Lambda नंतर process करतं, retry logic built-in (2 retries).

**Q9. Dead Letter Queue (DLQ) Lambda सोबत कसं वापरतात?**
A: Async invocation fail झाल्यास (सगळे retries संपल्यावर) event SQS/SNS DLQ मध्ये पाठवला जातो, नंतर analyze/reprocess करण्यासाठी.

**Q10. Lambda Destinations म्हणजे काय?**
A: DLQ पेक्षा advanced — success आणि failure दोन्हीसाठी वेगळे targets (SQS, SNS, Lambda, EventBridge) configure करता येतात.

**Q11. Provisioned Concurrency म्हणजे काय?**
A: ठराविक संख्येने execution environments आधीच "warm" ठेवणे — cold start टाळण्यासाठी, extra cost लागतो.

**Q12. Reserved Concurrency म्हणजे काय?**
A: Function साठी max concurrent executions ची मर्यादा — इतर functions चं account-level concurrency वाचवण्यासाठी/throttle control साठी.

**Q13. Lambda VPC मध्ये असेल तर काय implications आहेत?**
A: ENI attach करावं लागतं (आधी slow, आता Hyperplane ENI मुळे fast), private resources (RDS) access करण्यासाठी गरजेचं, पण internet access साठी NAT Gateway लागतो.

**Q14. Lambda function version आणि alias म्हणजे काय?**
A: Version = immutable snapshot of code+config (numbered). Alias = pointer जो एका version कडे (किंवा traffic-split साठी दोन versions कडे) point करतो — production/staging सारखं manage करण्यासाठी.

**Q15. Lambda मध्ये environment variables कसे encrypt कराल?**
A: Default AWS managed key ने किंवा customer-managed KMS key वापरून encrypt होतात, sensitive data साठी Secrets Manager वापरणं जास्त चांगलं.

**Q16. Lambda@Edge म्हणजे काय?**
A: CloudFront edge locations वर चालणारं Lambda — viewer/origin request-response modify करण्यासाठी, low-latency edge processing.

**Q17. Lambda function मध्ये "Throttling" error आला तर काय अर्थ आहे?**
A: Concurrency limit ओलांडली गेली — account/function level concurrent execution limit पेक्षा जास्त requests आले, वाढवण्यासाठी limit increase request करावी लागते किंवा reserved concurrency वाढवा.

**Q18. Lambda Function URL म्हणजे काय?**
A: API Gateway शिवाय direct HTTPS endpoint Lambda ला expose करण्याची feature — simple use-cases साठी.

**Q19. Lambda मध्ये idempotency का महत्त्वाची आहे?**
A: Async invocations retries करतात (duplicate events शक्य) — त्यामुळे function ने same input वर multiple वेळा चालवलं तरी same result/side-effect यावं (उदा. duplicate DB entries टाळण्यासाठी).

**Q20. Lambda cost कसा calculate होतो?**
A: Number of requests + duration (GB-seconds: memory allocated x execution time) यावर आधारित — Free tier नंतर pay-per-use.

**Q21. Step Functions सोबत Lambda कसं वापरतात?**
A: Complex, multi-step workflows (state machine) मध्ये प्रत्येक step एक Lambda function असू शकतो — orchestration, error handling, retries built-in.

**Q22. Lambda function "ENOMEM"/Out of memory error देतोय, काय कराल?**
A: Memory allocation वाढवा (config update), code मध्ये memory leaks/large payload processing check करा, streaming approach वापरा मोठ्या data साठी.

**Q23. Lambda मध्ये /tmp storage किती मिळते?**
A: Default 512MB, configurable up to 10,240MB (ephemeral storage) — temporary file processing साठी.

**Q24. Lambda function local testing कसं कराल?**
A: SAM CLI (`sam local invoke`), Docker-based local Lambda runtime, unit tests mock events सह.

**Q25. Lambda मध्ये Custom Runtime म्हणजे काय?**
A: AWS-supported runtimes (Python/Node/Java इ.) व्यतिरिक्त तुमची स्वतःची language/runtime वापरण्याची सोय (Runtime API वापरून).

**Q26. Lambda function API Gateway सोबत integrate करताना timeout mismatch issue काय आहे?**
A: API Gateway चा max timeout 29 seconds आहे, पण Lambda 15 min पर्यंत चालू शकतो — यामुळे long-running tasks साठी Gateway timeout आधी येऊ शकतो, Async pattern वापरावा लागतो.

**Q27. Lambda mध्ये concurrent executions चं account-level default limit काय आहे?**
A: Default 1000 concurrent executions per region (increase request करता येतो).

**Q28. Lambda "unreserved concurrency" म्हणजे काय?**
A: Account concurrency limit मधून reserved concurrency असलेल्या functions वजा करून उरलेला pool — बाकीच्या (non-reserved) functions नी share केलेला.

**Q29. Lambda function मध्ये external API call slow आहे, काय optimize कराल?**
A: Connection reuse (global scope मध्ये client initialize करा, handler च्या बाहेर), timeout/retry tuning, parallel calls (Promise.all/asyncio).

**Q30. Lambda Powertools म्हणजे काय?**
A: AWS ची open-source library जी logging, tracing, metrics, idempotency यासाठी best practices सोप्या पद्धतीने implement करायला मदत करते.

**Q31. Lambda function deploy करताना package size limit काय आहे?**
A: Zipped: 50MB (direct upload), unzipped: 250MB, container image: 10GB (ECR वापरून).

**Q32. Container image म्हणून Lambda deploy का करतात (ZIP ऐवजी)?**
A: मोठ्या dependencies (ML models, native libraries), existing Docker workflow reuse, 10GB पर्यंत size support.

**Q33. Lambda function मध्ये X-Ray tracing कसं enable कराल?**
A: Function configuration मध्ये "Active Tracing" enable करा, execution role ला X-Ray permissions द्या — distributed tracing/latency breakdown मिळतो.

**Q34. Lambda function एकाच वेळी multiple events (batch) कसे process करतं (SQS trigger)?**
A: SQS trigger batch size configure करता येतो (उदा. 10 messages together), function एका invocation मध्ये array process करतं.

**Q35. Lambda function SQS मधून messages process करताना partial failure कसं handle कराल?**
A: "Report Batch Item Failures" feature वापरून फक्त fail झालेले specific messages queue मध्ये परत ठेवा (सगळा batch retry नको).

**Q36. Lambda चं cold start Java मध्ये जास्त का असतं?**
A: JVM startup + class loading overhead जास्त आहे Python/Node च्या तुलनेत — SnapStart feature (Java साठी) वापरून हे कमी करता येतं.

**Q37. Lambda SnapStart म्हणजे काय?**
A: Pre-initialized execution environment snapshot (Firecracker microVM) घेऊन तो resume करण्याची technique — Java cold start drastically कमी करते.

**Q38. Lambda मध्ये environment variable "AWS_LAMBDA_FUNCTION_NAME" सारखे built-in variables का उपयोगी आहेत?**
A: Runtime info (function name, memory size, log group) code मध्ये access करण्यासाठी — hardcode न करता dynamic behavior साठी.

**Q39. Lambda function ला RDS शी connect करताना connection pooling issue काय येते?**
A: प्रत्येक concurrent invocation नवीन DB connection उघडू शकतं — DB connection limit संपू शकते. RDS Proxy वापरून connection pooling/reuse करावं.

**Q40. RDS Proxy म्हणजे काय आणि Lambda सोबत का वापरतात?**
A: Managed connection pooler जो Lambda च्या high-concurrency connections ला efficiently pool/reuse करतो, DB overload टाळतो.

**Q41. Lambda function मध्ये retries कसे manage कराल (custom logic)?**
A: Exponential backoff + jitter implement करा (विशेषतः external API calls साठी), max retry count define करा, circuit breaker pattern वापरा.

**Q42. Event Source Mapping म्हणजे काय?**
A: Lambda आणि streaming/queue sources (SQS, Kinesis, DynamoDB Streams) मधलं configuration जे poll करून events Lambda ला पाठवतं.

**Q43. Lambda function मध्ये global/static variables (handler बाहेर) का ठेवतात?**
A: Execution environment reuse झाल्यास (warm start) हे variables persist राहतात — DB connections, SDK clients cache करण्यासाठी उपयुक्त, performance सुधारते.

**Q44. Lambda function fail झालं तर CloudWatch मध्ये कुठे बघाल?**
A: `/aws/lambda/<function-name>` log group मध्ये — errors, stack traces, START/END/REPORT lines (duration, memory used) असतात.

**Q45. Lambda function ला scheduled (cron) पद्धतीने कसं चालवाल?**
A: EventBridge Rule मध्ये schedule expression (`cron()` किंवा `rate()`) वापरून Lambda ला target म्हणून जोडा.

**Q46. Multi-region Lambda deployment strategy काय असू शकते?**
A: Same code/infra (Terraform/SAM) वेगवेगळ्या regions मध्ये deploy, Route 53 latency/failover routing वापरून traffic direct करा.

**Q47. Lambda function मधली "REPORT" log line काय सांगते?**
A: Duration, Billed Duration, Memory Size, Max Memory Used, Init Duration (cold start असेल तर) — performance tuning साठी उपयुक्त.

**Q48. Lambda security best practices कोणत्या?**
A: Least privilege IAM role, secrets hardcode न करता Secrets Manager/SSM वापरा, VPC मध्ये गरज असेल तरच ठेवा, dependencies regularly update करा (vulnerability scanning).

**Q49. Lambda मध्ये "Provisioned Concurrency" आणि Auto Scaling एकत्र कसं वापराल?**
A: Application Auto Scaling वापरून Provisioned Concurrency ला schedule/target-tracking based वाढवा-कमी करा (उदा. traffic pattern नुसार).

**Q50. Lambda function टेस्ट करताना "test event" कसं वापराल आणि production मध्ये मॉनिटर कसं कराल?**
A: Console मध्ये sample test event (JSON) तयार करून manually invoke करा; production साठी CloudWatch Alarms (Errors, Throttles, Duration metrics) + Datadog APM वापरून सतत monitor करा.

---
