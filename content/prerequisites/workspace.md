---
title: "Cloud9 workspace"
chapter: false
weight: 14
---


{{% notice info %}}
Before you deploy the CloudFormation template, feel free to view it <a href="https://github.com/paavan98pm/cont-net-ws-staging/blob/master/static/yaml/cloud9.yaml" target="_blank">here</a href>."
{{% /notice %}}

<!---
{{% notice tip %}}
Ad blockers, javascript disablers, and tracking blockers should be disabled for
the cloud9 domain, or connecting to the workspace might be impacted.
Cloud9 requires third-party-cookies. You can whitelist the [specific domains]( https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).
{{% /notice %}}
-->

### Launch Cloud9 in the recommended region:
{{< tabs name="Region" >}}
{{{< tab name="Virginia" include="us-east-1.md" />}}
{{{< tab name="Oregon" include="us-west-2.md" />}}
{{{< tab name="Ireland" include="eu-west-1.md" />}}
{{{< tab name="Ohio" include="us-east-2.md" />}}
{{{< tab name="Singapore" include="ap-southeast-1.md" />}}
{{< /tabs >}}


- When the Cloud9 environment comes up, open the AWS Cloud9 service in the console and click the `Open IDE` button as shown below.
![c9open](/images/cloud9open.png)


- Customize the environment by closing the **welcome tab**
and **lower work area**, and opening a new **terminal** tab in the main work area:
![c9before](/images/c9before.png)

- Your workspace should now look like this:
![c9after](/images/c9after.png)
