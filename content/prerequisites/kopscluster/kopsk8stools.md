---
title: "Install Kubernetes Tools"
chapter: false
weight: 17
pre: "<b>3. </b>"
---

Creating kubernetes cluster using kops require kubectl, kops and kubelet binaries and aws-cli

{{% notice tip %}}
In this workshop we will give you the commands to download the Linux binaries.
{{% /notice %}}

#### Install kubectl:
```
sudo curl --silent --location -o /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v1.13.7/bin/linux/amd64/kubectl


sudo chmod +x /usr/local/bin/kubectl
```

#### Install kops:
```
wget https://github.com/kubernetes/kops/releases/download/1.10.0/kops-linux-amd64

chmod +x kops-linux-amd64

sudo mv kops-linux-amd64 /usr/local/bin/kops
```

#### Install JQ and envsubst:
```
sudo yum -y install jq gettext
```

#### Verify the binaries are in the path and executable:
```
for command in kubectl kops jq envsubst
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```

#### Enable bash_completion for kubectl and kops:
```
kubectl completion bash >> ~/.bash_completion
kops completion bash >> ~/.bash_completion
```
