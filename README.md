# Bastion Host Terraform Project

This Terraform project provisions a secure bastion host infrastructure in AWS/Azure/GCP (specify your cloud provider).

## Overview

The bastion host serves as a secure gateway to access private resources in your cloud infrastructure. This project creates:

- Bastion host EC2 instance (or equivalent)
- Security groups with minimal required access
- VPC and networking components (if needed)
- SSH key management
- Optional: Auto Scaling Group for high availability

## Prerequisites

- Terraform >= 1.0
- AWS CLI configured (or appropriate cloud provider CLI)
- SSH key pair for bastion access

## Quick Start

1. Clone this repository
2. Copy `terraform.tfvars.example` to `terraform.tfvars`
3. Update variables in `terraform.tfvars`
4. Initialize Terraform:
   ```bash
   terraform init
   ```
5. Plan the deployment:
   ```bash
   terraform plan
   ```
6. Apply the configuration:
   ```bash
   terraform apply
   ```

## Variables

| Variable | Description | Type | Default | Required |
|----------|-------------|------|---------|----------|
| `region` | AWS region | string | `us-west-2` | no |
| `instance_type` | EC2 instance type | string | `t3.micro` | no |
| `key_name` | SSH key pair name | string | - | yes |
| `allowed_cidr_blocks` | CIDR blocks allowed to connect | list(string) | - | yes |

## Outputs

| Output | Description |
|--------|-------------|
| `bastion_public_ip` | Public IP of the bastion host |
| `bastion_security_group_id` | Security group ID for the bastion |

## Security Considerations

- Only allow SSH access from trusted IP ranges
- Regularly update the bastion host OS and packages
- Consider using AWS Systems Manager Session Manager for additional security
- Monitor bastion host access logs

## Usage

### Connecting to the Bastion Host

```bash
ssh -i /path/to/your/key.pem ec2-user@<bastion_public_ip>
```

### Connecting to Private Resources via Bastion

```bash
ssh -i /path/to/your/key.pem -J ec2-user@<bastion_public_ip> ec2-user@<private_instance_ip>
```

## Cleanup

To destroy the infrastructure:

```bash
terraform destroy
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
