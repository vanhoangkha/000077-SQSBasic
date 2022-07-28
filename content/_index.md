---
title : "Building an Event-driven Architecture with SNS and SQS"
date : "`r Sys.Date()`"
weight : 1
chapter : false
---
# Build Even-driven architecture with SNS and SQS

#### Overview

Many customers are choosing to build event-driven application architectures – those in which subscriber or target services automatically perform work in response to events triggered by publisher or source services. This pattern can enable development teams to operate more independently so they can release new features faster, while also making their applications more scalable.

An Amazon SNS topic is a logical access point that acts as a communication channel. A topic lets you group multiple endpoints (such as AWS Lambda, Amazon SQS, HTTP/S, or an email address).

To broadcast the messages of a message-producer system (for example, an e-commerce website) working with multiple other services that require its messages (for example, checkout and fulfilment systems), you can create a topic for your producer system.

![SQS](/images/3/0000.png?featherlight=false&width=90pc)

By default, an Amazon SNS topic subscriber receives every message published to the topic. To receive a subset of the messages, a subscriber must assign a filter policy to the topic subscription. A filter policy is a simple JSON object containing attributes that define which messages the subscriber receives.

When you publish a message to a topic, Amazon SNS compares the message attributes to the attributes in the filter policy for each of the topic's subscriptions. If any of the attributes match, Amazon SNS sends the message to the subscriber. Otherwise, Amazon SNS skips the subscriber without sending the message.

You can simplify your use of Amazon SNS by consolidating your message filtering criteria into your topic subscriptions. This allows you to offload the message filtering logic from subscribers and the message routing logic from publishers, eliminating the need to filter messages by creating a separate topic for each condition. You can use a single topic, differentiating your messages using attributes. Each subscriber receives and processes only the messages accepted by its filter policy.

In this section, you will create a new SQS queue for EU Orders, and create a subscription to the Orders SNS topic with a filter policy to route each message to the EU Orders SQS queue. To indicate EU Orders, you will assign an attribute, location, with a value eu-west to the message.

![SQS](/images/4/0000.png?featherlight=false&width=90pc)

#### Content

1. [Introduction](1-introduce/)
2. [Preparation steps](2-prerequiste/)
3. [Simple Pub/Sub](3-simplesubpub/)
4. [Message Filtering](4-messagefiltering/)
5. [Advanced Message Filtering](5-advancemessage/)
6. [Resource Cleanup](6-cleanup/)