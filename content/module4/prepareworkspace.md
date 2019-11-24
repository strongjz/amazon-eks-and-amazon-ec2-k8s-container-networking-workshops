---
title: "Prepare Workspace"
date: 2019-11-22T16:54:52-08:00
weight: 20
pre: "<b>1. </b>"
draft: false
---

{{% notice warning %}}
Before you begin, verify you are on:**[k8s-kops-mgmt-cloud9-instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:tag:Name=k8s-kops-mgmt-cloud9-instance;sort=desc:launchTime)**
{{% /notice %}}

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

<!--
# create /home/ec2-user/bin for packages to install
mkdir -p /home/ec2-user/bin
# change ownership for /home/ec2-user/
# chown ec2-user:ec2-user -R /home/ec2-user/
# change pwd to /home/ec2-user/bin
cd /home/ec2-user/bin
echo "# net410-workshop specific environment variables:" >> /home/ec2-user/.bash_profile
# set GOPATH env variable: https://github.com/golang/go/wiki/SettingGOPATH#bash
echo "export GOPATH=/home/ec2-user/go" >> /home/ec2-user/.bash_profile

# export AWS account id, used to create unique s3 bucket:
export AWS_ACCOUNT_ID=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document |grep accountId |awk -F': ' '{print $2}')
echo "export AWS_ACCOUNT_ID=$(sed -e 's/"//g' -e 's/,$//' <<< "$AWS_ACCOUNT_ID")" >> /home/ec2-user/.bash_profile
# export default AWS region ami is instantiated in:
echo "export AWS_DEFAULT_REGION=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document/ | grep region | awk -F' : ' '{print $2}' | sed 's/"//g' | sed 's/,//g')" >> /home/ec2-user/.bash_profile
# export public key that was assigned to ec2 instance:
# this key is used to create kops cluster:
export PUBKEY=$(ec2-metadata |grep ssh-rsa)
export PUBKEYNAME=$(ec2-metadata |grep keyname | awk -F':' '{print $2}')
echo "export PUBKEYNAME=$(ec2-metadata |grep keyname | awk -F':' '{print $2}')" >> /home/ec2-user/.bash_profile
echo $PUBKEY > /home/ec2-user/.ssh/$PUBKEYNAME.pub
# configure default region for AWS CLI:
# it does not require access and secret, it uses the token.
echo "[default]" >> /home/ec2-user/.aws/config
echo "region = ${AWS_DEFAULT_REGION}" >> /home/ec2-user/.aws/config
# download kops and make it executable:
wget -O kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
# download kubectl and make it executable:
wget -O kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
# retrieve kops cluster configuration file from s3
wget https://s3-${AWS_DEFAULT_REGION}.amazonaws.com/net410-workshop-${AWS_DEFAULT_REGION}/kops/net410-kops-cluster-${AWS_DEFAULT_REGION}.yaml --output-document=/home/ec2-user/kopsCluster/net410-kops-cluster-${AWS_DEFAULT_REGION}.yaml
# insert public key for kops cluster creation:
sed -i 's*  publicKey:*  publicKey: "'"$PUBKEY"'"*g' /home/ec2-user/kopsCluster/net410-kops-cluster-${AWS_DEFAULT_REGION}.yaml
# create kops cluster:
kops create -f /home/ec2-user/kopsCluster/net410-kops-cluster-${AWS_DEFAULT_REGION}.yaml
# deploy/update cluster:
kops update cluster net410-kops-cluster.k8s.local --yes
# change ownership for /home/ec2-user/
chown -R ec2-user:ec2-user /home/ec2-user/
-->
