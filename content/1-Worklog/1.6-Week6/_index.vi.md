
---
title: "Worklog Tuần 6"
date: 2026-09-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Triển khai kết nối AWS Site-to-Site VPN giữa mạng doanh nghiệp mô phỏng và VPC trên AWS.
- Cấu hình các thành phần VPN cần thiết để thiết lập kết nối an toàn giữa mạng nội bộ và AWS.
- Cấu hình định tuyến để cho phép các mạng nội bộ tại doanh nghiệp giao tiếp với mạng VPC trên AWS.
- Kiểm tra trạng thái đường hầm VPN và xác minh khả năng truyền dữ liệu giữa hai hệ thống mạng.
- Đánh giá khả năng kết nối dự phòng và chuẩn bị môi trường cho việc triển khai máy chủ web trong tuần tiếp theo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Kiểm tra cấu hình VPC, Virtual Private Gateway và các thông tin VPN đã chuẩn bị trong tuần 5.<br>- Kiểm tra địa chỉ IP public của router tại mạng doanh nghiệp mô phỏng và các dải địa chỉ mạng cần kết nối.<br>- Đối chiếu thông tin mạng nội bộ với cấu hình AWS để tránh trùng lặp dải CIDR.<br>- Chuẩn bị các thông số cần thiết trước khi cấu hình VPN. | 19/09/2026 | 19/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Cấu hình Customer Gateway và kết nối AWS Site-to-Site VPN theo thiết kế đã xây dựng.<br>- Tải và kiểm tra tệp cấu hình VPN do AWS cung cấp.<br>- Cấu hình các thông số IPsec, khóa chia sẻ trước và địa chỉ đầu cuối đường hầm trên router.<br>- Kiểm tra trạng thái thiết lập của các đường hầm VPN. | 20/09/2026 | 21/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Cấu hình định tuyến giữa mạng doanh nghiệp và VPC trên AWS.<br>- Kiểm tra Route Table của VPC và bổ sung các tuyến đến mạng nội bộ khi cần thiết.<br>- Cấu hình các tuyến mạng trên router để chuyển lưu lượng đến AWS qua đường hầm VPN.<br>- Kiểm tra bảng định tuyến và xác minh đường đi của lưu lượng mạng. | 22/09/2026 | 23/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Kiểm tra trạng thái hoạt động của các đường hầm VPN và khả năng trao đổi dữ liệu giữa hai hệ thống mạng.<br>- Thực hiện kiểm tra kết nối bằng lệnh ping và các lệnh kiểm tra định tuyến phù hợp.<br>- Kiểm tra cấu hình dự phòng và xác định khả năng chuyển đổi khi đường hầm chính gặp sự cố, nếu môi trường cho phép.<br>- Tổng hợp kết quả triển khai, ghi nhận lỗi và chuẩn bị cho giai đoạn triển khai máy chủ web trong tuần 7. | 24/09/2026 | 25/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 6:

- Kiểm tra và hoàn thiện các thông tin mạng cần thiết để triển khai kết nối Site-to-Site VPN giữa mạng doanh nghiệp mô phỏng và AWS.
- Tìm hiểu và thực hiện cấu hình Customer Gateway, kết nối VPN và các tham số IPsec theo thiết kế.
- Hiểu cách kiểm tra trạng thái đường hầm VPN và xác định các thông số cần thiết để xử lý sự cố kết nối.
- Cấu hình hoặc rà soát định tuyến giữa mạng nội bộ doanh nghiệp và VPC trên AWS.
- Thực hiện kiểm tra kết nối và đường đi của lưu lượng mạng bằng các công cụ phù hợp.
- Đánh giá cấu hình dự phòng của các đường hầm VPN trong phạm vi môi trường thử nghiệm.
- Chuẩn bị hạ tầng mạng Hybrid Cloud cho giai đoạn triển khai và giám sát máy chủ web trong các tuần tiếp theo.
