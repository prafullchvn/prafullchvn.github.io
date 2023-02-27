---
title: 'Resource Dependencies in Terraform'
date: 2023-02-22T08:33:07+05:30
draft: false
---

Have you ever wondered how does Terraform knows the order in which to create the resources? When we provision the infra one resource might have depedency on other for e.g. if we have create some resource on azure we need to create resource group first for it and then create the resource under that resource group.

Terraform uses this dependency information to determine the correct order in which to create the different resources. To do so, it creates a dependency graph of all of the resources defined by the configuration

Terraform have two types of depedencies through which it determines the order.

- Implicit Depedency
- Explicity Depedency

# Implicit Depedency

When we use format reference of some resource inside the block of some other resource. Let's take following example

```
resource "azurerm_resource_group" "example" {
  name     = "example-rg"
  location = "West Europe"
}

resource "azurerm_dns_zone" "example" {
  name                = "mydomain.com"
  resource_group_name = azurerm_resource_group.example.name
}
```

Here dns zone is created in resource group 'example'. So Terraform will create the resource group first and then proceeds to create the dns zone. Here terraform will internally determines order such depedency is called implicit depepedency.

# Explicit depedency

Sometimes we need to tell _explicitly_ that this resource should be created after some other resource. Then in that case we can specify property called `depends_on` block which takes list of resource reference which it waits for to be created.

```
resource "azurerm_key_vault_access_policy" "storage" {
  key_vault_id = azurerm_key_vault.example.id
  tenant_id    = data.azurerm_client_config.current.tenant_id
  object_id    = azurerm_storage_account.example.identity.0.principal_id

  key_permissions    = [...]
  secret_permissions = [...]
}

resource "azurerm_key_vault_access_policy" "client" {
  key_vault_id = azurerm_key_vault.example.id
  tenant_id    = data.azurerm_client_config.current.tenant_id
  object_id    = data.azurerm_client_config.current.object_id

  key_permissions    = [...]
  secret_permissions = [...]
}


resource "azurerm_key_vault_key" "example" {
  name         = "tfex-key"
  key_vault_id = azurerm_key_vault.example.id
  key_type     = "RSA"
  key_size     = 2048
  key_opts     = ["decrypt", "encrypt", "sign", "unwrapKey", "verify", "wrapKey"]

  depends_on = [
    azurerm_key_vault_access_policy.client,
    azurerm_key_vault_access_policy.storage,
  ]
}
```

In above example, we need those access policies to be created first before we provision a key in that key vault that depedency is specified using `depends_on` block.

# Reference

[Resource Depedencies](https://developer.hashicorp.com/terraform/tutorials/configuration-language/dependencies)
