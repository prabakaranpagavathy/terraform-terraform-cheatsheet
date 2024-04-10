- Terraform: Managing multiple environments (dev, staging, production)

```hcl
terraform workspace new dev
terraform workspace new staging
terraform workspace new production
```

- Switch between workspaces to apply changes specific to that environment:
```hcl
terraform workspace select dev
```

- Environment-specific Configuration
Using variables and workspaces, you can customize your Terraform configuration for each environment. You can define environment-specific variables in separate files, e.g., dev.tfvars, staging.tfvars, and production.tfvars.

```hcl
variable "environment" {}

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = var.ami
  instance_type = "t2.micro"
  tags = {
    Environment = var.environment
  }
}
```
Apply your configuration with the corresponding variable file:
```hcl
terraform apply -var-file=dev.tfvars
```
