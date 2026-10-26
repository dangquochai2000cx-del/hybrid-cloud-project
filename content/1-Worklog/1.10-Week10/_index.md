
---
title: "Worklog Tuần 10"
date: 2026-10-17
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

- Kiểm thử tổng thể mô hình Hybrid Cloud kết nối mạng doanh nghiệp với AWS thông qua Site-to-Site VPN.
- Kiểm tra khả năng định tuyến và trao đổi dữ liệu giữa mạng nội bộ và VPC trên AWS.
- Đánh giá hoạt động của máy chủ web và hệ thống giám sát tập trung sử dụng Prometheus, Node Exporter và Grafana.
- Kiểm tra các cấu hình bảo mật liên quan đến Security Group, VPN và quyền truy cập tài nguyên AWS.
- Đánh giá chi phí sử dụng dịch vụ AWS và đề xuất các biện pháp tối ưu tài nguyên.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Kiểm tra lại kiến trúc tổng thể của hệ thống Hybrid Cloud đã triển khai.<br>- Kiểm tra trạng thái VPC, Subnet, Route Table, Virtual Private Gateway và kết nối Site-to-Site VPN.<br>- Kiểm tra cấu hình định tuyến giữa mạng doanh nghiệp và mạng AWS.<br>- Xác định các thành phần cần kiểm thử trong toàn bộ hệ thống. | 17/10/2026 | 17/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Thực hiện kiểm tra kết nối giữa mạng nội bộ và các tài nguyên trong VPC trên AWS.<br>- Sử dụng lệnh ping và các công cụ kiểm tra mạng để xác minh khả năng truyền dữ liệu.<br>- Kiểm tra trạng thái đường hầm VPN và cấu hình định tuyến khi xảy ra sự cố.<br>- Ghi nhận kết quả kiểm thử và các vấn đề phát sinh. | 18/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Kiểm tra khả năng truy cập máy chủ web Nginx trên EC2.<br>- Kiểm tra hoạt động của Prometheus, Node Exporter và Grafana.<br>- Đánh giá khả năng thu thập, truy vấn và trực quan hóa các chỉ số CPU, RAM và dung lượng ổ đĩa.<br>- Rà soát Security Group, cổng dịch vụ và các quy tắc truy cập để hạn chế lưu lượng không cần thiết. | 20/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Kiểm tra thông tin sử dụng và chi phí các dịch vụ AWS trong quá trình triển khai.<br>- Xác định các tài nguyên có thể phát sinh chi phí khi không sử dụng, chẳng hạn như EC2, EBS và các thành phần mạng liên quan.<br>- Đề xuất biện pháp tối ưu chi phí bằng cách dừng hoặc giải phóng tài nguyên không cần thiết sau khi hoàn thành kiểm thử.<br>- Tổng hợp kết quả, đánh giá ưu điểm và hạn chế của mô hình Hybrid Cloud, đồng thời đề xuất hướng cải tiến. | 22/10/2026 | 23/10/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 10:

- Kiểm tra và đánh giá kiến trúc tổng thể của mô hình Hybrid Cloud kết nối mạng doanh nghiệp với AWS.
- Thực hiện kiểm thử kết nối, định tuyến và trao đổi dữ liệu giữa mạng nội bộ và VPC trên AWS.
- Kiểm tra trạng thái hoạt động của Site-to-Site VPN và đánh giá khả năng xử lý các vấn đề kết nối.
- Kiểm tra hoạt động của máy chủ web Nginx và hệ thống giám sát sử dụng Prometheus, Node Exporter và Grafana.
- Rà soát các cấu hình bảo mật cơ bản, bao gồm Security Group, cổng dịch vụ và quyền truy cập tài nguyên.
- Tìm hiểu cách theo dõi chi phí AWS và xác định các tài nguyên có thể gây phát sinh chi phí ngoài dự kiến.
- Đề xuất các biện pháp tối ưu tài nguyên, tổng hợp kết quả triển khai và đánh giá những ưu điểm, hạn chế của mô hình Hybrid Cloud.
