# cloud-platform-terraform

A Terraform infrastructure repository for managing cloud platform resources across multiple environments.

## Repository Structure

```
cloud-platform-terraform/
│
├─ environments/          # Environment-specific configurations
│   ├─ dev/              # Development environment
│   │   └─ main.tf
│   ├─ stage/            # Staging environment
│   │   └─ main.tf
│   └─ prod/             # Production environment
│       └─ main.tf
│
├─ modules/              # Reusable Terraform modules
│   ├─ network/          # VPC, subnets, and networking resources
│   ├─ compute/          # EC2 instances and compute resources
│   └─ eks/              # Amazon EKS cluster resources
│
├─ .github/workflows/    # CI/CD workflows
│   └─ terraform.yml     # Terraform validation and planning
│
└─ README.md
```

## Environments

- **dev**: Development environment for testing and development
- **stage**: Staging environment for pre-production testing
- **prod**: Production environment for live workloads

## Modules

### Network Module
Creates VPC, subnets, and internet gateway for network infrastructure.

**Inputs:**
- `vpc_cidr`: CIDR block for VPC (default: "10.0.0.0/16")
- `availability_zones`: List of availability zones
- `environment`: Environment name

**Outputs:**
- `vpc_id`: ID of the VPC
- `public_subnet_ids`: List of public subnet IDs
- `vpc_cidr`: CIDR block of the VPC

### Compute Module
Manages EC2 instances and associated security groups.

**Inputs:**
- `instance_type`: EC2 instance type (default: "t3.micro")
- `vpc_id`: VPC ID
- `subnet_ids`: List of subnet IDs
- `environment`: Environment name

**Outputs:**
- `instance_id`: ID of the EC2 instance
- `instance_public_ip`: Public IP of the EC2 instance
- `security_group_id`: ID of the security group

### EKS Module
Provisions Amazon EKS clusters for Kubernetes workloads.

**Inputs:**
- `cluster_name`: Name of the EKS cluster
- `cluster_version`: Kubernetes version (default: "1.28")
- `vpc_id`: VPC ID
- `subnet_ids`: List of subnet IDs for EKS
- `environment`: Environment name

**Outputs:**
- `cluster_id`: ID of the EKS cluster
- `cluster_endpoint`: Endpoint of the EKS cluster
- `cluster_security_group_id`: Security group ID of the EKS cluster
- `cluster_arn`: ARN of the EKS cluster

## Usage

### Initialize Terraform

```bash
cd environments/dev
terraform init
```

### Validate Configuration

```bash
terraform validate
```

### Plan Changes

```bash
terraform plan
```

### Apply Changes

```bash
terraform apply
```

## CI/CD

The repository includes a GitHub Actions workflow that:
- Validates Terraform configuration on push and pull requests
- Runs `terraform fmt` to check formatting
- Runs `terraform validate` for each environment
- Generates `terraform plan` for pull requests

## Requirements

- Terraform >= 1.0
- AWS Provider ~> 5.0

## License

This project is licensed under the MIT License.