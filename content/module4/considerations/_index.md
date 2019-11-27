---
title: "Considerations"
date: 2019-11-24T22:44:22-08:00
weight: 40
pre: "<b>7. </b>"
draft: false
---

* Kubernetes default networking provider, kubenet, is a simple network plugin that works with various cloud providers.
* kubenet is basic and does not many features
* When running kubenet in AWS, you are limited to 50 EC2 instances
  * Route tables are used to configure network traffic between kubernetes node
  * Limited to 50 entries per VPC
  * Please visit [Amazon VPC Limits](https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html) for latest information on limits.
* Cluster cannot be set up in a public-private topology in VPC
  * Public-Private topology uses multiple route tables, kubenet uses only one route table
* Other more advanced features, such as BGP, egress control, and mesh networking, are only available with different CNI providers.
* When it comes to network providers, their are different options. One should choose option that meets their requirements
