---
title: 'Modules in Terraform'
date: 2023-02-22T08:34:41+05:30
draft: false
---

You can reuse the block of terraform configuration code used to create part of infrastructure instead of writing new one. This will initialise that module in your current project.

Syntax -

```
module "name-of-module" {
  source = "path/to/module"
}
```

While initialising project using `terraform init` this will download the module.

# Using the variables in module

In order to make the module more flexible you can parameterise the values of configuration.

Syntax -

```
module "name-of-module" {
  source = "path/to/module"
  parameter = var.var_name_used_in_module
}
```

# Using locals in module

Sometimes we want to take advantage of using varibles in module but don't want user to override the changes. In such case we can make use of local variables. Disadvantage with above method is that user is able to override the variable.

Syntax -

```
locals {
  variable = value
}

resource "some-random-rs" {
  property = local.variable
}
```
