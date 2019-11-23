---
title: "Module 3: Amazon EKS Cluster Networking"
chapter: true
weight: 30
pre: "<b>3. </b>"
---

## Objectives:

* Examine major components of AWS VPC routed CNI and demonstrate how it handles traffic for:
	* Pod to Pod communication
	* Pod to Service communication
* Examine  the communication channels between Amazon EKS Kubernetes Control Plane and Customer worker nodes.

## Overview
* Perform intra-node Pod to Pod communication and exam the major components involved in the life of a ping packet
* Perform inter-node Pod to Pod communication and exam the major components involved in the life of a ping packet
* Exam the IPtable for kubernete services
