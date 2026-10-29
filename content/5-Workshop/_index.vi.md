---
title: "Workshop"
date: 2026-10-27
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Thiết kế và triển khai hệ thống Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh bằng VPN Site-to-Site tích hợp giải pháp giám sát tập trung

#### Tổng quan

Trong workshop này, chúng ta sẽ tìm hiểu cách thiết kế và triển khai hệ thống **Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh bằng VPN Site-to-Site tích hợp giải pháp giám sát tập trung**.

Mô hình sử dụng EVE-NG để mô phỏng hạ tầng mạng doanh nghiệp tại chỗ (On-premises), kết hợp với Amazon Web Services (AWS) để xây dựng môi trường điện toán đám mây. Các mạng nội bộ tại trung tâm và các chi nhánh được kết nối với AWS thông qua các đường hầm VPN Site-to-Site sử dụng giao thức IPsec, giúp đảm bảo tính bảo mật khi trao đổi dữ liệu giữa hai môi trường.

Bên cạnh việc triển khai kết nối Hybrid Cloud, hệ thống còn tích hợp cơ chế định tuyến dự phòng nhằm tăng tính sẵn sàng của kết nối mạng. Giải pháp giám sát tập trung sử dụng Prometheus, Node Exporter và Grafana để thu thập, theo dõi và trực quan hóa các chỉ số hoạt động của máy chủ, hỗ trợ quản trị viên giám sát tài nguyên và phát hiện sự cố.

Thông qua workshop này, chúng ta sẽ thực hành xây dựng hạ tầng mạng Hybrid Cloud, thiết lập kết nối VPN an toàn, cấu hình định tuyến giữa các mạng, kiểm tra khả năng kết nối và triển khai hệ thống giám sát tập trung.

Các nội dung chính bao gồm:

- **Thiết kế kiến trúc Hybrid Cloud:** Xây dựng mô hình kết nối giữa mạng doanh nghiệp đa chi nhánh và môi trường AWS.
- **Triển khai hạ tầng AWS:** Cấu hình Amazon VPC, Subnet, Internet Gateway, Virtual Private Gateway và Route Table.
- **Cấu hình VPN Site-to-Site:** Thiết lập các đường hầm VPN IPsec kết nối hạ tầng On-premises với AWS.
- **Cấu hình định tuyến và dự phòng:** Thiết lập định tuyến giữa các mạng nội bộ, kiểm tra kết nối và đánh giá khả năng chuyển đổi khi đường truyền gặp sự cố.
- **Triển khai giám sát tập trung:** Cài đặt Prometheus, Node Exporter và Grafana để theo dõi tài nguyên máy chủ.
- **Kiểm tra và đánh giá hệ thống:** Kiểm tra kết nối mạng, trạng thái VPN, khả năng dự phòng và hoạt động của hệ thống giám sát.
#### Nội dung

1. [Tổng quan kiến trúc Hybrid Cloud](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường triển khai](5.2-Prerequisite/)
3. [Thiết kế và triển khai hạ tầng mạng AWS](5.3-AWS-Network-Infrastructure/)
4. [Triển khai máy chủ EC2 và cấu hình Security Groups](5.4-EC2-Security-Groups/)
5. [Cấu hình VPN Site-to-Site kết nối mạng doanh nghiệp đa chi nhánh](5.5-Site-to-Site-VPN/)
6. [Cấu hình định tuyến và cơ chế dự phòng VPN](5.6-VPN-Routing-Failover/)
7. [Triển khai hệ thống giám sát tập trung Prometheus và Grafana](5.7-Centralized-Monitoring/)
8. [Kiểm tra hệ thống Hybrid Cloud và dọn dẹp tài nguyên AWS](5.8-System-Testing-Cleanup/)