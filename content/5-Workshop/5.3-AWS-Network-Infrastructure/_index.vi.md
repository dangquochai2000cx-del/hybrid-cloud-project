---
title: "Thiết kế và triển khai hạ tầng mạng AWS"
date: 2026-10-30
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Tổng quan về hạ tầng mạng AWS

Trong mô hình Hybrid Cloud, Amazon Web Services (AWS) cung cấp môi trường điện toán đám mây để kết nối với hệ thống mạng doanh nghiệp được mô phỏng trên EVE-NG. Hạ tầng mạng AWS được thiết kế nhằm cung cấp kết nối giữa các máy chủ trên cloud và các mạng nội bộ tại trụ sở chính, chi nhánh.

Các thành phần mạng chính được sử dụng bao gồm Amazon VPC, subnet, Internet Gateway và route table. Ngoài ra, Virtual Private Gateway được sử dụng để thiết lập kết nối VPN Site-to-Site giữa AWS và mạng On-premises.

#### Mục tiêu triển khai

- Tạo và cấu hình Amazon VPC với dải địa chỉ IP phù hợp.
- Xây dựng public subnet để triển khai các máy chủ EC2.
- Kết nối VPC với Internet thông qua Internet Gateway.
- Cấu hình route table để điều khiển lưu lượng mạng giữa AWS, Internet và mạng doanh nghiệp.
- Chuẩn bị Virtual Private Gateway phục vụ kết nối VPN Site-to-Site.

#### Thiết kế địa chỉ IP

Hạ tầng mạng AWS sử dụng dải địa chỉ riêng `10.100.0.0/16`. Dải mạng này được lựa chọn để tránh trùng lặp với các mạng nội bộ trong môi trường On-premises.

| Thành phần | Tên tài nguyên | Dải địa chỉ / cấu hình |
|---|---|---|
| Amazon VPC | HYBRID-CLOUD-VPC | `10.100.0.0/16` |
| Public Subnet | AWS-PUBLIC-SUBNET | `10.100.1.0/24` |
| Internet Gateway | HYBRID-CLOUD-IGW | Kết nối VPC với Internet |
| Virtual Private Gateway | VGW | Phục vụ kết nối VPN Site-to-Site |
| Route Table | AWS-PUBLIC-RT | Điều khiển định tuyến cho public subnet |

#### Triển khai Amazon VPC

Amazon VPC là mạng ảo riêng biệt trên AWS, cho phép quản trị viên kiểm soát dải địa chỉ IP, subnet, định tuyến và kết nối mạng.

Các bước thực hiện:

1. Truy cập AWS Management Console.
2. Mở dịch vụ **Amazon VPC**.
3. Chọn **Your VPCs**, sau đó nhấn **Create VPC**.
4. Chọn tạo VPC và nhập tên `HYBRID-CLOUD-VPC`.
5. Nhập IPv4 CIDR là `10.100.0.0/16`.
6. Giữ các tùy chọn khác theo yêu cầu của môi trường lab.
7. Nhấn **Create VPC** để hoàn tất.

**[Chèn hình ảnh tại đây: Giao diện tạo Amazon VPC trên AWS]**

Sau khi tạo thành công, kiểm tra lại tên VPC và dải địa chỉ IPv4 trong danh sách Your VPCs.

#### Tạo Public Subnet

Public subnet được sử dụng để triển khai các máy chủ cần kết nối Internet, chẳng hạn như máy chủ web và máy chủ giám sát.

Các bước thực hiện:

1. Trong giao diện Amazon VPC, chọn **Subnets**.
2. Nhấn **Create subnet**.
3. Chọn VPC `HYBRID-CLOUD-VPC`.
4. Đặt tên subnet là `AWS-PUBLIC-SUBNET`.
5. Chọn Availability Zone phù hợp, ví dụ `us-east-1b`.
6. Nhập IPv4 subnet CIDR là `10.100.1.0/24`.
7. Nhấn **Create subnet**.
8. Chọn subnet vừa tạo, mở phần **Actions** và bật **Enable auto-assign public IPv4 address** nếu cần tự động cấp địa chỉ IPv4 công khai cho các EC2 mới.

**[Chèn hình ảnh tại đây: Cấu hình tạo Public Subnet trên AWS]**

Lưu ý: Việc bật tự động cấp IPv4 công khai không thay thế cấu hình Internet Gateway và route table.

#### Tạo và gắn Internet Gateway

Internet Gateway cho phép các tài nguyên trong VPC giao tiếp với Internet khi có định tuyến và cấu hình bảo mật phù hợp.

Các bước thực hiện:

1. Trong Amazon VPC, chọn **Internet gateways**.
2. Nhấn **Create internet gateway**.
3. Đặt tên là `HYBRID-CLOUD-IGW`.
4. Nhấn **Create internet gateway**.
5. Chọn Internet Gateway vừa tạo.
6. Mở **Actions** và chọn **Attach to a VPC**.
7. Chọn `HYBRID-CLOUD-VPC`, sau đó xác nhận gắn kết.

**[Chèn hình ảnh tại đây: Internet Gateway đã được tạo và gắn với VPC]**

Sau khi hoàn tất, kiểm tra trạng thái Internet Gateway đã được gắn với VPC.

#### Cấu hình Route Table

Route table xác định đường đi của lưu lượng mạng từ subnet đến các đích khác nhau. Trong mô hình này, route table công khai được sử dụng để định tuyến lưu lượng Internet và lưu lượng đến các mạng doanh nghiệp qua VPN.

Các bước thực hiện:

1. Trong Amazon VPC, chọn **Route tables**.
2. Tạo hoặc chọn route table có tên `AWS-PUBLIC-RT`.
3. Đảm bảo route table được liên kết với `HYBRID-CLOUD-VPC`.
4. Mở tab **Routes**, chọn **Edit routes**.
5. Thêm route `0.0.0.0/0` với Target là `HYBRID-CLOUD-IGW`.
6. Bổ sung các route đến mạng doanh nghiệp qua Virtual Private Gateway sau khi VPN được tạo và cấu hình, sử dụng các dải mạng thực tế của lab.
7. Lưu thay đổi và mở tab **Subnet associations**.
8. Liên kết `AWS-PUBLIC-SUBNET` với `AWS-PUBLIC-RT`.

**[Chèn hình ảnh tại đây: Bảng định tuyến AWS-PUBLIC-RT với route mặc định đến Internet Gateway]**

Các route đến mạng On-premises chỉ hoạt động khi VPN và cấu hình định tuyến tương ứng đã sẵn sàng. Không thêm các dải địa chỉ chưa được sử dụng trong mô hình thực tế.

#### Kiểm tra kết quả triển khai

Sau khi hoàn thành các bước cấu hình, cần kiểm tra:

- Amazon VPC có CIDR `10.100.0.0/16`.
- Public subnet có CIDR `10.100.1.0/24`.
- Internet Gateway đã được gắn với VPC.
- Route table có route mặc định `0.0.0.0/0` trỏ đến Internet Gateway.
- Public subnet đã được liên kết với route table phù hợp.
- Các route đến mạng doanh nghiệp được bổ sung khi VPN Site-to-Site đã được cấu hình.

**[Chèn hình ảnh tại đây: Tổng quan VPC, Subnet, Internet Gateway và Route Table sau khi cấu hình]**

#### Kết quả mong đợi

Sau khi hoàn thành phần này, hạ tầng mạng cơ bản trên AWS đã sẵn sàng cho việc triển khai máy chủ EC2 và tích hợp với mạng doanh nghiệp. Amazon VPC, public subnet, Internet Gateway và route table tạo nền tảng cho việc triển khai các dịch vụ cloud.

Ở phần tiếp theo, chúng ta sẽ tiếp tục cấu hình máy chủ Amazon EC2 và Security Groups để triển khai các dịch vụ cần thiết cho hệ thống Hybrid Cloud.