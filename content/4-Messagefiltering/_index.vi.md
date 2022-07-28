---
title : "Message filtering"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

#### Message filtering

Theo mặc định, subscriber topic Amazon SNS nhận được mọi message được xuất bản cho topic. Để nhận được một tập hợp con các message, subscriber phải chỉ định chính sách lọc cho topic đã đăng ký. Chính sách bộ lọc là một đối tượng JSON đơn giản chứa các thuộc tính xác định message nào mà subscriber nhận được.

Khi bạn xuất bản message cho một topic, Amazon SNS sẽ so sánh các thuộc tính message với các thuộc tính trong chính sách bộ lọc cho từng đăng ký của topic. Nếu bất kỳ thuộc tính nào khớp, Amazon SNS sẽ gửi message đến subscriber. Nếu không, Amazon SNS sẽ bỏ qua subscriber mà không gửi message.

Bạn có thể đơn giản hóa việc sử dụng Amazon SNS bằng cách hợp nhất các tiêu chí lọc message vào các topic đã đăng ký của mình. Điều này cho phép bạn giảm tải logic lọc message từ subscriber và logic định tuyến message từ các nhà xuất bản, loại bỏ nhu cầu lọc message bằng cách tạo một topic riêng biệt cho từng điều kiện. Bạn có thể sử dụng một topic duy nhất, phân biệt các message của mình bằng cách sử dụng các thuộc tính. Mỗi subscriber chỉ nhận và xử lý các message được chấp nhận bởi chính sách lọc của nó.

Trong phần này, bạn sẽ tạo hàng đợi SQS mới cho Đơn hàng ở EU và tạo đăng ký cho topic SNS Đơn hàng với chính sách bộ lọc để định tuyến từng thư đến hàng đợi SQS Đơn hàng ở EU. Để chỉ ra Đơn đặt hàng ở EU, bạn sẽ chỉ định một thuộc tính, vị trí, với một giá trị eu-west cho message.

![SQS](/images/4/0000.png?featherlight=false&width=90pc)

1. Truy cập vào giao diện quản trị dịch vụ [**SQS**](https://console.aws.amazon.com/sqs/)

   - Chọn **Create queue**

![SQS](/images/4/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **Create queue**

   - **Name**, nhập **```Orders-EU```**

![SQS](/images/4/0002.png?featherlight=false&width=90pc)

3. Chọn **Create queue**

![SQS](/images/4/0003.png?featherlight=false&width=90pc)

4. Hoàn thành tạo queue.

![SQS](/images/4/0004.png?featherlight=false&width=90pc)

5. Click tab **SNS subscriptions**.
  + Click **Subscribe to Amazon SNS topic**.
  + Click chọn **Orders** topic.
  + Click **Save**

![SQS](/images/4/0005.png?featherlight=false&width=90pc)

6. Truy cập vào giao diện quản trị dịch vụ [**SNS**](https://console.aws.amazon.com/sns/)
  + Click **Topics**.
  + Click chọn **Orders** topic

![SQS](/images/4/0007.png?featherlight=false&width=90pc)

7. Trong giao diện **Orders** tìm  **Orders-EU** SQS queue subscription.

   - Chọn **Orders-EU subscription** và chọn **Edit**

![SQS](/images/4/0008.png?featherlight=false&width=90pc)

8. Trong giao diện chỉnh sửa subscription, thêm **Subscription filter policy**

```
{
  "location": [
    "eu-west"
  ]
}
```

   - Chọn **Save changes**

![SQS](/images/4/0009.png?featherlight=false&width=90pc)

9. Hoàn thành tạo policy. 

![SQS](/images/4/00010.png?featherlight=false&width=90pc)

#### Message 1: No message attributes

1. Sử dụng **Event Generator** để kiểm tra đẩy message.

   - Chọn **Orders**
   - Chọn **PUBLISH EVENT**

![SQS](/images/4/00011.png?featherlight=false&width=90pc)

#### Message 2: Non-present message attributes

2. Trong giao diện **Event Generator**

   - Chọn **Add attribute**
   - Đối với **attribute Type**, chọn **String**
   - **Name**, nhập **```category```**
   - **Value**, nhập **```books```**
   - Chọn **PUBLISH EVENT**, đẩy message đến Orders SNS topic.

![SQS](/images/4/00012.png?featherlight=false&width=90pc)

####  Message 3: Non-matching message attributes

3. Trong giao diện **Event Generator**

   - Đối với **```attribute Type```**, chọn **String**
   - **Name**, nhập **```location```**
   - **Value**, nhập **```us-west```**
   - Chọn **PUBLISH EVENT** đẩy message đến Orders SNS Topic.

![SQS](/images/4/00013.png?featherlight=false&width=90pc)

#### Message 4: Matching message attributes

4.  Trong giao diện **Event Generator**

    - Đối với **```attribute Type```**, chọn **String**
    - **Name**, nhập **```location```**
    - **Value**, nhập **```eu-west```**
    - Chọn **PUBLISH EVENT** đẩy message đến Orders SNS Topic.

![SQS](/images/4/00014.png?featherlight=false&width=90pc)

{{% notice note %}}
Ở bước này chúng ta sẽ generate một message có attribute và value phù hợp với filter policy chúng ta đã thiết lập.
{{% /notice %}}


5. Xác nhận đẩy message thành công.

   - Đối với **Orders-EU** sẽ có 1 **Messages  available** 
   - Đối với **OrdersQueue** sẽ có 4 **Messages  available** 

![SQS](/images/4/00015.png?featherlight=false&width=90pc)

6. Chọn **Orders-EU** và chọn **Actions**. Sau đó, chọn **Purge**

![SQS](/images/4/00016.png?featherlight=false&width=90pc)

