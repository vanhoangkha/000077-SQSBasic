---
title : "Clean up resources"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

#### Clean up resources

- Delete OrdersQueue, Order-EU, Order-XL and Order-XL-EU SQS queues.

#### Delete CloudFormation Stack.

1. Access the AWS CloudFormation console at https://console.aws.amazon.com/cloudformation
2. In the CloudFormation interface, select **Stack** then select the stacks related to the lab
3. Select **Delete**
4. Select **Delete stack** to confirm the deletion.