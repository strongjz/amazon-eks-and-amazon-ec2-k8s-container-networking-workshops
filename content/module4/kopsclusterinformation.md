---
title: "Kops Cluster Information"
date: 2019-11-22T16:54:52-08:00
weight: 22
pre: "<b>3. </b>"
draft: false
---

### Cluster information:

**1. Display cluster information:**
```
kubectl cluster-info
```
* Expected output:
```
Kubernetes master is running at https://api-kops-cluster-k8s-loca-945gpc-785396473.eu-west-1.elb.amazonaws.com
KubeDNS is running at https://api-kops-cluster-k8s-loca-945gpc-785396473.eu-west-1.elb.amazonaws.com/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

**2. Get cluster details: cluster and instance group:**
```
kops get cluster kops-cluster.k8s.local
```
* Expected output:
```
NAME                    CLOUD   ZONES
kops-cluster.k8s.local  aws     eu-west-1a,eu-west-1b,eu-west-1c
```

**3. Validate cluster state:**
```
kops validate cluster kops-cluster.k8s.local
```
* Expected output:
```
Validating cluster kops-cluster.k8s.local

INSTANCE GROUPS
NAME                    ROLE    MACHINETYPE     MIN     MAX     SUBNETS
master-eu-west-1a       Master  t2.small        1       1       eu-west-1a
nodes                   Node    t2.small        2       2       eu-west-1a,eu-west-1b,eu-west-1c

NODE STATUS
NAME                                            ROLE    READY
ip-10-0-113-206.eu-west-1.compute.internal      node    True
ip-10-0-32-125.eu-west-1.compute.internal       master  True
ip-10-0-93-45.eu-west-1.compute.internal        node    True

Your cluster kops-cluster.k8s.local is ready
```

**4. View/Verify cluster node information:**

* You can use option: '-o wide' to see IP address and more
```
kubectl get nodes
kubectl get nodes -o wide
```
* Expected output:
```
kubectl get nodes:
NAME                                         STATUS   ROLES    AGE   VERSION
ip-10-0-113-206.eu-west-1.compute.internal   Ready    node     7m    v1.11.10
ip-10-0-32-125.eu-west-1.compute.internal    Ready    master   7m    v1.11.10
ip-10-0-93-45.eu-west-1.compute.internal     Ready    node     7m    v1.11.10

kubectl get nodes -o wide:
NAME                                         STATUS   ROLES    AGE   VERSION    INTERNAL-IP    EXTERNAL-IP     OS-IMAGE                       KERNEL-VERSION   CONTAINER-RUNTIME
ip-10-0-113-206.eu-west-1.compute.internal   Ready    node     7m    v1.11.10   10.0.113.206   54.171.116.48   Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
ip-10-0-32-125.eu-west-1.compute.internal    Ready    master   7m    v1.11.10   10.0.32.125    34.241.108.7    Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
ip-10-0-93-45.eu-west-1.compute.internal     Ready    node     7m    v1.11.10   10.0.93.45     34.241.27.75    Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
```

**5. View/Verify cluster pod information:**

* You can use option: '-o wide' to see IP address and more
* Since there is application is not deployed yet, you won't see any pods running in default name space
```
kubectl get pods
kubectl get pods -o wide
```
* Expected output:
```
kubectl get pods:
No resources found.

kubectl get pods -o wide:
No resources found.
```

**6. For cluster operations, it creates pods in kube-system namespace:**
```
kubectl get pods -o wide -n kube-system
```
* Expected output:
```
NAME                                                                READY   STATUS    RESTARTS   AGE   IP             NODE                                         NOMINATED NODE
dns-controller-6bbd657cd7-t97fz                                     1/1     Running   0          11m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
etcd-server-events-ip-10-0-32-125.eu-west-1.compute.internal        1/1     Running   0          11m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
etcd-server-ip-10-0-32-125.eu-west-1.compute.internal               1/1     Running   0          11m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
kube-apiserver-ip-10-0-32-125.eu-west-1.compute.internal            1/1     Running   0          11m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
kube-controller-manager-ip-10-0-32-125.eu-west-1.compute.internal   1/1     Running   0          10m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
kube-dns-6b4f4b544c-8fbrm                                           3/3     Running   0          11m   100.96.1.2     ip-10-0-113-206.eu-west-1.compute.internal   <none>
kube-dns-6b4f4b544c-8nmpp                                           3/3     Running   0          10m   100.96.2.2     ip-10-0-93-45.eu-west-1.compute.internal     <none>
kube-dns-autoscaler-6b658bd4d5-cctz5                                1/1     Running   0          11m   100.96.1.3     ip-10-0-113-206.eu-west-1.compute.internal   <none>
kube-proxy-ip-10-0-113-206.eu-west-1.compute.internal               1/1     Running   0          10m   10.0.113.206   ip-10-0-113-206.eu-west-1.compute.internal   <none>
kube-proxy-ip-10-0-32-125.eu-west-1.compute.internal                1/1     Running   0          11m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
kube-proxy-ip-10-0-93-45.eu-west-1.compute.internal                 1/1     Running   0          10m   10.0.93.45     ip-10-0-93-45.eu-west-1.compute.internal     <none>
kube-scheduler-ip-10-0-32-125.eu-west-1.compute.internal            1/1     Running   0          11m   10.0.32.125    ip-10-0-32-125.eu-west-1.compute.internal    <none>
```
