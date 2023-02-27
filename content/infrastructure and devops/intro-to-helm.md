---
title: 'Intro to Helm'
date: 2023-02-24T09:05:31+05:30
draft: true
---

Helm acts like package manager for kubernetes. Kubernetes at its core doesn't care about application as whole. It just cares that all the deployment told to it are up and running. But for us creating those resources one by one and applying them is tedious job especially in case of application with various resources such as ConfigMap, Secretes, Services etc.

Suppose you have to create resources for wordpress

> helm install wordpress

> helm upgrade wordpress

> helm rollback wordpress

> helm unistall wordpress
