- Assigning values to variables

```hcl
variable "my_variable" {
  type        = string
  default     = "ami-12345678"
}
```

- Terraform supports a variety of types, including:

string
number
bool
list()
map()
object({})

- list ()
```hcl
variable "regions" {
  type    = list(string)
  default = ["us-west-1", "us-east-1"]
}
```
- map()
```hcl
variable "instance_sizes" {
  type    = map(number)
  default = {
    small  = 1
    medium = 2
    large  = 3
  }
}

resource "aws_instance" "example" {
  ami = lookup(var.instance_sizes, var.size, "small")
}
```
This example selects the instance size based on a variable called size. If the size is not found, it defaults to “small”.

- Conditional Expressions
```hcl
variable "environment" {
  type    = string
  default = "development"
}

resource "aws_instance" "example" {
  count = var.environment == "production" ? 2 : 1
}
```
- Local Variables
  
For more advanced Terraform users, local variables can be instrumental in handling complex data structures and conditionals. Consider this scenario where you need to conditionally include certain resource properties.
```hcl
locals {
  instance_settings = {
    instance_type = "t2.micro",
    ami = var.use_custom_ami ? var.custom_ami : "ami-123456"
  }
}

resource "aws_instance" "advanced_example" {
  ami = local.instance_settings.ami
  instance_type = local.instance_settings.instance_type
  tags = local.common_tags
}
```
This setup highlights the power of local variables in managing conditional logic and complex data structures, simplifying your Terraform configurations significantly.

- YAML decode and read in Terraform local variable:-

```hcl
# conditional.yaml
env: "production"
tags:
  production: "true"
  development: "false"
```

To apply this logic within Terraform:
```hcl
locals {
  env_config = yamldecode(file("${path.module}/conditional.yaml"))
}

resource "some_resource" "example" {
  tags = {
    Environment = local.env_config.env
    Production = local.env_config.tags.production
    Development = local.env_config.tags.development
  }
}
```
This setup allows you to maintain environmental configurations in YAML, making it easier to manage and understand.
