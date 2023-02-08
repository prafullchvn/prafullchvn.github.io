---
title: 'Nodeport Service in K8'
date: 2023-02-08T15:51:55+05:30
draft: false
---

Here to demonstrate the use of nodeport service we will create some nginx pod and nodeport service to access it.

# Deployment file

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: testing
  template:
    metadata:
      labels:
        app: testing
        for: nodeport-svc
    spec:
      containers:
        - name: nginx
          image: nginx:1.14.2
          ports:
            - containerPort: 80
```

Here we are creating 3 pods with nginx running inside of it. We have exposed port 80 of container.
Nginx service runs by default on port 80 hence port 80.

# Nodeport service

```yml
apiVersion: v1
kind: Service
metadata:
  name: test-nodeport-servie-v1
spec:
  type: NodePort
  selector:
    for: nodeport-svc
  ports:
    - protocol: TCP
      port: 4444
      targetPort: 80
      nodePort: 30002
```

Here we are creating nodeport service to expose a static port on service that is denoted by .spec.ports[0].nodePort.
Point to note that you have fixed set of ips to use from 30000-32768.

About nodeport, this service exposes a static port on each node. Through this port and ip of node we can access the pod abstracted by the service selector.

Internally Nodeport service inturn creates clusterIP service which then binds the pods. Here port 4444 can be assumed of that clusterIP service created fromt their it is traffic is targeted to port 80.
