#kubernetes #k8s 


* View active nodes:
```
kubectl get nodes/pods/replicationcontroller/replicaset/deployments

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

``` 
# replace the already up replica-set to update its content

kubectl replace -f replica-definition.yml

# without changing the file

kubectl scale --replicas=6  -f replicaset-definition.yml

kubectl scale --replicas=5 replicaset new-replica-set 

# Modify manually a Kubernetes object that is active. Configuration changes will be applied once we exit.

kubectl edit replicaset myReplicaSet
```
