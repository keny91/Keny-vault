#todo #jenkins 



JENKINS REQUIRED AN INITIAL "INSTALLATION PASSWORD TO SET UP"

```
sudo dpkg -i openjdk-17*.deb
sudo apt -f install   # to fix dependencies
```


#TODO WHAT IS A GROOVY script
in the GROOVY script (default is `~/.jenkins`):
	hudsonRealm.createAccount("admin", "changeme123")


THE GROOBY SCRIPT & FOLDER MUST BE IN THE DEFAULT JENKINS HOME (/var/lib/jenkins/). Find a way to determine it otherwise. (At least when installed from package)



FIRST TIME INSTALL BY HAND. 

SECOND PREPARE THE THEORICAL PACKAGES TO BE AUTODEPLOYED WITH ANSIBLE

THE PACKAGE SHOULD BE AN ANSIBLE INSTALLER? LIKE GMV? A WORKER SHOULD BUILD IT

CHICKEN OR THE EGG FIRST? LETS CREATE A CHICKEN THEN LAY EGGS for more chicken

### Journal



Downloaded packages:

#### **[plugin-installation-manager-tool](https://github.com/jenkinsci/plugin-installation-manager-tool)**

LINK: https://github.com/jenkinsci/plugin-installation-manager-tool?tab=readme-ov-file
Requires **Java & mvn**

```
# to find about which are plugins are supported 
unzip -p jenkins.war META-INF/MANIFEST.MF | grep Jenkins-Version
```

Downloaded plugins.txt, 

```
## plugins.txt
git:4.15.0
pipeline-model-definition:1.11.5
pipeline-stage-view:2.25
configuration-as-code:1.72
blueocean:1.27.4
workflow-aggregator:2.7
job-dsl:1.85
mailer:1.34
credentials-binding:1.26

### The previous did not work, leaving the version automatically filled them 
git
pipeline-model-definition
pipeline-stage-view
configuration-as-code
blueocean
workflow-aggregator
job-dsl
mailer
credentials-binding

```

**Top pick for offline practice:**

- **Git Plugin** — essential for SCM integration.
    
- **Pipeline: Multibranch / Pipeline Model / Stage View** — build powerful pipeline scripts.
    
- **Configuration as Code (JCasC)** — define your entire Jenkins configuration in YAML.
    
- **Job DSL** — automate job creation via scripts.
    
- **Blue Ocean** — modern UI to visualize pipelines.
    
- **SonarQube / Artifactory** — simulate quality and artifact steps.
    
- **Slack or Email (Mailer) Plugins** — for notifications.

Also original repository was not available so we used a different one:

```
- [https://get.jenkins.io](https://get.jenkins.io)
    
- https://mirror.xmission.com/jenkins/
    
- https://ftp-chi.osuosl.org/pub/jenkins/
```

Downloaded .war for jenkins (this determines the version of the plugins version)

The **`jenkins.war`** is the main Jenkins application archive — it contains all the core Jenkins code and is what gets launched by Java when Jenkins starts.

I downloaded a the war file WHICH SHOULD MATCH THE ONE WE GET WHEN WE INSTALL the .deb:

```
# should be here once installed:
/usr/share/jenkins/jenkins.war
```

Command for jenkins plugin manager:

```
java -jar jenkins-plugin-manager-*.jar --war ./jenkins.war --plugin-download-directory ./local_plugins/ --plugin-file ./plugins.txt --plugins delivery-pipeline-plugin:1.3.2 deployit-plugin --jenkins-update-center https://mirror.xmission.com/jenkins/
```




## **2. Configure Before First Start**

Jenkins loads most settings from:

- **`/var/lib/jenkins/config.xml`** — core settings (port, security, etc.)
    
- **`/var/lib/jenkins/users/`** — per-user configs
    
- **`/var/lib/jenkins/credentials.xml`** — stored credentials (you can preseed defaults)
    
- **`/var/lib/jenkins/jobs/<jobname>/config.xml`** — job definitions
    
- **`init.groovy.d/*.groovy`** — scripts run _before_ Jenkins starts for the first time



The groovy script:
mkdir -p /var/jenkins_home/init.groovy.d


```
#!groovy

import jenkins.model.*
import hudson.security.*

def instance = Jenkins.getInstance()

println "--> creating local admin user"

def hudsonRealm = new HudsonPrivateSecurityRealm(false)
hudsonRealm.createAccount("admin", "changeme123")  // username, password
instance.setSecurityRealm(hudsonRealm)

def strategy = new FullControlOnceLoggedInAuthorizationStrategy()
strategy.setAllowAnonymousRead(false)
instance.setAuthorizationStrategy(strategy)

instance.save()
```


Set up (offline):

```
sudo mkdir -p /opt/jenkins
sudo mv jenkins.war /opt/jenkins/


sudo mkdir /var/jenkins_home
sudo chown -R $USER:$USER /var/jenkins_home
(or change `$USER` to the one running Jenkins)


mkdir -p /var/jenkins_home/init.groovy.d
```

nano /var/jenkins_home/init.groovy.d/basic-security.groovy   :
content:
```
#!groovy
import jenkins.model.*
import hudson.security.*

def instance = Jenkins.getInstance()

println "--> Creating default admin user"

def hudsonRealm = new HudsonPrivateSecurityRealm(false)
hudsonRealm.createAccount("admin", "admin123")
instance.setSecurityRealm(hudsonRealm)

def strategy = new FullControlOnceLoggedInAuthorizationStrategy()
strategy.setAllowAnonymousRead(false)
instance.setAuthorizationStrategy(strategy)

instance.save()
```


POSSIBLE LAUNCH OF JENKINS:
From the folder containing `jenkins.war`:
```
java -jar jenkins.war --httpPort=8080 --httpListenAddress=0.0.0.0 --prefix=/jenkins --enable-future-java
```

Now it will:

- Start on port `8080`
    
- Use `/jenkins` as the base URL path
    
- Create user **admin** with password **admin123** automatically.


If you have `.hpi` plugin files, place them into /var/jenkins_home/plugins/:

```
cp /path/to/plugin.hpi /var/jenkins_home/plugins/
pkill -f jenkins.war
java -jar jenkins.war --httpPort=8080
```


### AS A ROLE:

```
roles/
└── jenkins_offline/
    ├── files/
    │   └── packages/
    │       ├── openjdk-17-jre.deb
    │       ├── jenkins.war
    │       └── plugins/
    │           ├── git.hpi
    │           ├── workflow-aggregator.hpi
    │           └── blueocean.hpi
    ├── tasks/
    │   └── main.yml
    ├── templates/
    │   └── basic-security.groovy.j2
    └── defaults/
        └── main.yml
```



once Jenkins has applied your `init.groovy.d` setup (e.g., created the admin user), you are free — and actually _encouraged_ — to remove those Groovy init scripts.

```
sudo rm -f /var/lib/jenkins/init.groovy.d/01-create-admin.groovy
sudo systemctl restart jenkins
```

