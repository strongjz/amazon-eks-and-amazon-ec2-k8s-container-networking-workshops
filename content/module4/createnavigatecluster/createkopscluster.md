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
* Select kops create command for appropriate region:

{{< tabs name="RegionSpecificKopsCreateCommand" >}}
{{{< tab name="Oregon" include="kops-cluster-us-west-2.md" />}}
{{< /tabs >}}

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
