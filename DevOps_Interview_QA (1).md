# DevOps Tools — Interview Q&A (50 Questions Each)

Topics: Terraform, Jenkins, GitHub Actions, Bitbucket, Docker, Docker Compose, AWS CloudWatch, Datadog

---

## 1. Terraform

1. **What is Terraform?**
An open-source Infrastructure as Code (IaC) tool by HashiCorp used to provision and manage cloud infrastructure using declarative configuration files.

2. **What language does Terraform use?**
HashiCorp Configuration Language (HCL), a declarative language; it also supports JSON syntax.

3. **What is a Terraform provider?**
A plugin that lets Terraform interact with APIs of cloud platforms like AWS, Azure, GCP, etc.

4. **What is the Terraform state file?**
A file (terraform.tfstate) that stores the current state of managed infrastructure, mapping resources to real-world objects.

5. **Why is the state file important?**
It allows Terraform to track resource metadata, detect drift, and plan changes accurately.

6. **What is remote state?**
Storing the state file in a remote backend (like S3, Terraform Cloud) instead of locally, enabling team collaboration.

7. **What is state locking?**
A mechanism to prevent concurrent operations on the same state file, avoiding corruption, often via DynamoDB with S3 backend.

8. **What command initializes a Terraform project?**
`terraform init` — downloads providers and sets up the backend.

9. **What does `terraform plan` do?**
Shows an execution plan of what changes will be made without applying them.

10. **What does `terraform apply` do?**
Applies the changes required to reach the desired state defined in configuration files.

11. **What does `terraform destroy` do?**
Destroys all resources managed by the current Terraform configuration.

12. **What is a Terraform module?**
A reusable, self-contained package of Terraform configurations used to organize and reuse code.

13. **What is a variable in Terraform?**
An input parameter defined using `variable` block to make configurations dynamic and reusable.

14. **What is an output in Terraform?**
A way to display or export values from a Terraform configuration after apply.

15. **What is the difference between variables.tf and terraform.tfvars?**
variables.tf declares variables; terraform.tfvars assigns actual values to those variables.

16. **What is a data source in Terraform?**
A way to fetch information about existing infrastructure not managed by the current configuration.

17. **What is the purpose of `terraform validate`?**
Checks whether the configuration files are syntactically valid.

18. **What is `terraform fmt`?**
Formats configuration files into a canonical style.

19. **What is a workspace in Terraform?**
An isolated instance of state, allowing multiple environments (dev/staging/prod) with the same configuration.

20. **What is drift in Terraform?**
A mismatch between actual infrastructure and the state file, usually caused by manual changes.

21. **How do you import existing infrastructure into Terraform?**
Using `terraform import` to bring an existing resource under Terraform management.

22. **What is a provisioner in Terraform?**
A block used to execute scripts on local or remote machines during resource creation/destruction, e.g., `remote-exec`.

23. **What is the difference between count and for_each?**
`count` creates resources based on a number; `for_each` creates resources based on a map or set, giving more control over identity.

24. **What is a Terraform backend?**
Configuration that determines where state is stored, e.g., local, S3, Terraform Cloud.

25. **What is the lifecycle block used for?**
To control resource behavior like `create_before_destroy`, `prevent_destroy`, and `ignore_changes`.

26. **What is Terraform Cloud?**
A HashiCorp-managed service providing remote state, run management, and collaboration features for Terraform.

27. **What is a null_resource?**
A resource that doesn't create any infrastructure but is used to trigger provisioners.

28. **How do you handle secrets in Terraform?**
Using environment variables, vault integration, or encrypted variable files; avoid hardcoding secrets in .tf files.

29. **What is the difference between `terraform apply` and `terraform apply -auto-approve`?**
The latter skips the manual confirmation prompt and applies changes automatically.

30. **What is a Terraform plan file?**
A saved output of `terraform plan` that can be applied later using `terraform apply <planfile>`.

31. **How does Terraform handle dependencies between resources?**
Automatically via implicit references, or explicitly using `depends_on`.

32. **What is the difference between Terraform and CloudFormation?**
Terraform is cloud-agnostic and multi-provider; CloudFormation is AWS-specific.

33. **What is a resource block?**
The core building block in Terraform that defines a piece of infrastructure to be created.

34. **What happens if you delete the state file?**
Terraform loses track of existing resources and may try to recreate them, potentially causing duplication.

35. **What is the purpose of `.terraform.lock.hcl`?**
Locks provider versions to ensure consistent behavior across team members and environments.

36. **How can you split Terraform configuration into multiple files?**
Terraform automatically merges all `.tf` files in a directory; you can organize by main.tf, variables.tf, outputs.tf.

37. **What is a target apply?**
Using `-target` flag to apply changes to specific resources instead of the whole configuration.

38. **What is the taint command used for?**
`terraform taint` marks a resource for recreation on the next apply (deprecated in favor of `-replace`).

39. **What are local values in Terraform?**
Named expressions defined using `locals` block to simplify and reuse values within configuration.

40. **How do you manage multiple environments in Terraform?**
Using separate workspaces, directories, or variable files per environment.

41. **What is the difference between a module and a provider?**
A module is a group of resources reused together; a provider is a plugin to interact with an API.

42. **What is Sentinel in Terraform?**
A policy-as-code framework used by Terraform Cloud/Enterprise to enforce compliance rules.

43. **How do you handle version constraints in providers?**
Using version arguments like `version = "~> 4.0"` in the provider or required_providers block.

44. **What is the difference between `terraform refresh` and `terraform plan`?**
`refresh` updates the state file with real infrastructure data; `plan` compares desired vs current state.

45. **What is a dynamic block?**
A block used to generate repeated nested configuration blocks dynamically based on a list or map.

46. **How do you rollback infrastructure changes in Terraform?**
By reverting configuration code and reapplying, or restoring a previous state file version.

47. **What is the purpose of the `required_version` setting?**
Specifies the minimum/maximum Terraform CLI version compatible with the configuration.

48. **What is idempotency in Terraform?**
Applying the same configuration multiple times produces the same result without unintended side effects.

49. **What is the difference between Terraform apply and terraform-plan-only pipelines?**
Plan-only pipelines run checks/reviews without changing infrastructure; apply pipelines actually provision resources.

50. **How does Terraform ensure consistency across teams?**
Through remote state, state locking, version pinning, and modules shared via a registry.

---

## 2. Jenkins

1. **What is Jenkins?**
An open-source automation server used for building, testing, and deploying software through CI/CD pipelines.

2. **What is a Jenkins pipeline?**
A suite of plugins supporting implementation of continuous delivery pipelines as code, defined via Jenkinsfile.

3. **What is a Jenkinsfile?**
A text file containing the pipeline definition, checked into source control.

4. **What are the two types of Jenkins pipeline syntax?**
Declarative pipeline and Scripted pipeline.

5. **What is the difference between declarative and scripted pipelines?**
Declarative is structured and easier to read using predefined syntax; scripted uses Groovy for full flexibility.

6. **What is a Jenkins agent/node?**
A machine that executes Jenkins jobs, can be master or a separate worker node.

7. **What is the Jenkins master?**
The central server that schedules jobs, manages configurations, and dispatches builds to agents.

8. **What is a Jenkins plugin?**
An extension that adds functionality to Jenkins, such as Git integration, Docker support, or Slack notifications.

9. **What is a freestyle project in Jenkins?**
A simple, GUI-configured Jenkins job type without pipeline-as-code, suited for basic build tasks.

10. **What is the purpose of the `stage` block in a pipeline?**
Groups a sequence of steps representing a distinct phase like Build, Test, or Deploy.

11. **What is a post section in a Jenkinsfile?**
Defines actions to run after pipeline execution based on status like success, failure, or always.

12. **How do you trigger a Jenkins job automatically?**
Using triggers like SCM polling, webhooks, cron-based scheduling, or upstream job triggers.

13. **What is a webhook in Jenkins CI/CD?**
An HTTP callback from a source control system (like GitHub) that notifies Jenkins of code changes to trigger builds.

14. **What is the Blue Ocean plugin?**
A modern UI for Jenkins that visualizes pipelines in a more intuitive way.

15. **What is a Jenkins credential store?**
A secure place to store secrets like passwords, tokens, and SSH keys used in pipelines.

16. **What is parallel execution in Jenkins pipelines?**
Running multiple stages or steps concurrently to reduce overall build time using the `parallel` block.

17. **What is the purpose of `agent any` in a pipeline?**
Tells Jenkins to run the pipeline on any available executor/node.

18. **What is a Jenkinsfile checked into SCM called?**
Pipeline as Code, enabling version control of build configurations.

19. **What is the difference between Jenkins and GitHub Actions?**
Jenkins is a self-hosted, plugin-based automation server; GitHub Actions is a managed CI/CD service tightly integrated with GitHub.

20. **What is a Jenkins shared library?**
Reusable Groovy code that can be shared across multiple Jenkinsfiles/pipelines.

21. **How do you pass parameters to a Jenkins job?**
Using the `parameters` block to define string, boolean, or choice parameters accessible in the pipeline.

22. **What is the purpose of the `when` directive?**
Conditionally executes a stage based on specified criteria like branch name or environment variable.

23. **What is the Jenkins queue?**
A holding area for builds waiting for an available executor.

24. **What is an executor in Jenkins?**
A slot on a node capable of running one build at a time.

25. **How does Jenkins integrate with Docker?**
By using Docker agents to run builds inside containers, or building/pushing Docker images as pipeline steps.

26. **What is the purpose of `checkout scm` in a Jenkinsfile?**
Checks out source code from the configured SCM repository into the workspace.

27. **What is a multibranch pipeline?**
A pipeline type that automatically creates jobs for each branch containing a Jenkinsfile.

28. **How do you handle secrets securely in Jenkins?**
Using the Credentials plugin and referencing them via `withCredentials` block instead of hardcoding.

29. **What is the difference between `sh` and `bat` steps?**
`sh` runs shell commands on Unix/Linux agents; `bat` runs batch commands on Windows agents.

30. **What is a Jenkins build artifact?**
Files generated during a build (like JARs, WARs, or reports) that can be archived for later use.

31. **How do you archive artifacts in Jenkins?**
Using the `archiveArtifacts` step in a pipeline to save build outputs.

32. **What is the purpose of the `input` step?**
Pauses the pipeline to wait for manual user approval before proceeding.

33. **What is a distributed build in Jenkins?**
Running builds across multiple agent nodes to balance load and speed up execution.

34. **How can you restart a failed Jenkins pipeline from a specific stage?**
Using the "Restart from Stage" feature available in declarative pipelines.

35. **What is the Jenkins Configuration as Code (JCasC) plugin?**
Allows Jenkins configuration to be defined and managed via YAML files instead of manual UI setup.

36. **What is the purpose of environment variables in Jenkins pipelines?**
Store reusable values like credentials, paths, or flags accessible throughout the pipeline via the `environment` block.

37. **What is a Jenkins trigger for upstream/downstream jobs?**
Using `build job:` step or "Build after other projects are built" to chain jobs together.

38. **How do you clean the workspace in Jenkins?**
Using the `cleanWs()` step or Workspace Cleanup plugin to delete files after a build.

39. **What is the difference between `stage` and `step`?**
A stage is a logical grouping of the pipeline (e.g., Build); a step is an individual task/command within a stage.

40. **How does Jenkins support notifications?**
Through plugins for email, Slack, Microsoft Teams, etc., triggered on build status changes.

41. **What is the Jenkinsfile `tools` directive used for?**
Automatically installs and configures tools like Maven, JDK, or Node.js for the pipeline.

42. **What is a Jenkins agent label?**
A tag assigned to nodes so jobs can be directed to run on specific machines with required capabilities.

43. **How do you retry a failed step in Jenkins pipeline?**
Using the `retry(n) { }` block to attempt a step multiple times before failing.

44. **What is the difference between Jenkins X and traditional Jenkins?**
Jenkins X is a Kubernetes-native CI/CD solution for cloud-native applications, whereas traditional Jenkins is more general-purpose.

45. **How do you secure a Jenkins instance?**
Enable authentication/authorization, use HTTPS, restrict script execution (sandboxing), and keep plugins updated.

46. **What is the purpose of the `timeout` directive?**
Fails a stage or pipeline if it exceeds a specified duration.

47. **What is the Jenkins Pipeline Utility Steps plugin used for?**
Provides utility functions like reading/writing JSON, YAML, and properties files within pipelines.

48. **How can Jenkins integrate with Kubernetes?**
Using the Kubernetes plugin to dynamically provision pod-based agents for builds.

49. **What is a Jenkinsfile `matrix` directive?**
Allows running the same stage across multiple combinations of variables (like OS and version) in parallel.

50. **How do you version control Jenkins pipeline configurations?**
By storing Jenkinsfiles in the same repository as the application code (Pipeline as Code).

---

## 3. GitHub Actions

1. **What is GitHub Actions?**
A CI/CD platform built into GitHub that automates build, test, and deployment workflows directly from a repository.

2. **What is a workflow in GitHub Actions?**
An automated process defined in a YAML file inside `.github/workflows/` that runs one or more jobs.

3. **What is a job in GitHub Actions?**
A set of steps executed on the same runner, part of a workflow.

4. **What is a step in GitHub Actions?**
An individual task within a job, either running a shell command or using an action.

5. **What is an action in GitHub Actions?**
A reusable unit of code that performs a specific task, can be custom-built or from the marketplace.

6. **What is a runner in GitHub Actions?**
A server (GitHub-hosted or self-hosted) that executes workflow jobs.

7. **What triggers a GitHub Actions workflow?**
Events like `push`, `pull_request`, `schedule`, `workflow_dispatch`, or external repository dispatch events.

8. **What is the `on` keyword used for?**
Specifies the event(s) that trigger the workflow.

9. **What is the difference between GitHub-hosted and self-hosted runners?**
GitHub-hosted runners are managed by GitHub with preinstalled tools; self-hosted runners are maintained by the user on their own infrastructure.

10. **What is a matrix strategy in GitHub Actions?**
Allows running a job across multiple combinations of variables like OS versions or language versions in parallel.

11. **What is the purpose of `actions/checkout`?**
Checks out the repository code into the runner so subsequent steps can access it.

12. **What are secrets in GitHub Actions?**
Encrypted environment variables stored at repo/org level, used to securely pass sensitive data like tokens or passwords.

13. **How do you reference a secret in a workflow?**
Using `${{ secrets.SECRET_NAME }}` syntax.

14. **What is a workflow_dispatch event?**
Allows manually triggering a workflow from the GitHub UI or API with optional input parameters.

15. **What is the difference between `needs` and `if` in GitHub Actions?**
`needs` defines job dependencies (execution order); `if` adds conditional logic to control whether a job/step runs.

16. **What is a composite action?**
An action combining multiple steps into a single reusable action, defined via an `action.yml` file.

17. **What is the GitHub Actions Marketplace?**
A repository of prebuilt, community and official actions that can be reused in workflows.

18. **What is caching in GitHub Actions?**
Storing dependencies (like node_modules) between workflow runs using `actions/cache` to speed up builds.

19. **What is the purpose of `env` in a workflow?**
Defines environment variables available to jobs or steps.

20. **What is an artifact in GitHub Actions?**
Files generated during a workflow run that can be uploaded and downloaded using `actions/upload-artifact` and `actions/download-artifact`.

21. **What is a reusable workflow?**
A workflow that can be called from other workflows using the `workflow_call` trigger, promoting DRY pipelines.

22. **How do you pass outputs between jobs?**
By defining `outputs` in one job and referencing them via `needs.<job_id>.outputs.<name>` in another.

23. **What is the difference between `push` and `pull_request` triggers?**
`push` runs on direct commits pushed to a branch; `pull_request` runs when a PR is opened/updated.

24. **What is concurrency control in GitHub Actions?**
Using the `concurrency` key to cancel or queue overlapping workflow runs for the same group.

25. **What is the purpose of `permissions` in a workflow?**
Controls the GITHUB_TOKEN's access scope for security (read/write to contents, issues, etc.).

26. **What is GITHUB_TOKEN?**
An automatically generated token used to authenticate workflow actions against the GitHub API.

27. **How can you schedule a workflow to run periodically?**
Using the `schedule` trigger with cron syntax.

28. **What is a self-hosted runner label?**
A tag used to target specific self-hosted runners for jobs requiring certain hardware/software.

29. **What is the difference between a workflow and an action?**
A workflow is the overall automated process; an action is a reusable building block used within workflow steps.

30. **How do you run jobs in parallel vs sequentially?**
Jobs run in parallel by default unless `needs` is specified to enforce sequential dependency.

31. **What is the purpose of `continue-on-error`?**
Allows a step to fail without stopping the entire job/workflow.

32. **How do environments work in GitHub Actions?**
Environments (like production, staging) can have protection rules, secrets, and required reviewers before deployment jobs run.

33. **What is the `uses` keyword in a workflow step?**
Specifies which action to run, referencing it by repo and version tag.

34. **How do you debug a GitHub Actions workflow?**
Enable debug logging via secrets `ACTIONS_STEP_DEBUG` and `ACTIONS_RUNNER_DEBUG`, and review run logs.

35. **What is the difference between org-level and repo-level secrets?**
Org-level secrets are shared across multiple repositories; repo-level secrets are scoped to a single repository.

36. **What is a composite run step vs a Docker container action?**
Composite steps combine shell commands/actions; Docker actions run inside a specified Docker container image.

37. **What is the purpose of `strategy.fail-fast`?**
Cancels all matrix jobs if one fails, unless set to false to let others continue.

38. **How do you restrict workflows to specific branches?**
Using `branches` filter under the `on.push` or `on.pull_request` trigger.

39. **What is a status check in GitHub Actions?**
A pass/fail indicator shown on PRs based on workflow job results, often required before merging.

40. **How can GitHub Actions integrate with Docker?**
By building and pushing Docker images as workflow steps, or running jobs inside Docker containers.

41. **What is the purpose of `workflow_run` trigger?**
Triggers a workflow when another specified workflow completes.

42. **How do you limit workflow execution time?**
Using `timeout-minutes` at the job or step level.

43. **What is the difference between `actions/cache` and artifacts?**
Cache speeds up repeated builds (like dependencies) across runs; artifacts store outputs for the current run for retrieval/inspection.

44. **How do you use a matrix to exclude specific combinations?**
Using the `exclude` key under `strategy.matrix` to skip certain OS/version combinations.

45. **What is required for deploying to AWS/Azure/GCP from GitHub Actions?**
Configuring OIDC-based authentication or storing cloud credentials as encrypted secrets.

46. **What is the purpose of `runs-on`?**
Specifies the type of machine/runner (e.g., ubuntu-latest, windows-latest) a job runs on.

47. **How can you reuse the same steps across multiple workflows?**
By creating a composite action or a reusable workflow.

48. **What is the difference between push-based and PR-based CI validation?**
Push-based validates code as it merges to a branch; PR-based validates proposed changes before merge.

49. **How do you approve deployments to protected environments?**
By configuring required reviewers in environment protection rules under repository settings.

50. **What is the benefit of using GitHub Actions over external CI tools?**
Native integration with GitHub repositories, PRs, and issues, reducing setup overhead and improving developer experience.

---

## 4. Bitbucket

1. **What is Bitbucket?**
A Git-based source code repository hosting service by Atlassian, supporting Git repositories and CI/CD via Bitbucket Pipelines.

2. **What is Bitbucket Pipelines?**
An integrated CI/CD service in Bitbucket that automates build, test, and deployment using a YAML configuration file.

3. **What is the bitbucket-pipelines.yml file?**
The configuration file defining pipeline steps, stages, and triggers for a Bitbucket repository.

4. **What is a Bitbucket repository?**
A Git repository hosted on Bitbucket used to store and version control source code.

5. **What is the difference between Bitbucket Cloud and Bitbucket Server/Data Center?**
Bitbucket Cloud is a hosted SaaS solution; Bitbucket Server/Data Center is self-hosted on-premises.

6. **What is a pull request in Bitbucket?**
A request to merge changes from one branch into another, allowing code review before merging.

7. **What are branch permissions in Bitbucket?**
Rules restricting who can push, merge, or delete specific branches (like main/master).

8. **What is a Bitbucket pipe?**
A reusable, pre-packaged script/action that can be used in Bitbucket Pipelines, similar to GitHub Actions.

9. **What is the purpose of deployment environments in Bitbucket Pipelines?**
Allow separating pipeline steps by stage (like Test, Staging, Production) with environment-specific variables.

10. **How are secrets managed in Bitbucket Pipelines?**
Using repository or deployment environment variables marked as "secured" to hide their values in logs.

11. **What is the difference between a step and a stage in Bitbucket Pipelines?**
A step runs a set of commands in an isolated Docker container; a stage groups multiple steps sequentially.

12. **What triggers a Bitbucket pipeline?**
Events like a push to a branch, a tag creation, or a pull request, based on rules in the YAML file.

13. **What is a custom pipeline in Bitbucket?**
A manually triggered pipeline defined under the `pipelines.custom` section of the YAML file.

14. **What is the `image` keyword used for in Bitbucket Pipelines?**
Specifies the Docker image used to run pipeline steps.

15. **How do you enable parallel steps in Bitbucket Pipelines?**
Using the `parallel` block to group steps that run concurrently.

16. **What is a Bitbucket Pipelines cache?**
A mechanism to store dependencies (like node_modules) between builds to speed up pipeline execution.

17. **What is Bitbucket's built-in Jira integration used for?**
Linking commits, branches, and pull requests to Jira issues for traceability.

18. **What is a webhook in Bitbucket?**
An HTTP callback that notifies external services (like Jenkins or Slack) about repository events.

19. **What is the difference between Bitbucket and GitHub?**
Bitbucket has deep integration with Jira/Trello and supports Mercurial (historically); GitHub has a larger open-source community and marketplace.

20. **What are deployment variables in Bitbucket?**
Environment-specific variables scoped to a deployment environment, like staging or production credentials.

21. **What is the purpose of `artifacts` in Bitbucket Pipelines?**
Preserves files generated in one step so they can be used in subsequent steps.

22. **How do you restrict a pipeline to run only on specific branches?**
Using branch-specific configuration blocks under the `branches` key in bitbucket-pipelines.yml.

23. **What is Bitbucket's default build minutes limit?**
Bitbucket Cloud plans include a monthly quota of build minutes, varying by subscription tier.

24. **What is the purpose of the `condition` clause in Bitbucket Pipelines?**
Allows conditional execution of a step, such as running only when specific files change.

25. **How can Bitbucket Pipelines deploy to AWS?**
Using AWS CLI within pipeline steps, along with securely stored AWS credentials as repository variables.

26. **What is a Bitbucket workspace?**
A container that holds multiple repositories, projects, and users under one organizational unit.

27. **What is repository access control in Bitbucket?**
Permissions settings (admin, write, read) controlling what actions users can perform on a repository.

28. **What is the purpose of branching models in Bitbucket?**
Predefined workflows like Git Flow to standardize how feature, release, and hotfix branches are managed.

29. **How do you trigger a pipeline manually in Bitbucket?**
By running a custom pipeline from the Bitbucket UI, selecting the branch and pipeline definition.

30. **What is the significance of the `default` pipeline block?**
Defines steps that run automatically for every push unless overridden by branch-specific rules.

31. **What is Bitbucket Pipes marketplace?**
A collection of official and community-built pipes for common integrations like Slack notifications or AWS deployments.

32. **How does Bitbucket handle merge checks?**
Through merge check settings requiring passing builds, approvals, or resolved tasks before allowing a merge.

33. **What is the difference between fast-forward and merge commit in Bitbucket PRs?**
Fast-forward moves the branch pointer without a new commit; merge commit creates a new commit combining both histories.

34. **What is the purpose of `size` in Bitbucket Pipelines configuration?**
Defines the amount of memory/CPU resources allocated to a pipeline step (e.g., 1x, 2x, 4x).

35. **How do you set up notifications for pipeline failures in Bitbucket?**
Using integrations with Slack/email or custom pipes that send alerts based on pipeline status.

36. **What is a Bitbucket Smart Mirror?**
A feature (in Bitbucket Server) that creates local mirrors of repositories for distributed teams to improve clone/fetch speed.

37. **What is the role of SSH keys in Bitbucket?**
Used for secure, passwordless authentication when cloning or pushing to repositories.

38. **What is Bitbucket's approval requirement feature?**
Allows setting a minimum number of approvals before a pull request can be merged.

39. **How do you integrate Bitbucket with Jenkins?**
Using webhooks or the Bitbucket plugin in Jenkins to trigger builds on repository events.

40. **What is a repository variable in Bitbucket?**
A key-value pair accessible in pipelines, used for configuration or non-secret data across all branches.

41. **What is the purpose of the `after-script` section?**
Defines commands to run after the main script in a step, regardless of success or failure.

42. **How do you version Docker images built in Bitbucket Pipelines?**
By tagging images with commit SHA, branch name, or build number during the build step.

43. **What is Bitbucket's Snippets feature?**
Allows sharing small pieces of code or text within a workspace, similar to GitHub Gists.

44. **How does Bitbucket support monorepos?**
Through path-based triggers and conditions to run specific pipeline steps only when relevant folders change.

45. **What is the significance of `definitions` in bitbucket-pipelines.yml?**
Allows defining reusable YAML anchors like custom caches or services used across multiple steps.

46. **How can you run Bitbucket Pipelines locally for testing?**
Using tools like `docker` directly to simulate steps, since native local pipeline runners aren't officially provided.

47. **What is a services block in Bitbucket Pipelines?**
Defines auxiliary Docker containers (like databases) that run alongside the main pipeline step for testing.

48. **How do you handle multi-branch deployment strategies in Bitbucket?**
Using branch-specific pipeline definitions mapped to different deployment environments.

49. **What is the purpose of Bitbucket's code insights feature?**
Displays results from external tools (linting, security scans) directly on pull requests as annotations.

50. **How does Bitbucket ensure repository security?**
Through IP allowlisting, two-step verification, branch permissions, and access tokens with scoped permissions.

---

## 5. Docker

1. **What is Docker?**
A platform for developing, shipping, and running applications inside lightweight, portable containers.

2. **What is a container?**
An isolated, lightweight runtime environment that packages an application with its dependencies, sharing the host OS kernel.

3. **What is the difference between a container and a virtual machine?**
Containers share the host OS kernel and are lightweight; VMs include a full guest OS, making them heavier and slower to start.

4. **What is a Docker image?**
A read-only template containing application code, libraries, and dependencies used to create containers.

5. **What is a Dockerfile?**
A text file containing instructions to build a Docker image.

6. **What is the purpose of the `FROM` instruction?**
Specifies the base image to build upon in a Dockerfile.

7. **What is the difference between `CMD` and `ENTRYPOINT`?**
`CMD` provides default arguments that can be overridden; `ENTRYPOINT` defines the fixed executable that always runs.

8. **What is the purpose of the `COPY` instruction?**
Copies files/directories from the host machine into the Docker image.

9. **What is the difference between `COPY` and `ADD`?**
`ADD` can also extract compressed files and fetch remote URLs; `COPY` only copies local files/directories.

10. **What is a Docker layer?**
Each instruction in a Dockerfile creates a layer, cached and reused to speed up builds.

11. **What is Docker Hub?**
A public registry for storing and sharing Docker images.

12. **What command builds a Docker image?**
`docker build -t <image_name> .`

13. **What command runs a container from an image?**
`docker run <image_name>`

14. **What is the difference between `docker run` and `docker start`?**
`docker run` creates and starts a new container; `docker start` starts an existing stopped container.

15. **What is a Docker volume?**
A persistent storage mechanism managed by Docker, used to store data outside the container's writable layer.

16. **What is the difference between a volume and a bind mount?**
Volumes are managed by Docker and stored in Docker's storage area; bind mounts map to a specific path on the host filesystem.

17. **What is Docker networking?**
The mechanism enabling containers to communicate with each other and the outside world, via bridge, host, or overlay networks.

18. **What is the default Docker network driver?**
Bridge network.

19. **What is the purpose of `EXPOSE` in a Dockerfile?**
Documents which port the container listens on, though it doesn't publish the port automatically.

20. **How do you publish a container's port to the host?**
Using the `-p host_port:container_port` flag with `docker run`.

21. **What is a multi-stage build in Docker?**
A technique using multiple `FROM` statements in one Dockerfile to reduce final image size by discarding build-time dependencies.

22. **What is the purpose of `.dockerignore`?**
Specifies files/directories to exclude when building a Docker image, similar to `.gitignore`.

23. **What is the difference between `docker stop` and `docker kill`?**
`stop` sends SIGTERM and waits for graceful shutdown; `kill` sends SIGKILL to terminate immediately.

24. **What is a container registry?**
A storage and distribution system for Docker images, e.g., Docker Hub, Amazon ECR, or private registries.

25. **How do you remove unused Docker images and containers?**
Using `docker system prune` to clean up unused data.

26. **What is the purpose of `docker exec`?**
Runs a command inside a running container, often used to open an interactive shell.

27. **What is the difference between an image and a container?**
An image is a static template; a container is a running (or stopped) instance of that image.

28. **What is Docker Compose?**
A tool for defining and running multi-container Docker applications using a YAML file.

29. **What is a Docker tag?**
A label attached to an image to identify its version, e.g., `myapp:1.0`.

30. **What is the purpose of `docker logs`?**
Displays the standard output/error logs generated by a running or stopped container.

31. **What is the difference between ENV and ARG in a Dockerfile?**
`ARG` is available only during the build process; `ENV` persists into the running container.

32. **What is a healthcheck in Docker?**
A configured command that Docker runs periodically to determine if a container is healthy.

33. **What is the purpose of `docker inspect`?**
Returns detailed low-level information about a container, image, or network in JSON format.

34. **What is an overlay network in Docker?**
A network type enabling communication between containers running on different Docker hosts, often used in Swarm mode.

35. **What is Docker Swarm?**
Docker's native clustering and orchestration tool for managing multiple containers across multiple hosts.

36. **How is Docker Swarm different from Kubernetes?**
Swarm is simpler and tightly integrated with Docker CLI; Kubernetes is more powerful and feature-rich but has a steeper learning curve.

37. **What is the purpose of `WORKDIR` in a Dockerfile?**
Sets the working directory for subsequent instructions like RUN, CMD, COPY.

38. **How do you reduce the size of a Docker image?**
Using multi-stage builds, minimal base images (like Alpine), and combining RUN commands to reduce layers.

39. **What is the purpose of `docker-compose up`?**
Starts and runs all services defined in a docker-compose.yml file.

40. **What is a bind mount used for?**
Sharing files/directories directly between the host and container, useful in development for live code reload.

41. **What is the difference between `docker rm` and `docker rmi`?**
`docker rm` removes a container; `docker rmi` removes an image.

42. **What is a named volume in Docker?**
A volume with a specific name, managed and persisted by Docker independent of any single container.

43. **What is the purpose of Docker's layered filesystem (UnionFS)?**
Combines multiple layers into a single filesystem view, enabling caching and image reuse.

44. **How do you pass environment variables to a container?**
Using the `-e` flag with `docker run` or an `env_file` in Docker Compose.

45. **What is the purpose of `docker-compose down`?**
Stops and removes containers, networks, and optionally volumes defined in the Compose file.

46. **What is container orchestration?**
Automated management of container deployment, scaling, networking, and availability, e.g., via Kubernetes or Swarm.

47. **What is the difference between a private and public Docker registry?**
Public registries are accessible to anyone; private registries restrict access to authorized users/organizations.

48. **How do you scan Docker images for vulnerabilities?**
Using tools like Docker Scout, Trivy, or Snyk to detect known CVEs in image layers.

49. **What is the purpose of `docker network create`?**
Creates a custom user-defined network for containers to communicate with better isolation and DNS resolution.

50. **What are best practices for writing Dockerfiles?**
Use minimal base images, leverage layer caching, avoid running as root, combine RUN commands, and use multi-stage builds.

---

## 6. Docker Compose

1. **What is Docker Compose?**
A tool that defines and manages multi-container Docker applications using a single YAML configuration file.

2. **What is the docker-compose.yml file?**
A YAML file describing services, networks, and volumes for a multi-container application.

3. **What is a service in Docker Compose?**
A definition of a container's configuration (image, ports, volumes, environment) within the Compose file.

4. **What command starts services defined in Compose?**
`docker-compose up` or `docker compose up` (v2 CLI plugin syntax).

5. **What command stops and removes Compose resources?**
`docker-compose down`.

6. **What is the difference between `docker-compose up` and `docker-compose up -d`?**
`-d` runs containers in detached (background) mode instead of attaching to the terminal.

7. **How do you scale a service using Docker Compose?**
Using `docker-compose up --scale <service>=<number>` to run multiple instances of a service.

8. **What is the purpose of the `depends_on` key?**
Specifies startup order dependencies between services, though it doesn't wait for the service to be fully ready.

9. **How do you define environment variables in Compose?**
Using the `environment` key directly in the YAML, or referencing an `.env` file via `env_file`.

10. **What is the purpose of the `volumes` key in Compose?**
Mounts host directories or named volumes into containers for persistent or shared storage.

11. **What is the purpose of the `networks` key in Compose?**
Defines custom networks for services to communicate, isolating them from other unrelated containers.

12. **What is the difference between named volumes and bind mounts in Compose?**
Named volumes are managed by Docker; bind mounts map directly to a host filesystem path.

13. **How do you rebuild images when using Compose?**
Using `docker-compose build` or `docker-compose up --build`.

14. **What is the purpose of the `.env` file in Docker Compose?**
Stores default values for variables referenced in the Compose file, like `${VARIABLE_NAME}`.

15. **How do you view logs for services in Compose?**
Using `docker-compose logs` or `docker-compose logs -f <service>` for real-time logs.

16. **What is the purpose of `docker-compose ps`?**
Lists the status of containers defined in the Compose project.

17. **What is the default network created by Docker Compose?**
A bridge network automatically created for the project, allowing services to communicate using service names as hostnames.

18. **How do you override configuration for different environments in Compose?**
Using multiple Compose files (e.g., docker-compose.override.yml) merged with the `-f` flag.

19. **What is the purpose of `restart: always` in Compose?**
Ensures a container automatically restarts if it stops or the Docker daemon restarts.

20. **What is the difference between `docker-compose stop` and `docker-compose down`?**
`stop` halts containers without removing them; `down` stops and removes containers, networks, and optionally volumes.

21. **How do you run a one-off command in a Compose service?**
Using `docker-compose run <service> <command>`.

22. **What is the purpose of `build.context` in Compose?**
Specifies the directory containing the Dockerfile and files needed for building the image.

23. **How do you define a custom Dockerfile path in Compose?**
Using the `build.dockerfile` key to point to a non-default Dockerfile name/location.

24. **What is the version key in older Compose files used for?**
Specifies the Compose file format version, determining available features (largely deprecated in Compose V2).

25. **How do you link services in Compose without exposing ports externally?**
By placing them on the same custom network; Compose provides internal DNS resolution by service name.

26. **What is the purpose of `docker-compose exec`?**
Executes a command inside a running Compose service container, e.g., opening a shell.

27. **How do you persist database data across container restarts in Compose?**
Using a named volume mapped to the database's data directory.

28. **What is the significance of service dependencies with healthchecks in Compose?**
Using `depends_on.condition: service_healthy` ensures a dependent service waits until another is confirmed healthy, not just started.

29. **How do you pass build arguments in Docker Compose?**
Using the `args` key under the `build` section to pass `ARG` values to the Dockerfile.

30. **What is the purpose of `docker-compose config`?**
Validates and displays the effective, merged Compose configuration.

31. **How do you limit CPU/memory resources for a service in Compose?**
Using the `deploy.resources.limits` section (mainly effective in Swarm mode) or `mem_limit`/`cpus` in Compose V2.

32. **What is the difference between Compose and Kubernetes?**
Compose is for local/simple multi-container setups on a single host; Kubernetes orchestrates containers at scale across clusters.

33. **How do you use multiple Compose files together?**
Using `docker-compose -f base.yml -f override.yml up` to merge configurations.

34. **What is the purpose of the `command` key in a service definition?**
Overrides the default command specified in the image's Dockerfile.

35. **How can you check the effective environment variables of a service?**
Using `docker-compose exec <service> env` to list variables inside the running container.

36. **What is the purpose of `external: true` for networks/volumes in Compose?**
Indicates the network/volume already exists outside the current Compose project and should be reused, not created.

37. **How do you set container names explicitly in Compose?**
Using the `container_name` key under a service definition.

38. **What is the purpose of the `profiles` key in Compose?**
Allows grouping services so they only start when a specific profile is activated, useful for optional services.

39. **How do you handle secrets in Docker Compose?**
Using the `secrets` key to mount sensitive files securely into containers, often paired with Docker Swarm.

40. **What is the purpose of `docker-compose top`?**
Displays the running processes for each service container.

41. **How do you troubleshoot a service that keeps restarting in Compose?**
Checking `docker-compose logs <service>` and inspecting exit codes and health check status.

42. **What is the difference between `restart: on-failure` and `restart: always`?**
`on-failure` restarts only if the container exits with a non-zero code; `always` restarts regardless of exit status.

43. **How do you expose a fixed host port for a service?**
Using the `ports` key, e.g., `"8080:80"` mapping host port 8080 to container port 80.

44. **What is the purpose of the `working_dir` key in Compose?**
Sets the working directory inside the container for the service's process.

45. **How do you share a volume between multiple services in Compose?**
Defining the volume once under the top-level `volumes` key and referencing it in multiple services.

46. **What is the significance of `docker-compose pull`?**
Pulls the latest images specified in the Compose file from the registry without starting containers.

47. **How can you validate a Compose file without running it?**
Using `docker-compose config` to check syntax and resolved values.

48. **What is the purpose of using Compose in CI/CD pipelines?**
To spin up consistent, reproducible multi-service test environments for integration testing.

49. **How do you remove only volumes when tearing down Compose services?**
Using `docker-compose down -v` to also delete named volumes.

50. **What are best practices when using Docker Compose?**
Use `.env` files for configuration, pin image versions, define healthchecks, and separate override files for dev/prod environments.

---

## 7. AWS CloudWatch

1. **What is AWS CloudWatch?**
A monitoring and observability service that collects metrics, logs, and events from AWS resources and applications.

2. **What is a CloudWatch metric?**
A time-ordered set of data points representing a variable being monitored, like CPU utilization.

3. **What is a CloudWatch namespace?**
A container for organizing related metrics, e.g., AWS/EC2 or a custom namespace for application metrics.

4. **What is a CloudWatch alarm?**
A rule that monitors a metric and triggers an action (like notification or auto-scaling) when a threshold is breached.

5. **What are the possible states of a CloudWatch alarm?**
OK, ALARM, and INSUFFICIENT_DATA.

6. **What is CloudWatch Logs?**
A service for collecting, storing, and monitoring log data from AWS resources and applications.

7. **What is a log group in CloudWatch?**
A container that holds multiple log streams, typically representing a single application or resource type.

8. **What is a log stream in CloudWatch?**
A sequence of log events from a single source, like a specific EC2 instance or Lambda invocation.

9. **What is the CloudWatch Agent?**
Software installed on EC2 instances or on-premises servers to collect system-level metrics and logs beyond default AWS metrics.

10. **What is the difference between standard and detailed monitoring in CloudWatch?**
Standard monitoring sends metrics every 5 minutes; detailed monitoring sends metrics every 1 minute (at additional cost).

11. **What is a CloudWatch dashboard?**
A customizable visual display of metrics and alarms across multiple AWS resources in one view.

12. **What is CloudWatch Logs Insights?**
A query tool for interactively searching and analyzing log data stored in CloudWatch Logs.

13. **What is a metric filter in CloudWatch?**
A pattern that extracts specific data from log events and converts it into a metric.

14. **What is CloudWatch Events / EventBridge?**
A service that delivers real-time event data and can trigger automated actions based on changes in AWS resources.

15. **What is the retention period for CloudWatch Logs?**
Configurable per log group, ranging from 1 day to indefinite retention (never expire).

16. **How do you send custom metrics to CloudWatch?**
Using the `PutMetricData` API call or AWS SDK/CLI to publish application-specific metrics.

17. **What is a composite alarm in CloudWatch?**
An alarm that combines the states of multiple other alarms using logical operators (AND, OR, NOT).

18. **What is the difference between CloudWatch and CloudTrail?**
CloudWatch monitors performance metrics and logs; CloudTrail records API calls and user activity for auditing.

19. **What is a CloudWatch alarm action?**
An automated response triggered by an alarm state change, such as sending an SNS notification or triggering Auto Scaling.

20. **What is the purpose of CloudWatch Synthetics?**
Allows creating canaries (scripts) that simulate user traffic to monitor endpoints and APIs proactively.

21. **What is CloudWatch Contributor Insights?**
A feature that analyzes log data to identify top contributors impacting system performance, like top users or IPs.

22. **What is the CloudWatch unified agent used for?**
Collects both metrics and logs from EC2 instances and on-premises servers in a single agent.

23. **What is a CloudWatch anomaly detection alarm?**
An alarm using machine learning to detect abnormal metric behavior instead of relying on static thresholds.

24. **How does CloudWatch integrate with Auto Scaling?**
Metrics like CPU utilization trigger scaling policies to add or remove EC2 instances automatically.

25. **What is the difference between a CloudWatch alarm and an SNS topic?**
An alarm monitors and detects a condition; an SNS topic is the notification mechanism the alarm can publish to.

26. **What is CloudWatch Logs subscription filter?**
A configuration that streams log data in real time to destinations like Lambda, Kinesis, or OpenSearch.

27. **What is the purpose of CloudWatch metric math?**
Allows performing calculations and transformations across multiple metrics to create derived metrics.

28. **How do you monitor Lambda functions using CloudWatch?**
Lambda automatically sends metrics like Invocations, Duration, and Errors, plus logs to CloudWatch Logs.

29. **What is a high-resolution metric in CloudWatch?**
A custom metric with a granularity as fine as 1 second, compared to the default 1-minute resolution.

30. **What is the purpose of CloudWatch Application Insights?**
Automatically detects problems in applications running on AWS by analyzing logs, metrics, and application resources.

31. **How does CloudWatch pricing work?**
Based on number of metrics, alarms, dashboard usage, log ingestion/storage volume, and API requests.

32. **What is the difference between CloudWatch Logs and CloudWatch Metrics?**
Logs store raw event data (text records); metrics store numerical time-series data for monitoring trends.

33. **What is a CloudWatch alarm's evaluation period?**
The number of consecutive periods a metric must breach the threshold before the alarm changes state.

34. **How can CloudWatch be used with ECS/EKS?**
Container Insights collects performance metrics and logs from ECS clusters and EKS pods for monitoring.

35. **What is CloudWatch cross-account observability?**
A feature enabling centralized monitoring of metrics, logs, and traces across multiple AWS accounts from one monitoring account.

36. **What is the purpose of CloudWatch ServiceLens?**
Provides a visual overview combining traces, metrics, and logs to help diagnose application issues end-to-end.

37. **How do you export CloudWatch Logs to S3?**
Using the `create-export-task` API/CLI command to export log data for long-term archival or analysis.

38. **What is the difference between push-based and pull-based metrics in CloudWatch?**
Pull-based metrics (like EC2 CPU) are collected automatically by AWS; push-based metrics require the application to send data via the API.

39. **What is a CloudWatch billing alarm?**
An alarm configured on estimated AWS charges to notify when spending crosses a defined threshold.

40. **How do you troubleshoot missing CloudWatch metrics?**
Check IAM permissions, agent configuration, correct namespace/region, and network connectivity to CloudWatch endpoints.

41. **What is the purpose of CloudWatch Logs retention policy?**
Automatically deletes log events older than the specified retention period to manage storage costs.

42. **What is a CloudWatch alarm's "treat missing data" setting?**
Configures how the alarm behaves when data points are missing, e.g., treat as missing, breaching, not breaching, or ignore.

43. **How does CloudWatch support tracing?**
Through integration with AWS X-Ray, correlating traces with logs and metrics for distributed application monitoring.

44. **What is the difference between CloudWatch Logs Insights and Athena for log analysis?**
Logs Insights is optimized for querying CloudWatch Logs directly; Athena queries logs stored in S3 using standard SQL.

45. **What is a CloudWatch metric stream?**
A feature that continuously streams CloudWatch metrics to a destination like Kinesis Data Firehose for third-party analytics tools.

46. **How do you monitor custom application logs with CloudWatch?**
By installing the CloudWatch agent or using an SDK to push logs directly, and defining log groups/streams.

47. **What IAM permissions are required to publish custom metrics?**
The `cloudwatch:PutMetricData` permission, along with resource-level access as needed.

48. **What is the significance of the CloudWatch "Automatic Dashboard"?**
AWS-generated default dashboards providing an overview of resource health without manual configuration.

49. **How can CloudWatch alarms trigger Auto Remediation?**
By configuring alarm actions to invoke Lambda functions or SSM Automation documents that fix issues automatically.

50. **What are best practices for using CloudWatch effectively?**
Set meaningful alarm thresholds, use log retention policies, tag resources for filtering, and use dashboards for centralized visibility.

---

## 8. Datadog

1. **What is Datadog?**
A cloud-based monitoring and analytics platform providing observability across infrastructure, applications, and logs.

2. **What are the core pillars of observability in Datadog?**
Metrics, Traces, and Logs.

3. **What is the Datadog Agent?**
A lightweight software process installed on hosts to collect metrics, traces, and logs and send them to Datadog.

4. **What is APM in Datadog?**
Application Performance Monitoring — tracks requests across distributed services to identify latency and errors.

5. **What is a Datadog dashboard?**
A customizable visual interface displaying metrics, graphs, and widgets for monitoring systems in real time.

6. **What is a Datadog monitor?**
An alerting mechanism that watches a metric, log, or event and notifies teams when thresholds are breached.

7. **What is a tag in Datadog?**
A key-value label attached to metrics, logs, or traces to filter, group, and organize monitoring data.

8. **What is the difference between Datadog Logs and Metrics?**
Logs are detailed, timestamped event records; metrics are aggregated numerical time-series data for trends.

9. **What is a Datadog integration?**
A pre-built connector that allows Datadog to collect data from specific technologies like AWS, Docker, or Kubernetes.

10. **What is Datadog Log Management?**
A feature for collecting, processing, and analyzing log data with powerful search and filtering capabilities.

11. **What is a facet in Datadog Logs?**
An indexed attribute extracted from logs used for filtering, grouping, and building visualizations.

12. **What is the purpose of Datadog's log pipeline?**
Processes incoming logs by parsing, enriching, and structuring them before indexing.

13. **What is Datadog Synthetic Monitoring?**
A feature that simulates user interactions and API calls to proactively test application availability and performance.

14. **What is a Datadog Service Level Objective (SLO)?**
A measurable target defining the desired reliability of a service, based on metrics or monitors over time.

15. **What is Datadog Infrastructure Monitoring?**
Real-time visibility into host, container, and cloud resource performance metrics like CPU, memory, and network.

16. **What is the Datadog Live Container view?**
A real-time visualization of running containers, their resource usage, and health status.

17. **What is a Datadog notebook?**
A collaborative document combining graphs, markdown notes, and analysis for investigating incidents or trends.

18. **What is distributed tracing in Datadog APM?**
Tracking a single request as it flows through multiple microservices, visualized as a flame graph or trace timeline.

19. **What is the difference between a monitor and an alert in Datadog?**
A monitor is the configured rule/check; an alert (notification) is generated when the monitor's condition is triggered.

20. **What is Datadog's Watchdog feature?**
An AI-driven engine that automatically detects anomalies and performance issues without manual threshold configuration.

21. **What is the purpose of Datadog's Unified Service Tagging?**
Standardizes tagging (env, service, version) across metrics, traces, and logs for consistent correlation.

22. **What is a composite monitor in Datadog?**
A monitor combining the results of multiple other monitors using logical operators for advanced alerting logic.

23. **What is Datadog RUM (Real User Monitoring)?**
A feature that tracks real user interactions, page load times, and errors directly from browsers/mobile apps.

24. **What is the purpose of Datadog's Network Performance Monitoring?**
Provides visibility into network traffic flows between services, hosts, and availability zones.

25. **What is a Datadog API key vs Application key?**
API key authenticates data submission from agents/integrations; Application key is used for authenticated API requests tied to a specific user.

26. **What is the purpose of Datadog Log Exclusion Filters?**
Reduces log ingestion costs by filtering out unwanted or noisy log data before indexing.

27. **What is a Datadog notebook vs dashboard?**
Notebooks are for narrative-style investigation/analysis; dashboards are for continuous real-time monitoring views.

28. **What is Datadog's Security Monitoring feature?**
Detects threats and misconfigurations in real time by analyzing logs, cloud configurations, and workloads.

29. **What is the Datadog Cluster Agent used for in Kubernetes?**
A centralized component that reduces load on the API server by aggregating cluster-level metadata for the node-level agents.

30. **What is a Datadog span?**
A single unit of work within a distributed trace, representing an operation like a database query or HTTP call.

31. **What is the purpose of Datadog's Error Tracking?**
Automatically aggregates and prioritizes errors from logs and traces to help identify and fix issues faster.

32. **How does Datadog support anomaly detection?**
Using machine learning algorithms applied to metrics to flag unusual patterns without manual threshold setting.

33. **What is the difference between Datadog APM and Infrastructure Monitoring?**
APM focuses on application-level traces and performance; Infrastructure Monitoring focuses on host/container resource metrics.

34. **What is a Datadog integration tile?**
A pre-configured dashboard and metric set automatically provided when enabling an integration, like AWS or Docker.

35. **What is the purpose of the Datadog Trace ID?**
A unique identifier correlating all spans belonging to a single request across distributed services.

36. **What is Datadog's Continuous Profiler?**
A tool that provides code-level visibility into CPU and memory usage of running applications with minimal overhead.

37. **What is the purpose of Datadog Log-Based Metrics?**
Converts log data into custom metrics for trend analysis and alerting without needing full log indexing.

38. **How do you reduce Datadog costs?**
By using log exclusion filters, sampling traces, optimizing custom metric cardinality, and setting retention policies.

39. **What is the Datadog Events Explorer?**
A feature to search, filter, and correlate discrete events (deployments, alerts, config changes) across your systems.

40. **What is Datadog's Cloud Security Posture Management (CSPM)?**
Continuously scans cloud infrastructure configurations against security best practices and compliance frameworks.

41. **What is the purpose of Datadog Service Catalog?**
Provides a centralized inventory of services with ownership, dependencies, and health information.

42. **How does Datadog integrate with CI/CD pipelines?**
Through CI Visibility, tracking pipeline execution, test performance, and failures across Jenkins, GitHub Actions, etc.

43. **What is Datadog's Database Monitoring feature?**
Provides deep visibility into query performance, execution plans, and resource usage for databases like PostgreSQL and MySQL.

44. **What is the purpose of multi-step API tests in Synthetic Monitoring?**
Simulates a sequence of API calls to validate complex workflows and dependencies between endpoints.

45. **What is a Datadog notebook cell?**
An individual block within a notebook that can contain a graph, markdown text, or log query.

46. **How does Datadog handle high-cardinality metrics?**
Through careful tag management and features like Log-Based Metrics to avoid excessive billing and performance issues.

47. **What is the purpose of Datadog's Incident Management feature?**
Helps teams declare, track, and resolve incidents with integrated timelines, postmortems, and notifications.

48. **What is the difference between Datadog and CloudWatch?**
Datadog is a unified, multi-cloud observability platform with richer APM/UX; CloudWatch is AWS-native and tightly integrated with AWS services only.

49. **What is a Datadog downtime/mute setting?**
Temporarily suppresses alert notifications for a monitor during planned maintenance or known issues.

50. **What are best practices for using Datadog effectively?**
Use consistent unified tagging, set meaningful SLOs, control log/metric cardinality for cost, and leverage dashboards/notebooks for team visibility.

---

**Total: 400 Questions & Answers across 8 DevOps/Cloud tools.**
