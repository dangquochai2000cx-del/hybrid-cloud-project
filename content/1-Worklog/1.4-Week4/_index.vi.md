
---
title: "Worklog Tuần 4"
date: 2026-09-05
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu tổng quan về Amazon EC2 và vai trò của EC2 trong hệ thống Hybrid Cloud.<br>- Tìm hiểu các loại Instance Type, Amazon Machine Image (AMI) và các tùy chọn lưu trữ EBS.<br>- Xác định cấu hình máy chủ phù hợp với nhu cầu thực hành và giới hạn chi phí.<br>- Lựa chọn hệ điều hành Ubuntu Server cho máy chủ thực hành. | 05/09/2026 | 05/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Khởi tạo EC2 instance trong VPC đã triển khai ở tuần 3.<br>- Lựa chọn AMI, Instance Type, subnet và dung lượng ổ đĩa phù hợp.<br>- Cấu hình key pair để phục vụ kết nối SSH.<br>- Kiểm tra trạng thái khởi chạy và thông tin địa chỉ IP của instance. | 06/09/2026 | 07/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Tạo và cấu hình Security Group cho EC2 instance.<br>- Thiết lập quy tắc inbound cho SSH (TCP port 22) từ địa chỉ IP quản trị được phép truy cập.<br>- Thiết lập quy tắc HTTP (TCP port 80) khi cần triển khai dịch vụ web.<br>- Tìm hiểu quy tắc outbound và nguyên tắc cấp quyền truy cập tối thiểu.<br>- Kiểm tra các quy tắc bảo mật đã cấu hình. | 08/09/2026 | 08/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Kết nối đến EC2 instance thông qua SSH bằng key pair đã tạo.<br>- Kiểm tra hệ điều hành, cấu hình mạng và tài nguyên cơ bản của máy chủ.<br>- Kiểm tra khả năng truy cập máy chủ và rà soát các thiết lập bảo mật.<br>- Tìm hiểu cách dừng, khởi động và chấm dứt EC2 instance để quản lý tài nguyên và chi phí. | 09/09/2026 | 09/09/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

- Hiểu được vai trò của Amazon EC2 trong việc cung cấp tài nguyên máy chủ cho hệ thống Hybrid Cloud.
- Nắm được các thành phần cơ bản khi khởi tạo EC2 instance:
  - **AMI:** Cung cấp hệ điều hành và cấu hình phần mềm ban đầu cho instance.
  - **Instance Type:** Xác định tài nguyên tính toán như CPU và bộ nhớ.
  - **Amazon EBS:** Cung cấp dung lượng lưu trữ dạng block cho instance.
  - **Key Pair:** Hỗ trợ xác thực khi kết nối SSH đến máy chủ.
- Tạo và cấu hình EC2 instance theo nhu cầu thực hành.
- Hiểu cách tạo và áp dụng Security Group để kiểm soát lưu lượng mạng đến và đi của máy chủ.
- Nắm được vai trò của các quy tắc inbound và outbound trong việc bảo vệ tài nguyên AWS.
- Hiểu cách kết nối SSH đến máy chủ Linux bằng key pair.
- Biết cách kiểm tra trạng thái EC2, địa chỉ IP và các thông tin cấu hình cơ bản.
- Nhận thức được tầm quan trọng của việc giới hạn nguồn truy cập SSH, chỉ mở các cổng dịch vụ cần thiết và quản lý vòng đời EC2 để kiểm soát chi phí.
- Hoàn thành bước chuẩn bị máy chủ và bảo mật cơ bản, tạo tiền đề cho việc cấu hình AWS Site-to-Site VPN và Virtual Private Gateway trong tuần 5.
