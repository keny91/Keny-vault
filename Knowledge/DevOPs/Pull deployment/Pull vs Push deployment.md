#devops #deployment

### ✅ What is a Pull-Based Deployment?

In a **pull model**, the _target system_ initiates the deployment by regularly (or on-demand) pulling its configuration, scripts, or container definitions from a **central source** (e.g., Git repository, object storage, config server). This contrasts with a **push model**, where a central orchestrator pushes updates to the target over SSH or an API.

### 🚦 Pull vs Push at a Glance

|Feature|Push (e.g., `ansible`, `ssh`)|Pull (e.g., `ansible-pull`, GitOps)|
|---|---|---|
|**Initiator**|Central orchestrator|Target node|
|**Connectivity**|Orchestrator must reach target (SSH, etc.)|Target pulls config (often via HTTPS/Git)|
|**Firewall-friendly**|❌ Often needs open SSH ports|✅ Can use outbound-only HTTPS|
|**Security model**|Keys on orchestrator|Secrets/config on the node or encrypted in Git|
|**Scalability**|Harder as infra grows|Scales easily — targets act independently|
|**Observability**|Centralized control/logs|Decentralized unless logs pushed back|
|**Resilience**|Central failure halts deployments|Nodes can still self-heal/pull if infra fails|

### 🔐 Why Some Consider Pull More Secure

1. **No SSH exposure**: You don’t need to expose SSH access to your nodes or rotate keys for all machines. Less attack surface.
    
2. **One-way connection**: Nodes only make outbound requests (usually HTTPS) to a trusted source — easier to firewall and monitor.
    
3. **Immutable or signed state**: If using GitOps (e.g., FluxCD), only signed or verified commits get deployed. Every change is traceable.
    
4. **Tamper detection**: With tools like **sops**, **age**, or **GPG**, secrets can be encrypted and version-controlled — and tampering is visible.
    

---

### 🔧 How Pull-Based Systems Work

#### 1. **Ansible-pull**

```
ansible-pull -U https://git.example.com/configs.git playbook.yml
```


You can set this up in a cron job or systemd timer. Each node fetches its config from Git and applies it locally.

#### 2. **GitOps (e.g., ArgoCD / FluxCD)**

Used in Kubernetes: the cluster continuously syncs its state from Git. This ensures Git is the "single source of truth" and drift is corrected automatically.

#### 3. **Puppet agent**

Puppet clients (agents) pull their desired state from a Puppet Master at intervals (every 30 mins by default).



### !!!! The machine must be "bootstrapped" for the pull model.

At minimum, the machine needs:

- Git client installed
    
- Ansible installed
    
- Internet access to pull from the Git repo
    
- A cron job or systemd timer running `ansible-pull`
  
  
### Know machines and nodes active in your deployment


**It’s both normal and _recommended_** that pull-based machines **register themselves** with some **orchestrator, inventory server, or monitoring system** during or after bootstrapping.

This is how systems stay **visible**, **manageable**, and **accountable** in larger infrastructures — even when they're acting autonomously.

---

### 🧭 Common Registration Practices

#### 🔹 1. **Call Home ("Phone Home")**

On first boot or after setup, the machine:

- Sends a request to a central endpoint (e.g., webhook, API)
    
- Includes metadata (hostname, IP, tags, SSH keys, etc.)
    
- Gets added to an inventory or dashboard
    

Example:

```
curl -X POST https://orchestrator.example.com/register \
     -d "hostname=myhost&ip=192.168.1.10&env=prod"
```


> 📦 This is how many IoT devices and appliances register themselves.

---

#### 🔹 2. **Dynamic CMDB (Config Management DB)**

If you use tools like:

- **Rudder**, **Foreman**, **NetBox**, **Collins**
    
- **PuppetDB** (for Puppet)
    
- **Consul** (for service registration)
    
- **Tailscale** or **Zerotier** (for overlay networks)
    

Machines can register dynamically and be queried later via API or UI.

---

#### 🔹 3. **GitOps Self-Registration**

In GitOps workflows (e.g., Flux or ArgoCD):

- A machine writes a file (e.g., `nodes/myhost.yaml`) into a Git repo.
    
- A central system watches the repo and updates its inventory.
    

Example:

```
# nodes/raspi01.yaml
hostname: raspi01
ip: 10.0.1.11
role: edge-node
```

#### 🔹 4. **Monitoring/Logging Auto-Registration**

Using agents like:

- **Prometheus Node Exporter**
    
- **Telegraf**
    
- **Vector.dev**
    
- **Zabbix agent**
    
- **Tailscale MagicDNS + tags**
    

The node connects to a central system and automatically appears in dashboards. Sometimes this is done via **service discovery**.


---

#### 🔹 5. **Custom Inventory Reporting**

Your `ansible-pull` run itself can:

- Register the machine by sending a webhook
    
- Upload inventory facts to a server
    
- Tag itself in GitLab CI, a Jenkins job, or a CMDB
    

---

### 🚨 Security Considerations

Machines that self-register must be:

- **Authenticated** (e.g., token-based, pre-shared secrets, client certs)
    
- **Authorized** to register only themselves (not impersonate others)
    
- Often **scoped by environment or network boundaries**

### 🧪 Summary: Common Registration Mechanisms

|Type|Example Tools|Trigger|
|---|---|---|
|Call home script|`curl`, `wget`, `POST`|On first boot|
|GitOps file creation|Commit to `inventory.git`|During pull|
|Monitoring agent|Prometheus Node Exporter, Telegraf|On agent start|
|Service registration|Consul, Tailscale, NetBox|Via agent or init|
|CMDB reporting|Custom script, API client|During config|


