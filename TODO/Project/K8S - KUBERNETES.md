#K8S #kubernetes 



dpkg: error processing package kubeadm (--install):
 dependency problems - leaving unconfigured
Setting up kubectl (1.33.4-1.1) ...
dpkg: dependency problems prevent configuration of kubelet:
 kubelet depends on kubernetes-cni (>= 1.2.0); however:
  Package kubernetes-cni is not installed.
 kubelet depends on conntrack; however:
  Package conntrack is not installed.
 kubelet depends on ethtool; however:
  Package ethtool is not installed.


To dowload the packages I used:

#### IMPORTANT! PACKAGES ARE DOWNLOADED TO BE COMPATIBLE TO THE ORIGINAL MACHINE (ARM/ARCH OR x86_64)

```
# For Kubernetes on Debian-based systems: # Method 1: Use the .deb packages I 
# mentioned earlier 


curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update

apt download kubeadm kubelet kubectl
```


