---
title: "Attach IAM role to your EKS Workspace"
chapter: false
weight: 15
pre: "<b>1. </b>"
---

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:tag:Name=k8s-eks-mgmt-cloud9-instance;instanceState=running,stopped;sort=desc:launchTime)
2. Select the instance, then choose **Actions / Instance Settings / Attach/Replace IAM Role**
![c9instancerole](/images/cloud9instancerole.png)
3. Choose **amazonk8snetworkshop-admin** from the **IAM Role** drop down, and select **Apply**
![c9attachrole](/images/cloud9attachrole.png)
