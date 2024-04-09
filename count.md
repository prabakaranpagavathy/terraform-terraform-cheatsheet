## Count

- Basic Usage of count.
  
```hcl
resource "aws_instance" "example" {
  count         = 3
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

- Accessing Individual Resources
```hcl
resource_type.resource_name[count_index]
```
- Conditionally Creating Resources
```hcl
resource "aws_instance" "conditional_example" {
  count         = var.create_instances ? 3 : 0
  ami           = var.ami_id
  instance_type = var.instance_type
}
```
- Creating Unique Resources with Loops
```hcl
resource "aws_instance" "loop_example" {
  count         = 3
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "Instance-${count.index+1}"
  }
}
```
- Complex Conditional Creation
```hcl
resource "aws_instance" "complex_conditional" {
  count         = length(var.amis) > 0 ? length(var.amis) : 0
  ami           = var.amis[count.index]
  instance_type = "t2.micro"
}
```
