# Terraform

Terraform is an Infrastructure as Code (IaC) tool that enables users to define and manage cloud and on-premises infrastructure resources using human-readable configuration files.
Instead of manually configuring resources through a console or API calls, Terraform allows you to describe your desired infrastructure state in code, making it easier to version, reuse, and maintain your infrastructure configurations.

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

## Core Concepts

- State File: Acts as the single source of truth for your infrastructure, storing the current state of all resources
- Configuration Files: Human-readable files (.tf) containing infrastructure definitions
- Execution Plan: A preview of planned changes before they're applied

## Best Practices for Dependency Management

- Prefer Implicit Over Explicit
- Let Terraform automatically detect dependencies whenever possible
- Use resource references rather than depends_on
- This leads to more efficient planning and updates
- Reference Output Attributes
  - Always reference output attributes (like id) rather than input arguments
  - This ensures proper ordering during creation
- Document Explicit Dependencies
  - Add comments explaining why explicit dependencies are needed
  - Helps other developers understand the rationale behind the design
- Keep Dependencies Minimal
  - Avoid unnecessary coupling between resources
  - Only declare dependencies that are truly required
  - This maintains flexibility in infrastructure updates

## Terraform Workflow

### Initialize Working Directory

`terraform init`

- Downloads required providers
- Sets up backend configuration
- Prepares working directory for operations

### Write Configuration Files

- Create .tf files describing desired infrastructure
- Define resources, variables, and modules
- Include dependency relationships

### Plan Changes

`terraform plan`

- Compares current state with configuration
- Shows planned additions, modifications, and deletions
- Helps catch potential issues before application

### Apply Changes

`terraform apply`

- Executes planned changes
- Updates infrastructure to match configuration
- Modifies state file to reflect new reality

### State Management

- State file tracks actual vs. desired state
- Enables idempotent operations
- Facilitates team collaboration

## State File

The Terraform state file is a JSON-formatted database that serves as the single source of truth for your infrastructure's current state.
It acts as a bridge between your infrastructure configuration and the actual resources in your cloud environment, enabling Terraform to track and manage your infrastructure effectively.

### Core Components of State Files

- Resource metadata and unique identifiers
- Current attribute values and properties
- Relationships between resources
- Dependency mappings
- Provider-specific information

### Recovery Options

#### Remote State Backup Recovery

```sh
terraform init -reconfigure
terraform state pull > backup.tfstate
```

- Restores state from remote backend
- Requires configured remote state storage
- Fastest recovery method

#### Infrastructure Import Process

```sh
# Example import command
terraform import aws_instance.web i-0123456789abcdef0

# Verify state
terraform state list
terraform show
```

- Import resources individually
- Verify each import
- Test functionality

#### Partial Recovery Steps

```sh
# Create new state file
terraform init

# Import resources incrementally
terraform import aws_instance.web i-0123456789abcdef0
terraform import aws_security_group.web sg-0123456789abcdef0

# Validate configuration
terraform plan
```

- Start with critical resources
- Build state incrementally
- Validate frequently
