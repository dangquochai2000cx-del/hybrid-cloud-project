
---
title: "Worklog Tuần 8"
date: 2026-10-03
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Tìm hiểu giải pháp giám sát tài nguyên máy chủ bằng Prometheus và Node Exporter.
- Cài đặt và cấu hình Prometheus trên máy chủ EC2 chạy Ubuntu Server.
- Cài đặt Node Exporter để thu thập dữ liệu về CPU, RAM, ổ đĩa và các thông số hệ thống.
- Cấu hình Prometheus thu thập dữ liệu từ Node Exporter và kiểm tra trạng thái hoạt động.
- Chuẩn bị dữ liệu giám sát để tích hợp với Grafana trong tuần tiếp theo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu kiến trúc và nguyên lý hoạt động của Prometheus.<br>- Tìm hiểu vai trò của Node Exporter trong việc thu thập dữ liệu hệ thống Linux.<br>- Xác định các thông số cần giám sát, bao gồm CPU, RAM, dung lượng ổ đĩa và trạng thái hệ thống.<br>- Kiểm tra trạng thái máy chủ EC2 đã triển khai ở tuần 7. | 03/10/2026 | 03/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Cập nhật danh sách gói phần mềm trên Ubuntu Server.<br>- Tải xuống và cài đặt Prometheus trên máy chủ EC2.<br>- Cấu hình Prometheus và kiểm tra tệp cấu hình trước khi khởi động dịch vụ.<br>- Khởi động Prometheus và kiểm tra trạng thái hoạt động của dịch vụ. | 04/10/2026 | 05/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Cài đặt Node Exporter để thu thập dữ liệu tài nguyên trên Ubuntu Server.<br>- Cấu hình Node Exporter chạy dưới dạng dịch vụ hệ thống.<br>- Kiểm tra trạng thái hoạt động và khả năng cung cấp dữ liệu tại cổng 9100.<br>- Cấu hình Prometheus thu thập dữ liệu từ Node Exporter thông qua mục tiêu giám sát phù hợp. | 06/10/2026 | 07/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Truy cập giao diện web của Prometheus và kiểm tra trạng thái hệ thống.<br>- Kiểm tra mục tiêu giám sát Node Exporter và xác nhận dữ liệu được thu thập thành công.<br>- Thử truy vấn một số chỉ số tài nguyên cơ bản của máy chủ.<br>- Tổng hợp kết quả và chuẩn bị tích hợp Prometheus với Grafana trong tuần 9. | 08/10/2026 | 09/10/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 8:

- Hiểu nguyên lý hoạt động của Prometheus và vai trò của Node Exporter trong hệ thống giám sát.
- Tìm hiểu và thực hiện cài đặt Prometheus trên máy chủ EC2 chạy Ubuntu Server.
- Cấu hình và kiểm tra dịch vụ Prometheus để bảo đảm hệ thống có thể khởi động và hoạt động.
- Cài đặt Node Exporter để thu thập dữ liệu về CPU, RAM, ổ đĩa và các thông số hệ thống Linux.
- Cấu hình Prometheus thu thập dữ liệu từ Node Exporter và kiểm tra trạng thái mục tiêu giám sát.
- Tìm hiểu cách truy vấn các chỉ số tài nguyên cơ bản thông qua giao diện Prometheus.
- Chuẩn bị nguồn dữ liệu Prometheus để tích hợp với Grafana và xây dựng dashboard giám sát trong tuần 9.
