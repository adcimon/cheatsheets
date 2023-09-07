# Terraform

<p align="center"><img align="center" width="40%" height="40%" src="assets/terraform.svg"></p>

[Terraform](https://www.terraform.io/) is an infrastructure-as-code (IaC) software tool created by [HashiCorp](https://www.hashicorp.com/).

## Index

* [Install](#install)
* [Usage](#usage)

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
