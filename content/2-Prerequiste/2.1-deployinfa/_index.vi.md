---
title : "Triển khai hạ tầng"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Triển khai hạ tầng 

{{% notice note %}} 
Chúng ta sẽ tận dụng AWS CloudFormation cho phép chúng ta triển khai cơ sở hạ tầng. Bài lab này triển khai ở Region Singapore.
{{% /notice %}}

1. Thực hiện triển khai hạ tầng bằng **CloudFormation**

   - Sử dụng [CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/review?stackName=aws-event-driven-architectures-workshop&templateURL=https://aws-event-driven-architecture-workshop-assets.s3.amazonaws.com/master-v2.yaml) sau để khởi tạo.
   - Chúng ta sẽ vào giao diện như hình.
   - Giữ nguyên **stack name**
   - Chọn 2 phần của **Capabilities**
   - Chọn **Create stack**

![SQS](/images/1/0001.png?featherlight=false&width=90pc)

Ngoài ra bạn cũng có thể download template ở link dưới.

{{%attachments style="green" title="Related files" pattern=".*\.(yaml)$"/%}}

2. Chúng ta sẽ mất 10-15 phút để hoàn thành tạo stack.

![SQS](/images/1/0002.png?featherlight=false&width=90pc)

3. Vào mục **Output** của stack vừa tạo.

   - Đây là những tài nguyên chúng ta sẽ sử dụng để thực hiện bài lab.

![SQS](/images/1/0003.png?featherlight=false&width=90pc)


