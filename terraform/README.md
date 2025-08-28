# Terraform

<p align="center"><img align="center" width="40%" height="40%" src="assets/terraform.svg"></p>

[Terraform](https://www.terraform.io/) is an infrastructure-as-code (IaC) software tool created by [HashiCorp](https://www.hashicorp.com/).

## Index

* [Install](#install)
* [Usage](#usage)
* [Files](#files)
* [Backends](#backends)
* [Modules](#modules)

## Install

HashiCorp distributes Terraform as a binary package.
* Go to the [Downloads](https://developer.hashicorp.com/terraform/downloads) page.
* Download the precompiled binary.
* Add the precompiled binary to the PATH.

## Usage

Check version.
```
terraform version
```

Initialize a working directory.
```
terraform init
```

Reconfigure a backend.
```
terraform init -reconfigure
```

Migrate the state to a backend.
```
terraform init -migrate-state
```

Download and update modules mentioned in the root module.
```
terraform get
```

Rewrite configuration files to a canonical format and style.
```
terraform fmt
terraform fmt -recursive
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

## Files

| File | Tracked In | Purpose |
|---|---|---|
| `*.tf` | ✅ Git | Infrastructure code |
| `.terraform.lock.hcl` | ✅ Git | Locks provider versions |
| `terraform.tfstate` | ✅ Backend | Infrastructure state |
| `.terraform/` | ❌ Local | Caches provider plugins and modules |

## Backends

Backends are a mechanism that determines how and where store state, and how to handle state locking and remote operations.

1. Create AWS S3 bucket for storage.
* Enable versioning.
* Enable server side encryption.
2. Create AWS DynamoDB table for locking mechanism.
* Partition key: `LockID`.
3. Use backend.
```
terraform {
  backend "s3" {
    bucket         = "terraform-state-bucket"
    key            = "terraform.tfstate"
    region         = "eu-west-1"
    dynamodb_table = "terraform_state_table"
  }
}
```
4. Migrate the state to the backend.
```
terraform init -migrate-state
```
5. Delete local state files.

## Modules

A [module](https://developer.hashicorp.com/terraform/language/modules/develop) is a container for multiple resources that are used together.

Configuration with multiple providers and modules.

```
root
├── main.tf
├── modules.tf
├── submodule1
│   ├── main.tf
│   ├── modules.tf
│   ├── submodule2
|   |   ├── main.tf
|   |   └── ...
│   ├── submodule3
|   |   ├── main.tf
|   |   └── ...
│   └── ...
└── ...
```

At `root` module, `main.tf` file.
```
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
```
module "submodule1" {
  source = "./submodule1"
  providers = {
    aws.prov1 = aws.prov1
    aws.prov2 = aws.prov2
  }
} 
```

At `submodule1` module, `main.tf` file.
```
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
```
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

At `submodule2` and `submodule3` modules, `main.tf` file.
```
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    } 
  }
}
```
