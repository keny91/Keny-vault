
### Requirements

python

ansible

jenkins

altered 8080 to -> 8081

fail2ban
	avoid brute force attacks

nginx
	|External Port|Internal Port|Protocol|Notes|
|---|---|---|---|
|8081|81|TCP|For HTTP (optional, only if using Let’s Encrypt via port 80 challenge)|
|8443|443|TCP|For HTTPS to NGINX/Jenkins|


Confirm port listening:
sudo ss -tulnp | grep 8081


Monit


##### sudo nano /etc/monit/monitrc

check process sshd with pidfile /run/sshd.pid
  start program = "/bin/systemctl start ssh"
  stop program  = "/bin/systemctl stop ssh"
  if 3 restarts within 5 cycles then exec "/sbin/reboot"
