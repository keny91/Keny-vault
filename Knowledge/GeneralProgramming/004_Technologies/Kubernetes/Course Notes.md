
#kubernetes #k8s

### NODE

A node is a physical or virtual machine in which Kubernetes runs. An application

****

### CLUSTER

Set of nodes grouped together. This is shares load and acts as a failsafe in case a node fails.


The information/monitor/failsafe (basically what it means to orchestrate) is controlled by the master and is responsible for the orchestration of the worker nodes.

****

### COMPONENTS

On installation, the following components will be installed.

* **API SERVER:**  the front end for Kubernetes. The user must interact with this component to manage the cluster. Runs in the master.

* **etcd keystore:** a service of Key-value storage. Contains the information of all nodes, clusters and masters in a distributed manner. Also implements logs within the cluster

* **Kubelet**: agent that runs in each node in the cluster. It checks that the process is running as expected.

* **Container Runtime**: underlying software to run containers (docker)

* **Controller:** brain behind orchestrations. Responds when container go down and made decisions to bring up new containers given the situation.

* **Scheduler:**  is responsible for distributing work and containers in Nodes. It looks for newly created containers and assigns them to Nodes.

****

### PODs

A capsule for container objects. A POD is a single instance of an application. Is the smallest object that can be created in Kubernetes.

In the use case that more users are accessing the app, it is as simple a creating a new POD of the same instance of the app. So we will have multiple PODs (instances of the app) running in the same NODE.

If the problem becomes that a bottleneck in your machine due to not having enough resources, creating new nodes for the POD( if not virtual).

****

### KUBERNETES CONTROLLERS

* Replication Controller.
HIGH AVAILABILITY
Ensures the application has the specified number of PODs are running at ALL TIMES.
With that being 1 or 1000.

LOAD BALANCE & SCALABILITY
If the number of users increases, new PODs are created to balance the load across PODs. If resources in a NODE are becoming scarce in resources, creating PODs in a different Node is an option to distribute work load.

* Replica SET:
THIS IS THE (NEWER) RECOMMENDED WAY to set up replication. (Has minor differences with the controller, which is also capable of setting up replication.)

THE DIFFERENCE BETWEEN **CONTROLLER** AND **REPLICASET** is the SELECTOR PROPERTY present in replicaset.

The selector has a "**matchLabels:**" property that allows us to filter PODs that contain such labels.

NOTE: 

The replica-set won´t allow any other number than that was specified. Additional containers will be KILLED while a lower number will trigger the creation of new ones till the specified number is reached.

****

### DEPLOYMENTS

How would you like to deploy:

- Production Environment.
- Upgrade docker instances (1 after the other, ROLLING UPDATE)
- Rollback changes if desired.
- Apply changes to the system when demanded (click update)
