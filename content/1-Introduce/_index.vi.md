---
title : "Giới thiệu"
date: 2024-01-01
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Tổng quan

Ngày càng nhiều khách hàng đang chọn xây dựng các kiến ​​trúc ứng dụng hướng sự kiện - những kiến ​​trúc trong đó người subscribe hoặc dịch vụ mục tiêu tự động thực hiện công việc để đáp ứng với các sự kiện do publisher hoặc dịch vụ nguồn kích hoạt. Mô hình này có thể cho phép các nhóm phát triển hoạt động độc lập hơn để họ có thể phát hành các tính năng mới nhanh hơn, đồng thời tăng khả năng mở rộng hơn.

Amazon SNS Topic là một điểm truy cập locic hoạt động như một kênh giao tiếp. Một Topic cho phép bạn nhóm nhiều điểm cuối (chẳng hạn như AWS Lambda, Amazon SQS, HTTP/S hoặc một địa chỉ email).

Để phát message của hệ thống từ hệ thống đóng vài trò message-producer  (ví dụ: một trang web thương mại điện tử) làm việc với nhiều dịch vụ khác yêu cầu message của nó (ví dụ: hệ thống thanh toán và thực hiện), bạn có thể tạo một topic cho hệ thống producer của mình.

![SQS](/images/3/0000.png?featherlight=false&width=90pc)

Theo mặc định, người subscribe topic Amazon SNS nhận được mọi message được xuất bản cho topic. Để nhận được một tập hợp con các message, người subscribe phải chỉ định chính sách lọc cho subscribe topic. Chính sách bộ lọc là một đối tượng JSON đơn giản chứa các thuộc tính xác định message nào mà người subscribe nhận được.

Khi bạn xuất bản message cho một topic, Amazon SNS sẽ so sánh các thuộc tính message với các thuộc tính trong chính sách bộ lọc cho từng subscribe của topic. Nếu bất kỳ thuộc tính nào khớp, Amazon SNS sẽ gửi message đến người subscribe. Nếu không, Amazon SNS sẽ bỏ qua người subscribe mà không gửi message.

Bạn có thể đơn giản hóa việc sử dụng Amazon SNS bằng cách hợp nhất các tiêu chí lọc message vào các subscribe topic của mình. Điều này cho phép bạn giảm tải logic lọc message từ người subscribe và logic định tuyến message từ các publisher, loại bỏ nhu cầu lọc message bằng cách tạo một topic riêng biệt cho từng điều kiện. Bạn có thể sử dụng một topic duy nhất, phân biệt các message của mình bằng cách sử dụng các thuộc tính. Mỗi người subscribe chỉ nhận và xử lý các message được chấp nhận bởi chính sách lọc của nó.

Trong workshop này, bạn sẽ tạo hàng đợi SQS mới cho Đơn hàng ở EU và tạo subscribe cho topic SNS Đơn hàng với chính sách bộ lọc để định tuyến từng message đến hàng đợi SQS Đơn hàng ở EU. Để chỉ ra Đơn đặt hàng ở EU, bạn sẽ chỉ định một thuộc tính, vị trí, với một giá trị eu-west cho message.
