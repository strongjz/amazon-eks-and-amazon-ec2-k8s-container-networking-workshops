---
title: "Deploy application"
date: 2019-11-24T11:51:22-08:00
weight: 20
pre: "<b>1. </b>"
draft: true
---

### In this activity we will deploy an application across the cluster:

* Application can be deployed on the cluster:
  * By directly passing arguments to kubectl cli
  * Define resource in a file (yaml or jason format; yaml preferred) and pass file as an argument to kubectl cli.
     * Advantage of using file base approach is it allows to keep track of what's launched and allows to make any changes.

* For this workshop we will deploy busybox application using a configuration file.
  * Configuration files are located on your Cloud9 workspace instance under **$HOME/kopsConfigFiles/**

* We have not created any deployment, so you will not find any resources:
```
kubectl get deployment
```
```
Expected output:

ec2-user:~/environment $ kubectl get deployment
No resources found.
ec2-user:~/environment $
```

* Create busyboxy deployment:
```
kubectl create -f $HOME/kopsConfigFiles/busyboxDeployment.yaml
```
```
Expected output:

ec2-user:~/environment $ kubectl create -f $HOME/kopsConfigFiles/busyboxDeployment.yaml
deployment.apps/kops-busybox created
ec2-user:~/environment $
```

* You should be able to see busybox deployment:
```
kubectl get deployment -o wide
kubectl get replicasets
```
```
Expected output:

ec2-user:~/environment $ kubectl get deployment -o wide
NAME           DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS     IMAGES    SELECTOR
kops-busybox   2         2         2            2           9s    kops-busybox   busybox   app=kops-busybox
ec2-user:~/environment $

ec2-user:~/environment $ kubectl get replicasets
NAME                      DESIRED   CURRENT   READY   AGE
kops-busybox-55cd99b769   2         2         2       1m
ec2-user:~/environment $
```

* It will create **two pods**, one on each worker node:
```
kubectl get pods -n default -o wide
```
```
Expected ouptut:

ec2-user:~/environment $ kubectl get pods -n default -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP           NODE                                         NOMINATED NODE
kops-busybox-55cd99b769-rlgp9   1/1     Running   0          1m    100.96.2.4   ip-10-0-93-45.eu-west-1.compute.internal     <none>
kops-busybox-55cd99b769-s5chn   1/1     Running   0          1m    100.96.1.5   ip-10-0-113-206.eu-west-1.compute.internal   <none>
ec2-user:~/environment $
```
