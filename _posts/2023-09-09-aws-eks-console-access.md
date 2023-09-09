---
layout: post
title: "accessing eks cluster from aws console"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - AWS
  - EKS
---

In order aws console to access to eks cluster to created

either one of the blow

```sh
kubectl edit configmap aws-auth -n kube-system
```

And add below fields to the same depth as mapRoles

```sh 
mapUsers: |
  - userarn: arn:aws:iam::[account_id]:root
  groups:
  - system:masters

```

or 

`
eksctl create iamidentitymapping --cluster [cluster-name] --arn arn:aws:iam::[account_id]:role/rolename --group system:masters --username admin
`