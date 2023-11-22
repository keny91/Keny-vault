 #kubernetes #k8s 


* View active nodes:
```
	kubectl get nodes/pods/replicationcontroller/replicaset/deployments/svc
	kubect get pods,svc # shows active pods and services
	kubectl get nodes/pods -o wide (expanded information regarding nodes)

# To see all active components run:
	kubectl get all
```

* View active Pods:
```
	kubectl get pods
```

* Expand detailed information about a node/pod:
```
	kubectl describe node/pod <node-name>
```

* Run Image 
```
	kubectl run imageName --image=imageNameReference
```


* Delete image
```
	kubectl delete pod <pod-name> -n <namespace>
```



****

### CONTROL

For replica-sets:

Replace the already up replica-set to update its content.

``` 
kubectl replace -f replica-definition.yml
```

 Without changing the file:
 
```
kubectl scale --replicas=6  -f replicaset-definition.yml
```

By replicaset name:

```
kubectl scale --replicas=5 replicaset new-replica-set 
```

Modify manually a Kubernetes object that is active. Configuration changes will be applied once we exit.

```
kubectl edit replicaset myReplicaSet
```


### ROLLOUTS

Check the status:

``` 
kubectl rollout deployement/myapp-deployment
```

See the history of rollouts of a deployment:

```
kubectl rollout history deployment/myapp-deployment
```

Update a deployment:

```
kubectl apply -f deployment-definition.yml
```

Can also modify the image of the deployment, BUT does NOT alter the file. So it won´t apply next time we rise the deployment.

```
kubect set image deployment/myapp-deployment \ nginx-container=nginx:1.9.1
# where "nginx-container=nginx" is the name of the container to update in spec:
```

Undo current rollout:

```
kubectl rollout undo deployment/myapp-deployment
```


*********
### SERVICES

Get service command:

```
kubectl get svc
```

