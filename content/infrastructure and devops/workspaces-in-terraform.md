---
title: 'Workspaces in Terraform'
date: 2023-02-22T16:17:28+05:30
draft: false
---

Workspaces in terraform gives us freedom to have same infrastructure for different environment with different values.

You can interact with workspaces in terraform using following commands

For help

> terraform workspace -h

To view all workspaces

> terraform workspace show

To select workspace

> terraform workspace select <workspace>

# Using variables based on Environment

```
resource "aws_instance" "myec2"{
  ami           = "something random"
  instance_type = lookup(var.instance_type,terraform.workspace)
}

variable "instance_type" {
  type  = "map"
  default = {
    default = 't2.nano'
    dev     = 't2.micro'
    prd     = 't2.large'
  }
}
```

Here instance_type is selected based on workspace which is currently active. In order to select that we are using lookup function. For more on lookup function refer to link given in reference. Using the workspacesk creates different tfstate files which are stored in directory `terraform.tfstate.d` inside that separate directory for each environment.

# Reference to function

[lookup function](https://developer.hashicorp.com/terraform/language/functions/lookup)
