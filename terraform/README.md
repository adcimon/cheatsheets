# Terraform

<p align="center"><img align="center" width="40%" height="40%" src="assets/terraform.svg"></p>

[Terraform](https://www.terraform.io/) is an infrastructure-as-code (IaC) software tool created by [HashiCorp](https://www.hashicorp.com/).

## Index

* [Install](#install)
* [Usage](#usage)
* [Providers Within Modules](#providers-within-modules)

# Install

HashiCorp distributes Terraform as a binary package.
* Go to the [Downloads](https://developer.hashicorp.com/terraform/downloads) page.
* Download the precompiled binary.
* Add the precompiled binary to the PATH.

# Usage

Check version.
```
terraform version
```

Initialize a working directory.
```
terraform init
```

Download and update modules mentioned in the root module.
```
terraform get
```

Rewrite configuration files to a canonical format and style.
```
terraform fmt
```

Validate the configuration files without accessing any remote service.
```
terraform validate
```

Create an execution plan to preview changes in the infrastructure.
```
terraform plan
```

Execute the actions proposed in a plan.
```
terraform apply
```

Destroy all remote resources of a plan.
```
terraform destroy
```

# Providers Within Modules

Configuration with multiple providers and modules.

```
root
├── main.tf
├── modules.tf
├── submodule1
│   ├── main.tf
│   ├── modules.tf
│   ├── submodule1
|   |   ├── main.tf
|   |   └── ...
│   ├── submodule2
|   |   ├── main.tf
|   |   └── ...
│   └── ...
└── ...
```

At `root` module, `main.tf` file.
``` file=main.tf
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    } 
  }
}

provider "aws" {
  alias = "prov1"
  # ...
}

provider "aws" {
  alias = "prov2"
  # ...
}
```

At `root` module, `modules.tf` file.
``` file=modules.tf
module "submodule1" {
  source = "./submodule1"
  providers = {
    aws.prov1 = aws.prov1
    aws.prov2 = aws.prov2
  }
} 
```

At `submodule1` module, `main.tf` file.
``` file=main.tf
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      configuration_aliases = [
        aws.prov1,
        aws.prov2,
      ]
    } 
  }
}
```

At `submodule1` module, `modules.tf` file.
``` file=modules.tf
module "submodule2" {
  source = "./submodule2"
  providers = {
    aws = aws.prov1
  }
} 

module "submodule3" {
  source = "./submodule3"
  providers = {
    aws = aws.prov2
  }
}
```

At `submodule2` and `submodule3`, `main.tf` file.
``` file=main.tf
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    } 
  }
}
```
