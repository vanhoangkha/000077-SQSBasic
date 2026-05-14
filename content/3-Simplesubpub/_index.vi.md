---
title : "Simple pub/sub"
date: 2024-01-01
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

#### Simple pub/sub

{{% notice warning %}}
Vì lý do tránh trùng lặp trong bài lab, các bước  như khởi tạo giao diện **SQS**, **SNS** hay **EventGeneratorConfigurationUrl** sẽ được tóm lược. Ngoài ra chúng ta sẽ thực hiện **SQS** trong lab theo kiểu **Standard**
{{% /notice %}}

Trong phần lab này, bạn sẽ bắt đầu bằng cách xây dựng, triển khai một pub/sub đơn giản. Một **Amazon SNS Topic** sẽ được sử dụng để xuất bản các sự kiện mà bạn là người đăng ký hàng đợi Amazon SQS. Điều này sẽ cho phép bạn dễ dàng xác minh việc gửi thư thành công.

Amazon SNS Topic là một điểm truy cập hợp lý hoạt động như một kênh giao tiếp. Một Topic cho phép bạn nhóm nhiều endpoint (chẳng hạn như AWS Lambda, Amazon SQS, HTTP/S hoặc một địa chỉ email).

Để phát thông điệp của hệ thống nhà sản xuất thông điệp (ví dụ: một trang web thương mại điện tử) làm việc với nhiều dịch vụ khác yêu cầu thông điệp của nó (ví dụ: hệ thống thanh toán và thực hiện), bạn có thể tạo một topic cho hệ thống nhà sản xuất của mình.

![SQS](/images/3/0000.png?featherlight=false&width=90pc)

1. Mở **AWS Management Console** 

   - Tìm **SQS**
   - Chọn **SQS**
   - Trong giao diện **SQS**, chọn **Create queue** 

![SQS](/images/3/0001.png?featherlight=false&width=90pc)

{{% notice info %}}
Nếu bạn chưa tạo hàng đợi Amazon SQS trước đây, bạn sẽ thấy trang chủ **Simple Queue Service**. Chọn **Get Started Now**, nếu không, hãy nhấp vào **Create queue** ở đầu danh sách hàng đợi của bạn
{{% /notice %}}

2. Trong giao diện **Create queue**

   - **Name**, nhập **```OrdersQueue```**

![SQS](/images/3/0002.png?featherlight=false&width=90pc)

3. Chọn **Create queue**

![SQS](/images/3/0003.png?featherlight=false&width=90pc)

4. Từ **Queue Actions**, chọn **Subscribe Queue to SNS Topic**

![SQS](/images/3/0004.png?featherlight=false&width=90pc)

{{% notice info %}}
Để nhận message được xuất bản cho một topic, bạn phải đăng ký một endpoint cho topic đó. Trong trường hợp này, chúng ta sẽ đăng ký hàng đợi SQS mà bạn đã tạo ở bước trước làm endpoint. Khi bạn đăng ký một endpoint cho một topic, endpoint bắt đầu nhận các message được xuất bản cho topic được liên kết.
{{% /notice %}}

5. Chọn SNS Topic **Orders**.
  + Chọn **Save**

![SQS](/images/3/0005.png?featherlight=false&width=90pc)

6. Xác thực **OrdersQueue SQS queue** đăng ký thành công 

![SQS](/images/3/0006.png?featherlight=false&width=90pc)

7. Chọn và xem chi tiết **Access policy**

![SQS](/images/3/0007.png?featherlight=false&width=90pc)

8. Bắt đầu kiểm tra đẩy tin nhắn bằng **Event Generator** 

   - Chọn **Orders** topic từ danh sách Topics.
   - Chọn **PUBLISH EVENT**

![SQS](/images/3/0008.png?featherlight=false&width=90pc)

{{% notice note %}}
Bạn sẽ cần phải chọn đúng Region.
{{% /notice %}}

9. Truy cập vào **SQS**

   - Tìm **OrdersQueue**
   - Trong phần **Messages Available** có giá trị là **1**

![SQS](/images/3/0009.png?featherlight=false&width=90pc)

10. Chọn **Send and receive messages.**

![SQS](/images/3/00010.png?featherlight=false&width=90pc)

11. Trong màn hình chi tiết

    - Chọn **Poll for messages**

![SQS](/images/3/00011.png?featherlight=false&width=90pc)

12. Chúng ta sẽ thấy các cột **ID, Sent, Size và Receive Count**

![SQS](/images/3/00012.png?featherlight=false&width=90pc)

13. Xem chi tiết message.

![SQS](/images/3/00013.png?featherlight=false&width=90pc)

14. Sau đó chúng ta sẽ xoá message

![SQS](/images/3/00014.png?featherlight=false&width=90pc)

15. Xóa message thành công.

![SQS](/images/3/00015.png?featherlight=false&width=90pc)

{{% notice tip %}}
Phần lab các bước thực hiện khá dài nên cẩn thận tránh sai sót nhé. Bạn có thể tìm hiểu thêm về [Pub/sub pattern](https://docs.aws.amazon.com/prescriptive-guidance/latest/modernization-integrating-microservices/pub-sub.html)
{{% /notice %}}
