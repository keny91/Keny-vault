#todo #bootstrap


## 🔧 What Is a "Bootstrap" Playbook?

**"Bootstrapping"** means bringing a system **from nothing to something functional.**

In Ansible (or any automation tool), a **bootstrap playbook** is typically used to:

| Step  | Purpose                                                               |
| ----- | --------------------------------------------------------------------- |
| 🧼 1. | Prepare a fresh or newly imaged system                                |
| 🔐 2. | Set up SSH keys and disable password logins                           |
| 👤 3. | Create or configure the admin user                                    |
| 🐧 4. | Set hostname, timezone, locales                                       |
| 📦 5. | Install required packages (e.g. Python, Docker, Git)                  |
| 🧩 6. | Add the node to your orchestrator’s `/etc/hosts`, DNS or mesh network |
| 🔁 7. | Reboot or reconnect if necessary                                      |


## 🧠 Why the Name “Bootstrap”?

It comes from the expression **"pulling oneself up by one's bootstraps"** — doing something self-starting with minimal initial help.

In computing:

- A bootstrap process is what initializes a system (e.g. BIOS → bootloader → kernel)
    
- In DevOps, it’s your **first automation** run on a new host to make it manageable
    

---

## ✅ Expected Function of _Your_ Bootstrap Playbook

For your home lab setup, the `bootstrap.yml` playbook might:

1. Ensure your `keny` user exists and has passwordless `sudo`
    
2. Set the hostname and timezone
    
3. Configure `/etc/hosts` with local DNS entries
    
4. Install packages like:
    
    - `openssh-server`
        
    - `python3`
        
    - `git`
        
    - `docker.io` or `docker-ce`
        
5. Add SSH public keys (maybe from a shared repo or local file)
    
6. Setup systemd-resolved or mDNS for internal hostnames
    
7. Optionally, reboot if needed
## 💡 Summary

| Term                   | Meaning                                                                  |
| ---------------------- | ------------------------------------------------------------------------ |
| **Bootstrap playbook** | A minimal setup script to get a fresh machine ready to be managed        |
| **When to run it**     | On new hosts, VMs, containers, or machines you’re adding to your fleet   |
| **Why**                | To automate the boring and risky first-time setup, safely and repeatably |