---
title: "Cleanup"
date: 2019-11-24T11:51:22-08:00
weight: 22
pre: "<b>3. </b>"
draft: false
---

### In this activity we will perform the clean up by deleting busybox deployment:

{{% notice info %}}
You should be on **k8s-kops-mgmt-cloud9-instance:**
{{% /notice %}}

* Delete busybox applicaiton/deployment:
```
kubectl delete deployment kops-busybox
```
```
Expected output:

ec2-user:~/environment $ kubectl delete deployment kops-busybox
deployment.extensions "kops-busybox" deleted
ec2-user:~/environment $
```

* Verify deployment was deleted:
```
kubectl get deployment
kubectl get pods -n default -o wide
```
```
ec2-user:~/environment $ kubectl get deployment
No resources found.
ec2-user:~/environment $ kubectl get pods -n default -o wide
No resources found.
ec2-user:~/environment $
```
* While pods are being deleted you might see STATUS as Terminating
