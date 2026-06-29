# DevOps & Cloud Interview Questions and Answers
### Linux | Git | GitHub | AWS (EC2, VPC, IAM, RDS, Auto Scaling, ELB, EFS, S3, DynamoDB, CloudWatch) | Docker | Terraform
**Level: Fresher to 1.5 Years Experience**

This guide blends core concept questions with the practical, scenario-based questions interviewers commonly ask candidates with around 1.5 years of hands-on experience.

---

## 1. Linux (30 Questions)

**Q1. What is Linux and why is it preferred for servers/DevOps work?**
Linux is an open-source, Unix-like OS kernel. It's preferred because it's free, stable, secure, lightweight, and highly scriptable — ideal for automation and cloud infrastructure.

**Q2. What is the Linux boot process (high level)?**
BIOS/UEFI → Bootloader (GRUB) → Kernel loads → `init`/`systemd` starts → runlevel/target services start → login prompt.

**Q3. Difference between a process and a thread?**
A process has its own independent memory space; a thread is a lightweight unit of execution within a process that shares the process's memory with other threads.

**Q4. How do you check disk usage and free space?**
`df -h` for filesystem-level free space; `du -sh /path` for the size of a specific file/folder.

**Q5. How do you check running processes and kill one?**
`ps -ef` or `top`/`htop` to view processes; `kill -9 <PID>` to forcefully terminate one.

**Q6. Difference between a soft link and a hard link?**
A soft link is a pointer to a file's path (breaks if the original is deleted). A hard link points directly to the same inode/data, so the data persists even if the original filename is removed.

**Q7. What does `chmod 755 file.sh` mean?**
Owner gets read/write/execute (7), group and others get read/execute (5) — commonly used to make a script executable for everyone but writable only by the owner.

**Q8. How do you search for text inside files recursively?**
`grep -rn "text" /path/` — `-r` recursive, `-n` shows line numbers.

**Q9. What is `cron` used for, and how do you edit it?**
`cron` schedules recurring jobs. Edit your user's schedule with `crontab -e`; format is `min hour day month weekday command`.

**Q10. How do you check listening ports on a server?**
`ss -tulnp` (modern) or `netstat -tulnp` (legacy) — shows the port, protocol, and owning process.

**Q11. Difference between `systemctl` and `service`?**
`systemctl` is the systemd-based service manager (modern distros) with richer features like enable-on-boot and dependency management; `service` is the older SysV-init style wrapper.

**Q12. How do you check system logs for troubleshooting?**
`journalctl -xe` for systemd logs, or check files under `/var/log/` (e.g., `/var/log/syslog`, `/var/log/messages`).

**Q13. What is the difference between `>` and `>>` in shell redirection?**
`>` overwrites a file with output; `>>` appends output to the end of an existing file.

**Q14. How do you find which process is using a specific port (e.g., 8080)?**
`sudo lsof -i :8080` or `ss -tulnp | grep 8080`.

**Q15. What is the difference between `apt` and `yum`/`dnf`?**
`apt` is the package manager for Debian/Ubuntu-based systems; `yum`/`dnf` are used on RHEL/CentOS/Amazon Linux-based systems.

**Q16. How do you check memory usage in Linux?**
`free -h` shows total/used/free RAM and swap in human-readable form.

**Q17. What is a zombie process?**
A process that has completed execution but still has an entry in the process table because its parent hasn't read its exit status yet.

**Q18. How do you copy files between a local machine and a remote server?**
`scp file.txt user@remote:/path/` to copy to remote, or `rsync -avz file.txt user@remote:/path/` for more efficient/incremental transfers.

**Q19. What is the difference between `kill`, `kill -9`, and `pkill`?**
`kill` sends SIGTERM (graceful shutdown request); `kill -9` sends SIGKILL (immediate force kill); `pkill` kills processes by name instead of PID.

**Q20. How do you check which Linux distribution and version you're running?**
`cat /etc/os-release` shows distro name and version details.

**Q21. What is the difference between `/etc`, `/var`, and `/usr` directories?**
`/etc` holds configuration files; `/var` holds variable data like logs and caches; `/usr` holds user-installed programs and libraries.

**Q22. How do you set an environment variable temporarily vs. permanently?**
Temporarily: `export VAR_NAME=value` (lasts for the session). Permanently: add the export line to `~/.bashrc`, `~/.bash_profile`, or `/etc/environment`.

**Q23. What is the difference between hard and soft limits in `ulimit`?**
The soft limit is the currently enforced limit a user/process can raise up to the hard limit; the hard limit is the maximum ceiling, typically set by root.

**Q24. How would you troubleshoot a server that's running out of disk space?**
Run `df -h` to confirm, then `du -sh /*` or `du -sh /var/log/*` to find large directories/files, check for old logs or core dumps, and clean up or rotate logs (`logrotate`).

**Q25. What is `logrotate` used for?**
A utility that automatically rotates, compresses, and removes old log files to prevent disks from filling up.

**Q26. How do you check CPU load average and interpret it?**
`uptime` or `top` shows load average (1, 5, 15 min). A load average close to or above the number of CPU cores indicates the system is under heavy load.

**Q27. What is the difference between a shell script's `$0`, `$1`, and `$@`?**
`$0` is the script name, `$1` is the first argument passed to it, and `$@` represents all arguments passed.

**Q28. How do you create a swap file in Linux?**
`fallocate -l 1G /swapfile`, then `chmod 600 /swapfile`, `mkswap /swapfile`, and `swapon /swapfile` to activate it.

**Q29. What's the difference between `su` and `sudo`?**
`su` switches to another user (commonly root) and requires that user's password; `sudo` runs a single command with elevated privileges using your own password, based on permissions in `/etc/sudoers`.

**Q30. You SSH into a server and it's extremely slow/unresponsive — what's your troubleshooting approach?**
Check `top`/`htop` for CPU/memory hogs, `df -h` for disk space, `uptime` for load average, `dmesg` for hardware/kernel errors, and network latency — narrowing down whether it's a CPU, memory, disk, or network bottleneck.

---

## 2. Git (32 Questions)

**Q1. What is Git and why is it used?**
Git is a distributed version control system that tracks changes to source code, allowing multiple developers to collaborate, branch, and merge work without overwriting each other's changes.

**Q2. Difference between `git pull` and `git fetch`?**
`git fetch` downloads remote changes without merging them; `git pull` fetches and automatically merges them into your current branch.

**Q3. Difference between `git merge` and `git rebase`?**
`merge` combines branch histories with a new merge commit (preserves full history); `rebase` replays your commits on top of another branch, producing a cleaner, linear history.

**Q4. How do you resolve a merge conflict?**
Open the conflicting file(s), manually edit the sections marked with `<<<<<<<`, `=======`, `>>>>>>>` to keep the correct code, then `git add <file>` and `git commit` (or `git rebase --continue` if rebasing).

**Q5. What does `git stash` do, and how do you retrieve stashed changes?**
It temporarily shelves uncommitted changes so you can switch branches cleanly; retrieve them with `git stash pop` (applies and removes from stash) or `git stash apply` (applies but keeps in stash).

**Q6. Difference between `git reset` and `git revert`?**
`git reset` moves the branch pointer and can discard commits/history (risky on shared branches); `git revert` creates a new commit that undoes a previous commit's changes without rewriting history (safe for shared branches).

**Q7. What is `.gitignore` used for?**
It lists file/folder patterns Git should not track, like build artifacts, `node_modules/`, `.env` files, or logs.

**Q8. How do you create and switch to a new branch in one command?**
`git checkout -b branch-name` or `git switch -c branch-name`.

**Q9. What is the difference between `git reset --soft`, `--mixed`, and `--hard`?**
`--soft` keeps changes staged; `--mixed` (default) unstages changes but keeps them in the working directory; `--hard` discards changes completely, resetting the working directory too.

**Q10. How do you undo the last commit but keep the changes?**
`git reset --soft HEAD~1` keeps your changes staged but removes the commit.

**Q11. What's the difference between `git log` and `git reflog`?**
`git log` shows commit history reachable from the current branch; `git reflog` shows a record of where HEAD has pointed, including commits that may no longer be reachable (useful for recovering "lost" commits).

**Q12. How do you squash multiple commits into one?**
Use interactive rebase: `git rebase -i HEAD~N`, then mark commits as `squash` (or `s`) except the first one, and save.

**Q13. What is a detached HEAD state?**
When you check out a specific commit (not a branch), HEAD points directly to that commit instead of a branch reference — any new commits there can be lost unless you create a branch from them.

**Q14. Difference between `git diff` and `git status`?**
`git status` shows which files are modified/staged/untracked; `git diff` shows the actual line-by-line changes in those files.

**Q15. How do you rename a local and remote branch?**
Local: `git branch -m old-name new-name`. Then push the new branch and delete the old one remotely: `git push origin new-name` and `git push origin --delete old-name`.

**Q16. What is `cherry-pick` used for?**
`git cherry-pick <commit-hash>` applies a specific commit from one branch onto another, without merging the entire branch.

**Q17. How do you see the changes in a specific commit?**
`git show <commit-hash>`.

**Q18. What is the difference between a local and remote branch?**
A local branch exists only on your machine; a remote branch (e.g., `origin/main`) is a reference to the state of a branch on the remote repository.

**Q19. How do you delete a branch locally and remotely?**
Locally: `git branch -d branch-name` (or `-D` to force). Remotely: `git push origin --delete branch-name`.

**Q20. What does `git fetch --prune` do?**
It removes local references to remote branches that no longer exist on the remote.

**Q21. What is the difference between `git clone` and `git init`?**
`git clone` copies an existing remote repository to your local machine; `git init` creates a brand-new, empty Git repository locally.

**Q22. How do you check which commit introduced a bug?**
`git bisect` — it performs a binary search through commit history, letting you mark commits as good/bad until it isolates the offending commit.

**Q23. What's the purpose of a commit hash (SHA)?**
It's a unique identifier (checksum) generated from the commit's content and metadata, ensuring integrity and allowing precise referencing of any commit.

**Q24. How do you amend the last commit message?**
`git commit --amend -m "new message"`.

**Q25. What happens if you `git push` after rewriting history (e.g., after a rebase)?**
A normal push will be rejected since history diverged; you typically need `git push --force` (or `--force-with-lease`, which is safer as it checks no one else has pushed in the meantime).

**Q26. What is the difference between `git pull --rebase` and a normal `git pull`?**
A normal `git pull` merges remote changes (creating a merge commit if needed); `git pull --rebase` replays your local commits on top of the fetched changes, avoiding an extra merge commit.

**Q27. How would you recover a deleted branch?**
Use `git reflog` to find the last commit hash of the deleted branch, then `git checkout -b branch-name <commit-hash>` to recreate it.

**Q28. What is a Git tag, and what's it used for?**
A tag marks a specific commit, typically used for release versions (e.g., `v1.0.0`). Created via `git tag v1.0.0` and pushed with `git push origin v1.0.0`.

**Q29. Difference between annotated and lightweight tags?**
Annotated tags (`git tag -a`) store extra metadata (tagger, date, message) and are recommended for releases; lightweight tags (`git tag`) are just a pointer to a commit.

**Q30. What is the staging area (index) in Git?**
An intermediate area where changes are placed via `git add` before being committed — it lets you control exactly what goes into the next commit.

**Q31. How do you check the difference between your local branch and the remote branch?**
`git fetch` followed by `git diff branch origin/branch` or `git log branch..origin/branch` to see what commits are missing locally.

**Q32. Scenario: You accidentally committed sensitive data (like a password) to a repo that's already pushed — what do you do?**
Remove it from history (e.g., using `git filter-branch` or the `BFG Repo-Cleaner`), force-push the cleaned history, and — most importantly — rotate/invalidate the exposed credential immediately, since it may already be cached or visible to others.

---

## 3. GitHub (30 Questions)

**Q1. What is a Pull Request (PR)?**
A request to merge changes from one branch into another, enabling code review, discussion, and automated checks before merging.

**Q2. Difference between forking and cloning?**
Cloning copies a repo locally while keeping a link to the original remote. Forking creates an independent copy under your own GitHub account, commonly used to contribute to projects you don't have write access to.

**Q3. What are GitHub Actions?**
A built-in CI/CD automation tool that runs workflows (defined in YAML under `.github/workflows/`) triggered by events like pushes, PRs, or schedules.

**Q4. What is branch protection, and why use it?**
A rule set on a branch (e.g., `main`) requiring things like PR approvals or passing status checks before merging — protects critical branches from accidental or unreviewed changes.

**Q5. Difference between a public and private repository?**
Public repos are visible to anyone; private repos are restricted to the owner and explicitly invited collaborators.

**Q6. How do you give someone access to a repository?**
Repo → Settings → Collaborators and teams → Add people, then assign a role (read, write, admin, etc.).

**Q7. What is a GitHub Issue used for?**
Tracking bugs, feature requests, or tasks — can be linked to PRs, assigned to people, and labeled/organized into milestones or project boards.

**Q8. What's the difference between a draft PR and a regular PR?**
A draft PR signals the work is still in progress and isn't ready for final review/merge, though it can still receive early feedback.

**Q9. What is a GitHub Webhook?**
A configured HTTP callback that notifies an external service when certain events happen in a repo (e.g., a push), commonly used to trigger external CI/CD or notification systems.

**Q10. What is the difference between GitHub Actions and Jenkins?**
GitHub Actions is tightly integrated with GitHub repos and triggered natively by GitHub events; Jenkins is a standalone, self-hosted CI/CD server that's more flexible/plugin-driven but requires separate setup and maintenance.

**Q11. What is a `CODEOWNERS` file used for?**
It defines individuals or teams responsible for reviewing changes to specific files/paths, automatically requesting their review on relevant PRs.

**Q12. How do you resolve a merge conflict directly in the GitHub UI?**
On the PR page, GitHub shows a "resolve conflicts" option if conflicts are simple, allowing you to edit and mark them resolved directly in the browser.

**Q13. What is a GitHub Release?**
A way to package and publish a specific version of your software, usually tied to a Git tag, often including release notes and binary artifacts.

**Q14. Difference between "Merge", "Squash and merge", and "Rebase and merge" options in a PR?**
"Merge" creates a merge commit preserving all individual commits; "Squash and merge" combines all PR commits into a single commit; "Rebase and merge" replays the PR's commits onto the base branch without a merge commit.

**Q15. What are GitHub Secrets?**
Encrypted environment variables (e.g., API keys, credentials) stored at the repo/org level and used securely within GitHub Actions workflows without exposing them in code.

**Q16. What is a GitHub Project (Project Board)?**
A Kanban-style board for organizing and tracking issues/PRs across columns like "To Do", "In Progress", "Done."

**Q17. How do you trigger a GitHub Actions workflow only on a specific branch?**
Use the `on.push.branches` (or `pull_request.branches`) key in the workflow YAML to restrict triggers to specific branch names.

**Q18. What is the difference between an Organization and a Personal account on GitHub?**
A personal account belongs to an individual; an Organization account is a shared space for teams/companies with role-based access control across multiple repos.

**Q19. How do you protect the `main` branch from direct pushes?**
Enable branch protection rules requiring PRs (no direct pushes), required reviews, and passing status checks before merge.

**Q20. What is a GitHub Action "runner"?**
A server (GitHub-hosted or self-hosted) that executes the jobs defined in a workflow.

**Q21. How do you reference an issue in a commit message to auto-close it?**
Include keywords like `Fixes #12` or `Closes #12` in the commit message or PR description — GitHub automatically closes that issue when merged.

**Q22. What is the difference between GitHub Packages and GitHub Container Registry?**
GitHub Packages hosts various package types (npm, Maven, NuGet, etc.); GitHub Container Registry (ghcr.io) is specifically for hosting Docker container images.

**Q23. What is a "status check" in GitHub?**
A pass/fail indicator (often from CI pipelines like GitHub Actions) shown on a PR, which can be configured as required before merging is allowed.

**Q24. How do you compare two branches in GitHub?**
Use the "Compare" feature (`github.com/user/repo/compare/branch1...branch2`) to see the diff and commits between them.

**Q25. What is a self-hosted runner in GitHub Actions, and why use one?**
A runner you set up on your own infrastructure instead of using GitHub's hosted runners — useful for custom hardware needs, internal network access, or cost control at scale.

**Q26. How do you restrict a GitHub Action from running on forks (for security)?**
Use conditions (`if`) checking the event context, and avoid exposing repo secrets to workflows triggered from forked PRs (GitHub already restricts secrets on fork-originated PRs by default).

**Q27. What is the difference between `workflow_dispatch` and `push` triggers?**
`push` triggers a workflow automatically on a code push; `workflow_dispatch` allows manually triggering a workflow from the GitHub UI/API, often with custom input parameters.

**Q28. Scenario: A teammate's PR shows failing CI checks but works fine locally — how do you debug it?**
Check the Actions logs for the exact failing step, compare environment differences (versions, env vars, secrets), confirm the workflow uses the same dependencies/lockfile, and reproduce locally using the same OS/runner image if possible.

**Q29. What is GitHub Codespaces?**
A cloud-based development environment that spins up a fully configured container (via a devcontainer config) accessible from the browser or VS Code, without local setup.

**Q30. Scenario: How would you set up a basic CI pipeline for a Node.js app using GitHub Actions?**
Create a workflow YAML triggered on push/PR that checks out code, sets up Node.js, runs `npm install`, then `npm test` (and optionally `npm run build`), failing the workflow if any step errors out.

---

## 4. AWS — EC2 (32 Questions)

**Q1. What is EC2?**
AWS's service for provisioning resizable virtual servers (instances) in the cloud, where you choose the OS, compute, memory, and storage.

**Q2. What is an AMI?**
Amazon Machine Image — a template containing the OS and pre-configured software used to launch EC2 instances.

**Q3. Difference between Security Groups and NACLs?**
Security Groups are stateful, instance-level firewalls (return traffic auto-allowed); NACLs are stateless, subnet-level firewalls requiring explicit inbound and outbound rules.

**Q4. On-Demand vs Reserved vs Spot Instances?**
On-Demand: pay-as-you-go, no commitment. Reserved: 1-3 year commitment for a discount. Spot: bid for unused capacity at steep discounts, but can be reclaimed by AWS with short notice.

**Q5. What is an Elastic IP?**
A static public IPv4 address you allocate and attach to an instance, which stays the same even after stop/start (unlike the default public IP that changes).

**Q6. Difference between EBS and instance store?**
EBS is persistent, network-attached block storage that survives stop/terminate; instance store is temporary, directly attached storage that's lost when the instance stops or terminates.

**Q7. How do you connect to a Linux EC2 instance?**
`ssh -i mykey.pem ec2-user@<public-ip>` using the key pair generated/selected at launch.

**Q8. What is a key pair used for in EC2?**
A public/private key pair for secure SSH access — AWS stores the public key on the instance; you keep the private key for authentication.

**Q9. What's the difference between stopping and terminating an EC2 instance?**
Stopping shuts the instance down but keeps its EBS volumes/data (and you stop paying for compute, though storage cost remains). Terminating permanently deletes the instance and, by default, its root EBS volume.

**Q10. What is an EC2 instance type, and how do you choose one?**
A combination of CPU, memory, storage, and networking capacity (e.g., `t3.micro`, `m5.large`). Choice depends on workload: general purpose (T/M series), compute-optimized (C series), memory-optimized (R series), etc.

**Q11. What is User Data in EC2?**
A script (e.g., bash) you can pass at launch time that runs automatically on first boot — commonly used to install software or configure the instance.

**Q12. Difference between a public and private EC2 instance (in terms of networking)?**
A public instance is in a subnet with a route to an Internet Gateway and typically has a public IP; a private instance has no direct internet route and is only reachable internally (or via a NAT Gateway for outbound traffic).

**Q13. What is an EC2 placement group?**
A logical grouping of instances to influence their placement on underlying hardware — Cluster (low latency, same AZ), Spread (across distinct hardware, fault tolerance), or Partition (large distributed workloads).

**Q14. How do you resize an EC2 instance (change instance type)?**
Stop the instance, change the instance type from the console/CLI, then start it again (note: this isn't possible for instance-store-backed instances).

**Q15. What is the EC2 instance metadata service used for?**
An internal endpoint (`http://169.254.169.254/latest/meta-data/`) that lets an instance retrieve its own metadata (like instance ID, IAM role credentials, region) without needing external network calls.

**Q16. What is IMDSv2 and why is it more secure than IMDSv1?**
IMDSv2 requires a session token (via a PUT request) before retrieving metadata, protecting against SSRF attacks that could otherwise exploit IMDSv1's simpler GET-based access.

**Q17. How do you attach an IAM role to a running EC2 instance?**
Select the instance in the console → Actions → Security → Modify IAM role, and attach the desired role (no restart required).

**Q18. What is the difference between gp2/gp3, io1/io2, and st1/sc1 EBS volume types?**
gp2/gp3 are general-purpose SSDs for most workloads; io1/io2 are high-performance, high-IOPS SSDs for critical databases; st1/sc1 are HDD-based, optimized for throughput (big data) or infrequent cold storage respectively.

**Q19. How do you take a backup of an EC2 instance?**
Create an EBS snapshot of its volumes, or create a full AMI from the instance, which captures the OS, configuration, and attached storage.

**Q20. What is an EC2 Auto Recovery alarm?**
A CloudWatch alarm that automatically recovers an instance (on the same host or a new one) if it becomes impaired due to underlying hardware issues.

**Q21. What is the difference between EC2 and Lambda?**
EC2 provides full virtual servers you manage (OS, scaling, patching); Lambda is serverless — you just deploy code, and AWS manages all underlying infrastructure and scaling automatically.

**Q22. How do you troubleshoot an EC2 instance you can't SSH into?**
Check Security Group/NACL rules for port 22, confirm the instance status checks are passing, verify you're using the correct key and username, check the subnet's route table, and review system logs via "Get System Log" in the console if it won't boot.

**Q23. What are EC2 instance status checks?**
AWS-provided checks — System Status Check (underlying hardware/network) and Instance Status Check (the instance's own OS/software) — used to detect and alert on instance health issues.

**Q24. What is the difference between Spot Instance interruption notice types?**
AWS gives a two-minute warning before reclaiming a Spot Instance, via either an interruption notice in the instance metadata or an EventBridge event, allowing graceful shutdown handling.

**Q25. How would you reduce EC2 costs in a non-production environment?**
Use Spot or smaller instance types, schedule start/stop for non-business hours, right-size based on actual usage (via CloudWatch metrics), and use Savings Plans/Reserved Instances for predictable workloads.

**Q26. What is the difference between an EBS-backed and Instance Store-backed AMI?**
EBS-backed AMIs use persistent EBS volumes as root storage (can stop/start, preserves data); instance store-backed AMIs use ephemeral storage (can't be stopped, only run/terminate, and data is lost on shutdown).

**Q27. What happens to data on an attached EBS volume if you terminate the instance?**
By default, the root EBS volume is deleted on termination (configurable via "Delete on Termination"), but additional (non-root) EBS volumes are preserved unless explicitly set to delete too.

**Q28. How do you migrate an EC2 instance from one AZ to another?**
You can't move an instance directly between AZs — create an AMI from it, then launch a new instance from that AMI in the target AZ.

**Q29. What's the difference between Dedicated Instances and Dedicated Hosts?**
Dedicated Instances run on hardware dedicated to your account but AWS manages host allocation; Dedicated Hosts give you visibility/control over the specific physical server, useful for licensing requirements tied to sockets/cores.

**Q30. Scenario: An EC2 web app is running slow under load — what would you check first?**
CloudWatch metrics for CPU/memory/network utilization, check if it's hitting instance limits (consider scaling up/out), review application/database bottlenecks, and check if Auto Scaling or Load Balancer health checks are configured correctly.

**Q31. How do you securely store and use a database password that an EC2 app needs?**
Avoid hardcoding it — use AWS Secrets Manager or Systems Manager Parameter Store (with encryption), and grant the EC2 instance's IAM role permission to retrieve it at runtime.

**Q32. What is EC2 Hibernate, and how is it different from Stop?**
Hibernate saves the instance's RAM contents to the root EBS volume before stopping, so when restarted, the OS resumes from where it left off (faster boot, preserved in-memory state) — unlike a normal Stop, which discards RAM contents.

---

## 5. AWS — VPC (30 Questions)

**Q1. What is a VPC?**
A logically isolated private network within AWS where you launch resources, with full control over IP ranges, subnets, routing, and gateways.

**Q2. Public vs. private subnet?**
A public subnet has a route to an Internet Gateway (direct internet access); a private subnet has no such route (internet access, if any, goes through a NAT Gateway).

**Q3. What is an Internet Gateway (IGW)?**
A VPC component allowing resources in public subnets to send/receive traffic to/from the internet.

**Q4. What is a NAT Gateway, and why is it needed?**
It allows instances in private subnets to initiate outbound internet traffic (e.g., software updates) while remaining unreachable from the internet directly.

**Q5. What is a Route Table?**
A set of rules determining where network traffic from a subnet is directed (e.g., to the IGW, NAT Gateway, or another subnet).

**Q6. What is VPC Peering?**
A direct network connection between two VPCs allowing them to communicate using private IPs, without traversing the public internet (non-transitive — peering doesn't automatically extend through a third VPC).

**Q7. What is a CIDR block?**
A range of IP addresses (e.g., `10.0.0.0/16`) defining the size/scope of a VPC or subnet.

**Q8. Difference between Security Groups and Subnets?**
A subnet is a network segmentation tied to an AZ; a Security Group is a firewall controlling traffic to/from specific resources, regardless of subnet.

**Q9. What is a VPC Endpoint, and why use one?**
A way to privately connect your VPC to supported AWS services (like S3 or DynamoDB) without going through the public internet/NAT Gateway — improves security and can reduce data transfer costs.

**Q10. Difference between a Gateway Endpoint and an Interface Endpoint?**
Gateway Endpoints (for S3/DynamoDB) work via route table entries; Interface Endpoints (for most other services) create an ENI with a private IP in your subnet, powered by AWS PrivateLink.

**Q11. What is the default VPC, and how is it different from a custom VPC?**
The default VPC is automatically created by AWS in each region with default subnets (public, internet-accessible) for quick starts; a custom VPC is one you design yourself with specific CIDR ranges, subnets, and routing.

**Q12. What is a Bastion Host?**
A hardened EC2 instance placed in a public subnet used as a secure gateway/jump server to SSH into instances in private subnets.

**Q13. How many subnets/AZs should a highly available architecture span at minimum?**
At least two Availability Zones, so if one AZ fails, resources in the other AZ continue serving traffic.

**Q14. What is a Network ACL's default behavior on a new VPC vs. a custom subnet?**
The default NACL allows all inbound/outbound traffic; a custom NACL, by default, denies all traffic until rules are explicitly added.

**Q15. What is the difference between a Security Group's "stateful" nature and a NACL's "stateless" nature?**
A Security Group automatically allows outbound response traffic for an allowed inbound request (and vice versa); a NACL requires you to explicitly permit both directions of traffic separately.

**Q16. What is Transit Gateway?**
A hub-and-spoke networking service that lets you connect multiple VPCs (and on-premises networks) through a single gateway, simplifying complex multi-VPC architectures versus full-mesh peering.

**Q17. How do you allow internet access for a private subnet's instances?**
Route their subnet's outbound traffic (0.0.0.0/0) to a NAT Gateway placed in a public subnet.

**Q18. What is the difference between VPC Flow Logs and CloudTrail?**
VPC Flow Logs capture IP traffic metadata (source/destination, ports, accept/reject) going through network interfaces; CloudTrail logs API-level account activity, unrelated to packet-level network traffic.

**Q19. Can two peered VPCs have overlapping CIDR blocks?**
No — VPC peering requires non-overlapping CIDR ranges between the two VPCs, since AWS can't route correctly with duplicate IP ranges.

**Q20. What is a Site-to-Site VPN in AWS?**
An encrypted IPsec connection between your on-premises network and your AWS VPC over the public internet, via a Virtual Private Gateway and Customer Gateway.

**Q21. Difference between Site-to-Site VPN and Direct Connect?**
VPN runs over the public internet (cheaper, variable latency); Direct Connect is a dedicated private physical network link to AWS (more consistent performance/lower latency, but costs more and takes longer to provision).

**Q22. What is a subnet's relationship to an Availability Zone?**
Each subnet exists entirely within a single AZ — it cannot span multiple AZs.

**Q23. How do you restrict an S3 bucket to only be accessible from within your VPC?**
Use a VPC Endpoint Policy combined with an S3 bucket policy that conditionally checks `aws:sourceVpce` or `aws:sourceVpc`, denying access from outside that endpoint/VPC.

**Q24. Scenario: An EC2 instance in a private subnet can't reach the internet for `yum update` — what would you check?**
Confirm there's a NAT Gateway in a public subnet, the private subnet's route table points 0.0.0.0/0 to that NAT Gateway, the NAT Gateway has an Elastic IP, and security groups/NACLs aren't blocking outbound traffic.

**Q25. What is the maximum number of VPC peering connections from a single VPC?**
There's a soft limit per VPC (default often 50, adjustable via AWS support) — for large-scale interconnection, Transit Gateway is usually recommended instead of many-to-many peering.

**Q26. What is an Elastic Network Interface (ENI)?**
A virtual network card you can attach to an EC2 instance, with its own private IP, security groups, and MAC address — useful for failover or multi-homed network setups.

**Q27. How does DNS resolution work within a VPC by default?**
AWS provides a default DNS resolver (at the VPC's base + .2 address) if `enableDnsSupport` and `enableDnsHostnames` are turned on, resolving instance hostnames and AWS service endpoints.

**Q28. What's the difference between a VPC's primary and secondary CIDR block?**
The primary CIDR is set at VPC creation and can't be changed; secondary CIDR blocks can be added later to expand the available IP address range without recreating the VPC.

**Q29. How would you design a 3-tier VPC architecture (web, app, database)?**
Public subnets (across 2+ AZs) for the load balancer/web tier with IGW access; private subnets for the app tier (via NAT Gateway for outbound); and further-isolated private subnets for the database tier with no internet route at all, only reachable from the app tier's security group.

**Q30. Scenario: You need two VPCs in different AWS accounts to communicate privately — what are your options?**
Cross-account VPC Peering, a Transit Gateway shared via AWS Resource Access Manager (RAM), or PrivateLink (if you only need to expose a specific service rather than full network connectivity).

---

## 6. AWS — IAM (30 Questions)

**Q1. What is IAM?**
AWS's service for securely managing identities (users, groups, roles) and controlling their permissions to access AWS resources.

**Q2. IAM User vs. IAM Role?**
A User has permanent credentials tied to a person/application; a Role provides temporary credentials assumed by users, applications, or AWS services as needed.

**Q3. What is an IAM Policy?**
A JSON document defining permissions — specifying allowed/denied actions on specific resources, optionally with conditions.

**Q4. What is the Principle of Least Privilege?**
Granting only the minimum permissions necessary for a task — nothing more — to reduce security risk.

**Q5. What is MFA, and why use it?**
Multi-Factor Authentication adds a second verification step (like a one-time code) beyond a password, significantly reducing the risk of compromised credentials.

**Q6. IAM Group vs. IAM Role?**
A Group bundles Users together to apply shared permissions; a Role isn't tied to a specific identity — it's assumed temporarily by whoever/whatever needs those permissions.

**Q7. What is the difference between an Identity-based policy and a Resource-based policy?**
Identity-based policies are attached to users/groups/roles; resource-based policies (like an S3 bucket policy) are attached directly to a resource and can grant access to other accounts/principals.

**Q8. What is an IAM Policy's "Effect", "Action", and "Resource" structure?**
"Effect" is Allow or Deny; "Action" specifies the API operations (e.g., `s3:GetObject`); "Resource" specifies which AWS resource(s) the policy applies to (often via ARN).

**Q9. What happens if there's both an explicit Allow and an explicit Deny for the same action?**
Deny always wins — an explicit Deny overrides any Allow, regardless of where it's defined.

**Q10. What is an IAM Role's "Trust Policy"?**
A policy attached to the role itself defining who (which principal — user, service, or account) is allowed to assume that role.

**Q11. How does an EC2 instance access AWS services securely without hardcoded credentials?**
By attaching an IAM Role (Instance Profile) to the instance, which provides temporary credentials automatically via the instance metadata service.

**Q12. What is the difference between AWS Managed Policies and Customer Managed Policies?**
AWS Managed Policies are pre-built and maintained by AWS (covering common use cases); Customer Managed Policies are created and maintained by you for custom permission requirements.

**Q13. What is an Inline Policy?**
A policy embedded directly within a single user, group, or role (rather than a standalone, reusable managed policy) — tightly coupled to that one identity.

**Q14. What is IAM Access Analyzer?**
A tool that identifies resources in your account shared with external entities, helping you spot unintended public or cross-account access.

**Q15. What is the root user, and why should it rarely be used?**
The original account owner with unrestricted access to everything, including billing — it's recommended to lock it down (enable MFA, avoid daily use) and create individual IAM users/roles for actual work.

**Q16. What is cross-account access in IAM?**
Using IAM Roles to allow users/services in one AWS account to assume a role and access resources in another account, without sharing long-term credentials.

**Q17. What is the difference between `AssumeRole` and using an IAM User's access keys?**
`AssumeRole` grants short-lived, temporary credentials (typically 15 min–12 hrs) that auto-expire; IAM User access keys are long-lived and must be manually rotated, posing more risk if leaked.

**Q18. What is an IAM Policy condition? Give an example.**
A condition restricts when a policy applies, e.g., `"Condition": {"IpAddress": {"aws:SourceIp": "203.0.113.0/24"}}` only allows the action from a specific IP range.

**Q19. How do you audit who has access to what in your AWS account?**
Use IAM's "Access Advisor" tab (shows last-used services per identity), Access Analyzer, and review CloudTrail logs for actual API call history.

**Q20. What is the difference between `iam:PassRole` and assuming a role directly?**
`iam:PassRole` permission is needed when you assign a role to a service (e.g., letting EC2 or Lambda use that role) rather than assuming it yourself — it controls who can "hand off" a role to a service.

**Q21. What is a Service-Linked Role?**
A predefined role created and managed by an AWS service itself (e.g., for Auto Scaling or RDS) to perform actions on your behalf, with permissions scoped by AWS to that service's needs.

**Q22. Scenario: A developer says they're getting "Access Denied" trying to upload to S3, despite having an Allow policy for `s3:PutObject` — what could be the cause?**
Check for a conflicting explicit Deny (in another policy, an SCP, or a bucket policy), check if the bucket policy itself restricts access, verify the resource ARN in the policy matches exactly, and confirm there's no condition (like source IP or VPC) blocking it.

**Q23. What is the difference between an IAM Policy and a Permissions Boundary?**
A regular policy grants permissions; a Permissions Boundary sets the maximum permissions an identity can ever have, even if other policies grant more — used to safely delegate role/policy creation to others.

**Q24. What is an IAM Access Key, and what are best practices around it?**
A long-term credential pair (access key ID + secret) for programmatic access; best practice is to avoid them where possible (use roles instead), rotate regularly if used, and never hardcode them in code/repos.

**Q25. What is AWS Organizations' Service Control Policy (SCP) and how does it relate to IAM?**
An SCP is applied at the AWS Organizations level across accounts/OUs, setting guardrails on the maximum permissions allowed — even an account's Administrator can't exceed what the SCP permits, unlike regular IAM policies which only grant permissions.

**Q26. How would you grant a third-party vendor temporary, limited access to your AWS account?**
Create an IAM Role with a trust policy allowing the vendor's AWS account to assume it, scoped with only the permissions/resources they need, optionally with an external ID and time-bound session duration.

**Q27. What is the IAM policy evaluation logic order (high level)?**
By default, deny — then explicit Deny anywhere overrides everything; otherwise, if there's at least one applicable explicit Allow (and no Deny), the action is permitted.

**Q28. What is the difference between authentication and authorization in the context of IAM?**
Authentication verifies who you are (e.g., login credentials, MFA); authorization determines what you're allowed to do once authenticated (governed by IAM policies).

**Q29. How can you enforce MFA before allowing destructive actions (like deleting resources)?**
Add a policy condition like `"Condition": {"BoolIfExists": {"aws:MultiFactorAuthPresent": "true"}}` on sensitive actions, denying them unless MFA was used in that session.

**Q30. Scenario: You need a Lambda function to read from an S3 bucket and write to DynamoDB — how do you set up permissions?**
Create an IAM Role with a trust policy allowing the Lambda service to assume it, attach a policy granting `s3:GetObject` on the specific bucket/prefix and `dynamodb:PutItem` (etc.) on the specific table, then assign that role as the Lambda function's execution role.

---

## 7. AWS — RDS (30 Questions)

**Q1. What is RDS?**
A managed relational database service (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server) where AWS handles patching, backups, and underlying infrastructure.

**Q2. Multi-AZ vs. Read Replicas?**
Multi-AZ creates a synchronous standby in another AZ purely for high availability/failover; Read Replicas are asynchronous copies used to scale out read traffic, and can be promoted to standalone instances.

**Q3. How does RDS handle backups?**
Automated daily backups with point-in-time recovery within a retention window (1–35 days), plus manual snapshots you can take any time.

**Q4. What happens during a Multi-AZ failover?**
AWS detects the primary's failure and automatically switches to the standby, updating the DNS endpoint so the application reconnects with minimal downtime (typically under a couple of minutes).

**Q5. Can you SSH into an RDS instance?**
No — RDS is fully managed, so there's no OS-level shell access; you only connect via the database engine's standard port/protocol.

**Q6. RDS vs. DynamoDB?**
RDS is a managed relational (SQL) database; DynamoDB is a managed NoSQL database built for massive scale and low-latency key-based access.

**Q7. What is an RDS Parameter Group?**
A set of database engine configuration values (like `max_connections`) applied to your RDS instance — can be default or custom.

**Q8. What is an RDS Option Group?**
A way to enable additional engine-specific features (like Oracle's APEX or SQL Server's Transparent Data Encryption) for an RDS instance.

**Q9. How do you scale an RDS instance vertically vs. horizontally?**
Vertically: change the instance class to a larger one (requires a brief restart). Horizontally (for reads): add Read Replicas to distribute read traffic.

**Q10. What is RDS Storage Auto Scaling?**
A feature that automatically increases allocated storage when RDS detects you're running low, without manual intervention or downtime.

**Q11. Difference between RDS snapshots and automated backups?**
Automated backups are taken daily (with transaction logs for point-in-time recovery) and deleted when the instance is deleted (unless retained); manual snapshots are user-initiated and persist independently until you delete them.

**Q12. What is Amazon Aurora, and how does it relate to RDS?**
Aurora is AWS's own MySQL/PostgreSQL-compatible database engine offered through RDS, designed for higher performance, scalability, and availability than standard RDS engines.

**Q13. How do you connect an EC2 application to RDS securely?**
Place RDS in a private subnet, use a Security Group that only allows inbound traffic on the DB port from the application's Security Group (not from open IP ranges), and avoid hardcoding credentials (use Secrets Manager).

**Q14. What is the maintenance window in RDS?**
A configurable weekly time window during which AWS applies pending patches/updates to your RDS instance, potentially with brief downtime (unless Multi-AZ).

**Q15. Can you change the database engine of an existing RDS instance (e.g., MySQL to PostgreSQL)?**
Not directly in-place — you'd need to migrate the data using a tool like AWS Database Migration Service (DMS) to a new instance running the target engine.

**Q16. What is RDS Performance Insights?**
A monitoring feature that visualizes database load and helps identify performance bottlenecks (like top SQL queries or wait events) without manual instrumentation.

**Q17. How do you encrypt an RDS instance's data at rest?**
Enable encryption (using a KMS key) at creation time — note that encryption can't be enabled after the fact on an existing unencrypted instance; you'd need to snapshot, copy with encryption enabled, then restore.

**Q18. What is the difference between RDS Proxy and connecting directly to RDS?**
RDS Proxy pools and manages database connections, reducing connection overhead and improving failover handling for applications (especially serverless/Lambda) that open many short-lived connections.

**Q19. Scenario: Your RDS instance is experiencing high CPU usage — how would you troubleshoot?**
Check CloudWatch metrics (CPUUtilization, connections), use Performance Insights to identify expensive queries, check for missing indexes, review recent schema/query changes, and consider scaling up or adding read replicas if it's read-heavy.

**Q20. What is the difference between a DB Subnet Group and a regular subnet?**
A DB Subnet Group is a collection of subnets (across multiple AZs) that RDS uses to determine where it can place the instance and its Multi-AZ standby/replicas.

**Q21. How does RDS handle minor vs. major version upgrades?**
Minor version upgrades can often be applied automatically (if enabled) with minimal risk; major version upgrades typically require manual initiation and more thorough compatibility testing, as they may include breaking changes.

**Q22. What is the difference between "Reboot with failover" and a regular reboot in a Multi-AZ RDS setup?**
A regular reboot restarts the same instance; "Reboot with failover" forces a failover to the standby in another AZ, useful for testing failover behavior or applying certain changes that require switching instances.

**Q23. How would you migrate an on-premises database to RDS with minimal downtime?**
Use AWS Database Migration Service (DMS) with continuous replication (CDC) to keep the target in sync until cutover, minimizing the downtime window during the final switch.

**Q24. What is RDS event notification?**
A feature (via SNS) that notifies you of specific RDS events (like failovers, backups, or low storage), useful for proactive monitoring/alerting.

**Q25. What is the difference between "Deletion Protection" and a final snapshot when deleting an RDS instance?**
Deletion Protection prevents accidental deletion entirely (must be disabled first); the "final snapshot" option, when deletion is allowed, takes one last backup before removing the instance.

**Q26. How can applications fail over gracefully when using Read Replicas vs. Multi-AZ?**
With Multi-AZ, the endpoint stays the same after failover (DNS updates automatically). With Read Replicas, since they have separate endpoints, your application needs logic (or a layer like RDS Proxy) to redirect traffic if a replica is promoted to primary.

**Q27. What is cross-region Read Replica used for?**
Replicating data to a different AWS region — useful for disaster recovery, reducing read latency for geographically distributed users, or data locality/compliance needs.

**Q28. How do you monitor RDS storage to avoid running out of space?**
Set CloudWatch alarms on the `FreeStorageSpace` metric, and either enable Storage Auto Scaling or manually increase allocated storage proactively.

**Q29. What is the difference between RDS and self-managing a database on EC2?**
RDS handles patching, backups, failover, and scaling for you (less control, less ops overhead); running a DB on EC2 gives full control (custom configs, plugins) but requires you to manage all of that yourself.

**Q30. Scenario: An application intermittently loses connection to RDS during a Multi-AZ failover — how do you make the app more resilient?**
Implement connection retry logic with exponential backoff, use a connection pool/RDS Proxy that handles reconnects gracefully, and ensure the app re-resolves DNS rather than caching the old IP indefinitely.

---

## 8. AWS — Auto Scaling (30 Questions)

**Q1. What is Auto Scaling?**
A service that automatically adjusts the number of EC2 instances in a group based on demand, scaling out under load and scaling in when demand drops.

**Q2. What is an Auto Scaling Group (ASG)?**
A logical collection of EC2 instances managed together with defined minimum, maximum, and desired capacity.

**Q3. What are the types of scaling policies?**
Target tracking (maintain a metric at a target value), step scaling (scale in defined steps based on alarm thresholds), scheduled scaling (predictable time-based scaling), and predictive scaling (ML-based demand forecasting).

**Q4. What is a Launch Template, and how is it different from a Launch Configuration?**
Both define instance configuration (AMI, type, key pair, etc.) for an ASG; Launch Templates are the newer, more flexible version supporting versioning and more instance options — AWS recommends Launch Templates over the legacy Launch Configurations.

**Q5. How does Auto Scaling decide when to scale?**
Via CloudWatch alarms/metrics (like average CPU utilization, request count per target) tied to a scaling policy that triggers scale-out or scale-in actions.

**Q6. What is a cooldown period?**
A configurable pause after a scaling action during which further scaling activities are temporarily suspended, allowing the system to stabilize.

**Q7. What is the difference between "Desired Capacity," "Minimum," and "Maximum" in an ASG?**
Minimum/Maximum define the allowed range of instance count; Desired Capacity is the target number ASG actively tries to maintain within that range.

**Q8. What is a Health Check Grace Period in ASG?**
A buffer time after an instance launches during which ASG ignores failed health checks, giving the instance time to fully boot and initialize before being marked unhealthy.

**Q9. How does ASG integrate with an Elastic Load Balancer for health checks?**
ASG can use the ELB's health check status (in addition to EC2 status checks) to determine if an instance is unhealthy and needs replacing.

**Q10. What is a Lifecycle Hook in Auto Scaling?**
A pause point during instance launch or termination that lets you run custom actions (like installing software or draining connections) before the instance fully enters/leaves service.

**Q11. What is the difference between scale-out and scale-in?**
Scale-out adds instances to handle increased load; scale-in removes instances when load decreases, to save cost.

**Q12. What is Instance Refresh in Auto Scaling?**
A feature that gradually replaces instances in an ASG (e.g., after updating the Launch Template with a new AMI) while maintaining a minimum healthy percentage during the rollout.

**Q13. What's the difference between simple scaling and step scaling policies?**
Simple scaling triggers one fixed adjustment per alarm and then waits out a cooldown; step scaling can apply different-sized adjustments based on how far the metric is from the threshold, responding more precisely to severity.

**Q14. How do you ensure ASG instances are spread across multiple AZs?**
Configure the ASG with subnets from multiple AZs — AWS automatically attempts to balance instances evenly across them.

**Q15. What happens to an instance manually terminated that belongs to an ASG?**
The ASG detects the capacity drop below desired count and automatically launches a replacement instance to restore desired capacity.

**Q16. What is "Termination Policy" in ASG?**
Rules determining which instance ASG removes first during scale-in (e.g., oldest launch configuration, instance closest to the next billing hour, or which AZ has the most instances).

**Q17. Can Auto Scaling be used with on-premises servers?**
Not natively for traditional EC2 ASGs — Auto Scaling is AWS-specific, though hybrid setups can use other tools/Outposts for similar elasticity on-prem.

**Q18. What is the difference between target tracking based on CPUUtilization vs. ALBRequestCountPerTarget?**
CPUUtilization scales based on compute load; ALBRequestCountPerTarget scales based on actual incoming request volume per instance — often a better indicator for request-heavy, lightweight-CPU applications.

**Q19. Scenario: Your ASG keeps launching and terminating instances repeatedly ("flapping") — what's likely wrong?**
Likely an overly aggressive scaling policy or too-short cooldown period reacting to normal metric fluctuations; the fix is usually to use target tracking with a more stable target value or increase the cooldown/evaluation period.

**Q20. What is "Warm Pools" in Auto Scaling?**
A feature that keeps pre-initialized instances in a stopped/running state outside the ASG, ready to be quickly added when scaling out — reducing launch latency for applications with slow boot/initialization times.

**Q21. How do Auto Scaling and Spot Instances work together?**
You can configure an ASG (via a mixed instances policy) to launch a combination of On-Demand and Spot Instances, balancing cost savings with availability/reliability needs.

**Q22. What is a Mixed Instances Policy?**
An ASG configuration allowing multiple instance types and purchase options (On-Demand + Spot) within the same group, improving availability and cost optimization.

**Q23. How would you safely deploy a new application version using Auto Scaling?**
Update the Launch Template with the new AMI/version, then trigger an Instance Refresh (or use a blue/green approach with a new ASG behind the load balancer) to gradually replace old instances with minimal disruption.

**Q24. What metric would you typically use to scale a queue-processing worker fleet?**
A custom CloudWatch metric like SQS `ApproximateNumberOfMessagesVisible`, scaling workers up as the queue backlog grows.

**Q25. What's the difference between "Suspended Processes" in ASG and just deleting the ASG?**
Suspending a process (like scaling actions) temporarily pauses specific ASG behaviors while keeping the group and instances intact — useful during maintenance — versus deleting the ASG, which removes the group entirely (and optionally terminates its instances).

**Q26. How do you handle in-flight requests when an instance is being terminated during scale-in?**
Use ALB connection draining (deregistration delay) so the load balancer stops sending new requests to that instance but lets existing in-flight requests finish before it's terminated.

**Q27. What is predictive scaling, and when would you use it?**
A scaling policy using machine learning on historical load patterns to proactively scale resources ahead of expected demand (e.g., daily traffic peaks), rather than purely reacting after the fact.

**Q28. Can an ASG span multiple regions?**
No — an Auto Scaling Group is region-specific (though it can span multiple AZs within that region); multi-region resilience requires separate ASGs per region, often coordinated via Route 53 or Global Accelerator.

**Q29. What is the relationship between an ASG and CloudWatch alarms in target tracking?**
AWS automatically creates and manages the necessary CloudWatch alarms behind the scenes for target tracking policies — you don't need to manually configure them as you would with step scaling.

**Q30. Scenario: You need zero downtime when rolling out a critical config change across all ASG instances — what's your approach?**
Use Instance Refresh with a defined minimum healthy percentage (e.g., 90%) and a warm-up time, so instances are replaced gradually in small batches while the load balancer continues serving traffic from the remaining healthy instances.

---

## 9. AWS — Elastic Load Balancer (ELB) (30 Questions)

**Q1. What is a Load Balancer, and why use one?**
It distributes incoming traffic across multiple targets to improve availability, fault tolerance, and performance, preventing any single server from being overwhelmed.

**Q2. What types of AWS Load Balancers are there?**
Application Load Balancer (ALB, Layer 7), Network Load Balancer (NLB, Layer 4), Gateway Load Balancer (for third-party appliances), and the legacy Classic Load Balancer.

**Q3. What is a Target Group?**
A group of resources (EC2 instances, IPs, Lambda functions) a load balancer routes requests to, with its own health check settings.

**Q4. What is a health check in a Load Balancer, and how does it work?**
A periodic request the load balancer sends to each target to verify it's healthy; targets that fail consecutively are marked unhealthy and temporarily removed from receiving traffic.

**Q5. ALB vs. NLB — when would you choose each?**
Choose ALB for HTTP/HTTPS traffic needing content-based routing (path/host rules, redirects); choose NLB for ultra-high-performance TCP/UDP traffic, static IP requirements, or preserving client IP at Layer 4.

**Q6. How does an ALB support host-based and path-based routing?**
You define listener rules that route requests to different target groups based on the request's hostname (e.g., `api.example.com`) or URL path (e.g., `/images/*`).

**Q7. What is SSL/TLS termination at the load balancer?**
The load balancer decrypts HTTPS traffic itself (using an attached certificate, e.g., from ACM) and forwards plain HTTP to backend targets, offloading encryption overhead from your instances.

**Q8. What is connection draining (deregistration delay)?**
A configurable time period during which a load balancer stops sending new requests to a deregistering/unhealthy target but allows existing in-flight requests to complete.

**Q9. How does an ALB integrate with Auto Scaling?**
New instances launched by the ASG are automatically registered to the ALB's target group, and as instances are terminated during scale-in, they're deregistered (with connection draining).

**Q10. What is a Listener in a Load Balancer?**
A process that checks for connection requests on a specific port/protocol and applies rules to route matching requests to target groups.

**Q11. What is sticky sessions (session affinity) in ALB?**
A feature that routes a client's requests consistently to the same target for the duration of a session, using a cookie — useful for stateful applications that don't share session data across servers.

**Q12. Difference between Layer 4 and Layer 7 load balancing?**
Layer 4 (NLB) routes based on IP/port/protocol info without inspecting the request content; Layer 7 (ALB) understands HTTP(S) and can route based on URL paths, headers, hostnames, and cookies.

**Q13. What is cross-zone load balancing?**
A setting that ensures traffic is evenly distributed across targets in all enabled AZs, rather than just within the AZ that received the request.

**Q14. How would you redirect all HTTP traffic to HTTPS on an ALB?**
Add a listener rule on the HTTP (80) listener with a redirect action to HTTPS (443), typically as the default action.

**Q15. What is a Network Load Balancer's static IP feature used for?**
NLB provides a fixed IP per AZ (or supports Elastic IPs), useful for clients/firewalls that require whitelisting a stable IP address, unlike ALB which uses DNS-resolved, changing IPs.

**Q16. How do you configure HTTPS on an ALB?**
Request/import a certificate via AWS Certificate Manager (ACM), attach it to an HTTPS (443) listener on the ALB, and choose an appropriate security policy (TLS version/ciphers).

**Q17. What is the X-Forwarded-For header used for with a Load Balancer?**
Since the load balancer's IP appears as the source IP to your backend, this header preserves the original client's IP address so your application can log/use the real client IP.

**Q18. Scenario: Some requests through your ALB are returning 502 Bad Gateway — what would you check?**
Check target health status, confirm the security group on targets allows traffic from the ALB, verify the application is actually listening on the configured target port, and check for timeouts/crashes in application logs.

**Q19. What is the difference between Idle Timeout settings on an ALB?**
The idle timeout defines how long the load balancer keeps an inactive connection open before closing it; if your backend takes longer to respond than this timeout, you may see errors and need to increase it.

**Q20. What is a Gateway Load Balancer used for?**
Deploying, scaling, and managing third-party virtual network appliances (like firewalls or intrusion detection systems) transparently in-line with traffic, operating at Layer 3.

**Q21. How does an NLB preserve the source IP of clients, unlike a Classic Load Balancer in some configs?**
NLB operates at Layer 4 and passes the original client IP directly to the target (unless using certain NAT modes), so backend servers see the real client IP without needing X-Forwarded-For.

**Q22. What is the difference between an internal and an internet-facing Load Balancer?**
An internet-facing LB has a publicly resolvable DNS name and accepts traffic from the internet; an internal LB only has a private IP/DNS, used for routing traffic within a VPC (e.g., between microservices).

**Q23. How do unhealthy threshold and healthy threshold settings work in health checks?**
"Unhealthy threshold" is the number of consecutive failed checks before marking a target unhealthy; "healthy threshold" is the number of consecutive successful checks needed to mark it healthy again.

**Q24. What is the purpose of a WAF (Web Application Firewall) in front of an ALB?**
AWS WAF can be attached to an ALB to filter malicious traffic (SQL injection, XSS, bad bots) at the edge, before requests even reach your backend targets.

**Q25. Can a single ALB route traffic to both EC2 instances and Lambda functions?**
Yes — ALB target groups support EC2 instances, IP addresses, and Lambda functions, allowing a mix within the same load balancer setup using different listener rules.

**Q26. What is the difference between a "weighted" target group and a regular one in ALB?**
Weighted target groups let you split traffic by percentage across multiple target groups (e.g., 90/10) under a single listener rule — commonly used for canary deployments or blue/green rollouts.

**Q27. How would you implement a blue/green deployment using ALB?**
Run the new ("green") version in a separate target group, then either shift traffic gradually using weighted target groups or switch the listener rule entirely from the old ("blue") target group once validated.

**Q28. Scenario: Your application behind an NLB intermittently fails health checks under load, but the app itself seems fine — what could be wrong?**
Possibly the health check interval/timeout is too aggressive for response times under load, or the target is hitting connection/file-descriptor limits — review health check thresholds and server-level connection limits.

**Q29. What is the typical request flow: Client → Route 53 → ALB → Target Group → EC2?**
Route 53 resolves the domain to the ALB's DNS; the ALB's listener evaluates rules and forwards the request to the appropriate target group; the target group then load-balances the request to a healthy EC2 instance/target.

**Q30. How do you monitor Load Balancer performance and errors?**
CloudWatch metrics like `HealthyHostCount`, `UnHealthyHostCount`, `TargetResponseTime`, `HTTPCode_Target_5XX_Count`, combined with ALB access logs (stored in S3) for detailed request-level analysis.

---

## 10. AWS — EFS (30 Questions)

**Q1. What is EFS?**
A managed, scalable NFS file storage service that multiple EC2 instances can mount and access concurrently, automatically growing/shrinking as files are added/removed.

**Q2. EFS vs. EBS vs. S3 — what's the difference?**
EBS is block storage attached to a single instance at a time; EFS is shared file storage multiple instances can mount simultaneously; S3 is object storage accessed via API/HTTP, not a traditional filesystem.

**Q3. What are EFS storage classes?**
Standard (frequent access) and Infrequent Access/IA (cheaper, for rarely accessed files), with Lifecycle Management to automatically transition files between them.

**Q4. When would you choose EFS over EBS?**
When multiple instances need concurrent read/write access to the same shared files — e.g., shared content directories, application logs, or CMS uploads across a web server fleet.

**Q5. Is EFS regional or zonal?**
Regional — it can be mounted from instances across multiple AZs in the same region, supporting high availability.

**Q6. How do you mount an EFS file system on an EC2 instance?**
Install the `amazon-efs-utils` package, then mount using `sudo mount -t efs fs-xxxxxx:/ /mnt/efs` (or via `/etc/fstab` for persistence across reboots).

**Q7. What are EFS performance modes?**
General Purpose (lower latency, suitable for most workloads) and Max I/O (higher throughput/IOPS at the cost of slightly higher latency, for highly parallelized workloads).

**Q8. What are EFS throughput modes?**
Bursting (throughput scales with storage size, with burst credits), Provisioned (fixed throughput you specify regardless of storage size), and Elastic (automatically scales throughput up/down based on actual workload).

**Q9. How is EFS billed?**
Pay for storage used (per GB-month, varying by storage class) plus throughput mode costs if using Provisioned throughput — no pre-provisioning of capacity required like EBS.

**Q10. What is EFS Lifecycle Management?**
A feature that automatically moves files to the Infrequent Access (IA) storage class after a configured period of inactivity (e.g., 30 days), reducing cost for cold data.

**Q11. How do you secure access to an EFS file system?**
Use Security Groups on the EFS mount targets (controlling which instances/subnets can connect via NFS port 2049), and IAM policies/EFS access points for finer-grained, application-level access control.

**Q12. What is an EFS Mount Target?**
A network interface created in each AZ/subnet where you want to mount the file system — instances mount EFS via the mount target's IP/DNS in their AZ.

**Q13. What is an EFS Access Point?**
An application-specific entry point into an EFS file system, enforcing a specific POSIX user/group identity and root directory — useful for restricting and simplifying access for different applications sharing the same file system.

**Q14. Can EFS be mounted from on-premises servers?**
Yes, via AWS Direct Connect or VPN, treating it as an extension of your VPC's network.

**Q15. How does EFS handle encryption?**
Supports encryption at rest (via KMS) configured at creation, and encryption in transit using TLS when mounting with the `amazon-efs-utils` helper.

**Q16. What is the difference between EFS Standard and One Zone storage classes?**
Standard replicates data across multiple AZs for higher availability; One Zone stores data in a single AZ at a lower cost, trading off resilience to AZ failure.

**Q17. How do you back up an EFS file system?**
Use AWS Backup, which can be configured for automated, policy-based backups of EFS file systems.

**Q18. Scenario: Multiple EC2 instances writing to the same EFS file system are seeing stale data — what could be wrong?**
Likely an application-level caching issue rather than EFS itself (since EFS provides strong read-after-write consistency for most operations) — check application or OS-level file caching, and confirm all instances are mounting the same file system/path correctly.

**Q19. What is the maximum size of a file system EFS supports?**
EFS scales elastically to petabyte-scale automatically — there isn't a fixed pre-provisioned capacity limit you need to manage like with EBS.

**Q20. How does EFS compare in latency to EBS for typical web application use?**
EFS, being network-attached NFS storage, generally has higher latency per operation than EBS (which is closer to local block storage) — EFS is chosen for sharing, not raw single-instance speed.

**Q21. Can you resize an EFS file system?**
There's no manual resizing needed — EFS automatically scales storage up or down as files are added or removed, unlike EBS volumes which require explicit resizing.

**Q22. What is the use case for EFS with containers (ECS/EKS)?**
Providing persistent, shared storage across multiple container tasks/pods (even across different EC2 hosts or Fargate), useful for shared configuration, uploads, or stateful applications in a containerized environment.

**Q23. How do you control which AZs an EFS file system is accessible from?**
By creating (or not creating) mount targets in specific subnets/AZs — instances can only mount EFS through a mount target available in their own AZ.

**Q24. What's a common reason an EC2 instance fails to mount an EFS file system?**
Usually a Security Group misconfiguration — the EFS mount target's security group must allow inbound NFS (port 2049) traffic from the EC2 instance's security group/subnet.

**Q25. What is the difference between NFSv4.0 and NFSv4.1 support in EFS mounting?**
EFS supports both, but NFSv4.1 (used by the `amazon-efs-utils` client by default) offers better performance characteristics and is generally recommended over the older 4.0 protocol.

**Q26. How does EFS pricing for Infrequent Access differ from Standard?**
IA storage costs less per GB than Standard but incurs a small per-GB retrieval fee when that data is accessed — ideal for data accessed rarely but still needed occasionally.

**Q27. Is EFS suitable for a high-transaction relational database workload?**
Generally no — EFS's network file system latency profile isn't ideal for the low-latency, high-IOPS random access patterns of relational databases; EBS or RDS is better suited for that.

**Q28. What happens to data in EFS if you terminate all EC2 instances mounting it?**
Nothing — EFS is independent of any specific EC2 instance; the file system and its data persist until you explicitly delete the file system itself.

**Q29. Scenario: You need shared storage for a Lambda function processing files — can you use EFS?**
Yes, Lambda supports mounting EFS file systems (via an Access Point), useful for sharing large files/datasets across invocations beyond Lambda's normal ephemeral storage limits.

**Q30. How would you migrate data from an existing NFS server into EFS?**
Use AWS DataSync, which can efficiently and securely transfer files from on-premises NFS (or other sources) into EFS, handling incremental syncs and validation.

---

## 11. AWS — S3 (32 Questions)

**Q1. What is S3?**
A highly durable, scalable object storage service for storing and retrieving any amount of data via a simple API, organized into buckets.

**Q2. S3 vs. EBS?**
S3 stores objects accessed over HTTP/API, not tied to a specific instance; EBS is block storage that must be attached to a single EC2 instance like a virtual disk.

**Q3. What are S3 storage classes?**
Standard, Intelligent-Tiering, Standard-IA, One Zone-IA, Glacier, Glacier Deep Archive, and Glacier Instant Retrieval — varying by access frequency, durability, and cost.

**Q4. What is S3 Versioning?**
A feature that keeps multiple versions of an object in the same bucket, letting you recover earlier versions if a file is overwritten or deleted.

**Q5. How do you control access to an S3 bucket?**
Bucket policies (resource-based JSON policies), IAM policies, Access Control Lists (ACLs, mostly legacy now), and S3 Block Public Access settings.

**Q6. S3 vs. S3 Glacier?**
S3 (Standard) offers millisecond retrieval for frequently accessed data; Glacier is low-cost archival storage with retrieval times from minutes to hours, meant for rarely accessed data.

**Q7. Is S3 data automatically replicated across AZs?**
Yes, S3 Standard automatically stores data redundantly across multiple AZs within a region, designed for 99.999999999% (11 nines) durability.

**Q8. What is a pre-signed URL?**
A temporary URL granting time-limited access to a private S3 object without requiring the requester to have AWS credentials.

**Q9. What is S3 Object Lock used for?**
Enforcing WORM (Write Once, Read Many) storage — preventing objects from being deleted or overwritten for a fixed retention period or indefinitely (legal hold), useful for compliance.

**Q10. What is the difference between S3 bucket policy and IAM policy for accessing S3?**
A bucket policy is attached directly to the bucket and can grant cross-account access; an IAM policy is attached to a user/role and governs what that identity can do across S3 (and other services).

**Q11. What is S3 Cross-Region Replication (CRR)?**
A feature that automatically copies objects from a bucket in one region to a bucket in another region, useful for disaster recovery, compliance, or latency reduction for global users.

**Q12. What is the difference between CRR and SRR (Same-Region Replication)?**
CRR replicates objects across different AWS regions; SRR replicates within the same region — both work similarly but serve different goals (DR/latency vs. log aggregation/compliance within a region).

**Q13. How do you make an S3 bucket's contents publicly accessible (like for static website hosting)?**
Disable Block Public Access (carefully), enable Static Website Hosting on the bucket, and attach a bucket policy explicitly allowing `s3:GetObject` to everyone (`"Principal": "*"`).

**Q14. What is S3 Transfer Acceleration?**
A feature that speeds up uploads to S3 over long distances by routing traffic through Amazon's globally distributed CloudFront edge locations to the nearest AWS region.

**Q15. What is a Multipart Upload in S3?**
A method for uploading large objects in smaller parts, in parallel, which can be retried independently if a part fails — recommended for objects over ~100MB.

**Q16. What's the difference between S3 Standard-IA and S3 One Zone-IA?**
Standard-IA replicates across multiple AZs for resilience; One Zone-IA stores in only a single AZ at a lower price, trading off availability/durability if that AZ fails.

**Q17. What is an S3 Lifecycle Policy?**
A rule set that automatically transitions objects between storage classes (e.g., Standard → IA → Glacier) or expires (deletes) them after a defined period, based on object age.

**Q18. How does S3 ensure strong consistency?**
S3 provides strong read-after-write consistency for all operations (PUTs and DELETEs) — once a write succeeds, any subsequent read immediately reflects that change.

**Q19. What is an S3 bucket policy condition like `aws:SecureTransport` used for?**
It enforces that requests to the bucket must use HTTPS (encrypted in transit), denying any plain HTTP requests.

**Q20. What is S3 Event Notification used for?**
Triggering actions (like invoking a Lambda function, sending an SQS message, or SNS notification) automatically when specific events occur in a bucket, like object creation or deletion.

**Q21. Scenario: You need to process every image uploaded to an S3 bucket automatically — how would you architect this?**
Configure an S3 Event Notification on `s3:ObjectCreated` events to trigger a Lambda function, which processes (e.g., resizes/thumbnails) the image and optionally writes the result to another bucket.

**Q22. What is the difference between S3 ACLs and Bucket Policies in terms of granularity?**
ACLs grant permissions at the object or bucket level to specific AWS accounts/predefined groups (coarser, largely legacy); Bucket Policies offer fine-grained, condition-based JSON rules and are the recommended modern approach.

**Q23. What is Server-Side Encryption (SSE) in S3, and what types exist?**
Encrypting data at rest automatically — SSE-S3 (AWS-managed keys), SSE-KMS (using AWS KMS keys, with audit trail via CloudTrail), and SSE-C (customer-provided keys you manage yourself).

**Q24. How would you restrict an S3 bucket so it's only accessible from your company's VPC?**
Use a bucket policy with a condition like `"aws:sourceVpce"` (matching a specific VPC Endpoint) combined with a Deny statement for any request not coming through it.

**Q25. What is S3 Intelligent-Tiering, and why use it?**
A storage class that automatically moves objects between access tiers (frequent, infrequent, archive) based on actual usage patterns, without performance impact or manual lifecycle rules — good when access patterns are unpredictable.

**Q26. What is the maximum size of a single object you can store in S3?**
5 TB per object (uploaded via multipart upload); a single PUT request is limited to 5 GB.

**Q27. How do bucket and object-level "Block Public Access" settings interact?**
Block Public Access settings can be applied at the account level, bucket level, or both — the most restrictive setting always wins, so even a permissive bucket policy can be overridden by a stricter account-level block.

**Q28. Scenario: Your S3 costs have grown significantly — how would you investigate and reduce them?**
Use S3 Storage Lens or Cost Explorer to identify which buckets/storage classes are driving cost, check for old/unused versions (without versioning cleanup) or incomplete multipart uploads, and apply lifecycle policies to transition or expire cold data.

**Q29. What is the difference between "Requester Pays" buckets and normal buckets?**
In a Requester Pays bucket, the entity downloading the data (not the bucket owner) pays for the data transfer and request costs — useful when sharing large datasets publicly without bearing the cost yourself.

**Q30. What is S3 Select used for?**
Running simple SQL-like queries directly against an object stored in S3 (e.g., a CSV or JSON file) to retrieve only the data you need, reducing the amount of data transferred and processed.

**Q31. How would you set up a static website using S3 and CloudFront?**
Enable Static Website Hosting on the bucket (or keep it private and use Origin Access Control), create a CloudFront distribution pointing to the bucket as origin, attach an SSL certificate via ACM, and point your domain (via Route 53) to the CloudFront distribution.

**Q32. What's the difference between an S3 bucket name being globally unique vs. objects within it?**
Bucket names must be globally unique across all of AWS (not just your account); object keys only need to be unique within that specific bucket.

---

## 12. AWS — DynamoDB (30 Questions)

**Q1. What is DynamoDB?**
A fully managed, serverless NoSQL key-value and document database designed for fast, predictable performance at virtually any scale.

**Q2. Partition Key vs. Sort Key?**
The Partition Key (hash key) determines which partition stores an item and must be unique alone (unless paired with a Sort Key); the Sort Key (range key) lets multiple items share a partition key, sorted by that key's value.

**Q3. On-Demand vs. Provisioned capacity mode?**
Provisioned requires specifying read/write capacity units upfront (cheaper for steady, predictable workloads); On-Demand automatically scales with traffic and charges per-request (better for unpredictable/spiky workloads).

**Q4. What is a Global Secondary Index (GSI)?**
An index with a partition key/sort key different from the base table, letting you query using attributes other than the primary key — can be added/removed after table creation.

**Q5. What is a Local Secondary Index (LSI)?**
An index sharing the same partition key as the base table but with a different sort key — must be created at table creation time and can't be added later.

**Q6. What is DynamoDB Streams?**
A feature capturing a time-ordered log of item-level changes (insert/update/delete) in a table, often used to trigger Lambda functions for event-driven processing.

**Q7. Is DynamoDB a SQL database?**
No, it's NoSQL — no joins or SQL syntax; queries are based on keys, indexes, and (optionally) the newer PartiQL syntax for SQL-like querying without traditional relational features.

**Q8. What is the difference between `Query` and `Scan` in DynamoDB?**
`Query` efficiently retrieves items matching a specific partition key (and optional sort key condition); `Scan` reads every item in the table (or index), which is much slower and more expensive at scale.

**Q9. What is DynamoDB Accelerator (DAX)?**
A fully managed, in-memory caching layer for DynamoDB that can reduce response times from milliseconds to microseconds for read-heavy workloads.

**Q10. What is the difference between Strongly Consistent and Eventually Consistent reads?**
Strongly Consistent reads always return the most up-to-date data (slightly higher latency/cost); Eventually Consistent reads (the default) may occasionally return slightly stale data but are faster and cheaper.

**Q11. What is a DynamoDB item's maximum size?**
400 KB per item, including attribute names and values.

**Q12. How does DynamoDB achieve high availability?**
By automatically replicating data synchronously across multiple Availability Zones within a region.

**Q13. What is TTL (Time to Live) in DynamoDB?**
A feature letting you set an expiration timestamp attribute on items, after which DynamoDB automatically deletes them — useful for session data, logs, or temporary records.

**Q14. What is DynamoDB Global Tables?**
A feature providing fully managed, multi-region, multi-active replication of tables, allowing low-latency reads/writes from multiple regions with automatic conflict resolution.

**Q15. How does DynamoDB pricing differ between Provisioned and On-Demand?**
Provisioned charges based on reserved read/write capacity units per hour (cheaper if usage is steady/predictable); On-Demand charges per actual request made, with no need to plan capacity in advance.

**Q16. What is a hot partition, and how do you avoid it?**
A situation where a disproportionate amount of traffic hits a single partition key, causing throttling; avoided by choosing a partition key with high cardinality and even access distribution (e.g., adding a random suffix or composite key).

**Q17. What is the difference between BatchGetItem and individual GetItem calls?**
`BatchGetItem` retrieves multiple items (even across different tables) in a single API call, reducing round trips compared to issuing many separate `GetItem` requests.

**Q18. What is conditional writes in DynamoDB used for?**
Ensuring a write only succeeds if a specified condition on the existing item is met (e.g., only update if a version attribute matches), useful for optimistic locking and preventing race conditions.

**Q19. What is DynamoDB Transactions?**
A feature allowing multiple `PutItem`/`UpdateItem`/`DeleteItem`/`ConditionCheck` operations across one or more tables to be executed atomically — all succeed or all fail together.

**Q20. Scenario: Your application is getting `ProvisionedThroughputExceededException` errors — what would you do?**
Switch to On-Demand mode (if traffic is unpredictable), increase provisioned capacity, implement exponential backoff/retry logic in the application, or review the access pattern for a possible hot partition issue.

**Q21. What is the difference between DynamoDB and a traditional RDBMS in terms of schema?**
DynamoDB is schemaless for non-key attributes — only the primary key (partition/sort key) needs to be defined upfront; other attributes can vary freely between items, unlike a fixed relational schema.

**Q22. How do you model one-to-many relationships in DynamoDB, given there are no joins?**
Common patterns include using composite sort keys (e.g., `CUSTOMER#123` / `ORDER#456`) within a single table design, or denormalizing/duplicating data to avoid needing joins at query time.

**Q23. What is PartiQL in the context of DynamoDB?**
A SQL-compatible query language AWS offers for DynamoDB, letting you use familiar SQL-like SELECT/INSERT/UPDATE/DELETE syntax while still operating within DynamoDB's underlying key-value model and constraints.

**Q24. What is the difference between RCU and WCU?**
A Read Capacity Unit (RCU) represents one strongly consistent read per second (up to 4KB); a Write Capacity Unit (WCU) represents one write per second (up to 1KB) — used to calculate provisioned throughput needs.

**Q25. How would you back up a DynamoDB table?**
Use On-Demand backups (manual, full table snapshot anytime) or Point-in-Time Recovery (PITR), which continuously backs up the table and lets you restore to any second within the last 35 days.

**Q26. What is the single-table design pattern in DynamoDB, and why is it used?**
Storing multiple, different entity types within one table (distinguished by key structure/prefixes) to optimize for DynamoDB's strengths — minimizing the number of requests needed to fetch related data, since there are no joins.

**Q27. What is the difference between an attribute being of type String, Number, and Binary in DynamoDB?**
These are DynamoDB's basic scalar data types — String (text), Number (numeric, stored as a string internally for precision), and Binary (raw byte data, e.g., for encoded files) — alongside types like Boolean, List, Map, and Set.

**Q28. How does DynamoDB integrate with Lambda for event-driven processing?**
Via DynamoDB Streams — a Lambda function can be configured as a trigger, automatically invoked whenever items in the table are inserted, updated, or deleted.

**Q29. What is auto scaling in DynamoDB (Provisioned mode)?**
A feature that automatically adjusts provisioned RCU/WCU within defined min/max bounds based on actual traffic, using a target utilization percentage, similar in spirit to EC2 Auto Scaling.

**Q30. Scenario: You're designing a DynamoDB table for an e-commerce order system with unpredictable traffic spikes during sales — what capacity mode and design would you choose?**
On-Demand capacity mode to handle unpredictable spikes without manual provisioning, combined with a well-distributed partition key (e.g., customer ID or order ID) to avoid hot partitions, and possibly DAX if read latency during peak traffic becomes a concern.

---

## 13. AWS — CloudWatch (30 Questions)

**Q1. What is CloudWatch?**
A monitoring and observability service for AWS resources and applications — collecting metrics, logs, and events, and triggering alarms or automated actions.

**Q2. What is a CloudWatch Alarm?**
A watcher on a metric that triggers an action (notification, Auto Scaling, etc.) when the metric crosses a defined threshold for a specified evaluation period.

**Q3. CloudWatch Logs vs. CloudWatch Metrics?**
Logs store raw log data from applications/services; Metrics are numerical time-series data points (like CPUUtilization) used for monitoring trends and triggering alarms.

**Q4. What is a CloudWatch Dashboard?**
A customizable visual page displaying multiple metrics/graphs from different AWS resources in one place for at-a-glance monitoring.

**Q5. What is the CloudWatch Agent used for?**
Software installed on EC2 instances or on-prem servers to collect additional system-level metrics (like memory, disk) and custom logs not available by default.

**Q6. CloudWatch vs. CloudTrail?**
CloudWatch focuses on performance monitoring (metrics, logs, alarms); CloudTrail focuses on auditing — logging API calls and user activity for security/compliance.

**Q7. What is a CloudWatch Log Group and Log Stream?**
A Log Group is a container for related log streams (e.g., all logs from one Lambda function); a Log Stream is a sequence of log events from a single source (e.g., one specific instance or invocation).

**Q8. What is a Metric Filter in CloudWatch Logs?**
A pattern that scans incoming log data for matches (e.g., the word "ERROR") and converts matches into a numeric CloudWatch metric, which can then trigger alarms.

**Q9. What is the difference between a Standard and a High-Resolution metric?**
Standard metrics are reported at 1-minute granularity by default; High-Resolution metrics can be reported as frequently as 1-second intervals, useful for catching rapid spikes.

**Q10. What is CloudWatch Logs Insights?**
A query tool for interactively searching and analyzing log data stored in CloudWatch Logs, using a purpose-built query language.

**Q11. How do you monitor custom application metrics not provided by AWS by default?**
Publish custom metrics using the `PutMetricData` API (or via the CloudWatch Agent/embedded metric format) from within your application code.

**Q12. What is a CloudWatch Composite Alarm?**
An alarm that combines the states of multiple other alarms using logical operators (AND/OR), triggering only when the overall combined condition is met — reduces noisy, isolated alerts.

**Q13. What is the difference between "Alarm State: OK", "ALARM", and "INSUFFICIENT_DATA"?**
OK means the metric is within the defined threshold; ALARM means it breached the threshold for the configured period; INSUFFICIENT_DATA means there isn't enough data yet to evaluate the alarm's condition.

**Q14. How does CloudWatch integrate with SNS for notifications?**
An alarm action can publish a message to an SNS topic when triggered, which can then fan out to email, SMS, Lambda, or other subscribers.

**Q15. What is CloudWatch Events / EventBridge, and how does it relate to CloudWatch?**
EventBridge (formerly CloudWatch Events) is AWS's event bus service for routing events between AWS services and triggering targets (like Lambda) based on rules — distinct from but often used alongside core CloudWatch monitoring.

**Q16. How long are CloudWatch Logs retained by default?**
Indefinitely (never expire) by default, unless you explicitly configure a retention policy (e.g., 7, 30, 90 days) on the log group.

**Q17. Scenario: You want to be alerted if your application's error rate exceeds 5% over 5 minutes — how would you set this up?**
Create a metric filter on the error logs to generate a custom metric, then set up a CloudWatch Alarm comparing that metric (or an error-rate expression) against a 5% threshold over a 5-minute evaluation period, with an SNS notification action.

**Q18. What is the difference between CloudWatch Metrics' "Average," "Sum," and "Maximum" statistics?**
Average gives the mean value over the period; Sum totals all data points; Maximum shows the highest single value recorded — chosen depending on what best represents the behavior you're monitoring.

**Q19. How can CloudWatch Alarms trigger Auto Scaling actions?**
A scaling policy is attached to a CloudWatch Alarm (e.g., high CPU), so when the alarm state changes to ALARM, it directly invokes the associated Auto Scaling action (scale-out or scale-in).

**Q20. What is a CloudWatch Synthetics Canary?**
A scripted, scheduled "fake user" check that monitors application endpoints/APIs/UI flows continuously, alerting you proactively if something breaks, even before real users are impacted.

**Q21. How do you monitor Lambda function performance using CloudWatch?**
Lambda automatically sends metrics (Invocations, Duration, Errors, Throttles) to CloudWatch, plus logs of each invocation to CloudWatch Logs, viewable per-function.

**Q22. What is the difference between CloudWatch's default metrics and detailed monitoring for EC2?**
Default (basic) monitoring reports metrics every 5 minutes for free; detailed monitoring reports every 1 minute for an additional cost, giving finer-grained visibility.

**Q23. Scenario: A CloudWatch Alarm is stuck in "INSUFFICIENT_DATA" — what's likely the cause?**
The metric isn't receiving data points yet (e.g., the resource was just created, the metric name/dimension is misconfigured, or no traffic/activity has occurred to generate that metric).

**Q24. What is CloudWatch Contributor Insights?**
A feature that analyzes log data to surface top contributors to a metric (e.g., which IP addresses or users are generating the most traffic/errors), helping pinpoint root causes quickly.

**Q25. How would you centralize logs from multiple EC2 instances into CloudWatch?**
Install and configure the CloudWatch Agent on each instance, pointing it to send specific log files into shared (or per-instance) Log Groups in CloudWatch Logs.

**Q26. What's the difference between a CloudWatch Alarm based on a single metric vs. a Metric Math expression?**
A standard alarm watches one metric directly; a Metric Math alarm can combine/transform multiple metrics using mathematical expressions (e.g., error rate = errors / total requests) before evaluating the threshold.

**Q27. What is CloudWatch's role in cost monitoring?**
While AWS Cost Explorer/Budgets are the primary tools, CloudWatch billing alarms (based on the `EstimatedCharges` metric) can notify you if account spending crosses a defined threshold.

**Q28. How do you troubleshoot a missing custom metric that your application is supposed to be sending?**
Check the application's IAM permissions for `cloudwatch:PutMetricData`, verify correct namespace/dimension naming, confirm network connectivity to the CloudWatch endpoint, and check for silent API errors in application logs.

**Q29. What is the difference between CloudWatch Logs subscription filters and metric filters?**
A metric filter converts matching log patterns into a numeric metric; a subscription filter streams matching log events in near real-time to a destination like Lambda, Kinesis, or OpenSearch for further processing.

**Q30. Scenario: You need end-to-end visibility for a microservices app (latency, errors, traces across services) — how does CloudWatch fit in, and what else might you use?**
CloudWatch provides metrics, logs, and alarms per service, but for full distributed tracing across microservices, you'd typically pair it with AWS X-Ray to visualize request flow and pinpoint latency/errors across service boundaries.

---

## 14. Docker (32 Questions)

**Q1. What is Docker, and why is it used?**
A containerization platform that packages an application with all its dependencies into a lightweight, portable container, ensuring consistent behavior across environments.

**Q2. Docker Image vs. Docker Container?**
An image is a read-only template/blueprint; a container is a running (or stopped) instance created from that image.

**Q3. What is a Dockerfile?**
A text file with instructions (`FROM`, `RUN`, `COPY`, `CMD`, etc.) used to automatically build a Docker image.

**Q4. CMD vs. ENTRYPOINT?**
`CMD` provides default arguments/command, easily overridden at runtime; `ENTRYPOINT` sets the main command that always runs, often combined with `CMD` to supply default arguments to it.

**Q5. VM vs. Docker Container?**
A VM virtualizes hardware with a full guest OS (heavier, slower to start); a container virtualizes at the OS level, sharing the host kernel (lightweight, fast to start).

**Q6. What is Docker Compose?**
A tool for defining and running multi-container applications using a single YAML file, configuring multiple services, networks, and volumes together.

**Q7. What is a Docker Volume?**
A mechanism for persisting data outside a container's writable layer, so data survives even if the container is removed.

**Q8. How do you list running and all containers?**
`docker ps` for running containers; `docker ps -a` for all containers, including stopped ones.

**Q9. docker stop vs. docker kill?**
`docker stop` sends a graceful SIGTERM (with timeout before forcing SIGKILL); `docker kill` immediately force-stops with SIGKILL.

**Q10. What is Docker Hub?**
A public/private cloud registry for storing and sharing Docker images.

**Q11. What is a multi-stage build in Docker, and why use one?**
A Dockerfile technique using multiple `FROM` stages, where you build/compile in one stage and copy only the final artifacts into a smaller, leaner final image — reducing image size and excluding build tools from production.

**Q12. What is the difference between `COPY` and `ADD` in a Dockerfile?**
`COPY` simply copies files/directories from the build context into the image; `ADD` does the same but also supports extracting tar archives automatically and fetching from remote URLs (generally `COPY` is preferred unless you specifically need those extras).

**Q13. How do you reduce the size of a Docker image?**
Use a smaller base image (e.g., Alpine), combine RUN commands to reduce layers, clean up cache/temp files within the same layer, use multi-stage builds, and use a `.dockerignore` file to exclude unnecessary files from the build context.

**Q14. What is a `.dockerignore` file used for?**
Similar to `.gitignore` — it excludes specified files/folders from being sent to the Docker build context, reducing build time and image bloat.

**Q15. What is the difference between bind mounts and named volumes?**
Bind mounts map a specific path on the host filesystem into the container; named volumes are managed entirely by Docker (stored in Docker's storage area), making them more portable and easier to back up/manage.

**Q16. How do containers communicate with each other in Docker?**
Via Docker networks — containers on the same user-defined bridge network can reach each other using their container name as a hostname, without needing to expose ports externally.

**Q17. What is the default Docker network driver, and what are the alternatives?**
`bridge` is the default for standalone containers; alternatives include `host` (shares the host's network namespace directly), `overlay` (for multi-host networking in Swarm/clusters), and `none` (no networking).

**Q18. How do you persist a container's logs and inspect them?**
`docker logs <container>` (with `-f` to follow in real time); by default, Docker captures stdout/stderr, which can also be configured to forward to external logging drivers.

**Q19. What is the difference between `docker run` and `docker start`?**
`docker run` creates a new container from an image and starts it; `docker start` restarts an existing (stopped) container without creating a new one.

**Q20. How do you pass environment variables into a container?**
Using `-e VAR_NAME=value` on `docker run`, an `--env-file`, or the `environment` key in a `docker-compose.yml`.

**Q21. What is a Docker network's "bridge" mode, and how is it different from "host" mode?**
Bridge mode gives the container its own isolated network namespace with NAT'd access to the host's network; host mode removes that isolation, letting the container share the host's network stack directly (no port mapping needed, but less isolation).

**Q22. Scenario: A container exits immediately after `docker run` — how do you debug it?**
Check `docker logs <container>` for the error, run `docker run -it <image> /bin/sh` to interactively explore, and verify the Dockerfile's `CMD`/`ENTRYPOINT` is a long-running foreground process (containers exit when their main process exits).

**Q23. What is the difference between `docker exec` and `docker attach`?**
`docker exec` runs a new command/process inside an already-running container (e.g., opening a new shell); `docker attach` connects your terminal to the container's already-running main process's stdin/stdout/stderr.

**Q24. How do you limit a container's CPU and memory usage?**
Using flags like `--memory=512m` and `--cpus=1.5` on `docker run`, or equivalent settings in a `docker-compose.yml` / orchestrator config.

**Q25. What is an Image Layer, and how does Docker's layer caching work?**
Each instruction in a Dockerfile creates a new, cacheable layer; if a layer's inputs haven't changed since the last build, Docker reuses the cached layer instead of rebuilding it, speeding up subsequent builds.

**Q26. Why is it best practice to avoid running containers as the root user?**
Running as root inside a container increases the security blast radius if the container is compromised (especially with certain misconfigurations); using a non-root user (via `USER` in the Dockerfile) follows least-privilege principles.

**Q27. What is Docker Swarm, and how does it differ from Kubernetes?**
Docker Swarm is Docker's native, simpler container orchestration tool for clustering and scaling containers across multiple hosts; Kubernetes is a more powerful, feature-rich (but more complex) orchestration platform that has become the industry standard.

**Q28. How do you push a custom image to a private registry?**
Tag the image appropriately (`docker tag myimage registry-url/myimage:tag`), log in (`docker login registry-url`), then `docker push registry-url/myimage:tag`.

**Q29. What is the difference between `docker-compose up` and `docker-compose up -d`?**
Without `-d`, containers run in the foreground with logs streamed to your terminal; with `-d` (detached mode), containers run in the background, freeing up your terminal.

**Q30. Scenario: Your Docker build is very slow because dependencies are reinstalled every time, even with no code changes — how do you fix it?**
Reorder the Dockerfile so dependency installation steps (like `COPY package.json` + `npm install`) come before copying the full application source code — this way, Docker's layer cache for the install step is reused unless the dependency file itself changes.

**Q31. What is the difference between an anonymous volume and a named volume?**
An anonymous volume is created without a specific name (harder to reference/reuse later, and easily orphaned); a named volume has an explicit name, making it easier to reference, share between containers, and manage/clean up intentionally.

**Q32. How would you troubleshoot high memory usage in a running container?**
Use `docker stats` to monitor real-time resource usage per container, check the application's own memory profiling/logs for leaks, and compare against configured memory limits to see if it's being throttled or OOM-killed.

---

## 15. Terraform (32 Questions)

**Q1. What is Terraform?**
An open-source Infrastructure as Code (IaC) tool by HashiCorp for defining and provisioning cloud infrastructure declaratively across providers like AWS, Azure, and GCP.

**Q2. Terraform vs. CloudFormation?**
CloudFormation is AWS-specific; Terraform is cloud-agnostic, managing infrastructure across multiple providers with a single, consistent workflow.

**Q3. What is the Terraform state file?**
A file (`terraform.tfstate`) recording the current state of managed infrastructure, mapping real-world resources to your configuration and used to detect drift.

**Q4. What is `terraform plan` used for?**
It generates an execution plan, showing what actions (create/update/destroy) Terraform will take to reach the desired state — without making any actual changes.

**Q5. What is `terraform apply` used for?**
It executes the planned changes, actually creating, updating, or destroying real infrastructure resources.

**Q6. What is a Terraform provider?**
A plugin that lets Terraform interact with a specific platform's API (e.g., the AWS provider manages AWS resources).

**Q7. Module vs. Resource in Terraform?**
A resource is a single infrastructure object (e.g., one EC2 instance); a module is a reusable, organized collection of resources/variables/outputs, callable multiple times with different inputs.

**Q8. What is `terraform destroy` used for?**
It removes all resources tracked in the Terraform state, tearing down the infrastructure that was created.

**Q9. Variables and Outputs in Terraform?**
`variable` blocks parameterize configurations for reusability; `output` blocks expose specific resulting values (like an instance's IP) after `apply`, useful for chaining or display.

**Q10. What happens without remote state locking if two people run `terraform apply` simultaneously?**
It can cause state file corruption or conflicting changes — remote backends (like S3 + DynamoDB for locking) prevent this in team environments.

**Q11. What is a remote backend in Terraform, and why use one?**
A storage location (e.g., S3, Terraform Cloud) for the state file outside your local machine — enables team collaboration, state locking, and avoids losing state if your local machine fails.

**Q12. What is the purpose of `terraform init`?**
It initializes a working directory — downloading required providers/modules and setting up the backend before any plan/apply can run.

**Q13. What is the difference between `terraform validate` and `terraform plan`?**
`validate` checks the configuration syntax and internal consistency without contacting the provider; `plan` actually communicates with the provider's API to compute the real diff against current infrastructure.

**Q14. What is a `.tfvars` file used for?**
A file to define variable values separately from the main configuration, keeping environment-specific values (like dev vs. prod settings) out of the core `.tf` files.

**Q15. What is the difference between `count` and `for_each` in Terraform?**
`count` creates a specified number of identical (or index-referenced) resource instances; `for_each` creates one resource instance per item in a map or set, offering more meaningful keys/identifiers than a simple index.

**Q16. What is a Terraform "data source"?**
A way to query and use information about existing infrastructure not managed by your current Terraform configuration (e.g., looking up an existing VPC's ID) without creating/managing it.

**Q17. How do you import existing infrastructure into Terraform's state?**
Use `terraform import <resource_address> <resource_id>` to bring an already-existing real-world resource under Terraform's management without recreating it.

**Q18. What is the difference between `terraform taint` (or the newer `-replace` flag) and a regular apply?**
Tainting/replacing marks a specific resource to be destroyed and recreated on the next apply, even if its configuration hasn't changed — useful when a resource is in a bad state outside of Terraform's awareness.

**Q19. What is a Terraform Workspace, and what's it used for?**
A way to maintain multiple distinct state files (e.g., dev, staging, prod) using the same configuration code, switching context via `terraform workspace select <name>`.

**Q20. Scenario: `terraform plan` shows it wants to recreate a resource you didn't intend to change — what's likely happening?**
Often caused by a change to an immutable attribute (forcing replacement) or "configuration drift" where someone manually changed the resource outside Terraform, causing a mismatch with the state file.

**Q21. What is the difference between a Terraform "resource" lifecycle block's `create_before_destroy` and the default behavior?**
By default, Terraform destroys the old resource before creating its replacement; `create_before_destroy = true` reverses that order, creating the new resource first — useful to avoid downtime for resources like Auto Scaling Launch Configs or DNS records.

**Q22. What is the purpose of `depends_on` in Terraform?**
Explicitly declaring a dependency between resources when Terraform can't automatically infer it from configuration references alone, ensuring correct creation/destruction order.

**Q23. What is the difference between local and remote state locking?**
Local state has no real locking mechanism (risky for teams); remote backends like S3 (with a DynamoDB table) or Terraform Cloud provide locking, preventing concurrent applies from corrupting the state.

**Q24. How do you handle secrets (like database passwords) in Terraform safely?**
Avoid hardcoding them in `.tf` files; instead use environment variables, a secrets manager (like AWS Secrets Manager/Vault) referenced via data sources, and ensure state files (which may contain sensitive values) are stored securely and not committed to version control.

**Q25. What is the difference between `terraform refresh` (or `plan -refresh-only`) and a normal plan?**
A refresh-only operation updates the state file to match real-world infrastructure without proposing any resource changes — purely syncing Terraform's knowledge of current reality.

**Q26. What is a "provisioner" in Terraform, and when would you use one (or avoid one)?**
A provisioner (like `remote-exec` or `local-exec`) runs scripts/commands on a resource after creation; generally considered a last resort, since Terraform recommends configuration management tools (Ansible, user-data scripts) for that purpose, as provisioners aren't tracked as cleanly in state.

**Q27. How do you structure Terraform code for multiple environments (dev/staging/prod)?**
Common patterns include separate state files/workspaces per environment, or separate directories with shared modules and environment-specific `.tfvars` files, to avoid accidentally applying dev changes to production.

**Q28. What is the Terraform "plan" file, and why save one (`terraform plan -out=plan.tfplan`)?**
It captures the exact computed plan to a file, which can later be applied with `terraform apply plan.tfplan` — guaranteeing the apply matches exactly what was reviewed, avoiding drift between plan and apply time (important in CI/CD pipelines).

**Q29. Scenario: You need to migrate Terraform state from local to an S3 backend without losing existing resources — what's the process?**
Add/configure the `backend "s3"` block in your Terraform configuration, run `terraform init`, and Terraform will detect the backend change and prompt to migrate the existing local state into the new remote backend automatically.

**Q30. What is the difference between a "module" sourced from a local path vs. a Terraform Registry/Git source?**
A local path module references code within your own repo/filesystem; a Registry or Git-sourced module pulls reusable, often versioned, community or organization-published code from an external source — useful for standardizing common infrastructure patterns.

**Q31. How would you safely roll out a Terraform change across a large team's shared infrastructure?**
Use a remote backend with state locking, integrate `terraform plan` into a CI/CD pipeline for mandatory review before merge, require PR approval, and apply only through a controlled pipeline (not ad hoc from individual laptops) to ensure consistency and auditability.

**Q32. Scenario: You ran `terraform apply` and it partially failed midway (some resources created, others not) — what do you do next?**
Review the error to fix the underlying issue (e.g., a naming conflict or quota limit), then simply run `terraform apply` again — Terraform's state-driven approach means it will only act on the remaining resources needed to reach the desired state, without recreating what already succeeded.

---

### Quick Tips for the Interview (Fresher + 1.5 Years Experience)
- At 1.5 years, interviewers expect you to go beyond definitions — be ready to explain **how you've actually used these tools** in real tasks (e.g., "I set up an ALB with target groups for a Node.js app behind an ASG").
- Expect at least 1-2 **scenario/troubleshooting questions** per topic ("X is broken/slow — what do you check first?") — practice talking through your debugging approach out loud, step by step.
- It's okay to say "I haven't hit that exact scenario, but based on how [service] works, I'd approach it by..." — structured reasoning matters more than memorized answers.
- Be ready to connect topics together — e.g., how EC2 + ASG + ALB + CloudWatch work as one system, or how IAM Roles tie into EC2, Lambda, and S3 access — since real interviews often ask "how would you design X" questions that span multiple services.
