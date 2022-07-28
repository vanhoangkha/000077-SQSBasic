---
title : "Deploy infrastructure"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Deploy infrastructure

{{% notice note %}}
We will leverage AWS CloudFormation which allows us to deploy the infrastructure. This lab is implemented in Region Singapore.
{{% /notice %}}

1. Implement infrastructure using **CloudFormation**

   - Use [CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/review?stackName=aws-event-driven-architectures-workshop&templateURL=https://aws-event-driven-architecture-workshop-assets.s3.amazonaws.com/master-v2.yaml) to initialize.
   - We will enter the interface as shown.
   - Keep **stack name**
   - Select 2 sections of **Capabilities**
   - Select **Create stack**

![SQS](/images/1/0001.png?featherlight=false&width=90pc)

You can also download the template from the link below.

{{%attachments style="green" title="Related files" pattern=".*\.(yaml)$"/%}}

2. It will take us 10-15 minutes to finish creating the stack.

![SQS](/images/1/0002.png?featherlight=false&width=90pc)

3. Go to the **Output** section of the stack just created.

   - These are the resources we will use to do the lab.

![SQS](/images/1/0003.png?featherlight=false&width=90pc)