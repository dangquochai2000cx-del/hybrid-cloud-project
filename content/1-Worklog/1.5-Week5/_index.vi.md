
---
title: "Worklog Tuần 5"
date: 2026-09-12
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

- Tìm hiểu các khái niệm và nguyên lý hoạt động của AWS Site-to-Site VPN.
- Tìm hiểu về Virtual Private Gateway (VGW), Customer Gateway (CGW) và kết nối VPN.
- Hiểu vai trò của các đường hầm IPsec trong việc thiết lập kết nối an toàn giữa mạng doanh nghiệp và AWS.
- Tìm hiểu cách định tuyến cho kết nối VPN và phân biệt định tuyến tĩnh với định tuyến động.
- Chuẩn bị môi trường mạng AWS để kết nối với hệ thống mạng doanh nghiệp trong tuần tiếp theo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu AWS Site-to-Site VPN và vai trò của dịch vụ trong việc kết nối mạng doanh nghiệp với VPC trên AWS.<br>- Tìm hiểu Virtual Private Gateway (VGW), Customer Gateway (CGW) và kết nối VPN.<br>- Nghiên cứu kiến trúc cơ bản của kết nối VPN IPsec giữa mạng nội bộ doanh nghiệp và AWS. | 12/09/2026 | 12/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Kiểm tra lại VPC và cấu hình mạng đã triển khai trong các tuần trước.<br>- Kiểm tra Virtual Private Gateway và tìm hiểu cách gắn VGW vào VPC.<br>- Xác định địa chỉ IP public và các thông tin mạng cần thiết để cấu hình Customer Gateway.<br>- Tìm hiểu các điều kiện cần thiết trước khi tạo kết nối Site-to-Site VPN. | 13/09/2026 | 14/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Tìm hiểu các tham số cấu hình của kết nối AWS Site-to-Site VPN.<br>- Nghiên cứu địa chỉ đầu cuối của đường hầm IPsec, khóa chia sẻ trước (Pre-Shared Key), thuật toán mã hóa và địa chỉ IP bên trong đường hầm.<br>- Hiểu mục đích của hai đường hầm VPN do AWS cung cấp nhằm tăng khả năng dự phòng kết nối.<br>- Tổng hợp các thông tin cấu hình VPN cần thiết cho các router tại doanh nghiệp. | 15/09/2026 | 16/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Ôn tập định tuyến tĩnh và định tuyến động trong kết nối Site-to-Site VPN.<br>- Xác định các dải địa chỉ CIDR của mạng nội bộ cần giao tiếp với VPC trên AWS.<br>- Xem xét yêu cầu về Route Table và đường đi của lưu lượng giữa mạng doanh nghiệp với AWS.<br>- Tổng hợp thiết kế VPN và chuẩn bị cho việc cấu hình, kiểm tra kết nối trong tuần 6. | 17/09/2026 | 18/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được trong tuần 5:

- Hiểu các khái niệm cơ bản và nguyên lý hoạt động của AWS Site-to-Site VPN.
- Nắm được vai trò của Virtual Private Gateway, Customer Gateway và kết nối VPN trong việc liên kết mạng doanh nghiệp với VPC trên AWS.
- Hiểu cách các đường hầm IPsec thiết lập kết nối an toàn giữa mạng nội bộ và AWS.
- Tìm hiểu các thông số của đường hầm VPN, bao gồm địa chỉ đầu cuối, khóa chia sẻ trước, tham số mã hóa và địa chỉ IP bên trong đường hầm.
- Hiểu mục đích của hai đường hầm VPN do AWS cung cấp nhằm tăng khả năng dự phòng kết nối.
- Ôn tập định tuyến tĩnh, định tuyến động và xác định các tuyến mạng cần thiết để giao tiếp giữa mạng doanh nghiệp với AWS.
- Hoàn thiện thông tin cấu hình VPN và phương án định tuyến để chuẩn bị tích hợp, kiểm tra kết nối trong tuần 6.
