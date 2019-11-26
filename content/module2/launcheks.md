---
title: "Launch EKS"
date: 2018-08-07T13:34:24-07:00
weight: 20
pre: "<b>2. </b>"
---


{{% notice warning %}}
**DO NOT PROCEED** with this step unless you have [validated the IAM role](/prerequisites/workspaceiam/#validate-the-iam-role) in use by the Cloud9 IDE. You will not be able to run the necessary kubectl commands in the later modules unless the EKS cluster is built using the IAM role.
{{% /notice %}}

#### Challenge:
**How do I check the IAM role on the workspace?**

{{%expand "Expand here to see the solution" %}}
Run `aws sts get-caller-identity` and validate that your _Arn_ contains `networkshop-admin` or `TeamRole`
(or the role created when starting the workshop) and an Instance Id.

```output
{
    "Account": "123456789012",
    "UserId": "AROA1SAMPLEAWSIAMROLE:i-01234567890abcdef",
    "Arn": "arn:aws:sts::123456789012:assumed-role/networkshop-admin/i-01234567890abcdef"
}
or
{
    "Account": "123456789012",
    "UserId": "AROA1SAMPLEAWSIAMROLE:i-01234567890abcdef",
    "Arn": "arn:aws:sts::123456789012:assumed-role/TeamRole/i-01234567890abcdef"
}
```

If you do not see the correct role, please go back and [validate the IAM role](/prerequisites/workspaceiam/#validate-the-iam-role) for troubleshooting.

If you do see the correct role, proceed to next step to create an EKS cluster.
{{% /expand %}}

### Create an EKS cluster
```
eksctl create cluster --name=networkshop-eksctl --nodes=2 --region=${AWS_REGION} --ssh-public-key=eksnetworkshop
```

{{% notice info %}}
Launching EKS and all the dependencies will take approximately 15-20 minutes.

Note that we use the ssh key created in [Prerequisites Section 0.2.4](/prerequisites/ekscluster/ekssshkey/)
{{% /notice %}}
