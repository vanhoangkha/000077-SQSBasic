---
title : "Advanced message filtering"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Advanced message filtering

Trong phần trước, bạn đã khám phá tính năng lọc thư cơ bản bằng cách sử dụng so sánh chuỗi và thể hiện hành vi định tuyến SNS bằng cách sử dụng các cấu hình thuộc tính thông báo khác nhau để xác minh việc gửi thông báo. Tiếp theo, bạn sẽ mở rộng về lọc thư cơ bản bằng cách sử dụng các kỹ thuật so sánh bổ sung.


Chúng ta sẽ tạo một Amazon SQS queue là **Orders-XL**

1. Truy cập vào giao diện [SQS](https://console.aws.amazon.com/sqs/home)

   - Chọn **Create New Queue**

![SQS](/images/5/0001.png?featherlight=false&width=90pc)


2. Đối với tên queue nhập **```Orders-XL```**

![SQS](/images/5/0002.png?featherlight=false&width=90pc)

3. Chọn **Create queue**

![SQS](/images/5/0003.png?featherlight=false&width=90pc)

4. Tạo **Orders-XL**

![SQS](/images/5/0004.png?featherlight=false&width=90pc)

5. Click tab **SNS subscriptions**.
  + Click **Subscribe to Amazon SNS topic**.
  + Click chọn **Orders** topic.
  + Click **Save**
  
![SQS](/images/5/0006.png?featherlight=false&width=90pc)

6. Xác thực **Orders-XL SQS queue** thành công subscriber **Orders SNS Topic** và chọn **OK**. 

![SQS](/images/5/0007.png?featherlight=false&width=90pc)

7. Chúng ta sẽ tạo **Orders-XL** subscription filter policy.

   - Truy cập vào **[SNS](https://console.aws.amazon.com/sns/home#/topics)**
   - Chọn **Orders**
   - Trong giao diện **Orders**
   - Tìm **Orders-XL** để tìm **Orders-XL SQS queue subscription**

![SQS](/images/5/0008.png?featherlight=false&width=90pc)

8. Chọn **Orders-XL subscription** và chọn **Edit**

![SQS](/images/5/0009.png?featherlight=false&width=90pc)

9. Thực hiện chỉnh sửa **Subscription filter policy** 

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

10. Hoàn thành chỉnh sửa **Subscription filter policy**

    - Chọn **Save changes**

![SQS](/images/5/00011.png?featherlight=false&width=90pc)

11. Thực hiện tạo tiếp một **Orders-X-EU**. 

    - Truy cập vào **[SQS](https://console.aws.amazon.com/sqs/home)**
    - Chọn **Create queue**

![SQS](/images/5/00012.png?featherlight=false&width=90pc)

12. Nhập **```Orders-XL-EU```** đối với queue name.

![SQS](/images/5/00013.png?featherlight=false&width=90pc)

13. Chọn **Create queue**

![SQS](/images/5/00014.png?featherlight=false&width=90pc)

14. Chọn **Subscribe Queue to SNS Topic.**

![SQS](/images/5/00015.png?featherlight=false&width=90pc)

15. Từ **Choose a Topic**, 

    - Chọn **Orders** topic 
    - Chọn **Save**

![SQS](/images/5/00016.png?featherlight=false&width=90pc)

16. Xác thực **Orders-XL-EU SQS queue** thành công đăng ký **Order SNS Topic**

![SQS](/images/5/00017.png?featherlight=false&width=90pc)

17. Chọn **Orders-XL-EU SQS queue subscription** 

![SQS](/images/5/00018.png?featherlight=false&width=90pc)

18. Chỉnh sửa **Subscription filter policy**

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

19. Hoàn thành chỉnh sửa **Subscription filter policy**

![SQS](/images/5/00020.png?featherlight=false&width=90pc)

#### Message 1: Non-matching numeric message attributes

1. Truy nhập vào **[Event Generator](https://event-generator.awsworkshops.io/#/)**

   - Chọn **Add attribute**
   - **Type**, chọn **Number**
   - **Name**, nhập **```quantity```**
   - **Value**, nhập **```50```**
   - Chọn **PUBLISH EVENT** để đẩy tin nhắn đến **Orders SNS topic.**

![SQS](/images/5/00021.png?featherlight=false&width=90pc)

#### Message 2: Matching numeric message attributes

1. Thay đổi quantity attribute lên **100**. Sau đó, chọn **PUBLISH EVENT** để đẩy tin nhắn đến **Orders SNS topic**

![SQS](/images/5/00022.png?featherlight=false&width=90pc)

#### Message 3: Matching AND comparison message attributes

1. Chúng ta sẽ thêm attribute

   - Chọn **Add attribute**
   - Đối với **Type**, chọn **String**
   - Đối với **Name**, nhập **location**
   - Đối với **Value**, nhập **eu-west**
   - Chọn **PUBLISH EVENT** để đẩy tin nhắn đến **Orders SNS topic.**

![SQS](/images/5/00023.png?featherlight=false&width=90pc)

2. Xác thực các tin nhắn đã được gửi 

   - Truy cập vào [SQS](https://console.aws.amazon.com/sqs/home)
   - Quan sát **Messages Available**:
     + **OrdersQueue**, sẽ có 3 messages bởi vì  **Orders subscription** không lọc tin nhắn theo policy.
     + **Orders-EU** queue sẽ có 1 message bởi vì có một tin nhắn đẩy với **location = eu-west.**
     + **Orders-XL** queue có 2 messages bởi vì có 2 tin nhắn đẩy với **quantity = 100**
     + **Orders-XL-EU** queue sẽ có 1 message bởi vì có 1 tin nhắn đẩy với **quantity = 100 và location = eu-west.**

![SQS](/images/5/00024.png?featherlight=false&width=90pc)

Xin chúc mừng! Bạn đã sử dụng thành công bộ lọc đăng ký để định tuyến các tin nhắn được xuất bản đến đăng ký chủ đề SNS và xác minh rằng nó đã được gửi đến đúng hàng đợi SQS.