---
title: "Prepare workspace"
date: 2019-11-22T16:54:52-08:00
weight: 20
pre: "<b>1. </b>"
draft: false
---

{{% notice warning %}}
For this module, you should be on: **k8s-kops-mgmt-cloud9-instance**
{{% /notice %}}

#### Launch Cloud9 console in the recommended region and open cloud9 IDE for k8s-kops-mgmt-cloud9-instance:

{{< tabs name="Region" >}}
{{{< tab name="Virginia" include="../cloud9-us-east-1.md" />}}
{{{< tab name="Oregon" include="../cloud9-us-west-2.md" />}}
{{{< tab name="Ireland" include="../cloud9-eu-west-1.md" />}}
{{{< tab name="Ohio" include="../cloud9-us-east-2.md" />}}
{{{< tab name="Singapore" include="../cloud9-ap-southeast-1.md" />}}
{{< /tabs >}}

### Configure [k8s-kops-mgmt-cloud9-instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:tag:Name=k8s-kops-mgmt-cloud9-instance;sort=desc:launchTime) to create Kops cluster:

1. **Create .kube for kops configuration**
```
mkdir -p $HOME/.kube
```
2. **Create $HOME/kopsCluster folder to store kops related artifacts**
```
mkdir -p $HOME/kopsCluster
```

3. **Export Cloud9 Workspace's role, ID and AMI ID to $HOME/.bash_profile:**
```
echo "export AWS_INSTANCE_IAM_ROLE=$(curl -s http://169.254.169.254/latest/meta-data/iam/security-credentials/)" >> $HOME/.bash_profile

echo "export AWS_INSTANCE_ID=$(ec2-metadata  |grep instance-id | awk -F': ' '{print $2}')" >> $HOME/.bash_profile

echo "export AMI_ID=$(curl -s http://169.254.169.254/latest/meta-data/ami-id)" >> $HOME/.bash_profile
```

4. **Export KUBECONFIG variable used for storing kops cluster configuration to $HOME/.bash_profile:**
```
echo "export KUBECONFIG=$HOME/.kube/config" >> $HOME/.bash_profile
```

5. **Source $HOME/.bash_profile so that we can use the exported variables:**
```
source $HOME/.bash_profile
```

6. **Export kops cluster state to $HOME/.bash_profile:**
```
echo "export KOPS_STATE_STORE=s3://amazon-kops-cluster-state-${AWS_ACCOUNT_ID}-${AWS_REGION}" >> $HOME/.bash_profile
```
7. **Source $HOME/.bash_profile update KOPS_STATE_STORE:**
```
source $HOME/.bash_profile
```

8. **Create Amazon S3 bucket:**
  * Amazon S3 bucket is used for storing kops cluster state:
  * Note: Amazon S3 requires --create-bucket-configuration LocationConstraint=<region> for regions other than us-east-1:
```
aws s3api create-bucket --bucket amazon-kops-cluster-state-${AWS_ACCOUNT_ID}-${AWS_REGION} --region ${AWS_REGION} --create-bucket-configuration LocationConstraint=${AWS_REGION}
```
  * Note: it is strongly recommend versioning your S3 bucket in case you ever need to revert or recover a previous state store:
```
aws s3api put-bucket-versioning --bucket amazon-kops-cluster-state-${AWS_ACCOUNT_ID}-${AWS_REGION} --versioning-configuration Status=Enabled
```

9. **Copy configuration files to $HOME/kopsConfigFiles/:**
```
aws s3 sync s3://net410-workshop-us-west-2/kopsConfigFiles/ $HOME/kopsConfigFiles/
```
