# Challenge Lab

## Create development VPC

```bash
gcloud compute networks create griffin-dev-vpc --subnet-mode=custom
```

```bash
gcloud compute networks subnets create griffin-dev-wp --network=griffin-dev-vpc --zone=ZONE --range=192.168.16.0/20
```

```bash
gcloud compute networks subnets create griffin-dev-mgmt --network=griffin-dev-vpc --zone=ZONE --range=192.168.32.0/20
```

## Create production VPC

```bash
gcloud compute networks create griffin-prod-vpc --subnet-mode=custom
```

```bash
gcloud compute networks subnets create griffin-prod-wp --network=griffin-prod-vpc --zone=ZONE --range=192.168.16.0/20
```

```bash
gcloud compute networks subnets create griffin-prod-mgmt --network=griffin-prod-vpc --zone=ZONE --range=192.168.32.0/20
```

## Create bastion host

```bash
gcloud compute instances create griffin-bastion-host \
    --zone=ZONE \
    --machine-type=e2-micro \
    --network-interface=no-address,network-tier=PREMIUM,subnet=griffin-dev-mgmt \
    --network-interface=no-address,network-tier=PREMIUM,subnet=griffin-prod-mgmt
```

## Create and configure Cloud SQL Instance

```bash
gcloud sql instances create griffin-dev-db --database-version=MYSQL_5_7 --cpu=2 --memory=4GB --region=REGION --root-password=password123
```

```sql
CREATE DATABASE wordpress;
CREATE USER "wp_user"@"%" IDENTIFIED BY "stormwind_rules";
GRANT ALL PRIVILEGES ON wordpress.* TO "wp_user"@"%";
FLUSH PRIVILEGES;
```

## Create Kubernetes cluster

```bash
gcloud container clusters create griffin-dev --num-nodes=2 --zone=ZONE --machine-type=e2-standard-4 --subnetwork=griffin-dev-wp
```

## Prepare the Kubernetes cluster

```bash
cp -r gs://cloud-training/gsp321/wp-k8s .
```

- Add the following secrets and volume to the cluster using wp-env.yaml.
- Make sure you configure the username to wp_user and password to stormwind_rules before creating the configuration.

```bash
gcloud iam service-accounts keys create key.json \
    --iam-account=cloud-sql-proxy@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com
kubectl create secret generic cloudsql-instance-credentials \
    --from-file key.json
```

## Create a WordPress deployment

- Before you create the deployment you need to edit wp-deployment.yaml.
- Replace YOUR_SQL_INSTANCE with griffin-dev-db's Instance connection name.
- Get the Instance connection name from your Cloud SQL instance.
- After you create your WordPress deployment, create the service with wp-service.yaml.

## Enable monitoring

```bash
gcloud monitoring uptime create DISPLAY_NAME --resource-type=uptime-url --resource-labels=host=google.com,project_id=PROJECT_ID
```

## Provide access for an additional engineer

On console, add user to the project with editor role.
