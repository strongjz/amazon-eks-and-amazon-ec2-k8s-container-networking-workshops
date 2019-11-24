---
title: "Kops Cluster Information"
date: 2019-11-22T16:54:52-08:00
weight: 22
pre: "<b>2. </b>"
draft: false
---

### Cluster information:

1. Display cluster information:
```
kubectl cluster-info
```
Expected output:
```
something like this
```

2. Get cluster details: cluster and instance group:
```
kops get cluster net410-kops-cluster.k8s.local
```
Expected output:
```
something like this
```

3. Validate cluster state:
```
kops validate cluster net410-kops-cluster.k8s.local
```
Expected output:
```
something like this
```

4. View/Verify cluster node information. You can use option: '-o wide' to see IP address and more:
```
kubectl get nodes
kubectl get nodes -o wide
```
Expected output:
something like this

5. View/Verify cluster pod information. You can use option: '-o wide' to see IP address and more. Since there is application is not deployed yet, you won't see any pods running in default name space:
```
kubectl get pods
kubectl get pods -o wide
```
Expected output:
```
something like this
```

6. For cluster operations, it creates pods in kube-system namespace:
```
kubectl get pods -o wide -n kube-system
```
Expected output:
```
something like this
```
