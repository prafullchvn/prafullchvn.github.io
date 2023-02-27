---
title: 'Provider in Tf'
date: 2023-02-17T08:19:09+05:30
draft: false
---

# TF Provider

- Plugins to interact with various cloud vendors.
- Available in TF registry

# Provider configuration

It is generally stored in root directory of module.

These configuration are global to all files.

```yaml
provider "name-of-provider" {
	# config required by provider
		lias   = "some-alias"
	vaersion = "~>3.0"
}
```

These provider need to be declared in `required_provider` block of `terraform` block.

```yaml
terraform {
required_providers {
mycloud = {
source  = "mycorp/mycloud"
version = "~>1.0"
}
}
}
```

Here mycloud is local name that can be used to refer within module.

use `provider` property refer to which provider to use in resource block

# Provider versioning

| Version Number Arguments | Description                                    |
| ------------------------ | ---------------------------------------------- |
| >= 1.0                   | All version greater than or equal to 1.0       |
| <= 1.0                   | All version less than or equal to 1.0          |
| >= 1.0, <= 2.0           | All version greater than 1.0 and less than 2.0 |
| ~> 1.0                   | All versioi in 1.x range                       |
