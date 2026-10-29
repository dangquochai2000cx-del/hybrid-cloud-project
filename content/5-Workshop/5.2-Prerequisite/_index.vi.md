
---
title: "Chuẩn bị"
date: 2026-10-29
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Tổng quan về môi trường triển khai

Để triển khai hệ thống Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh bằng VPN Site-to-Site tích hợp giải pháp giám sát tập trung, chúng ta cần chuẩn bị môi trường mạng On-premises và môi trường điện toán đám mây AWS.

Môi trường On-premises được mô phỏng bằng EVE-NG, cho phép xây dựng hệ thống mạng doanh nghiệp gồm nhiều router và các mạng nội bộ tại trụ sở chính và các chi nhánh. Môi trường AWS được sử dụng để triển khai hạ tầng mạng cloud, thiết lập kết nối VPN và chạy các máy chủ phục vụ giám sát tập trung.

#### Các thành phần cần chuẩn bị

- **EVE-NG:** Sử dụng để mô phỏng hạ tầng mạng doanh nghiệp đa chi nhánh, bao gồm các router, thiết bị mạng và các mạng LAN nội bộ.

- **Amazon Web Services (AWS):** Sử dụng để triển khai hạ tầng Hybrid Cloud, bao gồm Amazon VPC, Subnets, Internet Gateway, Virtual Private Gateway, Route Tables và các tài nguyên liên quan.

- **AWS Site-to-Site VPN:** Sử dụng để thiết lập các đường hầm VPN IPsec kết nối mạng On-premises với AWS, đảm bảo trao đổi dữ liệu an toàn giữa hai môi trường.

- **Amazon EC2:** Sử dụng để triển khai máy chủ chạy dịch vụ web và các thành phần giám sát hệ thống.

- **Prometheus và Node Exporter:** Sử dụng để thu thập các chỉ số hoạt động và thông tin tài nguyên của máy chủ.

- **Grafana:** Sử dụng để trực quan hóa dữ liệu giám sát thông qua các dashboard, giúp quản trị viên theo dõi tình trạng hoạt động của hệ thống.

- **Máy tính quản trị:** Sử dụng để cấu hình thiết bị mạng trên EVE-NG, quản lý tài nguyên AWS và truy cập giao diện giám sát thông qua trình duyệt web.

#### Hình ảnh môi trường triển khai

Hình 5.2.1: Mô hình mạng doanh nghiệp được mô phỏng trên EVE-NG.

![EVE-NG Network Topology](/images/5-Workshop/5.2-Prerequisite/eve-ng-topology.png)

Hình 5.2.2: Môi trường Amazon VPC trên AWS.

![AWS VPC Environment](/images/5-Workshop/5.2-Prerequisite/aws-vpc-fixed.png)
#### Yêu cầu trước khi triển khai

Trước khi bắt đầu workshop, bạn cần đảm bảo các yêu cầu sau:

1. Có tài khoản AWS và quyền truy cập để tạo, cấu hình các tài nguyên cần thiết.
2. Đã cài đặt và có thể truy cập EVE-NG để mô phỏng mạng doanh nghiệp.
3. Đã chuẩn bị các thiết bị router và sơ đồ mạng cho trụ sở chính cùng các chi nhánh.
4. Đã xây dựng kế hoạch địa chỉ IP cho các mạng nội bộ và mạng AWS, đảm bảo không bị trùng lặp giữa các dải mạng.
5. Có kết nối Internet để thiết lập các đường hầm VPN Site-to-Site giữa On-premises và AWS.
6. Đã chuẩn bị môi trường Amazon EC2 để triển khai Prometheus, Node Exporter và Grafana.

#### Kết quả mong đợi

Sau khi hoàn thành bước chuẩn bị, chúng ta sẽ có môi trường mô phỏng mạng doanh nghiệp đa chi nhánh trên EVE-NG, tài khoản AWS sẵn sàng sử dụng và kế hoạch địa chỉ IP phù hợp.

Đây là cơ sở để tiếp tục triển khai Amazon VPC, cấu hình các thành phần mạng AWS, thiết lập kết nối VPN Site-to-Site và xây dựng hệ thống giám sát tập trung trong các phần tiếp theo.
