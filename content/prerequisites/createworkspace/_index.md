---
title: "Create Cloud9 Workspace"
date: 2019-11-23T22:33:47-08:00
weight: 5
pre: "<b>1. </b>"
draft: false
---

{{% notice info %}}
Before you deploy the CloudFormation template, feel free to view it [here](https://github.com/aws-samples/amazon-eks-and-amazon-ec2-k8s-container-networking-workshops/blob/master/templates/awsk8snetworking-cluster-mgmt-cloud9.yaml)
{{% /notice %}}

<!---
{{% notice tip %}}
Ad blockers, javascript disablers, and tracking blockers should be disabled for
the cloud9 domain, or connecting to the workspace might be impacted.
Cloud9 requires third-party-cookies. You can whitelist the [specific domains]( https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).
{{{< tab name="Virginia" include="us-east-1.md" />}}
{{{< tab name="Ireland" include="eu-west-1.md" />}}
{{{< tab name="Ohio" include="us-east-2.md" />}}
{{{< tab name="Singapore" include="ap-southeast-1.md" />}}
{{{< tab name="Virginia" include="cloud9-us-east-1.md" />}}
{{{< tab name="Ireland" include="cloud9-eu-west-1.md" />}}
{{{< tab name="Ohio" include="cloud9-us-east-2.md" />}}
{{{< tab name="Singapore" include="cloud9-ap-southeast-1.md" />}}
{{% /notice %}}
-->

### Launch Cloud9 in the recommended region:
{{< tabs name="Region" >}}
{{{< tab name="Oregon" include="us-west-2.md" />}}
{{< /tabs >}}


1. When the Cloud9 environment comes up, open the AWS Cloud9 service in the console in the region where you launched your Cloud9 above:

{{< tabs name="Cloud9RegionSpecificConsole" >}}
{{{< tab name="Oregon" include="cloud9-us-west-2.md" />}}
{{< /tabs >}}

2. Click the `Open IDE` button as shown below:
![c9open](/images/cloud9open.png)

3. Customize the environment by closing the **welcome tab**
and **lower work area**: and opening a new **terminal** tab in the main work area:
![c9before](/images/cloud9before.png)
![c9newterminal](/images/cloud9newterminal.png)

4. Your workspace should now look like this:
![c9after](/images/cloud9after.png)
