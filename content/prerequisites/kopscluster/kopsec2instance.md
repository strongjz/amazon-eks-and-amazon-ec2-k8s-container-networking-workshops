---
title: "Attach IAM role to your kops Workspace"
chapter: false
weight: 15
pre: "<b>1. </b>"
---

### IAM permission:
The IAM user/role to create the Kubernetes cluster using Kops must have the following permissions:

1. AmazonEC2FullAccess
2. AmazonRoute53FullAccess
3. AmazonS3FullAccess
4. IAMFullAccess
5. AmazonVPCFullAccess

We have already created a new IAM role, let's attach newly created IAM role to your kops workspace:

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:tag:Name=k8s-kops-mgmt-cloud9-instance;instanceState=running,stopped;sort=desc:launchTime)

2. Select the instance, then choose **Actions / Instance Settings / Attach/Replace IAM Role**
![c9instancerole](/images/cloud9kopsinstancerole.png)

1. Choose **amazonk8snetworkshop-admin** from the **IAM Role** drop down, and select **Apply**
![c9attachrole](/images/cloud9kopsattachrole.png)
