---
title: 'Attributes and Output Values'
date: 2023-02-17T08:57:30+05:30
draft: false
---

TF have capabilities to output the values of resources once they are applied. You can do that using `outout` block. You can use the attributes that is being created to create other resources.

E.g.

```
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

resource "azurerm_dns_zone" "example" {
  name                = "mydomain.com"
  resource_group_name = azurerm_resource_group.example.name
}
```

Here as you can see, first resource group is being created then inside that resource group a DNS zone is being created. Resource group is mensioned by `<resource_type>.<resource_name>.<property>`. You can see what all property are accessible to output block in it's documentation.

# Output block

Syntax

```
output "name-of-resource" {
  value = property-of-resource
}
```

You can save this in file called `outputs.tf`.
