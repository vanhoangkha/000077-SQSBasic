---
title : "Simple pub/sub"
date: 2024-01-01
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

#### Simple pub/sub

{{% notice warning %}}
For the sake of avoiding duplication in the lab, steps such as initializing the **SQS**, **SNS** or **EventGeneratorConfigurationUrl** interfaces will be summarized. In addition, we will perform **SQS** in the lab in the style of **Standard**
{{% /notice %}}

In this lab, you will start by building a simple pub/sub implementation. An Amazon SNS topic will be used to publish events you an Amazon SQS queue subscriber. This will allow you to easily verify the successful delivery of your messages.

An Amazon SNS topic is a logical access point that acts as a communication channel. A topic lets you group multiple endpoints (such as AWS Lambda, Amazon SQS, HTTP/S, or an email address).

To broadcast the messages of a message-producer system (for example, an e-commerce website) working with multiple other services that require its messages (for example, checkout and fulfilment systems), you can create a topic for your producer system.

![SQS](/images/3/0000.png?featherlight=false&width=90pc)

1. Open **AWS Management Console**

   - Find **SQS**
   - Select **SQS**
   - In the **SQS** interface, select **Create queue**

![SQS](/images/3/0001.png?featherlight=false&width=90pc)

{{% notice info %}}
If you have not created an Amazon SQS queue before, you will see the **Simple Queue Service** homepage. Select **Get Started Now**, otherwise click **Create queue** at the top of your queue list
{{% /notice %}}

2. In the **Create queue** interface

   - **Name**, enter **```OrdersQueue```**

![SQS](/images/3/0002.png?featherlight=false&width=90pc)

3. Select **Create queue**

![SQS](/images/3/0003.png?featherlight=false&width=90pc)

4. From **Queue Actions**, select **Subscribe Queue to SNS Topic**

![SQS](/images/3/0004.png?featherlight=false&width=90pc)

{{% notice info %}}
To receive published notifications for a topic, you must subscribe to an endpoint for that topic. In this case, we will register the SQS queue you created in the previous step as the endpoint. When you subscribe to an endpoint for a topic, the endpoint starts receiving published messages for the associated topic.
{{% /notice %}}

5. Select SNS Topic **Orders**.
  + Select **Save**

![SQS](/images/3/0005.png?featherlight=false&width=90pc)

6. Verify **OrdersQueue SQS queue** successfully registered

![SQS](/images/3/0006.png?featherlight=false&width=90pc)

7. Select and view details **Access policy**

![SQS](/images/3/0007.png?featherlight=false&width=90pc)

8. Start message push test with **Event Generator**

   - Select **Orders** topic from the Topics list.
   - Select **PUBLISH EVENT**

![SQS](/images/3/0008.png?featherlight=false&width=90pc)

{{% notice note %}}
You will need to choose the correct Region.
{{% /notice %}}

9. Access to **SQS**

   - Find **OrdersQueue**
   - In the **Messages Available** section, the value is **1**

![SQS](/images/3/0009.png?featherlight=false&width=90pc)

10. Select **Send and receive messages.**

![SQS](/images/3/00010.png?featherlight=false&width=90pc)

11. In the detail screen

    - Select **Poll for messages**

![SQS](/images/3/00011.png?featherlight=false&width=90pc)

12. We will see the columns **ID, Sent, Size, and Receive Count**

![SQS](/images/3/00012.png?featherlight=false&width=90pc)

13. View message details.

![SQS](/images/3/00013.png?featherlight=false&width=90pc)

14. Then we will delete the message

![SQS](/images/3/00014.png?featherlight=false&width=90pc)

15. Delete message successfully.

![SQS](/images/3/00015.png?featherlight=false&width=90pc)

{{% notice tip %}}
The steps in the lab are quite long, so be careful to avoid mistakes. You can learn more about [Pub/sub pattern](https://docs.aws.amazon.com/prescriptive-guidance/latest/modernization-integrating-microservices/pub-sub.html)
{{% /notice %}}