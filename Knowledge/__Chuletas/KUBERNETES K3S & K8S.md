#chuletas #kubernetes 


### SERVER

```
k3s kubectl get nodes
```

```
sudo k3s kubectl get nodes -o wide
```

```


```


```


```


```

# Port-forward or run on cluster host

kubectl -n monitoring port-forward svc/prometheus-operated 9090:9090 &>/dev/null &

curl -s http://localhost:9090/api/v1/targets | jq '.data.activeTargets[] | select(.labels.job|test("node-exporter|node_exporter")) | {instance:.labels.instance, job:.labels.job, health:.health}'
```


### AGENTS








### HELM 


1. ADD
helm repo add repo-name repo-url

2. **Update Helm repositories:**
helm repo update

3. **Search for charts:**

helm search repo keyword

4. **Install a chart:**

helm install release-name repo/chart [--values values.yaml]

5. **List installed releases:**
```
helm list [--all-namespaces]
```

6. **Upgrade a release:**

```
helm upgrade release-name> repo/chart> [--values values.yaml]
```

7. **Uninstall a release:**

```
helm uninstall <release-name>
```

8. **Show chart values:**

```
helm show values <repo/chart>
```

9. **Get release status:**
```
helm status <release-name>
```

10. **Rollback a release:**

```
helm rollback <release-name> <revision>
```



#secrets

### HOW TO GET A SECRET IN KUBERNETES

```
                   (cluster)            (workspace/env)
kubectl get secret prometheus-grafana -n monitoring -o yaml

# admin-password: e3sgZ3JhZmFuYV9hZG1pbl9wYXNzd29yZCB9fQ==
# admin-user: e3sgZ3JhZmFuYV9hZG1pbl91c2VyIH19

echo "e3sgZ3JhZmFuYV9hZG1pbl91c2VyIH19" | base64 --decode 
#{{ grafana_admin_user }}

```
