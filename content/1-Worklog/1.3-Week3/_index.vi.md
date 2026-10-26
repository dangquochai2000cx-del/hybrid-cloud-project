---
title: "Worklog Tuần 3"
date: 2026-08-24
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

- Triển khai hạ tầng mạng cơ bản trên AWS dựa trên kiến trúc và kế hoạch địa chỉ IP đã xây dựng trong tuần 2.
- Tạo và cấu hình Amazon VPC với dải địa chỉ CIDR phù hợp cho hệ thống Hybrid Cloud.
- Tạo subnet và tìm hiểu cách phân bổ tài nguyên mạng trong VPC.
- Cấu hình Internet Gateway và Route Table để xác định đường đi của lưu lượng mạng.
- Kiểm tra lại cấu hình mạng nhằm chuẩn bị cho việc triển khai máy chủ EC2 và kết nối VPN ở các tuần tiếp theo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Truy cập AWS Management Console và mở dịch vụ Amazon VPC.<br>- Tạo VPC phục vụ đề tài Hybrid Cloud.<br>- Cấu hình dải địa chỉ IPv4 CIDR cho VPC theo kế hoạch đã xây dựng.<br>- Kiểm tra thông tin và trạng thái của VPC sau khi tạo. | 24/08/2026 | 24/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Tạo subnet trong VPC theo kế hoạch địa chỉ IP.<br>- Xác định dải CIDR và Availability Zone cho subnet.<br>- Tìm hiểu sự khác nhau giữa public subnet và private subnet.<br>- Cấu hình tự động gán địa chỉ IPv4 công khai cho public subnet khi cần thiết. | 25/08/2026 | 26/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Tạo Internet Gateway và gắn vào VPC.<br>- Tạo Route Table phục vụ định tuyến cho public subnet.<br>- Thêm tuyến mặc định `0.0.0.0/0` trỏ đến Internet Gateway.<br>- Liên kết Route Table với subnet tương ứng và kiểm tra các tuyến đã cấu hình. | 27/08/2026 | 27/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Rà soát cấu hình VPC, subnet, Internet Gateway và Route Table.<br>- Kiểm tra dải CIDR, trạng thái liên kết và các tuyến định tuyến.<br>- Đối chiếu cấu hình thực tế với sơ đồ kiến trúc và kế hoạch địa chỉ IP.<br>- Tổng hợp kết quả triển khai làm cơ sở cho tuần 4. | 28/08/2026 | 28/08/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

- Tạo và cấu hình được Amazon VPC phục vụ việc triển khai hệ thống Hybrid Cloud.
- Xác định và cấu hình dải địa chỉ IPv4 CIDR cho VPC theo kế hoạch thiết kế.
- Tạo subnet và hiểu được vai trò của subnet trong việc phân chia mạng và triển khai tài nguyên AWS.
- Phân biệt được public subnet và private subnet dựa trên cấu hình định tuyến, thay vì chỉ dựa vào tên gọi.
- Tạo Internet Gateway và liên kết với VPC để chuẩn bị khả năng kết nối Internet cho các tài nguyên phù hợp.
- Tạo và cấu hình Route Table với các tuyến định tuyến cần thiết:
  - Tuyến local cho phép định tuyến giữa các subnet trong phạm vi VPC theo cấu hình mạng.
  - Tuyến mặc định `0.0.0.0/0` trỏ đến Internet Gateway cho lưu lượng Internet từ public subnet.
- Liên kết Route Table với subnet tương ứng và kiểm tra các tuyến định tuyến đã cấu hình.
- Đối chiếu cấu hình thực tế với sơ đồ kiến trúc và kế hoạch địa chỉ IP đã xây dựng trong tuần 2.
- Hoàn thành phần hạ tầng mạng AWS cơ bản, tạo tiền đề triển khai Amazon EC2 và cấu hình bảo mật bằng Security Group trong tuần 4.