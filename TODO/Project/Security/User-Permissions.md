#security #users 

## 🧭 Context Clarification (your goal)

You’re building a **hardware + software product** that runs on Raspberry Pis deployed at **customer premises**, **outside your LAN**, and accessible for orchestration, maintenance, and service delivery.

- These Raspberry Pis (workers) will be **pre-configured** by your orchestrator.
    
- Devices must support **remote management by you** (secure backdoor access).
    
- Customers may **interact with the device**, either through a web interface, local CLI, or API.
    
- Devices may run **services like Pi-hole, WireGuard, DuckDNS, Home Assistant**, which may expose ports or UIs.
    

Let’s explore the **user roles**, **access privileges**, **ownership**, and **hardening possibilities**.

---

## 👥 User Roles and Accounts

|User|Purpose|Where|Access|Notes|
|---|---|---|---|---|
|`orchestrator-admin`|**You**, for provisioning and managing devices|Orchestrator + all remote Pis|Full root/admin via Ansible/SSH (via Tailscale or exposed DNS+TLS)|Secure access required (SSH key, IP restriction, MFA later)|
|`device-maintenance`|**Backdoor user** for emergency debugging/upgrades|All Pis|SSH (restricted), sudo access, maybe Ansible access|Hidden or hardened (e.g., disabled by default or rate-limited)|
|`customer` or `piuser`|Customer-facing account (optional)|Raspberry Pi sold as product|Web access only, or CLI with limited rights|Should never have sudo by default unless part of product design|
|`container-user`|Runs Docker/Kubernetes services|Raspberry Pi only|No login; used for isolation (e.g., `docker` group or custom UID)|Least privilege; no shell access|
|`www-data` or `fastapi-user`|Web app interface user (React + FastAPI)|Raspberry Pi|No login; runs backend/frontend apps|Runs with app-specific permissions only|

## 🔐 Access Control Strategy

### 1. **SSH Access**

- **Only you** should have SSH access to customer devices.
    
- Use **Tailscale** or DNS+TLS for device discovery and authentication.
    
- Configure **allowlist of public SSH keys**, no password login.
    
- Optionally hide/disable SSH by default unless recovery is needed.
    

### 2. **Sudo + Root**

- `orchestrator-admin` has full sudo/root for Ansible provisioning.
    
- `device-maintenance` may have sudo, but:
    
    - Can be restricted to specific commands (`/etc/sudoers.d/maintenance`)
        
    - Can be rate-limited or triggered via physical button or signed request
        

### 3. **Customer Access**

- No shell access by default.
    
- Web UI login tied to internal user system, not Linux users.
    
- Limited to managing services (via FastAPI), not system-level control.


## 📁 Folder Ownership & Permissions

Here’s a common and clean pattern:

```
/opt/myproduct/                # Main product directory
├── backend/                   # FastAPI backend
├── frontend/                  # React static files
├── services/                  # Docker compose files or configs
├── logs/                      # Logs (customer-viewable)
├── internal/                  # Sensitive scripts, only for you
└── updates/                   # OTA or config updates

/var/lib/myproduct/            # Persistent data volumes
/etc/myproduct/                # Config files

```


|Path|Owner|Permissions|Description|
|---|---|---|---|
|`/opt/myproduct/*`|`fastapi-user` or root|`750` or `700`|Codebase and configs|
|`/opt/myproduct/logs/`|`fastapi-user`|`755`|Exposed via UI|
|`/opt/myproduct/internal/`|root|`700`|Only you via SSH|
|`/var/lib/myproduct/`|docker / root|`750`|Persistent container data|
|`/etc/myproduct/`|root|`600`|Configs|
|`~/.ssh/authorized_keys`|root / backdoor user|`600`|Limited to your key|

## 🤖 What You Control vs What They Control

| Aspect             | You                          | Customer                              |
| ------------------ | ---------------------------- | ------------------------------------- |
| System packages    | ✅ (via Ansible)              | ❌                                     |
| SSH keys           | ✅                            | ❌                                     |
| Installed services | ✅ (you define product image) | ❌ (unless sandboxed apps are offered) |
| Web UI content     | ✅                            | Partial (depending on config exposed) |
| Docker services    | ✅                            | ❌                                     |
| Logs / Status      | ✅                            | ✅ (filtered)                          |
| Reflashing or OTA  | ✅                            | ❌                                     |