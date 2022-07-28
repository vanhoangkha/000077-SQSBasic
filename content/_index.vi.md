---
title : "Xây dựng kiến trúc Event-driven với SNS và SQS "
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Xây dựng kiến trúc Even-driven với SNS và SQS

#### Tổng quan 

Nhiều khách hàng đang chọn xây dựng các kiến ​​trúc ứng dụng hướng sự kiện - những kiến ​​trúc trong đó subscriber hoặc dịch vụ mục tiêu tự động thực hiện công việc để đáp ứng với các sự kiện do nhà xuất bản hoặc dịch vụ nguồn kích hoạt. Mô hình này có thể cho phép các nhóm phát triển hoạt động độc lập hơn để họ có thể phát hành các tính năng mới nhanh hơn, đồng thời làm cho các ứng dụng của họ có thể mở rộng hơn.

Amazon SNS Topic là một điểm truy cập hợp lý hoạt động như một kênh giao tiếp. Một Topic cho phép bạn nhóm nhiều điểm cuối (chẳng hạn như AWS Lambda, Amazon SQS, HTTP/S hoặc một địa chỉ email).

Để phát message của hệ thống nhà sản xuất message (ví dụ: một trang web thương mại điện tử) làm việc với nhiều dịch vụ khác yêu cầu message của nó (ví dụ: hệ thống thanh toán và thực hiện), bạn có thể tạo một topic cho hệ thống nhà sản xuất của mình.

![SQS](/images/3/0000.png?featherlight=false&width=90pc)

Theo mặc định, subscriber topic Amazon SNS nhận được mọi message được xuất bản cho topic. Để nhận được một tập hợp con các message, subscriber phải chỉ định chính sách lọc cho topic đã đăng ký. Chính sách bộ lọc là một đối tượng JSON đơn giản chứa các thuộc tính xác định message nào mà subscriber nhận được.

Khi bạn xuất bản message cho một topic, Amazon SNS sẽ so sánh các thuộc tính message với các thuộc tính trong chính sách bộ lọc cho từng đăng ký của topic. Nếu bất kỳ thuộc tính nào khớp, Amazon SNS sẽ gửi message đến subscriber. Nếu không, Amazon SNS sẽ bỏ qua subscriber mà không gửi message.

Bạn có thể đơn giản hóa việc sử dụng Amazon SNS bằng cách hợp nhất các tiêu chí lọc message vào các topic đã đăng ký của mình. Điều này cho phép bạn giảm tải logic lọc message từ subscriber và logic định tuyến message từ các nhà xuất bản, loại bỏ nhu cầu lọc message bằng cách tạo một topic riêng biệt cho từng điều kiện. Bạn có thể sử dụng một topic duy nhất, phân biệt các message của mình bằng cách sử dụng các thuộc tính. Mỗi subscriber chỉ nhận và xử lý các message được chấp nhận bởi chính sách lọc của nó.

Trong phần này, bạn sẽ tạo hàng đợi SQS mới cho Đơn hàng ở EU và tạo đăng ký cho topic SNS Đơn hàng với chính sách bộ lọc để định tuyến từng thư đến hàng đợi SQS Đơn hàng ở EU. Để chỉ ra Đơn đặt hàng ở EU, bạn sẽ chỉ định một thuộc tính, vị trí, với một giá trị eu-west cho message.

![SQS](/images/4/0000.png?featherlight=false&width=90pc)

#### Nội dung 

1. [Giới thiệu](1-introduce/)
2. [Các bước chuẩn bị](2-prerequiste/)
3. [Pub/Sub đơn giản](3-simplesubpub/)
4. [Lọc message](4-messagefiltering/)
5. [Lọc message nâng cao](5-advancemessage/)
6. [Dọn dẹp tài nguyên](6-cleanup/)
