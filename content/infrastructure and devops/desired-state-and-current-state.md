---
title: 'Desired State and Current State'
date: 2023-02-17T08:45:49+05:30
draft: false
---

# Desired state

One of the primary funciton of Terraform is to create real world resource that is described in Terraform Configuration file.

# Current state

This is state of currently running resource.

Terraform tries to match the desired state mensioned in TF configuration file. So if any property that is mensioned in TF state file is manually changed, TF will try to change it to match the desired state. Note: _If some property that is not mensioned in TF configuration is changed then TF won't try to change it because it is not configured in configuratio file._
