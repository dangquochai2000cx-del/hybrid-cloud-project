---
title: "Giới thiệu"
date: 2026-10-29
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

### 1. Giới thiệu về hệ thống Hybrid Cloud

- **Hybrid Cloud** là mô hình kết hợp giữa hạ tầng mạng doanh nghiệp tại chỗ (On-premises) và môi trường điện toán đám mây AWS. Mô hình này cho phép doanh nghiệp tận dụng hạ tầng mạng hiện có, đồng thời sử dụng các dịch vụ cloud để mở rộng tài nguyên và triển khai ứng dụng.

- **VPN Site-to-Site** cung cấp kết nối an toàn giữa mạng doanh nghiệp đa chi nhánh và AWS thông qua các đường hầm IPsec được mã hóa. Giải pháp này cho phép các mạng nội bộ trao đổi dữ liệu với môi trường cloud mà không cần công khai các tài nguyên nội bộ ra Internet.

- **Giám sát tập trung** sử dụng Prometheus, Node Exporter và Grafana để thu thập, theo dõi và trực quan hóa các chỉ số hoạt động của máy chủ. Qua đó, quản trị viên có thể theo dõi tình trạng tài nguyên, phát hiện bất thường và hỗ trợ xử lý sự cố.

### 2. Tổng quan về workshop

Trong workshop này, sẽ xây dựng mô hình Hybrid Cloud bao gồm hạ tầng mạng doanh nghiệp đa chi nhánh được mô phỏng bằng EVE-NG và môi trường AWS sử dụng Amazon VPC.

- **"Mạng doanh nghiệp On-premises"** mô phỏng hệ thống mạng tại trụ sở chính và các chi nhánh. Các thiết bị định tuyến được cấu hình để kết nối những mạng nội bộ và thiết lập VPN Site-to-Site với AWS.

- **"Môi trường AWS Cloud"** sử dụng Amazon VPC để triển khai hạ tầng mạng cloud, bao gồm các subnet, Internet Gateway, Virtual Private Gateway và các bảng định tuyến. Máy chủ Amazon EC2 được triển khai để cung cấp dịch vụ và phục vụ kiểm tra kết nối giữa hai môi trường.

- **"Kết nối VPN Site-to-Site"** sử dụng các đường hầm IPsec để kết nối mạng doanh nghiệp với AWS. Hai đường hầm VPN được cấu hình nhằm kiểm tra khả năng kết nối và xây dựng phương án dự phòng khi đường truyền gặp sự cố.

- **"Hệ thống giám sát tập trung"** được triển khai trên Amazon EC2, sử dụng Prometheus để thu thập chỉ số, Node Exporter để cung cấp thông tin tài nguyên hệ thống, Grafana để hiển thị dữ liệu dưới dạng dashboard và Amazon S3 để lưu trữ bản sao lưu các tệp cấu hình, dữ liệu giám sát nhằm phục vụ khôi phục khi cần thiết.

Thông qua workshop này, bạn sẽ thực hành thiết kế kiến trúc Hybrid Cloud, triển khai kết nối VPN Site-to-Site, cấu hình định tuyến giữa các mạng, kiểm tra khả năng dự phòng và xây dựng hệ thống giám sát tập trung.

