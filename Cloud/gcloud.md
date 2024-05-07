# gcloud

## GKE

### Create cluster

```bash
gcloud container clusters create name \
    --num-nodes=3 \
    --region=us-east1-d \
    --machine-type=e2-standard-2 \
    --release-channel=regular
```

### Create node pool

```bash
gcloud container node-pools create POOL_NAME \
    --cluster CLUSTER_NAME \
    --num-nodes INT \
    --region REGION \
    --service-account SERVICE_ACCOUNT
```

### Delete node pool

```bash
gcloud container node-pools delete POOL_NAME \
    --cluster CLUSTER_NAME
```
