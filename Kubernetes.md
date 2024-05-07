# Kubernetes

## Namespaces

### List namespaces

`kubectl get namespace`

### Create namespace

`kubectl create namespace dev`

### Deploy pod in namespace

`kubectl run app-server --image=centos --namespace=dev --sleep infinity`

## Node Pools

### Cordon off and drain nodes in pool

```bash
for node in $(kubectl get nodes -l cloud.google.com/gke-nodepool=default-pool -o=name); do
  kubectl drain --force --ignore-daemonsets --grace-period=10 "$node";
done
```

## Disruption budget

### Create disruption budget

```bash
kubectl create poddisruptionbudget name --selector run=gb-frontend --min-available 4
```
