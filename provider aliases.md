**- Provider Aliases**
- 
```hcl
provider "aws" {
  region = "us-west-2"
}

provider "aws" {
  alias  = "east"
  region = "us-east-1"
  profile = "account-one"
}

provider "aws" {
  alias  = "europe"
  region = "eu-central-1"
  profile = "account-two"
}
```

- Using Providers with modules

```hcl
module "vpc" {
  source = "./modules/vpc"

  providers = {
    aws = aws.east
  }
}
```
