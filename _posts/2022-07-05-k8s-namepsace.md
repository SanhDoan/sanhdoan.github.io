---
title: K8s namespace
author: Sanh Doan
date: 2022-07-05 21:30:00 +0700
categories: [Devops, K8s]
tags: [Devops, K8s]
---

# K8s default namespaces

### kube-system:

- Do NOT create or modify in kube-system
- System processes
- Master and Kubectl processes

### kube-public

- Publicly accessible data

### kube-node-lease

- Heartbeats of nodes, availability of a node

### default

- Resources/Components will be created within this namespace if we do not set namespace when creating

```bash
kubectl create namespace my-namespace
```

<br/>

# Use cases

- Structure your components
- Avoid conflict between teams (order, payment, inventory,...)
- Share services between different environments (database, ELK stack, monitoring,...)
- Access and Resource Limits on Namespaces Level

Persistent volumes, node can't be created within a Namespace

```bash
kubectl api-resources --namespaced=false
```

<br/>

# Create component within a Namespace

```bash
kubectl apply -f my-service.yaml --namespace=my-namespace
```

or but it in .yaml file itself (**recommended**)

```yaml
apiVersion: v1
kind: Service
metadata:
  namespace: my-namespace
```

<br/>

# Change active namespace with `kubens`

1. Install

```bash
brew install kubectx
```

2. Get list

```bash
kubens
```

3. Switch active namespace

```bash
kubens my-namespace
```
