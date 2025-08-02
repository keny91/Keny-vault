
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

#### Deployment Rollouts

When first create a deployment it creates a ROLLOUT. A Rollout creates a deployment REVISION.
A Revision allows us to go back to a previous state of the deployment.

There are 2 types of deployment strategies:

- **RECREATE STRATEGY:** 
	Destroy OLD instances and create NEW ones. This makes the service unavailable until the containers are re-originated.

- **ROLLING UPDATE STRATEGY (default):** 
	We take down an old version and rise a new one before moving to the next one.

#### Updating a deployment.

When updating a deployment a new image is applied to the containers. Kubernetes then will create a new REPLICA-SET in which it will be rising the new containers (the previous replicaset will still be active if Rolling update).

A deployment can be undone by UNDO. This creates an update rollout to the previous rollout in the history. 


****

### SERVICES


Services come in many variants.

![[Knowledge/GeneralProgramming/000_1_Embedded_Data/ServiceTypes.png]]

#### NodePort

For example. Inside a cluster, each of the nods has its own address and it is addressable while inside the Node.
To access it from outside the Node, a SERVICE is required to expose the IP through a port for example:

![[Knowledge/GeneralProgramming/000_1_Embedded_Data/k8s_service.png]]

When configuring a service to find particular nodes, the service will be able to find them and link them even if they are part of different nodes.

![[Knowledge/GeneralProgramming/000_1_Embedded_Data/NodePort.png]]
#### ClusterIP

The service creates a virtual IP inside the server to help set up communication between services (like front and backend servers for example).

![[Knowledge/GeneralProgramming/000_1_Embedded_Data/ClusterIP.png]]
#### Load Balancer

Regulates the flow of information to distribute it across the PODs in the Node. 



### WHEN DESIGNING A DEPLOYMENT

Steps:
1. Deploy PODS of each of the apps.
2. Enable component connectivity (Create a map of what applications communicate with which and in which direction), Determine USERs, PORTS, 
3. Create SERVICES (ClusterIP)
	1. Databases: sql, redis, postgress 
	2. Create services NodePort (for external apps)