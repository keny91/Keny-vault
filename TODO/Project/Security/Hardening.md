#security #hardening 

## 🛡️ Security & Hardening Roadmap (Ideas for Later)

|Layer|Hardening Options|
|---|---|
|SSH|Disable password login, rate-limit, fail2ban, only key-based, separate port|
|Users|No sudo for customer, sudo restrictions for maintenance|
|File System|Immutable root parts, `chattr +i`, read-only rootfs where possible|
|Docker|Run as non-root, use rootless containers if possible|
|Backdoor|Use Tailscale auth or certificate-based validation|
|Services|Use systemd sandboxing, capabilities dropping (`NoNewPrivileges=yes`)|
|Monitoring|Audit logs, shell history (remote-synced), cron job alerts|
|OTA Updates|Signed update packages or verified deployment channel|
|Emergency Access|Physical switch or hidden mechanism to allow reset/debug|
