# cloud-platform-terraform

Infrastructure as Code for AWS Cloud Platform using Terraform.

## Project Structure

```
.
├── modules/
│   └── network/           # Network module (VPC and subnets)
│       ├── main.tf
│       └── variables.tf
└── environments/
    └── dev/               # Development environment
        └── main.tf
```

## Modules

### Network Module (`modules/network/`)

Creates AWS VPC with public subnets.

**Resources:**
- AWS VPC with configurable CIDR block
- 2 public subnets with auto-assigned public IPs

**Variables:**
- `cidr` - CIDR block for the VPC
- `name` - Name tag for the VPC

**Outputs:**
- `vpc_id` - The ID of the created VPC

## Environments

### Dev Environment (`environments/dev/`)

Development environment configuration.

**Configuration:**
- Region: `eu-central-1`
- VPC CIDR: `10.0.0.0/16`
- VPC Name: `dev-vpc`

## Usage

### Prerequisites

1. Install Terraform (v1.6+)
2. Configure AWS credentials:
   ```bash
   export AWS_ACCESS_KEY_ID="your-access-key"
   export AWS_SECRET_ACCESS_KEY="your-secret-key"
   ```

### Deploy Dev Environment

```bash
cd environments/dev
terraform init
terraform plan
terraform apply
```

### Verify Deployment

After successful deployment, you can verify the VPC creation in the AWS Console:
1. Navigate to VPC service
2. Look for VPC named "dev-vpc"
3. Verify CIDR block is 10.0.0.0/16
4. Check that 2 public subnets were created

## Clean Up

To destroy all resources:

```bash
cd environments/dev
terraform destroy
```