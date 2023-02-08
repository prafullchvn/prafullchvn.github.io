---
title: 'Yaml in Kubernetes'
date: 2023-02-06T15:43:13+05:30
draft: false
---

# Fields in kubernetes

Example :

```yml
apiVersion: v1
kind: Pod
metadata:
  name: pod-demo
  labels:
    pod-name: yaml-in-k8-tutorial
spec:
  containers:
    - name: nginx-container
      image: nginx
```

## `apiVersion` - String

Depending on what type of resource you are trying to create apiVersion will change.

| Syntax      | Description |
| ----------- | ----------- |
| POD         | v1          |
| Service     | v1          |
| Replica Set | app/v1      |
| Deployment  | app/v1      |

How to choose apiVersion if there are two options available:

- Latest
- Compatiblity
- Depedency

## `kind` - String

It is type of resource that we are trying to create. It can be replica set, deployment, service, job etc.

## `metadata` - Dictionary

It is data about object. This is dictionary. Here you can mension metadata like name, labels. It is little intended to right than it's parent.
Note: `labels` help to identify the pods easily while creating service or other resource. Think of it like already present fields used to identify pod. You are just overriding the details of it with your own.

## `spec` - Dictionary (specification)

Depending on object additional configuration we are going to write to create the resource.

### `containers` in spec - Array/List

In above example, containers is list/array not a dictionary. `-` indicates that this is first item in list.
