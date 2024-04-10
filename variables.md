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

