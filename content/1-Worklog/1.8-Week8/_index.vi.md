
---
title: "Worklog Tuần 8"
date: 2026-10-19
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Tìm hiểu giải pháp giám sát tài nguyên máy chủ bằng Prometheus và Node Exporter.
- Cài đặt và cấu hình Prometheus trên máy chủ EC2 chạy Ubuntu Server.
- Cài đặt Node Exporter để thu thập dữ liệu về CPU, RAM, ổ đĩa và các thông số hệ thống.
- Cấu hình Prometheus thu thập dữ liệu từ Node Exporter và kiểm tra trạng thái hoạt động.
- Tìm hiểu và triển khai giải pháp lưu trữ dữ liệu sao lưu bằng Amazon S3.
- Cấu hình IAM Role và IAM Policy cho phép máy chủ EC2 truy cập và thực hiện sao lưu dữ liệu lên S3.
- Thực hiện sao lưu các tệp cấu hình Prometheus, Node Exporter và Grafana lên S3, đồng thời kiểm tra khả năng tải dữ liệu sao lưu về EC2.
- Chuẩn bị dữ liệu giám sát để tích hợp với Grafana trong tuần tiếp theo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu kiến trúc và nguyên lý hoạt động của Prometheus.<br>- Tìm hiểu vai trò của Node Exporter trong việc thu thập dữ liệu hệ thống Linux.<br>- Xác định các thông số cần giám sát, bao gồm CPU, RAM, dung lượng ổ đĩa và trạng thái hệ thống.<br>- Kiểm tra trạng thái máy chủ EC2 đã triển khai ở tuần 7. | 19/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Cập nhật danh sách gói phần mềm trên Ubuntu Server.<br>- Tải xuống và cài đặt Prometheus trên máy chủ EC2.<br>- Cấu hình Prometheus và kiểm tra tệp cấu hình trước khi khởi động dịch vụ.<br>- Khởi động Prometheus và kiểm tra trạng thái hoạt động của dịch vụ. | 20/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Cài đặt Node Exporter để thu thập dữ liệu tài nguyên trên Ubuntu Server.<br>- Cấu hình Node Exporter chạy dưới dạng dịch vụ hệ thống.<br>- Kiểm tra trạng thái hoạt động và khả năng cung cấp dữ liệu tại cổng 9100.<br>- Cấu hình Prometheus thu thập dữ liệu từ Node Exporter thông qua mục tiêu giám sát phù hợp. | 22/10/2026 | 23/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Truy cập giao diện web của Prometheus và kiểm tra trạng thái hệ thống.<br>- Kiểm tra mục tiêu giám sát Node Exporter và xác nhận dữ liệu được thu thập thành công.<br>- Thử truy vấn một số chỉ số tài nguyên cơ bản của máy chủ.<br>- Tìm hiểu và tạo Amazon S3 Bucket để lưu trữ dữ liệu sao lưu.<br>- Tạo IAM Policy và IAM Role, cấu hình quyền truy cập S3 cho máy chủ EC2.<br>- Cài đặt và cấu hình AWS CLI trên Ubuntu Server để thực hiện thao tác với S3.<br>- Sao lưu các tệp cấu hình Prometheus, Node Exporter và Grafana, sau đó tải bản sao lưu lên S3.<br>- Kiểm tra khả năng tải file backup từ S3 về EC2 và xác nhận nội dung tệp sao lưu | 24/10/2026 | 25/10/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 8:

- Hiểu nguyên lý hoạt động của Prometheus và vai trò của Node Exporter trong hệ thống giám sát.
- Tìm hiểu và thực hiện cài đặt Prometheus trên máy chủ EC2 chạy Ubuntu Server.
- Cấu hình và kiểm tra dịch vụ Prometheus để bảo đảm hệ thống có thể khởi động và hoạt động.
- Cài đặt Node Exporter để thu thập dữ liệu về CPU, RAM, ổ đĩa và các thông số hệ thống Linux.
- Cấu hình Prometheus thu thập dữ liệu từ Node Exporter và kiểm tra trạng thái mục tiêu giám sát.
- Tìm hiểu cách truy vấn các chỉ số tài nguyên cơ bản thông qua giao diện Prometheus.
- Tìm hiểu và triển khai Amazon S3 để lưu trữ các tệp dữ liệu sao lưu của hệ thống giám sát.
- Tạo S3 Bucket và cấu hình IAM Policy, IAM Role để cấp quyền truy cập S3 cho máy chủ EC2.
- Cài đặt và sử dụng AWS CLI để thực hiện thao tác tải dữ liệu từ EC2 lên S3 và ngược lại.
- Thực hiện sao lưu các tệp cấu hình Prometheus, Node Exporter và Grafana lên S3.
- Kiểm tra khả năng tải file backup từ S3 về EC2 và xác nhận tính toàn vẹn cấu trúc của tệp sao lưu.
- Chuẩn bị nguồn dữ liệu Prometheus để tích hợp với Grafana và xây dựng dashboard giám sát trong tuần 9