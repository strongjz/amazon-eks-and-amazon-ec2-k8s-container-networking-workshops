---
title: "Create an IAM role for your Workspaces"
chapter: false
weight: 10
hidden: true
pre: "<b>1. </b>"
draft: false
---

1. Follow [this deep link to create an IAM role with Administrator access.](https://console.aws.amazon.com/iam/home#/roles$new?step=review&commonUseCase=EC2%2BEC2&selectedUseCase=EC2&policies=arn:aws:iam::aws:policy%2FAdministratorAccess)
2. Confirm that **AWS service** and **EC2** are selected, then click **Next** to view permissions.
![iamstart](/images/iamstart.png)
3. Confirm that **AdministratorAccess** is checked, then click **Next: Tags** to assign tags.
![iamselectpermission](/images/iamselectpermission.png)
4. Take the defaults, and click **Next: Review** to review.
![iamreview](/images/iamreview.png)
5. Enter **amazonk8snetworkshop-admin** for the Name, and click **Create role**.
![createrole](/images/iamrole.png)
