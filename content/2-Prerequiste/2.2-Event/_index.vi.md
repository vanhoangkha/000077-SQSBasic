---
title : "Cài đặt Event Generator"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

#### Cài đặt Event Generator

{{% notice info %}} 
Trong suốt bài lab chúng ta sẽ sử dụng chung một  **EventGeneratorConfigurationUrl** của **Output** stack.
{{% /notice %}}

1. Click chuột phải vào ** EventGeneratorConfigurationUrl **.
  + Click vào **Open link in new tab**.
![SQS](/images/2/0000.png?featherlight=false&width=90pc)

2. Chúng ta sử dụng **EventGeneratorConfigurationUrl** của **Output** stack vừa tạo.

   - Chọn **CONFIGURE COGNITO USER POOL**

![SQS](/images/2/0001.png?featherlight=false&width=90pc)

3. Thực hiện cấu hình 

   - CognitoPassword
   - CognitoUsername
   - Sau đó chọn **Configure**

![SQS](/images/2/0002.png?featherlight=false&width=90pc)



{{% notice note %}}
Nếu thông tin user không chính xác, bạn có thể đã copy dư khoảng trắng cuối thông tin CognitoPassword.
{{% /notice %}}


