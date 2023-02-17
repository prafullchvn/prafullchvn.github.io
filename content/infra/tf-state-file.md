---
title: 'Terraform State File'
date: 2023-02-17T08:32:10+05:30
draft: true
---

Terraform stores the state of real world resource created in file called terraform state file.
Whenever trying to create the resource it terraform fetches cross checks it against state file. Before doing that it fetches the states from real world i.e. it refreshes the state. It contains the information about all the live resources. It contains all the informtion about the live running resource.
