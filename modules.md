- Module Inputs
  
- Example 1: Basic Input Variable
```hcl
variable "instance_type" {
  description = "The instance type of the AWS EC2"
  type        = string
  default     = "t2.micro"
}
```

- Example 2: Advanced Input Variable
```hcl
variable "backend_config" {
  description = "Configuration map for the backend"
  type        = map(string)
  default     = {
    size = "large",
    colour = "red"
  }
}
```
-Module Outputs

- Example 3: Basic Output Variable
```hcl
output "instance_id" {
  value = aws_instance.web.id
  description = "ID of the instance"
}
```
- Example 4: Advanced Output Usage
```hcl
output "frontend_ip" {
  value = aws_elb.frontend.dns_name
  description = "The DNS name for the frontend load balancer"
}
```

- Passing Inputs and Outputs Between Modules
- Example 5: Inter-module Communication
```hcl
module "backend" {
  source = "./modules/backend"
  db_user = var.db_user
  db_password = var.db_password
}

module "frontend" {
  source = "./modules/frontend"
  backend_address = module.backend.address
}
```
Best Practices for Using Inputs and Outputs in Terraform Modules
Keep module interfaces clean and minimal. Only expose variables and outputs that are necessary.
Use descriptive names and descriptions for your variables and outputs to make your configurations more readable.
Consider using type constraints and validation rules to make your modules more robust and self-documenting.

- Loading Modules from the Local File System
```hcl
module "my_module" {
  source = "./modules/my-module"
}
```
- Loading Modules from a Terraform Registry
```hcl
module "aws_network" {
  source = "terraform-aws-modules/vpc/aws"
  version = "2.77.0"
}
```
- Loading Modules from GitHub
```hcl
module "vpc" {
  source = "git::https://github.com/terraform-aws-modules/terraform-aws-vpc.git?ref=v2.77.0"
}
```

- Using SSH for Private Repositories
```hcl
module "private_repo" {
  source = "git::ssh://git@github.com/terraform-aws-modules/terraform-aws-vpc.git?ref=tags/v2.77.0"
}
```

- Using Local Paths for Module Development
```hcl
module "local_dev" {
  source = "../local-modules/my-module"
}
```
