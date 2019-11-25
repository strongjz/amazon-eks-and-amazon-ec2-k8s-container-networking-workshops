---
title: "Cleanup"
date: 2019-11-24T22:40:27-08:00
weight: 35
pre: "<b>6. </b>"
draft: false
---

### We have completed kops activity, let's delete the kops cluster:

* Delete kops cluster:

```
kops delete cluster kops-cluster.k8s.local --yes
```
```
Expected output:

```

* Verify cluster was deleted:
```
kops get cluster
```
```
Expected output:

```
