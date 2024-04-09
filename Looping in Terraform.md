- Approach 1: Count Parameter
```hcl
resource "aws_instance" "example" {
  count         = 3
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "ExampleInstance-${count.index}"
  }
}
```
- Approach 2: For_each Loop

```hcl
variable "instance_details" {
  type = map(object({
    ami           = string
    instance_type = string
  }))
}

resource "aws_instance" "example" {
  for_each = var.instance_details

  ami           = each.value.ami
  instance_type = each.value.instance_type
  tags = {
    Name = "Instance-${each.key}"
  }
}
```

- Approach 3: Dynamic Blocks
```hcl
resource "aws_security_group" "example" {
  name        = "example-security-group"

  dynamic "ingress" {
    for_each = var.ingress_rules
    content {
      from_port   = ingress.value.from_port
      to_port     = ingress.value.to_port
      protocol    = ingress.value.protocol
      cidr_blocks = ingress.value.cidr_blocks
    }
  }
}
```
