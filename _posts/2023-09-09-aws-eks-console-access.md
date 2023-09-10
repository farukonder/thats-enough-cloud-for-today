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

after creating EKS cluster, granded user the one created the cluster only. in order the console user other then creator of the cluster to see the details, need to be granted specifiacally. below code allow every aws console user granded to kubernetes. be careful its not for production purpose.  ready only role need to be created for real case. 

either one of the below

 - option 1

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

 - option 2

```sh 
eksctl create iamidentitymapping --cluster [cluster-name] --arn arn:aws:iam::[account_id]:role/rolename --group system:masters --username admin
```