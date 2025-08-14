#AUTOMATION #jenkins #git_actions

## **1. Popular free CI/CD tools**

These are widely used, easy to find documentation for, and integrate with many platforms:

|Tool|Hosted?|Self-hosted?|Pros|Cons|
|---|---|---|---|---|
|**Jenkins**|No (self-host only)|✅|Huge plugin ecosystem, flexible, battle-tested, runs anywhere|Plugin bloat, upgrades can be risky, governance issues if many jobs are owned by different teams|
|**GitHub Actions**|✅ (free tier)|Partial (via runners)|Integrated with GitHub, YAML-based, strong community|Tied to GitHub, free tier limited by minutes/storage|
|**GitLab CI/CD**|✅ (with GitLab.com)|✅ (with self-managed GitLab)|First-class CI/CD integration, great for DevOps pipelines|Requires GitLab repo or extra setup|
|**CircleCI**|✅|❌|Easy to set up, good cloud integrations|Limited free plan, proprietary|
|**Azure Pipelines**|✅|❌|Works with any repo, free minutes for public projects|Tied to Azure DevOps ecosystem|

## 2. Self-hosted, open-source alternatives
If you want control, privacy, and no SaaS lock-in, these are strong candidates: Tool Key Features Why choose 

|Tool|Key Features|Why choose over Jenkins?|
|---|---|---|
|**Drone CI**|Container-native, YAML pipelines, integrates with GitHub/GitLab|Lightweight, less plugin overhead|
|**Woodpecker CI**|Drone fork, minimal deps, fast|Same as Drone but more community-driven|
|**Concourse CI**|Task-based, reproducible builds, stateless workers|Strong for highly repeatable, isolated builds|
|**Tekton Pipelines**|Kubernetes-native CI/CD|If your infra is K8s-heavy|
|**Buildbot**|Python-based, highly customizable|Flexible but more DIY effort|
|**GoCD**|Value stream mapping, good for complex workflows|Better visualization of multi-step pipelines|

## **3. More obscure / niche options**

These can be interesting if you want something **lightweight or experimental**:

- **Taskcluster** (Mozilla) – designed for massive distributed workloads
    
- **Laminar** – minimal CI server, no database, single binary
    
- **Bors-NG** – focused on merge queue automation (used by Rust community)
    
- **SourceHut Builds** – extremely minimal, text-based configs, fits UNIX philosophy
    
- **Jenkins X** – GitOps-focused, Kubernetes-native rewrite of Jenkins (often misunderstood as “Jenkins with plugins”)

## **4. Why Jenkins has a “governability” bad rep**

From experience, here’s why Jenkins gets nightmare stories:

1. **Plugin chaos** – Every team installs their own, versions drift, upgrades break things.
    
2. **Job sprawl** – Hundreds of freestyle jobs with no documentation. No standard templates.
    
3. **Shared state** – Jenkins master often has shared files/secrets that make jobs non-portable.
    
4. **No enforced code review** – People click buttons in UI to change jobs, bypassing version control.
    
5. **Single point of failure** – If the Jenkins master dies, pipelines halt (unless you cluster it).
    

💡 **Governability best practices if you stick with Jenkins**:

- Use **Jenkinsfile** in repo (pipeline as code)
- Maintain a **plugin allowlist** and central upgrade policy
- Use **folders + RBAC** for team separation
- Store configs in Git and restore from code
- Have a test/staging Jenkins instance for upgrades
  
  
  If your goal is **a base CI/CD stack with tests** and you want something:

- **Fast to set up** → GitHub Actions (if using GitHub) or Drone CI
    
- **Governable long term** → GitLab CI/CD or Tekton
    
- **Experimental but scalable** → Jenkins X or Concourse