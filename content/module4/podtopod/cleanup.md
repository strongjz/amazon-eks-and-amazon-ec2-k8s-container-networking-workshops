---
title: "Cleanup"
date: 2019-11-24T11:51:22-08:00
weight: 21
pre: "<b>2. </b>"
draft: true
---

### In this activity we will perform the clean up by deleting simple-http-server and simple-client deployment:

{{% notice info %}}
You should be on **k8s-kops-mgmt-cloud9-instance:**
{{% /notice %}}

* Delete simple-http-server and simple-client deployment:
```
kubectl delete deployment simple-http-server
kubectl delete deployment simple-client
```
```
Expected output:

ec2-user:~/environment $ kubectl delete deployment simple-http-server
deployment.extensions "simple-http-server" deleted
ec2-user:~/environment $ kubectl delete deployment simple-client
deployment.extensions "simple-client" deleted
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
