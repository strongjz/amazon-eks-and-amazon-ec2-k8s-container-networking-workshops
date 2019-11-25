---
title: "Create kubernetes cluster using kops"
date: 2019-11-22T16:54:52-08:00
weight: 20
pre: "<b>1. </b>"
draft: false
---

### Create cluster:

**1. Create a cluster:**

* In public subnet
* With one master node and two worker nodes across two availability zones
* It creates a new VPC and all the required AWS resources
```
kops create cluster \
  --name=kops-cluster.k8s.local \
  --master-count=1 \
  --master-size=t2.small \
  --node-count=2 \
  --node-size=t2.small \
  --network-cidr=10.0.0.0/16 \
  --zones=eu-west-1a,eu-west-1b,eu-west-1c \
  --ssh-public-key=~/.ssh/id_rsa.pub \
  --networking=kubenet
```

**2. Verify cluster creation:**

```
kops get cluster
```

**3. Once cluster is created, deploy/update cluster:**
```
kops update cluster kops-cluster.k8s.local --yes
```

{{% notice info %}}
**Launching cluster and all the dependencies will take approximately 10 minutes**
{{% /notice %}}
