# Challenge Lab

## Create development VPC

```bash
gcloud compute networks create griffin-dev-vpc --subnet-mode=custom
```

```bash
gcloud compute networks subnets create griffin-dev-wp --network=griffin-dev-vpc --region=us-west1 --range=192.168.16.0/20
```

```bash
gcloud compute networks subnets create griffin-dev-mgmt --network=griffin-dev-vpc --region=us-west1 --range=192.168.32.0/20
```

```bash
gcloud compute firewall-rules create griffin-dev --direction=INGRESS --priority=1000 --network=griffin-dev-vpc --action=ALLOW --rules=tcp:22 --source-ranges=0.0.0.0/0
```

## Create production VPC

```bash
gcloud compute networks create griffin-prod-vpc --subnet-mode=custom
```

```bash
gcloud compute networks subnets create griffin-prod-wp --network=griffin-prod-vpc --region=us-west1 --range=192.168.48.0/20
```

```bash
gcloud compute networks subnets create griffin-prod-mgmt --network=griffin-prod-vpc --region=us-west1 --range=192.168.64.0/20
```

```bash
gcloud compute firewall-rules create griffin-prod --direction=INGRESS --priority=1000 --network=griffin-prod-vpc --action=ALLOW --rules=tcp:22 --source-ranges=0.0.0.0/0
```

## Create bastion host

```bash
gcloud compute instances create griffin-bastion-host \
    --zone=us-west1-c \
    --machine-type=e2-micro \
    --network-interface=no-address,network-tier=PREMIUM,subnet=griffin-dev-mgmt \
    --network-interface=no-address,network-tier=PREMIUM,subnet=griffin-prod-mgmt
```

## Create and configure Cloud SQL Instance

```bash
gcloud sql instances create griffin-dev-db --database-version=MYSQL_5_7 --cpu=2 --memory=4GB --region=us-west1 --root-password=password123
```

```bash
gcloud sql connect griffin-dev-db --user=root --quiet
```

```sql
CREATE DATABASE wordpress;
CREATE USER "wp_user"@"%" IDENTIFIED BY "stormwind_rules";
GRANT ALL PRIVILEGES ON wordpress.* TO "wp_user"@"%";
FLUSH PRIVILEGES;
```

## Create Kubernetes cluster

```bash
gcloud container clusters create griffin-dev --num-nodes=2 --zone=us-west1-c --machine-type=e2-standard-4 --network=griffin-dev-vpc --subnetwork=griffin-dev-wp
```

## Prepare the Kubernetes cluster

```bash
gsutil cp -r gs://cloud-training/gsp321/wp-k8s .
cd wp-k8s
```

- Add the following secrets and volume to the cluster using wp-env.yaml.

```bash
vi wp-env.yaml
```

- Make sure you configure the username to wp_user and password to stormwind_rules before creating the configuration.

```bash
kubectl create -f wp-env.yaml
```

```bash
gcloud iam service-accounts keys create key.json \
    --iam-account=cloud-sql-proxy@qwiklabs-gcp-04-d4c575c82d8b.iam.gserviceaccount.com
kubectl create secret generic cloudsql-instance-credentials \
    --from-file key.json
```

## Create a WordPress deployment

- Before you create the deployment you need to edit wp-deployment.yaml.

```bash
vi wp-deployment.yaml
```

- Replace YOUR_SQL_INSTANCE with griffin-dev-db's Instance connection name: `qwiklabs-gcp-04-d4c575c82d8b:us-west1:griffin-dev-db`

```bash
kubectl create -f wp-deployment.yaml
```

- After you create your WordPress deployment, create the service with wp-service.yaml.

```bash
kubectl create -f wp-service.yaml
```

## Enable monitoring

```bash
gcloud monitoring uptime create griffin-check --resource-type=uptime-url --resource-labels=host=EXTERNAL_IP,project_id=qwiklabs-gcp-04-d4c575c82d8b
```

## Provide access for an additional engineer

On console, add user to the project with editor role.
