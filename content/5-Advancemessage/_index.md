---
title : "Advanced message filtering"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Advanced message filtering

In the previous section, you explored basic message filtering using string comparisons and demonstrated SNS routing behavior using different message property configurations to verify message delivery. Next, you'll expand on basic message filtering using additional comparison techniques.


We will create an Amazon SQS queue as **Orders-XL**

1. Access the interface [SQS](https://console.aws.amazon.com/sqs/home)

   - Select **Create New Queue**

![SQS](/images/5/0001.png?featherlight=false&width=90pc)


2. For queue name enter **```Orders-XL```**

![SQS](/images/5/0002.png?featherlight=false&width=90pc)

3. Select **Create queue**

![SQS](/images/5/0003.png?featherlight=false&width=90pc)

4. Create **Orders-XL**

![SQS](/images/5/0004.png?featherlight=false&width=90pc)

5. Click the **SNS subscriptions** tab.
  + Click **Subscribe to Amazon SNS topic**.
  + Click on **Orders** topic.
  + Click **Save**

![SQS](/images/5/0006.png?featherlight=false&width=90pc)

6. Verify **Orders-XL SQS queue** successfully subscriber **Orders SNS Topic** and select **OK**.

![SQS](/images/5/0007.png?featherlight=false&width=90pc)

7. We will create the **Orders-XL** subscription filter policy.

   - Go to **[SNS](https://console.aws.amazon.com/sns/home#/topics)**
   - Select **Orders**
   - In the **Orders** interface
   - Search **Orders-XL** to find **Orders-XL SQS queue subscription**

![SQS](/images/5/0008.png?featherlight=false&width=90pc)

8. Select **Orders-XL subscription** and select **Edit**

![SQS](/images/5/0009.png?featherlight=false&width=90pc)

9. Make edits **Subscription filter policy**

```
{
  "quantity": [
    {
      "numeric": [ ">=", 100 ]
    }
  ]
}
```

![SQS](/images/5/00010.png?featherlight=false&width=90pc)

10. Finish editing **Subscription filter policy**

    - Select **Save changes**

![SQS](/images/5/00011.png?featherlight=false&width=90pc)

11. Make another **Orders-X-EU**.

    - Go to **[SQS](https://console.aws.amazon.com/sqs/home)**
    - Select **Create queue**

![SQS](/images/5/00012.png?featherlight=false&width=90pc)

12. Enter **```Orders-XL-EU```** for the queue name.

![SQS](/images/5/00013.png?featherlight=false&width=90pc)

13. Select **Create queue**

![SQS](/images/5/00014.png?featherlight=false&width=90pc)

14. Select **Subscribe Queue to SNS Topic.**

![SQS](/images/5/00015.png?featherlight=false&width=90pc)

15. From **Choose a Topic**,

    - Select **Orders** topic
    - Select **Save**

![SQS](/images/5/00016.png?featherlight=false&width=90pc)

16. Confirmation **Orders-XL-EU SQS queue** successfully registered **Order SNS Topic**

![SQS](/images/5/00017.png?featherlight=false&width=90pc)

17. Select **Orders-XL-EU SQS queue subscription**

![SQS](/images/5/00018.png?featherlight=false&width=90pc)

18. Edit **Subscription filter policy**

```
{
  "location": [
    { "prefix": "eu" }
  ],
  "quantity": [
    {
      "numeric": [ ">=", 100 ]
    }
  ]
}

```

![SQS](/images/5/00019.png?featherlight=false&width=90pc)

19. Finish editing **Subscription filter policy**

![SQS](/images/5/00020.png?featherlight=false&width=90pc)

#### Message 1: Non-matching numeric message attributes

1. Go to **[Event Generator](https://event-generator.awsworkshops.io/#/)**

   - Select **Add attribute**
   - **Type**, select **Number**
   - **Name**, enter **```quantity```**
   - **Value**, enter **```50```**
   - Select **PUBLISH EVENT** to push messages to **Orders SNS topic.**

![SQS](/images/5/00021.png?featherlight=false&width=90pc)

#### Message 2: Matching numeric message attributes

1. Change quantity attribute to **100**. Then select **PUBLISH EVENT** to push the message to **Orders SNS topic**

![SQS](/images/5/00022.png?featherlight=false&width=90pc)

#### Message 3: Matching AND comparison message attributes

1. We will add the attribute

   - Select **Add attribute**
   - For **Type**, choose **String**
   - For **Name**, enter **location**
   - For **Value**, enter **eu-west**
   - Select **PUBLISH EVENT** to push messages to **Orders SNS topic.**

![SQS](/images/5/00023.png?featherlight=false&width=90pc)

2. Verify sent messages

   - Go to [SQS](https://console.aws.amazon.com/sqs/home)
   - Observe **Messages Available**:
     + **OrdersQueue**, there will be 3 messages because **Orders subscription** does not filter messages by policy.
     + **Orders-EU** queue will have 1 message because there is a push message with **location = eu-west.**
     + **Orders-XL** queue has 2 messages because there are 2 push messages with **quantity = 100**
     + **Orders-XL-EU** queue will have 1 message because there is 1 push message with **quantity = 100 and location = eu-west.**

![SQS](/images/5/00024.png?featherlight=false&width=90pc)

Congratulations! You have successfully used the subscription filter to route published messages to the SNS topic subscription and verified that it was delivered to the correct SQS queue.
