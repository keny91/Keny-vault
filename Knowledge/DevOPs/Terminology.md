#devops 

## 🛠️ **Core DevOps Terminology**

### 🔁 **CI/CD (Continuous Integration / Continuous Delivery or Deployment)**

|Term|Meaning|
|---|---|
|**CI (Continuous Integration)**|Automatically building and testing code whenever it's pushed (e.g. GitHub Actions, Jenkins).|
|**CD (Continuous Delivery)**|Automating release-ready builds; code can be deployed at any time with confidence.|
|**CD (Continuous Deployment)**|Every code change is automatically deployed to production once it passes tests.|
|**Pipeline**|A defined series of steps to build, test, and deploy an application.|
|**Artifact**|The result of a build process, like a `.jar`, `.tar.gz`, or Docker image.|

### 🔧 **Infrastructure as Code (IaC)**

|Term|Meaning|
|---|---|
|**Terraform**|Declarative tool for provisioning infrastructure across cloud providers (AWS, GCP, Azure).|
|**Ansible**|Configuration management and automation tool using YAML playbooks.|
|**CloudFormation**|AWS-specific IaC tool for defining infrastructure via templates.|
|**State File**|Used by tools like Terraform to track the deployed infrastructure state.|

## ☁️ **Cloud & Containerization**

### ☁️ **Cloud Computing Concepts**

|Term|Meaning|
|---|---|
|**IaaS (Infrastructure as a Service)**|Raw compute, storage, and network resources (e.g. EC2, GCP Compute Engine).|
|**PaaS (Platform as a Service)**|Abstracts server management; you deploy apps only (e.g. Heroku, AWS Elastic Beanstalk).|
|**SaaS (Software as a Service)**|Web-based apps you just use (e.g. Gmail, Slack).|
|**VPC (Virtual Private Cloud)**|A logically isolated section of the cloud for your infrastructure.|
|**Load Balancer**|Distributes incoming traffic across multiple servers.|
|**Auto-scaling**|Dynamically adds/removes servers based on load.|

### 🐳 **Containers & Orchestration**

|Term|Meaning|
|---|---|
|**Docker**|Platform for creating and running containers (lightweight, portable environments).|
|**Dockerfile**|Script to build Docker images.|
|**Image**|A snapshot of your app and its environment.|
|**Container**|A running instance of an image.|
|**Kubernetes (K8s)**|A container orchestration platform to manage containerized apps at scale.|
|**Pod**|The smallest deployable unit in Kubernetes (usually one container).|
|**Helm**|A package manager for Kubernetes (like `apt` or `brew`).|

## 🔒 **Security & Secrets**

|Term|Meaning|
|---|---|
|**Secrets Management**|Tools to store/manage credentials securely (e.g. Vault, AWS Secrets Manager).|
|**Least Privilege**|Users/services only get permissions they _need_, and no more.|
|**IAM (Identity and Access Management)**|Cloud-based permission system to manage who can do what.|
|**SSL/TLS**|Encryption for secure communication (HTTPS).|

#monitoring
## 📊 **Monitoring, Logging, Observability**

| Term              | Meaning                                                                              |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Logging**       | Capturing logs from apps and infrastructure (e.g. via Fluentd, Logstash).            |
| **Monitoring**    | Tracking metrics like CPU, memory, request rate (e.g. Prometheus, CloudWatch).       |
| **Alerting**      | Notifications based on metrics or logs (e.g. via Grafana, PagerDuty).                |
| **Tracing**       | Following a request as it travels across microservices (e.g. Jaeger, OpenTelemetry). |
| **Observability** | Holistic view of your system using logs + metrics + traces.                          |

#Testing 
## 🧪 **Testing & Automation**

| Term                 | Meaning                                                       |
| -------------------- | ------------------------------------------------------------- |
| **Unit Test**        | Tests a single function or module.                            |
| **Integration Test** | Tests components working together (e.g. app and DB).          |
| **Smoke Test**       | Basic check to verify system is working after deployment.     |
| **Linting**          | Static analysis to catch code issues before running it.       |
| **Pre-Commit Hooks** | Scripts that run before a Git commit (e.g. check formatting). |

## 🧰 **Version Control & Collaboration**

|Term|Meaning|
|---|---|
|**Git**|Distributed version control system.|
|**Branch**|A separate line of development (e.g. `main`, `feature/xyz`).|
|**Pull Request (PR)**|A request to merge code into another branch, with review.|
|**Merge Conflict**|When changes from two branches conflict.|
|**GitOps**|Managing infrastructure/deployments through Git (e.g. ArgoCD).|

## 🧠 Bonus Concepts Worth Knowing

| Concept                      | Use                                                             |
| ---------------------------- | --------------------------------------------------------------- |
| **Blue/Green Deployment**    | Deploy a new version in parallel, switch traffic when ready.    |
| **Canary Release**           | Deploy to a small % of users before full rollout.               |
| **Immutable Infrastructure** | Replace servers instead of patching them in place.              |
| **Service Mesh**             | Manages service-to-service communication (e.g. Istio, Linkerd). |
| **Feature Flags**            | Toggle app features without deploying new code.                 |
| **Rollback**                 | Revert to a known good state after a failed deployment.         |