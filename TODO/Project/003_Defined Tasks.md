#todo #tasks


### MVP PHASE:

#### FRONT-END

### **Phase 1 – Core Access & Structure**

1. **Improve login UI** (responsive layout, error messages, loading states).
    
2. **Protect routes** — prevent dashboard access without authentication.
    
3. **Add logout button** with session/token cleanup.
    
4. **Store auth token securely** (memory or `httpOnly` cookie).
    
5. **Main layout** — sidebar/menu for navigation, top bar for user info.
    

---

### **Phase 2 – Device Visibility**

6. **Devices page** — list connected devices (name, IP, status).
    
7. **Connect to backend API** for fetching devices.
    
8. **Loading indicators** while fetching device data.
    
9. **Error handling** if backend is down or returns an error.
    

---

### **Phase 3 – Service Control**

10. **Services page** — list available services (Pi-hole, WireGuard, Home Assistant).
    
11. **Connect to backend API** for fetching services.
    
12. **Service control UI** — install/start/stop/uninstall buttons.
    
13. **Install service dialog** — select device, choose service, confirm install.
    

---

### **Phase 4 – Interaction & Feedback**

14. **Auto-refresh** devices/services every 10 seconds.
    
15. **Show install progress** (progress bar or logs).
    
16. **Post-install summary** with success/fail status.
    

---

### **Phase 5 – Enhancements & QoL**

17. **Add device form** — manually add a device (IP, hostname).
    
18. **Remove device** from the orchestrator.
    
19. **Show device details** (OS, architecture, uptime, CPU, RAM).
    
20. **Responsive design** for mobile & desktop.
    
21. **Environment variables** for API base URL.
    
22. **Linting & formatting** setup (ESLint + Prettier).
    
    -------


    #### BACK-END

Auth & Security

- Implement login endpoint (JWT or session-based)
    
- Store passwords securely (bcrypt hashing)
    
- Add token validation middleware
    
- Implement logout and token invalidation
    

Device API

- List devices
    
- Add device (register to orchestrator)
    
- Remove device
    
- Get device details (OS, arch, uptime, CPU, RAM)
    
- Device health check
    

Service API

- List available services
    
- Get service status for a device
    
- Install service (trigger infrastructure task)
    
- Start/stop/uninstall service
    
- Service install progress
    

Server Setup

- Configure CORS for React
    
- Use .env for secrets and settings
    
- Add logging and error handling middleware
    
- Enable API documentation with OpenAPI (/docs)
  
  
### INFRASTRUCTURE

Core Orchestration

- Create Ansible playbooks for each service (Pi-hole, WireGuard, Home Assistant)
    
- Create device onboarding script (hostname, static IP, monitoring agent)
    
- Service management scripts (install/start/stop/uninstall)
    

Background Processing

- Background job runner (Celery or APScheduler)
    
- Task status tracking (logs/progress in DB or file)
    

Monitoring & Health

- Install Prometheus Node Exporter on devices
    
- Install cAdvisor for container monitoring
    
- API or data pipeline to expose metrics to backend
    

Security & Maintenance

- Implement Fail2ban and SSH hardening role (Ansible)
    
- Define remote recovery strategy (e.g., flashable image from stored config)