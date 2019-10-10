---
title: "1. Cluster information from Cloud9"
chapter: false
weight: 21
---


### Cluster Information

1. Amazon EKS cluster consists of 2 worker nodes.

```
aws eks list-clusters
```

2. Describe the cluster

```
aws eks describe-cluster --name <insertclustername>
```

3. Get cluster information through `kubectl`

```
kubectl cluster-info
```

4. Observe worker node details

```
kubectl get node -o wide
```

5. Observe cross-account ENIs from EC2 console

```
aws ec2 describe-network-interfaces --network-interface-ids <insert_ENI_IDs> --region <region>
```

6. 