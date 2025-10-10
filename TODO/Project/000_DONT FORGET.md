


Jenkins - packag pluggins as "files/jenkins/plugins/jenkins-plugins*.tar.gz"



LAST




- Bootstrap: 
	- create user:group
	- Install ansible
	- Install docker and k8s
	- Validate packages have been installed

- Ansible y kubernetes. 
  Determinar como guarlo las librerias. /cots/Linux/Distro/LIBxxXXX.xx
	Tools...


Instanciated at orchestrator_new.  /home/keny/data/  -> to be moved to a mounted drive (keep a local copy)

- Create storage:
  /mnt/data
  |
  | jenkins
  |    |   Plugins (Separate or label, orchestrator, agents...)
  |    |   Jobs
  |
  | - PACKAGES 
  |         |  Orchestrator Installer
  |         |  AgentInstaller
  |         |  ...
  |         |  
  |     
  |    | COTS
  |    |     |    LINUX/UBUNTU22.04/arm64/...
  |
  |
  

- Install ansible offline:

```
###UBUNTU
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```


```

```
- In front/back end expected port to connect is 5173. This should be part of config

- Ensure a newer version of nodejs/npm is installed
  (Install nvm which manages NODEJS)

- roles/docker/tasks/main.yml -> CONTENT INCORRECT

- In my creator machine I initialized the future Deploy BY PULL  repo. (Init, no origin)

- REMEMBER TO CHECK FOR "TODO" in code
  
  
  LAUCH FRONT
  npm run dev

  LAUNCH BACKEND 
  uvicorn main:app --reload