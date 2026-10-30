---
title: "Triển khai máy chủ Amazon EC2 và cấu hình Security Groups"
date: 2026-10-30
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Tổng quan về Amazon EC2

Amazon Elastic Compute Cloud (Amazon EC2) là dịch vụ cung cấp máy chủ ảo trên AWS. Trong mô hình Hybrid Cloud, EC2 được sử dụng để triển khai các dịch vụ cần thiết, bao gồm máy chủ web và các thành phần giám sát hệ thống.

Trong phạm vi dự án, một máy chủ EC2 chạy Ubuntu Server 24.04 được triển khai trong public subnet của VPC `HYBRID-CLOUD-VPC`. Máy chủ này được sử dụng để chạy Nginx, Prometheus, Node Exporter và Grafana phục vụ mục đích kiểm thử và giám sát.

#### Mục tiêu triển khai

- Tạo máy chủ EC2 trong public subnet của AWS VPC.
- Sử dụng Ubuntu Server 24.04 làm hệ điều hành.
- Cấu hình Security Group để kiểm soát lưu lượng truy cập vào máy chủ.
- Kết nối đến EC2 thông qua SSH.
- Cài đặt và kiểm tra dịch vụ Nginx.
- Chuẩn bị môi trường để triển khai các thành phần giám sát tập trung.

#### Thông số máy chủ EC2

| Thành phần | Cấu hình |
|---|---|
| Instance Name | `HYBRID-CLOUD-WEBSERVER-SG` |
| Operating System | Ubuntu Server 24.04 |
| Instance Type | `t3.micro` |
| VPC | `HYBRID-CLOUD-VPC` |
| Subnet | `AWS-PUBLIC-SUBNET` |
| Private IPv4 Address | `10.100.1.118` |
| Root Volume | 8 GiB gp3 |
| Web Server | Nginx |
| Monitoring Components | Prometheus, Node Exporter, Grafana |

**[Chèn hình ảnh tại đây: Thông tin máy chủ EC2 trên AWS Management Console]**

Lưu ý: Địa chỉ IPv4 công khai của EC2 có thể thay đổi sau khi dừng và khởi động lại máy chủ nếu không sử dụng Elastic IP. Khi truy cập dịch vụ, cần kiểm tra địa chỉ IP hiện tại trong AWS Console.

#### Triển khai máy chủ EC2

Các bước thực hiện:

1. Truy cập **AWS Management Console**.
2. Mở dịch vụ **Amazon EC2**.
3. Chọn **Instances**, sau đó nhấn **Launch instances**.
4. Nhập tên máy chủ `HYBRID-CLOUD-WEBSERVER-SG`.
5. Chọn hệ điều hành **Ubuntu Server 24.04 LTS**.
6. Chọn loại máy chủ `t3.micro` nếu phù hợp với hạn mức và ngân sách.
7. Tạo hoặc chọn key pair để sử dụng khi kết nối SSH.
8. Trong phần **Network settings**, chọn VPC `HYBRID-CLOUD-VPC`.
9. Chọn subnet `AWS-PUBLIC-SUBNET`.
10. Cấu hình Security Group phù hợp với các dịch vụ cần triển khai.
11. Cấu hình dung lượng ổ đĩa theo nhu cầu, ví dụ 8 GiB gp3.
12. Kiểm tra lại các thông số và nhấn **Launch instance**.

**[Chèn hình ảnh tại đây: Cấu hình Launch instance trên AWS Console]**

Sau khi khởi chạy, kiểm tra trạng thái máy chủ là **Running** và trạng thái kiểm tra hệ thống đã hoàn tất trước khi kết nối.

#### Cấu hình Security Groups

Security Group hoạt động như một tường lửa ảo ở cấp độ tài nguyên AWS, kiểm soát lưu lượng đi vào và đi ra khỏi máy chủ EC2.

Đối với máy chủ trong dự án, các quy tắc inbound cần được cấu hình theo nguyên tắc chỉ cho phép những kết nối thực sự cần thiết.

| Type | Protocol | Port Range | Source | Purpose |
|---|---|---|---|---|
| SSH | TCP | 22 | My IP `/32` | Quản trị máy chủ từ xa |
| HTTP | TCP | 80 | `0.0.0.0/0` | Truy cập website Nginx |
| Custom TCP | TCP | 3000 | My IP `/32` hoặc mạng quản trị | Truy cập Grafana khi cần |
| Custom TCP | TCP | 9090 | My IP `/32` hoặc mạng quản trị | Truy cập Prometheus khi cần |
| Custom TCP | TCP | 9100 | Chỉ máy chủ Prometheus hoặc mạng giám sát | Thu thập số liệu Node Exporter |

**[Chèn hình ảnh tại đây: Các inbound rules của Security Group trên AWS Console]**

Lưu ý bảo mật:

- Không nên mở SSH port 22 cho toàn bộ Internet nếu không thực sự cần thiết.
- Chỉ cho phép truy cập các cổng giám sát từ địa chỉ IP hoặc mạng quản trị phù hợp.
- Không mở port 9100 công khai vì Node Exporter cung cấp thông tin giám sát của máy chủ.
- Các quy tắc inbound phải phù hợp với mô hình triển khai thực tế. Nếu các dịch vụ chỉ được truy cập qua VPN, hãy giới hạn nguồn truy cập theo các dải mạng nội bộ tương ứng.
- Security Group có tính chất stateful, vì vậy lưu lượng phản hồi của kết nối được cho phép sẽ được tự động chấp nhận.

#### Kết nối đến máy chủ bằng SSH

Sau khi EC2 chạy ổn định, sử dụng SSH để quản trị hệ điều hành Ubuntu.

Trên máy tính Windows, mở PowerShell và chuyển đến thư mục chứa private key. Thực hiện lệnh sau, thay đường dẫn key và địa chỉ IP bằng thông tin thực tế:

```bash
ssh -i "hybrid-cloud-webserver-key.pem" ubuntu@<PUBLIC_IP>