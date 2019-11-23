---
title: "Attach the IAM role to your EKS Workspace"
chapter: false
weight: 15
pre: "<b>1. </b>"
---

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:tag:Name=k8s-eks-mgmt-cloud9-instance;sort=desc:launchTime)
1. Select the instance, then choose **Actions / Instance Settings / Attach/Replace IAM Role**
![c9instancerole](/images/c9instancerole.png)
1. Choose **eksworkshop-admin** from the **IAM Role** drop down, and select **Apply**
![c9attachrole](/images/c9attachrole.png)
