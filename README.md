# Amazon EKS Container Networking Workshop

This workshop was first delivered at [re:Invent 2019](https://reinvent.awsevents.com/) twice under NET403-R and NET403-R1.

We delivered the workshop in a modularised format where each module helps the individual complete an objective. The description of each module is described below.

The workshop can be delivered using AWS Event Engine at one of the AWS events. Individuals can use their own AWS accounts for the workshop.

#### Module 0: Prerequisites

In this module, users follow environment setup instructions to setup their environments (Event Engine or personal AWS account). The AWS CloudFormation script creates two Cloud9 environments - one for EKS and the other for `kops` cluster.

#### Module 1: Container networking basics

In this module, users gain understanding of the network namespace concept within Linux environment. Users create to Cloud9 terminals to understand how `veth` interfaces are created in a network namespace and subsequently attached to Docker bridge on an EC2 instance with Internet connectivity. This module can be run in either Cloud9 environments - EKS or `kops`.

#### Module 2: Create cluster using `eksctl`

In this module, users create a two-node Amazon EKS cluster within the EKS Cloud9 environment. For Amazon EKS cluster, `[eksctl](https://github.com/weaveworks/eksctl)` is used as it is the recommended CLI for creating EKS clusters.

#### Module 3: Amazon EKS cluster networking

In this module, users access Amazon EKS cluster nodes and run commands against the API server to observe networking configurations using `kubectl` and other tools.

#### Module 4: `kops` cluster networking

In this module, users create a kops cluster and observe networking configuration in the control and data plane using tools available for kops.

#### Module 5: Conclusion

We conclude the workshop with what the workshop delivered through each module to provide a deeper understanding of container networking, EKS and `kops` networking.

## Local testing and contribution:

#### Install Hugo:
On a Mac:

`brew install hugo`

On Linux:
  - Download from the releases page: https://github.com/gohugoio/hugo/releases/tag/v0.46
  - Extract and save the executable to `/usr/local/bin`

#### Clone this repo:
From wherever you checkout repos:
`git clone https://github.com/aws-samples/amazon-eks-and-amazon-ec2-k8s-container-networking-workshops`

#### Clone the theme submodule:
`cd cont-net-ws-staging`

```bash
pushd themes/learn
git submodule init
git submodule update --checkout --recursive
popd
```
Run hugo to generate the site, and point your browser to http://localhost:1313

```bash
hugo serve -D
```
.
