+++
title = "Module 4: Kops Cluster Networking"
date = 2019-11-20T23:32:35-08:00
weight = 35
chapter = true
pre = "<b>4. </b>"
+++

### Module 4: Kubernetes Cluster using Kops

# Introduction

[Kops](https://github.com/kubernetes/kops/blob/master/README.md), short for Kubernetes Operations, is a set of tools for installing, operating, and deleting Kubernetes clusters from the command line. A rolling upgrade of an older version of Kubernetes to a new version can also be performed. It also manages the cluster add-ons. It is supported on AWS and is another widely used tool to create Kubernetes cluster on AWS

# Objective:

<div style="text-align: left">Dive deep into networking construct of kubernetes cluster on Amazon EC2 created using Kops. In this module, we will:</div>

* Create kubernetes cluster using Kops
* Deploy application across the cluster
* Understand packet flow for Pod-to-Pod communication
* Understand concepts and limitations

{{% notice warning %}}
For this module, you should be on: **k8s-kops-mgmt-cloud9-instance**
{{% /notice %}}

#### Launch Cloud9 console in the recommended region and open cloud9 IDE for k8s-kops-mgmt-cloud9-instance:

{{< tabs name="Cloud9RegionSpecificConsole" >}}
{{{< tab name="Oregon" include="cloud9-us-west-2.md" />}}
{{< /tabs >}}
