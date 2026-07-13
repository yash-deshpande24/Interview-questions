# Interview Q&A — Part 2: ALB, VPC, RDS, S3, IAM (50 each)

---

# TOPIC 4: ALB — Application Load Balancer (50 Questions)

**Q1. ALB म्हणजे काय?**
A: Application Load Balancer — Layer 7 (HTTP/HTTPS) load balancer, path/host-based routing support करतो.

**Q2. ALB, NLB, CLB मध्ये फरक काय?**
A: ALB = Layer 7, advanced routing. NLB = Layer 4, high performance/static IP. CLB = legacy, basic Layer 4/7.

**Q3. Target Group म्हणजे काय?**
A: Backend resources (EC2, ECS tasks, Lambda, IP addresses) चा group जिथे ALB traffic route करतो.

**Q4. Health Check कसं काम करतं?**
A: ALB ठराविक interval ने target group मधल्या targets ला specific path वर request पाठवतो, response code (उदा. 200) बघून healthy/unhealthy ठरवतो.

**Q5. Health check fail होत असेल तर काय check कराल?**
A: Health check path/port बरोबर आहे का, app त्या path वर 200 देतंय का, Security Group मध्ये ALB->target traffic allow आहे का, response timeout threshold.

**Q6. Path-based routing म्हणजे काय?**
A: `/api/*` एका target group कडे, `/images/*` दुसऱ्याकडे — listener rules वापरून एकाच domain वर वेगवेगळे services.

**Q7. Host-based routing म्हणजे काय?**
A: `api.example.com` वेगळ्या target group कडे, `app.example.com` वेगळ्या कडे — same ALB, वेगवेगळे listener rules.

**Q8. Listener म्हणजे काय?**
A: ALB वर configured port+protocol (उदा. 443/HTTPS) जे incoming connections check करतं आणि rules नुसार target group कडे forward करतं.

**Q9. Listener Rule Priority कसं काम करतं?**
A: Rules ला priority number असतो (कमी number = आधी check होतो), match झाल्यावर बाकीच्या rules skip होतात, शेवटी default action.

**Q10. SSL/TLS termination ALB वर कसं होतं?**
A: ACM certificate ALB listener (443) ला attach करतात — client-ALB traffic encrypted, ALB-target traffic (backend) plain HTTP किंवा पुन्हा re-encrypt करता येतो.

**Q11. Sticky Sessions म्हणजे काय?**
A: Same client चे requests सतत same target कडे पाठवण्यासाठी cookie-based mechanism (application-based किंवा duration-based cookie).

**Q12. Cross-Zone Load Balancing म्हणजे काय?**
A: Traffic सगळ्या AZs मधल्या targets वर evenly distribute करणं (एकाच AZ पुरतं मर्यादित न ठेवता) — ALB मध्ये default enabled असतं.

**Q13. ALB Access Logs कुठे store होतात आणि का वापरतात?**
A: S3 bucket मध्ये store होतात — request details (client IP, latency, target, response code) analyze/audit साठी.

**Q14. ALB "504 Gateway Timeout" error चा अर्थ काय?**
A: Target ने ALB च्या idle timeout (default 60 sec) च्या आत response दिला नाही — application slow आहे किंवा target unresponsive आहे.

**Q15. ALB Idle Timeout कसं बदलाल?**
A: ALB attribute `idle_timeout.timeout_seconds` update करून (default 60s, वाढवता/कमी करता येतो).

**Q16. WAF ALB सोबत कसं integrate करतात?**
A: AWS WAF Web ACL ALB ला directly associate करतात — SQL injection, XSS, rate-limiting rules लावता येतात traffic वर.

**Q17. ALB Target Group मध्ये Deregistration Delay म्हणजे काय?**
A: Target unhealthy/removed झाल्यावर existing in-flight connections complete होण्यासाठी दिलेला वेळ (default 300s) — abrupt connection drop टाळण्यासाठी (connection draining).

**Q18. ALB HTTP ते HTTPS redirect कसं कराल?**
A: Port 80 listener वर एक rule बनवा जी automatically HTTPS (443) कडे redirect करते (Action: Redirect, 301).

**Q19. ALB मध्ये multiple target groups weighted routing कसं कराल (canary)?**
A: Listener rule action मध्ये "Forward" action साठी multiple target groups ला weight (%) देऊन traffic split करता येतो.

**Q20. ALB चा "Unhealthy Threshold" आणि "Healthy Threshold" म्हणजे काय?**
A: Consecutive failed checks नंतर target unhealthy मार्क होतो (Unhealthy Threshold), consecutive successful checks नंतर परत healthy होतो (Healthy Threshold).

**Q21. ALB Fixed Response Action म्हणजे काय?**
A: Backend target कडे न पाठवता ALB directly custom response (status code, body, content-type) देऊ शकतं — maintenance page सारख्या use case साठी.

**Q22. ALB वर multiple Security Groups का लावतात?**
A: Layered access control साठी — एक SG inbound traffic (internet) साठी, ते backend targets कडे कोणतं traffic पाठवायचं ते वेगळ्या SG rules ने control होतं.

**Q23. ALB ECS/Fargate सोबत कसं integrate होतं?**
A: ECS Service creation वेळी target group specify करतात, container port map होतो, ECS automatically tasks register/deregister करतं target group मध्ये (dynamic port mapping सह).

**Q24. ALB "502 Bad Gateway" कशामुळे येतो?**
A: Target ने invalid/malformed response पाठवला, target crash झाला, किंवा target group मध्ये कोणतेही healthy targets नाहीत.

**Q25. ALB मध्ये Authentication (OIDC/Cognito) कसं लावाल?**
A: Listener rule मध्ये "Authenticate" action वापरून Cognito User Pool किंवा कोणताही OIDC provider सोबत integrate करून backend च्या आधीच authentication करता येतं.

**Q26. Internal ALB vs Internet-facing ALB?**
A: Internet-facing = public IP, internet वरून access होतो. Internal = private IP फक्त, VPC च्या आतूनच access, microservices मधल्या internal communication साठी.

**Q27. ALB Access Log मध्ये "target_status_code" आणि "elb_status_code" वेगळे का असू शकतात?**
A: ALB स्वतःहून एरर देऊ शकतं (उदा. auth failure, WAF block) जे target पर्यंत पोहोचतच नाही — त्यामुळे दोन्ही codes वेगळे दिसू शकतात.

**Q28. ALB Connection Draining/Deregistration Delay कमी ठेवल्यास काय होईल?**
A: Deployment वेळी in-flight requests अचानक तुटू शकतात (abrupt termination), user experience वर परिणाम होतो — म्हणून पुरेसा वेळ ठेवणं महत्त्वाचं.

**Q29. ALB वापरून Blue/Green deployment कसं कराल manually?**
A: दोन target groups (Blue, Green) बनवा, listener rule मध्ये traffic gradually Green कडे shift करा (weighted routing), सगळं ठीक असल्यावर 100% shift करा.

**Q30. ALB Request Tracing कसं कराल (X-Amzn-Trace-Id)?**
A: ALB प्रत्येक request ला automatically trace ID header add करतो — distributed tracing (X-Ray) साठी वापरता येतो.

**Q31. ALB target group मध्ये IP type targets कधी वापरतात (Instance type ऐवजी)?**
A: Fargate tasks, on-premises servers (VPN/Direct Connect द्वारे), किंवा वेगळ्या VPC मधले targets जोडण्यासाठी.

**Q32. ALB चं "Slow Start" feature म्हणजे काय?**
A: नवीन जोडलेल्या target ला हळूहळू traffic पाठवणं (लगेच full traffic न देता) — warm-up period देण्यासाठी (JVM warm-up सारख्या cases साठी).

**Q33. ALB वर rate limiting कसं कराल?**
A: थेट ALB मध्ये built-in rate limiting नाही — WAF rate-based rule वापरून specific IP/pattern वरून येणारं traffic limit करता येतं.

**Q34. ALB Access Log format मध्ये कोणती महत्त्वाची fields असतात?**
A: Timestamp, client IP, target IP, request processing time, target processing time, response processing time, ELB status code, target status code, request (method/path).

**Q35. Multiple listeners एकाच ALB वर असू शकतात का?**
A: हो — उदा. 80 (redirect), 443 (HTTPS traffic), प्रत्येक listener ची स्वतःची rules असतात.

**Q36. ALB target group protocol version (HTTP1/HTTP2/gRPC) कधी बदलाल?**
A: gRPC-based microservices साठी HTTP/2 किंवा gRPC protocol version निवडावा लागतो target group मध्ये.

**Q37. ALB वर "Desync mitigation mode" म्हणजे काय?**
A: HTTP request smuggling attacks पासून बचाव करण्यासाठी strict/defensive/monitor modes उपलब्ध आहेत.

**Q38. ALB मध्ये Client IP preservation कसं होतं?**
A: X-Forwarded-For header मध्ये original client IP पाठवला जातो (कारण ALB स्वतः proxy असल्याने source IP backend ला थेट दिसत नाही).

**Q39. ALB वापरून Maintenance mode कसं implement कराल?**
A: Fixed response action (503 status + custom message) सर्व traffic साठी temporarily लावा, नंतर normal forward action परत आणा.

**Q40. ALB Target Group Attributes मध्ये "slow_start.duration_seconds" काय करतो?**
A: नवीन target ला किती सेकंदात हळूहळू 0% ते 100% traffic द्यायचं हे ठरवतो.

**Q41. ALB मध्ये multi-value headers कधी लागतात?**
A: Lambda targets साठी response मध्ये same header multiple वेळा (उदा. multiple Set-Cookie) असल्यास एनेबल करावं लागतं.

**Q42. Access logs enable करायला कोणती permission लागते S3 bucket ला?**
A: ALB service account ला bucket policy मध्ये PutObject permission द्यावी लागते (region-specific ELB service account ARN).

**Q43. ALB target group मध्ये "unused" targets राहिले तर काय issue येऊ शकतो?**
A: Deregistered/stale targets जर काढले नाहीत तर health check unnecessarily fail दाखवू शकतात, alerts trigger होऊ शकतात.

**Q44. ALB वर WebSocket support आहे का?**
A: हो, ALB WebSocket आणि HTTP/2 दोन्ही support करतो (Layer 7 असल्याने).

**Q45. ALB target group मध्ये Lambda function कसं target म्हणून वापराल?**
A: Target type "lambda" निवडून function ARN द्या — ALB HTTP request ला Lambda event format मध्ये convert करून पाठवतो.

**Q46. ALB चं pricing model कसं आहे?**
A: LCU (Load Balancer Capacity Unit) based — new connections, active connections, processed bytes, rule evaluations यावर आधारित.

**Q47. ALB troubleshooting साठी सर्वप्रथम कुठे बघाल?**
A: Target group health status, Access Logs (S3), CloudWatch metrics (HealthyHostCount, TargetResponseTime, HTTPCode_Target_5XX_Count).

**Q48. ALB मध्ये "TargetResponseTime" metric high दाखवत असेल तर काय अर्थ?**
A: Backend application स्वतः slow आहे (ALB चा issue नाही) — DB query, external API, resource contention तपासा.

**Q49. ALB वेगवेगळ्या Availability Zones मध्ये कसं काम करतं?**
A: ALB nodes प्रत्येक enabled AZ मध्ये असतात (redundancy साठी) — किमान 2 AZ subnets specify करणं mandatory आहे.

**Q50. ALB समोर CloudFront ठेवण्याचा फायदा काय?**
A: Edge caching, DDoS protection (extra layer), global latency कमी, static content offload होतं ALB/backend वरून.

---

# TOPIC 5: VPC (50 Questions)

**Q1. VPC म्हणजे काय?**
A: Virtual Private Cloud — तुमचं स्वतःचं logically isolated network AWS मध्ये, IP range, subnets, routing तुम्ही control करता.

**Q2. VPC चे मुख्य components कोणते?**
A: Subnets, Route Tables, Internet Gateway, NAT Gateway, Security Groups, NACLs, VPC Peering, VPN/Direct Connect.

**Q3. Public vs Private subnet?**
A: Public subnet route table मध्ये `0.0.0.0/0 -> IGW` route असतो. Private subnet ला direct internet access नसतो.

**Q4. Internet Gateway (IGW) म्हणजे काय?**
A: VPC ला internet सोबत जोडणारा horizontally scaled, redundant component — public subnet resources साठी.

**Q5. NAT Gateway म्हणजे काय आणि कधी वापरतात?**
A: Private subnet मधल्या instances ला outbound internet access देतो (inbound न देता) — package updates, external API calls साठी.

**Q6. NAT Gateway vs NAT Instance?**
A: NAT Gateway = managed, highly available, जास्त bandwidth, कमी maintenance. NAT Instance = self-managed EC2, स्वस्त पण manual scaling/HA.

**Q7. Security Group vs NACL?**
A: SG = instance-level, stateful, फक्त allow rules. NACL = subnet-level, stateless, allow+deny दोन्ही, rule numbers नुसार evaluate.

**Q8. VPC Peering म्हणजे काय?**
A: दोन VPCs मध्ये direct network connection (private IP द्वारे communication) — transitive नाही (A-B, B-C peered तरी A-C automatically जोडलं जात नाही).

**Q9. VPC Peering ची limitation काय आहे?**
A: Non-transitive peering, overlapping CIDR ranges असतील तर peering शक्य नाही, region/account across peering शक्य आहे पण जास्त complex.

**Q10. Transit Gateway म्हणजे काय?**
A: Central hub जो multiple VPCs आणि on-premises networks एकत्र जोडतो — VPC Peering च्या मानाने scalable (transitive routing शक्य).

**Q11. VPC Endpoint म्हणजे काय?**
A: Internet/NAT Gateway शिवाय privately AWS services (S3, DynamoDB इ.) कडे connect करण्याची सोय.

**Q12. Gateway Endpoint vs Interface Endpoint?**
A: Gateway Endpoint = फक्त S3 आणि DynamoDB साठी, route table मध्ये entry. Interface Endpoint = ENI-based (PrivateLink), बाकी बऱ्याच services साठी, cost लागतो per hour+data.

**Q13. CIDR block म्हणजे काय?**
A: Classless Inter-Domain Routing — IP address range define करण्याची पद्धत (उदा. 10.0.0.0/16 = 65,536 IPs).

**Q14. VPC मध्ये किती subnets ठेवावेत (design विचार)?**
A: प्रत्येक AZ साठी किमान एक public + एक private subnet (HA साठी), database साठी वेगळे isolated private subnets.

**Q15. Route Table म्हणजे काय?**
A: Subnet चं traffic कुठे जायचं (local, IGW, NAT, peering) हे ठरवणारा rules चा संच.

**Q16. VPC Flow Logs म्हणजे काय?**
A: VPC मधल्या network interfaces वरचं IP traffic capture करून CloudWatch Logs/S3 मध्ये पाठवणारी feature — troubleshooting/security analysis साठी.

**Q17. Default VPC आणि Custom VPC मध्ये फरक?**
A: Default VPC AWS automatically प्रत्येक region मध्ये तयार करतं (सगळे subnets public), Custom VPC तुम्ही स्वतःच्या गरजेनुसार design करता (better security control).

**Q18. VPC मध्ये instances एकमेकांशी बोलू शकत नाहीयेत, troubleshoot कसं कराल?**
A: Security Groups (दोन्ही बाजूंचे), NACLs, Route Tables, subnet placement (same/different VPC), VPC Peering status (जर वेगळ्या VPC मध्ये असतील) check करा.

**Q19. Elastic IP आणि VPC चा संबंध काय?**
A: Elastic IP public subnet मधल्या instance ला static public IP देतो — IGW route असल्याशिवाय उपयोगी नाही.

**Q20. VPC Peering मध्ये DNS resolution कसं enable कराल?**
A: Peering connection च्या options मध्ये "Enable DNS Resolution" flag enable करावा लागतो दोन्ही बाजूंनी.

**Q21. Multiple VPCs मध्ये overlapping CIDR असेल तर काय problem येते?**
A: Peering किंवा Transit Gateway जोडता येत नाही (routing ambiguity) — design वेळीच non-overlapping ranges ठरवणं महत्त्वाचं.

**Q22. VPC मध्ये Bastion Host म्हणजे काय?**
A: Public subnet मधला एक hardened EC2 instance जो private subnet मधल्या resources कडे secure SSH access देण्यासाठी entry point म्हणून वापरतात.

**Q23. Bastion Host ऐवजी काय modern alternative आहे?**
A: AWS Systems Manager Session Manager — SSH port उघडण्याची गरज नाही, IAM-based access, logging built-in.

**Q24. NACL rules कशा प्रकारे evaluate होतात?**
A: Rule numbers ascending order मध्ये (lowest first) check होतात, पहिला matching rule apply होतो — त्यामुळे rule ordering महत्त्वाची.

**Q25. VPC मध्ये "main route table" म्हणजे काय?**
A: Explicitly दुसऱ्या route table शी associate न केलेले सगळे subnets default main route table वापरतात.

**Q26. Site-to-Site VPN म्हणजे काय?**
A: On-premises network आणि VPC मधलं encrypted IPsec tunnel connection, internet द्वारे.

**Q27. Direct Connect म्हणजे काय आणि VPN पेक्षा वेगळं कसं?**
A: Direct Connect = dedicated private physical connection (internet न वापरता), जास्त reliable/consistent bandwidth. VPN = internet-based, स्वस्त, सोपं सेटअप.

**Q28. VPC Subnet चा size कसा ठरवाल (planning)?**
A: Expected number of resources + growth buffer विचारात घेऊन (AWS प्रत्येक subnet मधले पहिले 4 आणि शेवटचा IP reserve करतं).

**Q29. Egress-Only Internet Gateway म्हणजे काय?**
A: IPv6 resources साठी outbound-only internet access देणारा gateway (NAT Gateway चं IPv6 equivalent).

**Q30. VPC मध्ये multi-AZ architecture का design करतात?**
A: High Availability — एक AZ fail झाला तरी दुसऱ्या AZ मधले resources काम करत राहतात.

**Q31. Security Group मध्ये source म्हणून दुसरा Security Group कधी वापरतात?**
A: Dynamic IPs असलेल्या resources (Auto Scaling instances) मध्ये traffic allow करण्यासाठी — IP hardcode करण्याऐवजी SG-to-SG reference वापरतात.

**Q32. VPC Flow Logs मध्ये "REJECT" आणि "ACCEPT" काय दर्शवतात?**
A: Security Group/NACL ने traffic allow केलं (ACCEPT) की deny केलं (REJECT) ते दाखवतं — troubleshooting साठी उपयुक्त.

**Q33. PrivateLink म्हणजे काय?**
A: VPC Interface Endpoints च्या मागची technology जी internet न वापरता privately services (तुमचे स्वतःचे किंवा third-party SaaS) expose/consume करायला मदत करते.

**Q34. VPC मध्ये DHCP Options Set म्हणजे काय?**
A: DNS servers, domain name, NTP servers सारखे network configuration parameters instances ला देण्यासाठी.

**Q35. Subnet ला multiple Route Tables associate करता येतात का?**
A: नाही, एका subnet ला एकावेळी फक्त एकच route table associate असू शकतो (पण एक route table अनेक subnets ला associate करता येतो).

**Q36. VPC design मध्ये "three-tier architecture" कसं mapped होतं?**
A: Public subnet (ALB/web tier), Private subnet (app/compute tier - EC2/ECS), Private/Isolated subnet (database tier - RDS).

**Q37. VPC मध्ये IPv6 support कसं add कराल?**
A: VPC ला IPv6 CIDR block associate करा (Amazon-provided किंवा BYOIP), subnets ला IPv6 ranges द्या, route table मध्ये Egress-Only IGW route.

**Q38. Network Load Balancer (NLB) साठी VPC मध्ये काय विशेष लागतं?**
A: Static IP प्रति AZ (Elastic IP देखील attach करता येतो), Layer 4 असल्याने source IP preservation automatically होतं.

**Q39. VPC मध्ये Shared VPC (Resource Access Manager) म्हणजे काय?**
A: एका central account च्या VPC मधले subnets दुसऱ्या AWS accounts सोबत share करण्याची सोय — centralized networking, multiple teams.

**Q40. VPC Peering मध्ये Route Table update न केल्यास काय होतं?**
A: Peering connection active असूनही traffic route होणार नाही — दोन्ही बाजूंच्या route tables मध्ये peering CIDR कडे जाणारा route add करावाच लागतो.

**Q41. VPC troubleshooting टूल "Reachability Analyzer" म्हणजे काय?**
A: Source ते destination पर्यंत नेटवर्क path automatically analyze करून कुठे block होतंय ते दाखवणारं tool (SG/NACL/route issues ओळखायला मदत).

**Q42. NAT Gateway High Availability कशी design कराल?**
A: प्रत्येक AZ मध्ये स्वतंत्र NAT Gateway ठेवा (एकच शेअर्ड NAT Gateway single point of failure ठरू शकतं cross-AZ traffic charges सुद्धा).

**Q43. VPC मध्ये "ENI" (Elastic Network Interface) कोणकोणत्या ठिकाणी दिसते?**
A: EC2 instances, Lambda (VPC-attached), NAT Gateway, ALB nodes, RDS — सगळीकडे ENI असते (private IP + SG सह).

**Q44. Route 53 Resolver (VPC context मध्ये) म्हणजे काय?**
A: On-premises आणि VPC मधल्या DNS resolution ला जोडणारी service (hybrid DNS setups साठी, Inbound/Outbound endpoints).

**Q45. VPC मध्ये Security Group चा "stateful" behavior example द्या.**
A: Inbound rule ने port 443 traffic allow केला तर त्याच connection चा return traffic (outbound) automatically allow होतो, वेगळा outbound rule लागत नाही.

**Q46. NACL stateless असल्याने काय काळजी घ्यावी लागते?**
A: Inbound rule allow केलं तरी त्या response साठी outbound rule वेगळा (ephemeral ports 1024-65535 साठी) explicitly allow करावा लागतो.

**Q47. VPC design करताना subnet साठी IP exhaustion टाळण्यासाठी काय कराल?**
A: पुरेसा CIDR range आधीच plan करा (growth विचारात घेऊन), secondary CIDR blocks add करण्याची शक्यता ठेवा, IPv6 विचार करा मोठ्या scale साठी.

**Q48. VPC मध्ये Multiple NAT Gateways cost कसा कमी कराल?**
A: गरज नसेल तिथे VPC Endpoints (S3, DynamoDB) वापरून NAT Gateway traffic कमी करा (data processing charges वाचतात).

**Q49. Cross-Region VPC Peering शक्य आहे का?**
A: हो, Inter-Region VPC Peering शक्य आहे — पण Transit Gateway (with peering) मोठ्या multi-region setups साठी जास्त scalable पर्याय आहे.

**Q50. VPC security audit करताना कोणत्या गोष्टी सर्वात आधी check कराल?**
A: Open Security Groups (0.0.0.0/0 on sensitive ports), unused ENIs, Flow Logs enabled आहेत का, NACL rules योग्य आहेत का, public subnet मध्ये sensitive resources (DB) तर नाहीत ना.

---

# TOPIC 6: RDS (50 Questions)

**Q1. RDS म्हणजे काय?**
A: Relational Database Service — managed relational database (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora) — patching, backup, HA AWS manage करतं.

**Q2. RDS Multi-AZ म्हणजे काय?**
A: High Availability साठी — synchronous replication दुसऱ्या AZ मधल्या standby instance कडे, automatic failover.

**Q3. Read Replica म्हणजे काय?**
A: Asynchronous replication वापरून scalability साठी — read traffic offload करण्यासाठी, वेगळ्या region मध्येही असू शकतो.

**Q4. Multi-AZ vs Read Replica प्रमुख फरक?**
A: Multi-AZ = HA/DR साठी (एकच standby, automatic failover, read करता येत नाही सहसा — Aurora मध्ये करता येतं). Read Replica = read scalability साठी (multiple replicas, manual promote करावं लागतं failover साठी).

**Q5. RDS automated backups कसे काम करतात?**
A: Daily snapshot + transaction logs दर 5 मिनिटांनी — point-in-time recovery शक्य (retention period max 35 days).

**Q6. Manual snapshot vs automated backup?**
A: Manual = user-triggered, retention limit नाही (manually delete करेपर्यंत राहतो). Automated = scheduled, retention period नंतर automatically delete होतो.

**Q7. RDS Encryption कसं लावतात?**
A: Creation वेळी "Enable Encryption" (KMS key वापरून) — existing unencrypted DB ला encrypt करण्यासाठी snapshot घेऊन encrypted copy बनवावी लागते.

**Q8. RDS Parameter Group म्हणजे काय?**
A: Database engine configuration settings (उदा. max_connections) group करून apply करण्याची पद्धत — instance ला attach करतात.

**Q9. RDS Option Group म्हणजे काय?**
A: Additional database features (उदा. Oracle साठी specific plugins) enable करण्यासाठी वापरतात.

**Q10. RDS Aurora म्हणजे काय आणि वेगळं कसं आहे?**
A: AWS ची proprietary, cloud-native relational database (MySQL/PostgreSQL compatible) — better performance, storage auto-scaling (up to 128TB), 6-way replication across 3 AZs.

**Q11. Aurora Serverless म्हणजे काय?**
A: On-demand, auto-scaling Aurora — capacity automatically वाढते/कमी होते traffic नुसार, idle वेळेस pause होऊ शकतं (cost saving).

**Q12. RDS Proxy म्हणजे काय?**
A: Managed database proxy जो connection pooling करतो — विशेषतः Lambda सारख्या high-concurrency clients साठी उपयुक्त, failover वेळ कमी करतो.

**Q13. RDS storage types कोणते?**
A: General Purpose SSD (gp2/gp3), Provisioned IOPS SSD (io1/io2, high-performance workload), Magnetic (legacy).

**Q14. RDS Failover process कसं होतं (Multi-AZ)?**
A: Primary fail झाल्यास DNS endpoint automatically standby कडे point होतो (typically 60-120 sec) — application ला code change ची गरज नाही (same endpoint).

**Q15. RDS Maintenance Window म्हणजे काय?**
A: ठराविक weekly time slot जेव्हा AWS patches/updates apply करतं — यादरम्यान brief downtime (Multi-AZ असल्यास minimal) शक्य.

**Q16. RDS Performance Insights म्हणजे काय?**
A: Database load आणि performance bottlenecks (top SQL queries, wait events) visualize करणारी monitoring feature.

**Q17. RDS Snapshot दुसऱ्या region मध्ये कसं copy कराल (DR साठी)?**
A: `copy-db-snapshot` API/console वापरून cross-region copy करता येतो — Disaster Recovery strategy साठी.

**Q18. RDS instance खूप slow आहे, troubleshooting कसं कराल?**
A: Performance Insights/CloudWatch मध्ये CPU, Connections, ReadLatency/WriteLatency बघा, slow query logs enable करा, indexes check करा, connection pool exhaustion आहे का बघा.

**Q19. RDS मध्ये "Storage Autoscaling" म्हणजे काय?**
A: Storage जागा संपत आल्यास automatically वाढते (threshold + max limit define करून) — manual intervention शिवाय.

**Q20. RDS Subnet Group म्हणजे काय?**
A: RDS instance कोणत्या subnets मध्ये (कोणत्या AZs मध्ये) launch होऊ शकतो हे define करणारा group — Multi-AZ साठी किमान 2 AZs लागतात.

**Q21. RDS वर Security कशी लावाल (access control)?**
A: Security Groups (network level), IAM database authentication (password ऐवजी IAM token), encryption at rest+in transit, least-privilege DB users.

**Q22. IAM Database Authentication म्हणजे काय?**
A: Traditional password ऐवजी IAM-generated temporary tokens वापरून DB ला authenticate करण्याची पद्धत — credential rotation ची गरज नाही.

**Q23. RDS backup retention कमाल किती दिवस ठेवता येते?**
A: Automated backups साठी max 35 days, त्यापुढे manual snapshots (unlimited retention, manually delete करेपर्यंत).

**Q24. RDS Read Replica ला Master बनवणं (Promote) कधी करतात?**
A: Master fail झाल्यास किंवा planned failover/migration साठी — promote केल्यावर replica independent, writable instance बनतो.

**Q25. RDS instance resize (vertical scaling) करताना downtime येतो का?**
A: हो, सहसा brief downtime येतो (Multi-AZ असल्यास failover मुळे कमी होतो) — इंस्टन्स class बदलताना reboot आवश्यक असतो.

**Q26. RDS Connection Limit ओलांडली गेली, काय कराल?**
A: Parameter group मध्ये `max_connections` वाढवा (instance size नुसार मर्यादा असते), RDS Proxy वापरून connection pooling करा, application मधले idle connections बंद करा.

**Q27. Database migration RDS कडे कसं कराल (existing on-prem DB)?**
A: AWS Database Migration Service (DMS) वापरून — homogeneous किंवा heterogeneous (Schema Conversion Tool सह) migration, minimal downtime साठी CDC (Change Data Capture).

**Q28. RDS Event Notifications म्हणजे काय?**
A: SNS द्वारे RDS events (backup completed, failover, low storage इ.) साठी notifications subscribe करता येतात.

**Q29. RDS instance ला public access द्यावा का?**
A: सहसा नाही — Private subnet मध्ये ठेवावं, application/bastion मार्फतच access द्यावा, security best practice म्हणून public access disable ठेवावा.

**Q30. Aurora Global Database म्हणजे काय?**
A: Aurora primary region मधून इतर regions कडे low-latency replication (sub-second) — disaster recovery आणि global read scaling साठी.

**Q31. RDS वर "Blue/Green Deployment" feature म्हणजे काय?**
A: नवीन (Green) environment मध्ये changes (engine upgrade, schema) आधी test करून, नंतर switchover करण्याची managed feature — कमी downtime सह upgrade.

**Q32. RDS Instance class कसा निवडाल (sizing)?**
A: Workload प्रकार (OLTP/OLAP), expected connections, memory/CPU गरज, IOPS requirement यावर आधारित (Performance Insights वापरून बरोबर sizing ठरवता येतं).

**Q33. RDS instance वर "Deletion Protection" म्हणजे काय?**
A: Accidental delete होऊ नये म्हणून लावलेली safety flag — enable असल्यास आधी explicitly disable करावं लागतं delete करण्याआधी.

**Q34. RDS मध्ये Slow Query Log कसं enable कराल?**
A: Parameter group मध्ये `slow_query_log = 1` सेट करून, CloudWatch Logs export enable करून analyze करता येतो.

**Q35. RDS instance CPU 100% दाखवतोय, root cause कसं शोधाल?**
A: Performance Insights मध्ये top SQL statements बघा, missing indexes/inefficient queries शोधा, connection storm आहे का बघा, instance under-provisioned आहे का तपासा.

**Q36. RDS मध्ये Multi-AZ cluster (Aurora नाही) आणि Aurora Multi-AZ मध्ये फरक काय?**
A: Standard RDS Multi-AZ = 1 primary + 1 standby (storage independent replication). Aurora = shared distributed storage layer, 6 copies across 3 AZs, faster failover.

**Q37. RDS वर Cross-Region Read Replica का वापरतात?**
A: Disaster Recovery, latency कमी करण्यासाठी (जवळच्या region मधून वाचन), regional compliance requirements साठी.

**Q38. RDS instance वर "Enhanced Monitoring" म्हणजे काय?**
A: OS-level metrics (real-time, 1-60 sec granularity) — CPU, memory, disk, network — CloudWatch Basic Monitoring पेक्षा जास्त detailed.

**Q39. RDS मध्ये database credentials कसे secure ठेवाल?**
A: Secrets Manager वापरून auto-rotation सह store करा, application मध्ये hardcode कधीच करू नका, IAM auth वापरा शक्य असल्यास.

**Q40. RDS instance ला वेगळ्या VPC मधून कसं access कराल?**
A: VPC Peering किंवा Transit Gateway वापरून route जोडा, Security Group मध्ये source CIDR/SG allow करा.

**Q41. RDS Snapshot restore करताना नवीन instance च्या नावाबद्दल काय लक्षात ठेवाल?**
A: Snapshot restore केल्यावर नवीन DB instance (नवीन endpoint) तयार होतो — original instance replace होत नाही, application config update करावं लागतं.

**Q42. RDS मध्ये Character Set/Collation इशू आढळल्यास काय कराल?**
A: Parameter group मध्ये योग्य character_set/collation पॅरामीटर सेट करा, नवीन instance बनवताना initial creation वेळीच निवडणं सोपं असतं (नंतर बदलणं कठीण).

**Q43. RDS Automated minor version upgrade कसं काम करतं?**
A: "Auto minor version upgrade" enabled असल्यास maintenance window मध्ये automatically patch/upgrade होतो (security patches साठी उपयुक्त).

**Q44. Aurora Serverless v1 आणि v2 मध्ये फरक काय?**
A: v1 = coarse scaling steps, cold start delay असतो, pause/resume शक्य. v2 = fine-grained, fast scaling (seconds मध्ये), pause feature नाही पण जास्त production-ready.

**Q45. RDS instance ला Datadog सोबत कसं monitor कराल?**
A: Datadog Agent (integration) RDS CloudWatch metrics pull करतो (API-based, agent-less सुद्धा शक्य) — dashboards/alerts तयार करता येतात.

**Q46. RDS वर "Failover Priority" (tier) कशासाठी वापरतात (Read Replicas मध्ये)?**
A: Multi-AZ cluster (Aurora) मध्ये कोणता replica आधी promote व्हावा हे ठरवण्यासाठी tier (0-15) assign करता येतो.

**Q47. RDS restore point-in-time recovery (PITR) कसं कराल?**
A: Console/CLI मध्ये specific timestamp देऊन नवीन instance restore करता येतो (transaction logs वापरून) — 5-minute granularity पर्यंत.

**Q48. RDS instance disk जागा संपली तर काय होतं?**
A: Database "storage-full" state मध्ये जाऊन read-only/unavailable होऊ शकतो — Storage Autoscaling enable ठेवणं किंवा proactive monitoring (CloudWatch FreeStorageSpace alarm) महत्त्वाचं.

**Q49. RDS cost optimize करण्यासाठी काय कराल?**
A: Reserved Instances (predictable workload), right-sizing, unused read replicas काढा, storage type योग्य निवडा (gp3 सहसा स्वस्त), Aurora Serverless variable workload साठी.

**Q50. RDS Disaster Recovery strategy कशी design कराल?**
A: Multi-AZ (HA within region) + Cross-Region Read Replica/Snapshot copy (DR across regions) + regular automated backups + documented failover runbook + periodic DR drills.

---

# TOPIC 7: S3 (50 Questions)

**Q1. S3 म्हणजे काय?**
A: Simple Storage Service — object storage, 99.999999999% (11 nines) durability, unlimited scalability.

**Q2. S3 Storage Classes कोणते?**
A: Standard, Standard-IA, One Zone-IA, Intelligent-Tiering, Glacier Instant Retrieval, Glacier Flexible Retrieval, Glacier Deep Archive.

**Q3. S3 Standard vs Standard-IA कधी वापराल?**
A: Standard = frequently accessed data. Standard-IA = कमी वेळा access होणारा पण त्वरित हवा असणारा data (retrieval fee लागतो पण storage स्वस्त).

**Q4. S3 Intelligent-Tiering म्हणजे काय?**
A: Access pattern automatically monitor करून objects योग्य tier मध्ये move करतो (cost optimize करण्यासाठी), monitoring fee थोडा लागतो.

**Q5. S3 Versioning म्हणजे काय?**
A: Enable केल्यावर प्रत्येक object च्या सगळ्या versions store होतात — accidental delete/overwrite पासून संरक्षण.

**Q6. S3 Lifecycle Policy म्हणजे काय?**
A: ठराविक दिवसांनी objects एका storage class मधून दुसऱ्यात move किंवा delete करण्यासाठी rule.

**Q7. S3 bucket accidentally public झाला, कसं fix कराल?**
A: "Block Public Access" (account+bucket level) enable करा, bucket policy/ACL review करा, Access Analyzer वापरा.

**Q8. S3 Bucket Policy vs ACL?**
A: Bucket Policy = JSON-based, bucket-level, resource-based policy (granular control). ACL = legacy, object/bucket level basic permissions (आता कमी वापरतात).

**Q9. Presigned URL म्हणजे काय?**
A: Temporary, time-limited URL जो एखाद्याला (permission नसतानाही) विशिष्ट object access (upload/download) करू देतो.

**Q10. S3 Cross-Region Replication (CRR) म्हणजे काय?**
A: एका bucket मधले objects automatically दुसऱ्या region मधल्या bucket मध्ये replicate होतात — DR, latency reduction, compliance साठी.

**Q11. Same-Region Replication (SRR) कधी वापराल?**
A: Log aggregation, production-test account sync, compliance (data residency within region) साठी.

**Q12. S3 Event Notifications म्हणजे काय?**
A: Object create/delete सारख्या events वर Lambda/SQS/SNS trigger करण्याची feature.

**Q13. S3 Static Website Hosting म्हणजे काय?**
A: Bucket ला directly static website (HTML/CSS/JS) hosting साठी configure करता येतं — index/error document specify करून.

**Q14. S3 Encryption options कोणते?**
A: SSE-S3 (AWS managed key), SSE-KMS (customer/AWS managed KMS key, audit trail), SSE-C (customer-provided key), Client-side encryption.

**Q15. S3 Object Lock म्हणजे काय?**
A: WORM (Write Once Read Many) model — compliance requirements साठी objects ठराविक कालावधीसाठी delete/overwrite होऊ न देणे.

**Q16. S3 Transfer Acceleration म्हणजे काय?**
A: CloudFront edge locations वापरून faster upload/download (geographically दूरच्या clients साठी).

**Q17. S3 Multipart Upload कधी वापरतात?**
A: मोठ्या files (>100MB, recommended for >5GB) parallel parts मध्ये upload करण्यासाठी — faster, resume करता येतं fail झाल्यास.

**Q18. S3 Consistency Model काय आहे?**
A: आता S3 strong consistency देतो सगळ्या operations (read-after-write) साठी — पूर्वी eventual consistency होती काही cases मध्ये.

**Q19. S3 bucket नाव globally unique का असावं लागतं?**
A: कारण S3 bucket नावं DNS-compatible असतात आणि सगळ्या AWS accounts/regions मध्ये एकच namespace share होतं.

**Q20. S3 Access Points म्हणजे काय?**
A: मोठ्या shared buckets साठी वेगवेगळे applications/teams साठी वेगळे access points (त्यांचे स्वतःचे policy/network controls) तयार करण्याची feature.

**Q21. S3 Requester Pays म्हणजे काय?**
A: Bucket owner ऐवजी data download करणारा (requester) transfer cost भरतो — मोठ्या datasets share करताना उपयुक्त.

**Q22. S3 Glacier retrieval options कोणते?**
A: Expedited (1-5 min), Standard (3-5 hrs), Bulk (5-12 hrs) — जितकं जलद तितकं महाग.

**Q23. S3 bucket policy मध्ये "Deny" statement का महत्त्वाचा असतो?**
A: Explicit Deny सर्व Allow statements पेक्षा priority घेतो — विशिष्ट कठोर restrictions (उदा. non-HTTPS traffic deny) लावण्यासाठी उपयुक्त.

**Q24. S3 मध्ये "eventual consistency" कधी अजूनही लागू होते?**
A: List operations (काही edge cases) मध्ये — पण overall AWS ने (Dec 2020 पासून) strong read-after-write consistency आणली आहे सगळ्या operations साठी.

**Q25. CloudFront + S3 combo मध्ये Origin Access Control (OAC) कशासाठी वापरतात?**
A: S3 bucket फक्त CloudFront मार्फतच accessible ठेवण्यासाठी (direct S3 URL access block करून) — security best practice.

**Q26. S3 Inventory म्हणजे काय?**
A: Bucket मधल्या objects आणि त्यांच्या metadata चा scheduled report (CSV/ORC/Parquet) — auditing/analytics साठी.

**Q27. S3 Batch Operations म्हणजे काय?**
A: लाखो objects वर एकाच वेळी बल्क operation (copy, tag, ACL update, restore from Glacier) करण्याची feature.

**Q28. S3 bucket वर MFA Delete म्हणजे काय?**
A: Version delete/versioning disable करण्यासाठी MFA authentication compulsory करणारी extra security layer.

**Q29. S3 Select म्हणजे काय?**
A: SQL-like query वापरून object च्या आतल्या specific data (CSV/JSON/Parquet) फक्त retrieve करण्याची feature — संपूर्ण object न आणता.

**Q30. S3 mध्ये "prefix" आणि performance चा संबंध काय?**
A: पूर्वी prefix-based partitioning throughput वर परिणाम करत होती, आता S3 automatically scale होतं — तरी randomized prefixes high-throughput workload साठी अजूनही best practice मानतात.

**Q31. S3 bucket ला cross-account access कसा द्याल?**
A: Bucket policy मध्ये target account ID/role ARN ला specific actions (GetObject, PutObject) allow करा.

**Q32. S3 Object Tagging चा उपयोग काय?**
A: Cost allocation, lifecycle rules (tag-based), access control (IAM policy condition) साठी key-value tags लावतात.

**Q33. S3 CORS Configuration कधी लागते?**
A: Browser मधून वेगळ्या domain वरून (JavaScript) S3 objects directly access करायचे असल्यास (उदा. website वरून file upload).

**Q34. S3 Bucket Logging (Server Access Logging) म्हणजे काय?**
A: Bucket वरच्या सगळ्या requests चा detailed log दुसऱ्या bucket मध्ये store करणारी feature (audit/troubleshooting साठी).

**Q35. S3 आणि EBS मध्ये मूलभूत फरक काय?**
A: S3 = object storage (files, key-value, HTTP API), unlimited scale. EBS = block storage, EC2 ला attach होतो (single instance, filesystem level access).

**Q36. S3 Replication वापरताना delete markers replicate होतात का?**
A: Default मध्ये नाही — explicitly "Delete marker replication" enable करावं लागतं गरज असल्यास.

**Q37. S3 storage class analysis कसं कराल cost optimization साठी?**
A: S3 Storage Class Analysis tool access patterns बघून कोणते objects Standard-IA मध्ये move करावेत हे सुचवतं.

**Q38. S3 bucket मध्ये "orphaned" multipart uploads मुळे cost कसा वाढतो?**
A: Incomplete multipart uploads storage charge लावतात — Lifecycle rule वापरून ठराविक दिवसांनी automatically abort/cleanup करावं.

**Q39. S3 आणि IAM policy मध्ये "condition" कसा वापराल (उदा. IP restriction)?**
A: Bucket policy मध्ये `Condition` block (`aws:SourceIp`) वापरून specific IP ranges वरूनच access allow करता येतो.

**Q40. S3 pre-signed POST vs pre-signed GET URL मधला फरक काय?**
A: Pre-signed GET = download साठी. Pre-signed POST = browser वरून directly upload करण्यासाठी (form-based, additional policy conditions सह).

**Q41. S3 Object Ownership setting काय करते?**
A: Bucket owner सगळ्या uploaded objects चा owner राहील की uploader राहील हे ठरवतं — "Bucket owner enforced" सेटिंग ACLs disable करते (recommended).

**Q42. S3 mध्ये Glacier Deep Archive कधी वापराल?**
A: Compliance/long-term archival data जे वर्षातून क्वचितच access करावं लागतं (retrieval 12+ तास) — सर्वात स्वस्त storage class.

**Q43. S3 bucket delete करताना काय काळजी घ्याल?**
A: Bucket रिकामा (सगळे objects+versions delete) करावा लागतो आधी, Object Lock असल्यास delete शक्य नाही retention period संपेपर्यंत.

**Q44. S3 Access Analyzer म्हणजे काय?**
A: Bucket policies/ACLs analyze करून external/public access exposure ओळखणारं security tool.

**Q45. S3 मध्ये large file upload fail झाला तर काय कराल?**
A: Multipart upload वापरत असल्यास resume/retry करा failed parts, network issue असल्यास Transfer Acceleration वापरून बघा.

**Q46. S3 वापरून static + dynamic content (हायब्रिड website) कसं host कराल?**
A: Static assets S3+CloudFront वरून, dynamic API calls ALB/API Gateway+backend कडे — CloudFront मध्ये path-based behaviors वापरून route करा.

**Q47. S3 replication cross-account कधी वापरतात?**
A: Centralized backup/log account, compliance requirement (data separate account मध्ये ठेवणे) साठी.

**Q48. S3 bucket cost कसा कमी कराल?**
A: Lifecycle policies (IA/Glacier transition), Intelligent-Tiering, incomplete multipart cleanup, unnecessary versions delete करा, compression वापरा.

**Q49. S3 मध्ये "strong read-after-write consistency" चा practical फायदा काय?**
A: PUT केल्यानंतर लगेच GET केलं तरी latest data मिळतं (जुनी eventual consistency मध्ये race condition/stale read शक्य होतं).

**Q50. S3 troubleshooting साठी "Access Denied" error आल्यास काय check कराल?**
A: Bucket Policy, IAM Policy (user/role), ACL, Block Public Access settings, KMS key permissions (encrypted असल्यास), VPC Endpoint policy (private access असल्यास) — या क्रमाने.

---

# TOPIC 8: IAM (50 Questions)

**Q1. IAM म्हणजे काय?**
A: Identity and Access Management — AWS resources वर कोण (who), काय (what actions) करू शकतं हे control करणारी service.

**Q2. IAM User, Group, Role, Policy मध्ये फरक?**
A: User = individual identity. Group = users चा collection. Role = temporary credentials assume करण्यासाठी identity. Policy = actual permissions (JSON document).

**Q3. IAM Policy चे प्रकार कोणते?**
A: Managed Policy (AWS managed / Customer managed), Inline Policy (एका specific user/role/group ला directly attached).

**Q4. AWS Managed Policy vs Customer Managed Policy?**
A: AWS Managed = AWS ने तयार केलेली, standard use-cases साठी, AWS update करतं. Customer Managed = तुम्ही तयार केलेली, तुमच्या specific गरजेनुसार customize.

**Q5. IAM Role कधी वापरतात (User ऐवजी)?**
A: EC2/Lambda/ECS ला AWS services access देण्यासाठी, cross-account access साठी, federated users (SSO) साठी — temporary credentials असल्याने जास्त secure.

**Q6. Principle of Least Privilege म्हणजे काय?**
A: प्रत्येक identity ला त्यांच्या कामासाठी आवश्यक तेवढेच (जास्त नाही) permissions देणे.

**Q7. IAM Policy Evaluation Logic कसं काम करतं?**
A: Default Deny → Explicit Allow (कोणताही matching allow statement) → Explicit Deny (कोणताही deny असेल तर तो सर्वात आधी जिंकतो, override करतो).

**Q8. IAM मध्ये MFA (Multi-Factor Authentication) का महत्त्वाचं आहे?**
A: Password leak झाला तरी दुसरा factor (OTP/hardware token) शिवाय access मिळू शकत नाही — विशेषतः root account आणि privileged users साठी mandatory असावं.

**Q9. Root account कधी वापरावं?**
A: शक्यतो कधीच नाही daily operations साठी — फक्त account setup, billing changes, काही specific tasks (जे IAM user करू शकत नाही) साठीच.

**Q10. IAM Access Keys म्हणजे काय आणि कधी वापरतात?**
A: Programmatic access (CLI/SDK) साठी Access Key ID + Secret Access Key — शक्य असल्यास IAM Role वापरणं जास्त सुरक्षित (keys hardcode टाळण्यासाठी).

**Q11. IAM Access Key rotation कसं कराल?**
A: नवीन key तयार करा, application मध्ये update करा, जुनी key deactivate करा (काही दिवस), नंतर delete करा — zero-downtime rotation.

**Q12. Cross-Account Access कसा setup कराल IAM Role वापरून?**
A: Target account मध्ये Role तयार करा (Trust Policy मध्ये source account ID द्या), source account मधून `sts:AssumeRole` वापरून त्या role चे temporary credentials घ्या.

**Q13. IAM Policy मध्ये "Condition" block का वापरतात?**
A: विशिष्ट परिस्थितीतच (उदा. specific IP, MFA present, time-based) policy लागू व्हावी यासाठी extra restrictions.

**Q14. Resource-based Policy vs Identity-based Policy?**
A: Identity-based = user/group/role ला attach (काय actions करू शकतो हे सांगते). Resource-based = resource (S3 bucket, SQS queue) ला attach (कोण access करू शकतं हे सांगते).

**Q15. IAM Permission Boundary म्हणजे काय?**
A: User/Role ला maximum permissions ची मर्यादा घालणारी advanced feature — actual policy आणि boundary दोन्हीचा intersection म्हणजे effective permission.

**Q16. IAM Service Control Policies (SCP) म्हणजे काय?**
A: AWS Organizations मध्ये संपूर्ण account/OU साठी maximum permissions ची मर्यादा घालणारी policy (guardrails) — IAM policy पेक्षा वरच्या स्तरावर.

**Q17. IAM Access Analyzer म्हणजे काय?**
A: Resource policies analyze करून external/unintended access ओळखणारं tool (S3, IAM Role, KMS इ. साठी).

**Q18. IAM Credentials Report म्हणजे काय?**
A: सगळ्या users चे credentials status (password age, MFA enabled, access key age) दाखवणारा CSV report — audit साठी उपयुक्त.

**Q19. IAM Policy Simulator म्हणजे काय?**
A: Actual API call न करता एखादी policy काय permissions देते ते test करण्याचं tool.

**Q20. Federated Identity (SSO) म्हणजे काय?**
A: External identity provider (Okta, Azure AD, Google) वापरून AWS मध्ये login करणे — IAM users न बनवता SAML/OIDC वापरून.

**Q21. AWS SSO (IAM Identity Center) म्हणजे काय?**
A: Multiple AWS accounts साठी centralized single sign-on management — permission sets वापरून role-based access.

**Q22. IAM Instance Profile म्हणजे काय?**
A: IAM Role ला EC2 instance ला attach करण्यासाठी container — role थेट instance ला attach न करता instance profile द्वारे होतं.

**Q23. IAM Policy मध्ये wildcard (`*`) का टाळावा?**
A: Overly broad permissions देतो (सगळे resources/actions) — security risk, least privilege तत्त्वाच्या विरुद्ध.

**Q24. IAM मध्ये "Trust Policy" म्हणजे काय?**
A: Role कोण assume करू शकतं (कोणता principal — user/service/account) हे define करणारी policy — Role च्या permission policy पेक्षा वेगळी.

**Q25. IAM User साठी Password Policy कशी configure कराल?**
A: Minimum length, complexity requirements, expiration period, reuse prevention — Account settings मध्ये संपूर्ण account साठी लागू होते.

**Q26. IAM मध्ये "Deny" statement नेहमी "Allow" पेक्षा जिंकतो का?**
A: हो — Explicit Deny सगळ्या Allow statements ला override करतो, मग ते कोणत्याही policy मध्ये असो (identity/resource/SCP).

**Q27. Temporary Security Credentials (STS) म्हणजे काय?**
A: AWS Security Token Service द्वारे मिळणारे short-lived credentials (AssumeRole, GetSessionToken) — expiry असते, दीर्घकालीन keys पेक्षा सुरक्षित.

**Q28. IAM मध्ये "tag-based access control" (ABAC) म्हणजे काय?**
A: Resources/users वरच्या tags वापरून dynamic access control (उदा. "Project=X" tag असलेल्या resources नाच access) — role-based access पेक्षा जास्त flexible/scalable.

**Q29. IAM Role Session Duration म्हणजे काय?**
A: Assumed role चे credentials किती वेळ valid राहतील (default 1hr, max 12hrs पर्यंत configure करता येतं).

**Q30. IAM मध्ये अनोळखी/unused permissions कसे ओळखाल?**
A: IAM Access Analyzer + Access Advisor (last accessed data) वापरून कोणते services/actions खरंच वापरले गेलेत ते बघून unused permissions काढा.

**Q31. AssumeRole करताना "External ID" कशासाठी वापरतात?**
A: Third-party (vendor) cross-account access देताना "Confused Deputy Problem" टाळण्यासाठी — extra shared secret सारखं काम करतं.

**Q32. IAM Groups वर policy attach करणं का चांगली practice आहे (individual users ऐवजी)?**
A: Management सोपं होतं — नवीन user group मध्ये add केला की automatically त्याला त्या group च्या permissions मिळतात, individually manage करावं लागत नाही.

**Q33. IAM मध्ये Break Glass (Emergency Access) प्रोसेस म्हणजे काय?**
A: Critical परिस्थितीत (normal access बंद पडली तर) वापरण्यासाठी वेगळे, highly restricted, audited emergency credentials/procedure.

**Q34. IAM Role chaining म्हणजे काय?**
A: एका role मधून दुसऱ्या role ला assume करणे (role A -> role B) — session duration मर्यादित होते (max 1hr) अशा chained calls मध्ये.

**Q35. IAM Policy version कशी manage होते?**
A: Customer managed policy मध्ये max 5 versions ठेवता येतात, एक "default" version active असतो, rollback साठी जुनी version परत default करता येते.

**Q36. IAM मध्ये "NotAction"/"NotResource" कधी वापरतात?**
A: सगळ्या actions/resources ला allow/deny करून specific काही exclude करायचं असल्यास (उलट logic) — काळजीपूर्वक वापरावं लागतं कारण unintended broad access देऊ शकतं.

**Q37. Service-Linked Role म्हणजे काय?**
A: AWS service स्वतःसाठी automatically तयार करते (उदा. ECS, Auto Scaling साठी) — predefined permissions, delete/modify मर्यादित असतं.

**Q38. IAM Access Key exposed झाली (leaked) तर आधी काय कराल?**
A: लगेच ती key deactivate/delete करा, CloudTrail मध्ये त्या key ने काय actions झाल्या ते audit करा, नवीन key generate करा, root cause (कुठून leak झाली) शोधा.

**Q39. IAM मध्ये Organizations सोबत centralized logging कसं design कराल?**
A: सगळ्या member accounts चं CloudTrail एका central (log archive) account च्या S3 bucket मध्ये aggregate करा (cross-account bucket policy वापरून).

**Q40. IAM Policy मध्ये "Effect", "Action", "Resource" या तीन मुख्य elements चा अर्थ काय?**
A: Effect = Allow/Deny, Action = कोणती API operation (उदा. s3:GetObject), Resource = कोणत्या specific resource वर (ARN).

**Q41. IAM Users साठी programmatic access पूर्णपणे बंद करून काय alternative वापराल?**
A: IAM Identity Center (SSO) + Roles वापरून — users ला console/CLI साठी temporary federated credentials मिळतात, permanent access keys नकोत.

**Q42. IAM मध्ये "PassRole" permission का संवेदनशील (sensitive) मानतात?**
A: एखाद्या user ला दुसऱ्या (जास्त privileged) role एखाद्या service ला (EC2/Lambda) pass करण्याची परवानगी देतो — privilege escalation चा धोका असतो जर काळजीपूर्वक restrict केलं नाही तर.

**Q43. IAM मध्ये multi-account strategy साठी काय best practice आहे?**
A: AWS Organizations वापरून वेगवेगळे accounts (dev/staging/prod/security/logging), SCPs guardrails साठी, centralized IAM Identity Center access साठी.

**Q44. IAM Policy मध्ये JSON syntax error आल्यास काय कराल?**
A: IAM Policy Editor/Visual Editor वापरून validate करा, AWS Policy Validator (Access Analyzer) warnings बघा.

**Q45. IAM Role ला EC2 instance वर runtime मध्ये कसं बदलाल (attach केलेली role बदलणे)?**
A: Instance profile दुसऱ्या role शी replace/associate करता येतो instance running असतानाच (reboot ची गरज नाही), पण existing processes ला नवीन credentials मिळायला थोडा वेळ लागू शकतो.

**Q46. IAM Access Undenied/CloudTrail वापरून access issues कसे debug कराल?**
A: CloudTrail मध्ये "AccessDenied" events शोधा — कोणती policy block करतेय ते event details मध्ये (errorMessage) दिसतं.

**Q47. IAM मध्ये compliance साठी periodic access review कसा कराल?**
A: Access Advisor (last accessed), Credentials Report, Access Analyzer regularly (उदा. quarterly) review करून unused/over-privileged access काढा.

**Q48. IAM policy मध्ये "aws:MultiFactorAuthPresent" condition कशासाठी वापरतात?**
A: संवेदनशील actions (उदा. resource delete) फक्त MFA-authenticated session असेल तरच allow करण्यासाठी.

**Q49. IAM मध्ये Terraform वापरून policies manage करण्याचा फायदा काय?**
A: Version controlled, reviewable (PR process), consistent across environments, drift detection शक्य (console मधून manual changes टाळता येतात).

**Q50. IAM troubleshooting साठी "Access Denied" आल्यास कोणत्या क्रमाने बघाल?**
A: 1) Identity-based policy (user/role/group), 2) Resource-based policy, 3) Permission Boundary, 4) SCP (Organizations), 5) Session policy (assumed role असल्यास) — सगळीकडे explicit deny नाहीये आणि किमान एक allow आहे याची खात्री करा.

---
