# Challenge Lab

## Setup

```bash
gcloud config set compute/zone "ZONE"
export ZONE=$(gcloud config get compute/zone)

gcloud config set compute/region "REGION"
export REGION=$(gcloud config get compute/region)
```

```bash
export VPC_NAME=vpc-network-rldz
export SUBNET_A=subnet-a-2lmw
export SUBNET_B=subnet-b-xt0k
export REGION_A=us-west1
export REGION_B=us-east4
export FIREWALL1=fsoq-firewall-ssh
export FIREWALL2=wrsk-firewall-rdp
export FIREWALL3=leqz-firewall-icmp
```

## Migrate to Cloud SQL

### Prepare the stand-alone PostgreSQL database for migration

- Enable Database Migration API
- Enable Service Networking API

- ssh into the antern-postgresql-vm instance
- `sudo apt get install postgresql-13-pglogical`

```bash
sudo su - postgres -c "gsutil cp gs://cloud-training/gsp918/pg_hba_append.conf ."
sudo su - postgres -c "gsutil cp gs://cloud-training/gsp918/postgresql_append.conf ."
sudo su - postgres -c "cat pg_hba_append.conf >> /etc/postgresql/13/main/pg_hba.conf"
sudo su - postgres -c "cat postgresql_append.conf >> /etc/postgresql/13/main/postgresql.conf"

sudo systemctl restart postgresql@13-main
```

`sudo su - postgres`

`psql`

```bash
CREATE USER replication_user PASSWORD 'DMS_1s_cool!';
ALTER DATABASE orders OWNER TO replication_user;
ALTER ROLE replication_user WITH REPLICATION;
```

`\c postgres;`

```bash
GRANT USAGE ON SCHEMA pglogical TO replication_user;
GRANT ALL ON SCHEMA pglogical TO replication_user;

GRANT SELECT ON pglogical.tables TO replication_user;
GRANT SELECT ON pglogical.depend TO replication_user;
GRANT SELECT ON pglogical.local_node TO replication_user;
GRANT SELECT ON pglogical.local_sync_status TO replication_user;
GRANT SELECT ON pglogical.node TO replication_user;
GRANT SELECT ON pglogical.node_interface TO replication_user;
GRANT SELECT ON pglogical.queue TO replication_user;
GRANT SELECT ON pglogical.replication_set TO replication_user;
GRANT SELECT ON pglogical.replication_set_seq TO replication_user;
GRANT SELECT ON pglogical.replication_set_table TO replication_user;
GRANT SELECT ON pglogical.sequence_state TO replication_user;
GRANT SELECT ON pglogical.subscription TO replication_user;
```

`\c orders;`

```bash
GRANT USAGE ON SCHEMA pglogical TO replication_user;
GRANT ALL ON SCHEMA pglogical TO replication_user;

GRANT SELECT ON pglogical.tables TO replication_user;
GRANT SELECT ON pglogical.depend TO replication_user;
GRANT SELECT ON pglogical.local_node TO replication_user;
GRANT SELECT ON pglogical.local_sync_status TO replication_user;
GRANT SELECT ON pglogical.node TO replication_user;
GRANT SELECT ON pglogical.node_interface TO replication_user;
GRANT SELECT ON pglogical.queue TO replication_user;
GRANT SELECT ON pglogical.replication_set TO replication_user;
GRANT SELECT ON pglogical.replication_set_seq TO replication_user;
GRANT SELECT ON pglogical.replication_set_table TO replication_user;
GRANT SELECT ON pglogical.sequence_state TO replication_user;
GRANT SELECT ON pglogical.subscription TO replication_user;
```

```bash
GRANT USAGE ON SCHEMA public TO replication_user;
GRANT ALL ON SCHEMA public TO replication_user;

GRANT SELECT ON public.distribution_centers TO replication_user;
GRANT SELECT ON public.inventory_items TO replication_user;
GRANT SELECT ON public.order_items TO replication_user;
GRANT SELECT ON public.products TO replication_user;
GRANT SELECT ON public.users TO replication_user;
```

```bash
\c orders;
\dt
```

```bash
ALTER TABLE public.distribution_centers OWNER TO replication_user;
ALTER TABLE public.inventory_items OWNER TO replication_user;
ALTER TABLE public.order_items OWNER TO replication_user;
ALTER TABLE public.products OWNER TO replication_user;
ALTER TABLE public.users OWNER TO replication_user;
\dt
```

```bash
ALTER TABLE public.inventory_items ADD PRIMARY KEY(id);
\q
exit
```

### Migrate the stand-alone PostgreSQL database to a Cloud SQL for PostgreSQL instance

Console Database Migration

1. Connection Profile (VM Instance Internal IP)
    - USER replication_user
    - PASSWORD DMS_1s_cool!
2. Migration Job

### Promote a Cloud SQL to be a stand-alone instance for reading and writing data

## Update permissions

- Navigate to the Cloud SQL database you just created. In the Users section, add the Antern Editor user account to the database you created. Use Cloud IAM authentication and for the principal use their username above.

- Navigate to the Cloud SQL database you just created. In the Users section, add the Cymbal Owner user account to the database you created. Use Cloud IAM authentication and for the principal use their username above.

- Change the Cymbal Editor user role from Viewer to Editor. Their username is Cymbal Editor username.

## Create networks and firewalls

### Create a VPC network with two subnetworks

```bash
gcloud compute networks create $VPC_NAME --subnet-mode=custom
```

```bash
gcloud compute networks subnets create $SUBNET_A --network=$VPC_NAME --region=$REGION_A --range=10.10.10.0/24
```

```bash
gcloud compute networks subnets create $SUBNET_B --network=$VPC_NAME --region=$REGION_B --range=10.10.20.0/24
```

### Create firewall rules for the VPC network

```bash
gcloud compute firewall-rules create $FIREWALL1 --direction=INGRESS --priority=65535 --network=$VPC_NAME --action=ALLOW --rules=tcp:22 --source-ranges=0.0.0.0/24
```

```bash
gcloud compute firewall-rules create $FIREWALL2 --direction=INGRESS --priority=65535 --network=$VPC_NAME --action=ALLOW --rules=tcp:3389 --source-ranges=0.0.0.0/24
```

```bash
gcloud compute firewall-rules create $FIREWALL3 --direction=INGRESS --priority=65535 --network=$VPC_NAME --action=ALLOW --rules=icmp --source-ranges=0.0.0.0/24
```

## Troubleshoot and fix a broken GKE cluster

### Create a BigQuery log sink

- On Console, open BigQuery
- Use the Logs Explorer to investigate your running GKE app and investigate the service that has errors. Hint: you should be looking for logs with severity ERROR.
- More actions -> Create sink
- Name the sink SINK_NAME
- For the destination, create a BigQuery dataset named gke_app_errors_sink with a location of us (multiple regions in United States).
- In your inclusion filter, make sure to include: resource.type, INCLUSION_FILTER, and severity.
- Grant the Antern Editor user the BigQuery Data Viewer role for this project. Their username is: Antern Editor username.
- Grant the Antern Owner user the BigQuery Admin role for this project. Their username is: Antern Owner username.

### Fix the GKE cluster

Connect to the cloud-ops-sandbox GKE cluster and run the following commands to remediate the issue. Answer the verification questions when prompted.

```bash
git clone --depth 1 --branch csb_1220 https://github.com/GoogleCloudPlatform/cloud-ops-sandbox.git
cd cloud-ops-sandbox/sre-recipes
./sandboxctl sre-recipes restore recipe number
./sandboxctl sre-recipes verify recipe number
```
