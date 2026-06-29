# DevOps Interview Q&A — Linux, Git, GitHub, AWS, Docker, Terraform

---

## 🐧 LINUX

**Q1. What is Linux and why is it used in DevOps?**
A. Linux is an open-source operating system. DevOps mein use hota hai kyunki ye stable, secure, customizable, aur server environments (cloud, containers) mein most widely used OS hai.

**Q2. Difference between absolute path and relative path?**
A. Absolute path root (`/`) se start hota hai, jaise `/home/user/file.txt`. Relative path current directory se start hota hai, jaise `./file.txt` ya `../folder`.

**Q3. What is the use of `chmod` command?**
A. File/directory ki permissions change karne ke liye — read(4), write(2), execute(1). Example: `chmod 755 file.sh`.

**Q4. Difference between `chmod` and `chown`?**
A. `chmod` permissions change karta hai (read/write/execute). `chown` file ka owner/group change karta hai (`chown user:group file`).

**Q5. How do you check running processes in Linux?**
A. `ps aux` ya `top`/`htop` use karte hain. `top` real-time CPU/memory usage dikhata hai.

**Q6. How to kill a process?**
A. `kill <PID>` ya force kill ke liye `kill -9 <PID>`. PID `ps` ya `top` se milta hai.

**Q7. What is a cron job?**
A. Scheduled task automatically run karne ke liye — `crontab -e` se edit karte hain. Format: `* * * * * command` (minute hour day month weekday).

**Q8. Difference between soft link and hard link?**
A. Soft link (`ln -s`) ek pointer hota hai original file ko, agar original delete ho jaye to link broken ho jata hai. Hard link actual data block share karta hai, original delete hone par bhi data accessible rehta hai.

**Q9. What is grep used for?**
A. Text/pattern search karne ke liye. Example: `grep "error" logfile.txt`.

**Q10. Difference between `apt` and `yum`?**
A. Dono package managers hain — `apt` Debian/Ubuntu based systems mein use hota hai, `yum`/`dnf` RedHat/CentOS based systems mein.

**Q11. How to check disk space usage?**
A. `df -h` (disk free, human readable) overall disk space ke liye, `du -sh <folder>` specific folder size ke liye.

**Q12. What is the difference between `>` and `>>`?**
A. `>` file overwrite karta hai, `>>` existing file mein append karta hai.

**Q13. How to check network connectivity?**
A. `ping <ip/domain>`, `netstat -tulnp` (open ports check), `traceroute` (path check).

**Q14. What is the difference between a process and a thread?**
A. Process ek independent execution unit hai with its own memory space. Thread process ke andar ka lightweight unit hai jo same memory share karta hai.

**Q15. How to find a file in Linux?**
A. `find /path -name "filename"` ya `locate filename`.

---

## 🔧 GIT

**Q1. What is Git and why is it used?**
A. Git ek distributed version control system hai jo code changes track karta hai, multiple developers ko parallel kaam karne deta hai, aur history maintain karta hai.

**Q2. Difference between Git and GitHub?**
A. Git ek tool hai (version control system), GitHub ek cloud platform hai jaha Git repositories host hoti hain (collaboration ke liye).

**Q3. What is the difference between `git pull` and `git fetch`?**
A. `git fetch` remote se changes download karta hai but local branch merge nahi karta. `git pull` = fetch + merge dono ek saath.

**Q4. What is a merge conflict and how do you resolve it?**
A. Jab same line/file do branches mein alag-alag change hoti hai aur merge karte time Git decide nahi kar pata kaunsa rakhna hai, tab conflict aata hai. Manually conflict markers (`<<<<`, `====`, `>>>>`) edit karke resolve karte hain, then `git add` + `git commit`.

**Q5. Difference between `git merge` and `git rebase`?**
A. `git merge` dono branches ki history combine karta hai with a merge commit. `git rebase` commits ko replay karta hai dusri branch ke top par, jisse history linear/clean rehti hai.

**Q6. What is `git stash`?**
A. Uncommitted changes temporarily save karke working directory clean karne ke liye, baad mein `git stash pop` se wapas le sakte ho.

**Q7. Difference between `git reset` and `git revert`?**
A. `git reset` commit history change karta hai (HEAD move karta hai, dangerous on shared branches). `git revert` naya commit banata hai jo previous commit ko undo karta hai (safe for shared branches).

**Q8. What is `.gitignore` used for?**
A. Files/folders specify karne ke liye jo Git track nahi karega (jaise `node_modules`, `.env`, log files).

**Q9. What is the difference between `git branch` and `git checkout -b`?**
A. `git branch <name>` sirf branch create karta hai. `git checkout -b <name>` branch create + switch dono karta hai.

**Q10. What is HEAD in Git?**
A. HEAD ek pointer hai jo current branch ke latest commit ko point karta hai.

---

## 🐙 GITHUB

**Q1. What is a Pull Request (PR)?**
A. PR ek request hai apne changes ko ek branch se dusri branch (usually main) mein merge karne ke liye, review aur approval ke saath.

**Q2. Difference between Fork and Clone?**
A. Fork GitHub par repo ka apna copy banata hai (server side). Clone repo ko local machine par download karta hai.

**Q3. What is GitHub Actions?**
A. CI/CD automation tool jo GitHub repo mein hi workflows (build, test, deploy) automatically run karta hai using YAML files.

**Q4. What are GitHub Issues used for?**
A. Bugs, feature requests, tasks track karne ke liye — team collaboration aur project management ke liye.

**Q5. What is a README file?**
A. Project ka documentation file jo repo overview, setup instructions, usage explain karta hai.

**Q6. How do you protect a branch in GitHub?**
A. Branch protection rules set karke — jaise PR review mandatory karna, direct push block karna main branch par.

**Q7. What is the difference between public and private repository?**
A. Public repo sabko visible hota hai, private repo sirf authorized users ko.

**Q8. What is a GitHub webhook?**
A. Webhook ek event trigger hai jo specific action (push, PR) hone par external service ko notify karta hai (e.g., CI/CD trigger).

---

## ☁️ AWS

**Q1. What is AWS and name some core services?**
A. AWS Amazon ka cloud computing platform hai. Core services: EC2 (compute), S3 (storage), IAM (access management), VPC (networking), RDS (database), Lambda (serverless).

**Q2. What is IAM in AWS?**
A. Identity and Access Management — users, groups, roles, aur policies banane ke liye jo control karte hain kaun kya access kar sakta hai AWS resources par.

**Q3. Difference between IAM User and IAM Role?**
A. IAM User ek specific person/application identity hai with permanent credentials. IAM Role temporary permissions provide karta hai, services/users ko assume karne ke liye (no permanent credentials).

**Q4. What is EC2?**
A. Elastic Compute Cloud — virtual servers provide karta hai cloud mein, jisse applications run kar sakte hain.

**Q5. What is a Security Group?**
A. Virtual firewall jo EC2 instance ke inbound/outbound traffic control karta hai (port, protocol, IP based rules).

**Q6. Difference between Security Group and NACL?**
A. Security Group instance-level firewall hai (stateful). NACL (Network ACL) subnet-level firewall hai (stateless), explicit allow/deny rules ke saath.

**Q7. What is S3 and its storage classes?**
A. Simple Storage Service — object storage. Storage classes: Standard (frequent access), Intelligent-Tiering, Standard-IA (infrequent access), Glacier (archival/cheap, slow retrieval).

**Q8. What is VPC?**
A. Virtual Private Cloud — apna isolated private network AWS mein, jisme subnets, route tables, gateways define kar sakte ho.

**Q9. Difference between Public Subnet and Private Subnet?**
A. Public subnet ka route Internet Gateway se connected hota hai (internet access). Private subnet ka direct internet access nahi hota, NAT Gateway ke through outbound access milta hai.

**Q10. What is an Internet Gateway (IGW)?**
A. VPC ko internet se connect karne ka component — public subnet ke resources ko internet access dene ke liye.

**Q11. What is a NAT Gateway?**
A. Private subnet ke resources ko outbound internet access dene ke liye (bina unhe public IP diye), inbound traffic block rehta hai.

**Q12. What is RDS?**
A. Relational Database Service — managed database service (MySQL, PostgreSQL, etc), jisme AWS backup, patching, scaling manage karta hai.

**Q13. What is AWS Lambda?**
A. Serverless compute service — code run karta hai event trigger hone par, bina server manage kiye (pay per execution).

**Q14. What is CloudWatch?**
A. Monitoring service — logs, metrics, alarms track karne ke liye AWS resources ka.

**Q15. Difference between EBS and S3?**
A. EBS (Elastic Block Store) block storage hai, EC2 instance ke saath attach hota hai (like a hard disk). S3 object storage hai, standalone, scalable, internet accessible.

**Q16. What is Auto Scaling in AWS?**
A. EC2 instances ki number automatically increase/decrease karta hai traffic/load ke basis par, taaki performance aur cost optimize ho.

**Q17. What is Elastic Load Balancer (ELB)?**
A. Incoming traffic ko multiple EC2 instances mein distribute karta hai for high availability and fault tolerance.

**Q18. What is the difference between Availability Zone and Region?**
A. Region ek geographic area hai (e.g., Mumbai). Availability Zone region ke andar ek isolated data center location hai — fault tolerance ke liye multiple AZs use hote hain.

**Q19. What is AWS CLI?**
A. Command Line Interface — AWS resources ko terminal/command line se manage karne ka tool, console use kiye bina.

**Q20. How does AWS billing work — what is Free Tier?**
A. Pay-as-you-go model — jo use karo usi ka bill aata hai. Free Tier mein naye accounts ko limited usage (e.g., 750 hrs EC2/month) 12 months tak free milta hai.

---

## 🐳 DOCKER

**Q1. What is Docker and why is it used?**
A. Docker containerization platform hai jo application ko uske dependencies ke saath ek package (container) mein bundle karta hai, jisse "works on my machine" problem solve hoti hai.

**Q2. Difference between Image and Container?**
A. Image ek read-only template/blueprint hai. Container image ka running instance hai.

**Q3. Difference between Docker and Virtual Machine?**
A. VM full OS virtualize karta hai (heavy, slow boot). Docker container OS kernel share karta hai host ke saath (lightweight, fast boot).

**Q4. What is a Dockerfile?**
A. Text file jisme instructions hote hain image build karne ke liye (e.g., `FROM`, `RUN`, `COPY`, `CMD`).

**Q5. What is the difference between `CMD` and `ENTRYPOINT`?**
A. Dono container ka default command set karte hain. `CMD` easily override ho sakta hai `docker run` time. `ENTRYPOINT` fixed rehta hai, args append hoti hain.

**Q6. What is Docker Compose?**
A. Tool jisse multiple containers ko ek single `docker-compose.yml` file mein define karke ek command se manage (up/down) kar sakte ho.

**Q7. What is a Docker volume?**
A. Persistent data storage mechanism — container delete hone ke baad bhi data save rehta hai (database data ke liye useful).

**Q8. Difference between `docker run` and `docker start`?**
A. `docker run` naya container create + start karta hai. `docker start` already existing (stopped) container ko start karta hai.

**Q9. How do you check running containers?**
A. `docker ps` (running containers), `docker ps -a` (all containers including stopped).

**Q10. What is Docker Hub?**
A. Public registry jaha Docker images store/share ki jati hain (jaise GitHub but for images).

**Q11. How do you remove unused images/containers?**
A. `docker system prune` (sab cleanup), `docker rmi <image>` (specific image remove).

**Q12. What is a multi-stage build in Docker?**
A. Dockerfile mein multiple `FROM` stages use karke final image size chota karna — build dependencies sirf intermediate stage mein rehti hain, final image mein nahi.

**Q13. How do containers communicate with each other?**
A. Docker network ke through (bridge network default). Custom network banakar containers ek dusre ko container name se reach kar sakte hain.

**Q14. What is the difference between `COPY` and `ADD` in Dockerfile?**
A. `COPY` simple file/folder copy karta hai. `ADD` extra features support karta hai — URL se download aur tar files auto-extract.

**Q15. How do you check container logs?**
A. `docker logs <container_id>`.

---

## 🏗️ TERRAFORM

**Q1. What is Terraform and what is IaC?**
A. Terraform ek Infrastructure as Code (IaC) tool hai jisse cloud infrastructure (servers, networks, etc) ko code (HCL language) ke through define aur manage karte hain, manually console mein click karne ke instead.

**Q2. What is a Provider in Terraform?**
A. Plugin jo Terraform ko specific cloud platform (AWS, Azure, GCP) ke saath interact karne deta hai.

**Q3. Difference between `terraform plan` and `terraform apply`?**
A. `terraform plan` preview dikhata hai ki kya changes honge (bina actually karne). `terraform apply` un changes ko actually execute karta hai.

**Q4. What is a Terraform state file?**
A. `terraform.tfstate` file jo current infrastructure ka record maintain karti hai — Terraform ko pata chalta hai kya already created hai aur kya change karna hai.

**Q5. What is `terraform destroy`?**
A. Saare resources jo Terraform ne create kiye the, unhe delete/remove karne ka command.

**Q6. What is a Terraform module?**
A. Reusable group of resources (like a function) jise multiple jagah call kar sakte ho, code duplication kam karne ke liye.

**Q7. Difference between Terraform variables and outputs?**
A. Variables input values hote hain (configurable parameters). Outputs Terraform run ke baad resource ki specific information display karte hain (e.g., EC2 public IP).

**Q8. What is remote state in Terraform?**
A. State file ko local machine ke instead remote location (e.g., S3 bucket) mein store karna — team collaboration aur safety ke liye.

**Q9. What is `terraform init` used for?**
A. Working directory initialize karta hai — providers download karta hai, backend configure karta hai.

**Q10. What happens if two people run Terraform at the same time?**
A. State file conflict ho sakta hai. Isliye **state locking** use karte hain (e.g., DynamoDB lock with S3 backend) — taaki ek time par sirf ek person apply kar sake.

**Q11. Difference between Terraform and CloudFormation?**
A. CloudFormation AWS-specific IaC tool hai. Terraform multi-cloud support karta hai (AWS, Azure, GCP, etc) — ek hi tool se sab manage kar sakte ho.

**Q12. What is a `.tfvars` file?**
A. File jisme variable values define karte hain, jo `terraform apply` ke time automatically load ho jati hain (e.g., `terraform.tfvars`).

---

### 💡 Quick Tips for Interview
- Concept ke saath ek **real example/command** bolne ki practice karo — sirf definition mat bolo
- "Maine ye kiya hai" type confidence dikhane ke liye ek bar har command **practically** try karke jaana
- Follow-up questions ke liye ready raho ("why", "what if it fails", "difference from X")
