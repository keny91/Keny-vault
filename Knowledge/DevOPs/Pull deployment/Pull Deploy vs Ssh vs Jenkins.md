#jenkins #deployment #pull-deploy

At minimum, the machine needs:

- Git client installed
    
- Ansible installed
    
- Internet access to pull from the Git repo
    
- A cron job or systemd timer running `ansible-pull`
    

---

### 🧰 Common Bootstrapping Methods

#### 1. **Golden Image or Template**

Most common in real deployments.

- You prepare a base image (for VM, Pi, or cloud instance) with everything preinstalled (Ansible, crontab, pull script).
    
- On first boot, it auto-runs `ansible-pull`.
    
- Ideal for scaling and auto-replacement.
    

#### 2. **Cloud-init / Ignition (Cloud / CoreOS)**

If you're in cloud or using tools like cloud-init:

- You can auto-run setup scripts on first boot.
    
- It’s like embedding the pull setup in your launch metadata.
    

#### 3. **Initial SSH Access (one-time)**

- For existing systems, you might do an SSH push just once to:
    
    - Install Ansible
        
    - Set up the pull cronjob
        
    - Lock down SSH after that if you wish
        

---

### 🔐 SSH vs Jenkins vs Pull

#### ❌ If SSH is disabled

- Jenkins **cannot push jobs or run scripts** directly on the machine.
    
- But Jenkins **can commit changes to Git** — and the target node will pick them up on next pull cycle.
    
    - This is exactly how **GitOps** works.
        

#### ✅ If SSH is allowed **only temporarily** or **internally**

- You can use SSH from Jenkins to bootstrap once.
    
- After that, pull model kicks in — Jenkins only needs to update Git.

### ✅ Summary

|Method|Use Case|
|---|---|
|Golden image|Repeating many similar systems (VMs, containers, Pi)|
|SSH once then pull|Safe for environments with trusted setup windows|
|No SSH ever|Combine GitOps with pull, Jenkins updates Git only|
|Still want SSH|Pull model + SSH for manual override/debugging|

