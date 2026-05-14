---
title : "Message filtering"
date: 2024-01-01
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

#### Message filtering

By default, an Amazon SNS topic subscriber receives every message published to the topic. To receive a subset of the messages, a subscriber must assign a filter policy to the topic subscription. A filter policy is a simple JSON object containing attributes that define which messages the subscriber receives.

When you publish a message to a topic, Amazon SNS compares the message attributes to the attributes in the filter policy for each of the topic's subscriptions. If any of the attributes match, Amazon SNS sends the message to the subscriber. Otherwise, Amazon SNS skips the subscriber without sending the message.

You can simplify your use of Amazon SNS by consolidating your message filtering criteria into your topic subscriptions. This allows you to offload the message filtering logic from subscribers and the message routing logic from publishers, eliminating the need to filter messages by creating a separate topic for each condition. You can use a single topic, differentiating your messages using attributes. Each subscriber receives and processes only the messages accepted by its filter policy.

In this section, you will create a new SQS queue for EU Orders, and create a subscription to the Orders SNS topic with a filter policy to route each message to the EU Orders SQS queue. To indicate EU Orders, you will assign an attribute, location, with a value eu-west to the message.

![SQS](/images/4/0000.png?featherlight=false&width=90pc)

1. Access to [**SQS**](https://console.aws.amazon.com/sqs/)

   - Select **Create queue**

![SQS](/images/4/0001.png?featherlight=false&width=90pc)

2. In the **Create queue** interface

   - **Name**, enter **```Orders-EU```**

![SQS](/images/4/0002.png?featherlight=false&width=90pc)

3. Select **Create queue**

![SQS](/images/4/0003.png?featherlight=false&width=90pc)

4. Finish creating a queue.

![SQS](/images/4/0004.png?featherlight=false&width=90pc)


5. Click the **SNS subscriptions** tab.
  + Click **Subscribe to Amazon SNS topic**.
  + Click on **Orders** topic.
  + Click **Save**

![SQS](/images/4/0005.png?featherlight=false&width=90pc)


6. Access the service administration interface [**SNS**](https://console.aws.amazon.com/sns/)
  + Click **Topics**.
  + Click on **Orders** topic
  
![SQS](/images/4/0007.png?featherlight=false&width=90pc)

7. In the **Orders** interface find **Orders-EU** SQS queue subscription.

   - Select **Orders-EU subscription** and select **Edit**

![SQS](/images/4/0008.png?featherlight=false&width=90pc)

8. In the subscription editing interface, add **Subscription filter policy**

```
{
  "location": [
    "eu-west"
  ]
}
```

   - Select **Save changes**

![SQS](/images/4/0009.png?featherlight=false&width=90pc)

9. Complete policy creation.

![SQS](/images/4/00010.png?featherlight=false&width=90pc)

#### Message 1: No message attributes

1. Use **Event Generator** to test push messages.

   - Select **Orders**
   - Select **PUBLISH EVENT**

![SQS](/images/4/00011.png?featherlight=false&width=90pc)

#### Message 2: Non-present message attributes

2. In the **Event Generator** interface

   - Select **Add attribute**
   - For **attribute Type**, choose **String**
   - **Name**, enter **```category```**
   - **Value**, enter **```books```**
   - Select **PUBLISH EVENT**, push message to Orders SNS topic.

![SQS](/images/4/00012.png?featherlight=false&width=90pc)

#### Message 3: Non-matching message attributes

3. In the **Event Generator** interface

   - For **```attribute Type```**, select **String**
   - **Name**, enter **```location```**
   - **Value**, enter **```us-west```**
   - Select **PUBLISH EVENT** to push messages to Orders SNS Topic.

![SQS](/images/4/00013.png?featherlight=false&width=90pc)

#### Message 4: Matching message attributes

4. In the **Event Generator** interface

    - For **```attribute Type```**, select **String**
    - **Name**, enter **```location```**
    - **Value**, enter **```eu-west```**
    - Select **PUBLISH EVENT** to push messages to Orders SNS Topic.

![SQS](/images/4/00014.png?featherlight=false&width=90pc)

{{% notice note %}}
In this step we will generate a message with attributes and values ​​that match the filter policy we have set.
{{% /notice %}}

5. Confirm push message successfully.

   - For **Orders-EU** there will be 1 **Messages available**
   - For **OrdersQueue** there will be 4 **Messages available**

![SQS](/images/4/00015.png?featherlight=false&width=90pc)

6. Select **Orders-EU** and select **Actions**. Then select **Purge**

![SQS](/images/4/00016.png?featherlight=false&width=90pc)