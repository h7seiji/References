# Challenge Lab

## Create Cluster

```bash
gcloud container clusters create onlineboutique-cluster-793 --num-nodes=2 --zone=us-east1-d --machine-type=e2-standard-2 --release-channel=rapid
```

## Create namespaces

```bash
kubectl create namespace dev && kubectl create namespace prod
```

## Deploy app

```bash
git clone https://github.com/GoogleCloudPlatform/microservices-demo.git && cd microservices-demo && kubectl apply -f ./release/kubernetes-manifests.yaml --namespace dev
```

## Get frontend external IP

```bash
kubectl get service frontend-external --namespace=dev
```

## Create node pool

```bash
gcloud container node-pools create optimized-pool-5454 --cluster onlineboutique-cluster-793 --num-nodes 2 --zone=us-east1-d --machine-type=custom-2-3584
```

## Cordon off and drain nodes in default pool

```bash
for node in $(kubectl get nodes -l cloud.google.com/gke-nodepool=default-pool -o=name); do
  kubectl drain --force --ignore-daemonsets --grace-period=10 "$node";
done
```

## Delete default pool

```bash
gcloud container node-pools delete default-pool --cluster onlineboutique-cluster-793 --zone=us-east1-d
```

## Create disruption budget

```bash
kubectl create poddisruptionbudget onlineboutique-frontend-pdb --selector run=frontend --min-available 1 --namespace=dev
```

## Edit frontend workload

- image: `gcr.io/qwiklabs-resources/onlineboutique-frontend:v2.1`
- imagePullPolicy: `Always`

## Apply horizontal pod autoscaling

```bash
kubectl autoscale deployment frontend --cpu-percent=50 --min=1 --max=13 --namespace=dev
```

## Enable autoscaling

```bash
gcloud beta container clusters update onlineboutique-cluster-793 --enable-autoscaling --min-nodes 1 --max-nodes 6 --zone=us-east1-d
```

## Load test

```bash
kubectl exec $(kubectl get pod --namespace=dev | grep 'loadgenerator' | cut -f1 -d ' ') -it --namespace=dev -- bash -c 'export USERS=8000; locust --host="http://YOUR_FRONTEND_EXTERNAL_IP" --headless -u "8000" 2>&1'
```

## recommendationservice autoscaling

```bash
kubectl autoscale deployment recommendationservice --cpu-percent=50 --min=1 --max=5 --namespace=dev
```
