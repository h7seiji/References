# Terraform

`terraform init -migrate-state`

`terraform import module.module-name.resource-type.resource-name resource-id`

```tf
terraform {
  backend "gcs" {
    bucket = "tf-bucket-385570"
    prefix = "terraform/state"
  }
}
```
