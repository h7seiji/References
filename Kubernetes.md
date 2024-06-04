# Kubernetes

## Pods

Pods represent and hold a collection of one or more containers. Generally, if you have multiple containers with a hard dependency on each other, you package the containers inside a single pod.

Pods also have Volumes. Volumes are data disks that live as long as the pods live, and can be used by the containers in that pod. Pods provide a shared namespace for their contents which means that the two containers inside of our example pod can communicate with each other, and they also share the attached volumes.

Pods also share a network namespace. This means that there is one IP Address per pod.

## Services

Pods aren't meant to be persistent. They can be stopped or started for many reasons - like failed liveness or readiness checks - and this leads to a problem:

What happens if you want to communicate with a set of Pods? When they get restarted they might have a different IP address.

That's where Services come in. Services provide stable endpoints for Pods.

Services use labels to determine what Pods they operate on. If Pods have the correct labels, they are automatically picked up and exposed by our services.

The level of access a service provides to a set of pods depends on the Service's type. Currently there are three types:

- ClusterIP (internal) -- the default type means that this Service is only visible inside of the cluster,
- NodePort gives each node in the cluster an externally accessible IP and
- LoadBalancer adds a load balancer from the cloud provider which forwards traffic from the service to Nodes within it.

## Deployments

Deployments are a declarative way to ensure that the number of Pods running is equal to the desired number of Pods, specified by the user.

The main benefit of Deployments is in abstracting away the low level details of managing Pods. Behind the scenes Deployments use Replica Sets to manage starting and stopping the Pods. If Pods need to be updated or scaled, the Deployment will handle that. Deployment also handles restarting Pods if they happen to go down for some reason.

## Manifest

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

## Shell inside pod

```bash
kubectl exec monolith --stdin --tty -c monolith -- /bin/sh
```
