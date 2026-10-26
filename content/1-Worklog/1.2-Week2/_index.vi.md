---
title: "Worklog Tuần 2"
date: 2026-08-17
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

- Tìm hiểu kiến trúc mạng doanh nghiệp đa chi nhánh hiện có và yêu cầu kết nối với AWS Cloud.
- Xác định mô hình kiến trúc Hybrid Cloud phù hợp với đề tài thực tập.
- Quy hoạch địa chỉ IP cho mạng AWS và các mạng nội bộ tại doanh nghiệp, bảo đảm các dải mạng không bị trùng lặp.
- Xác định các thành phần mạng cần thiết để triển khai kết nối VPN Site-to-Site giữa doanh nghiệp và AWS.
- Chuẩn bị sơ đồ kiến trúc và kế hoạch địa chỉ IP làm cơ sở triển khai trong các tuần tiếp theo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Phân tích yêu cầu của đề tài Hybrid Cloud.<br>- Xác định các thành phần tham gia hệ thống: mạng doanh nghiệp tại các chi nhánh, thiết bị định tuyến, AWS Cloud và máy chủ dự kiến triển khai.<br>- Xác định nhu cầu trao đổi dữ liệu giữa mạng nội bộ và tài nguyên trên AWS.<br>- Phác thảo mô hình kết nối tổng thể giữa hệ thống on-premises và AWS. | 17/08/2026 | 17/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Tìm hiểu các thành phần mạng trong kiến trúc Hybrid Cloud.<br>- Phân tích vai trò của Amazon VPC, Subnet, Route Table, Internet Gateway và Virtual Private Gateway.<br>- Tìm hiểu nguyên lý kết nối mạng doanh nghiệp với AWS thông qua VPN Site-to-Site.<br>- Xác định luồng kết nối dự kiến giữa các mạng nội bộ và mạng AWS. | 18/08/2026 | 19/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Lập kế hoạch địa chỉ IP cho mạng AWS và các mạng nội bộ tại doanh nghiệp.<br>- Xác định dải CIDR cho VPC và các subnet dự kiến sử dụng.<br>- Phân chia địa chỉ IP cho các VLAN hoặc mạng LAN tại các chi nhánh theo sơ đồ mạng hiện có.<br>- Kiểm tra sự trùng lặp giữa các dải địa chỉ IP nội bộ và dải địa chỉ IP trên AWS. | 20/08/2026 | 20/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Hoàn thiện sơ đồ kiến trúc Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh với AWS.<br>- Tổng hợp bảng quy hoạch địa chỉ IP và xác định các thành phần cần triển khai trong tuần 3.<br>- Rà soát tính phù hợp của kiến trúc và kế hoạch địa chỉ IP trước khi triển khai thực tế. | 21/08/2026 | 21/08/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 2:

- Xác định được mục tiêu và yêu cầu kết nối giữa mạng doanh nghiệp đa chi nhánh với AWS Cloud.
- Xây dựng được phương án kiến trúc Hybrid Cloud ở mức thiết kế, làm cơ sở cho việc triển khai hệ thống.
- Hiểu rõ hơn vai trò của các thành phần mạng AWS:
  - **Amazon VPC:** Cung cấp mạng riêng trên AWS.
  - **Subnet:** Phân chia VPC thành các mạng con phục vụ từng mục đích triển khai.
  - **Route Table:** Xác định đường đi của lưu lượng mạng.
  - **Internet Gateway:** Cho phép các tài nguyên phù hợp trong VPC giao tiếp với Internet.
  - **Virtual Private Gateway:** Là đầu cuối VPN phía AWS để kết nối với mạng bên ngoài thông qua VPN Site-to-Site.
- Xây dựng kế hoạch phân bổ địa chỉ IP cho VPC, subnet và các mạng nội bộ tại doanh nghiệp.
- Xác định được sự cần thiết của việc tránh trùng lặp dải địa chỉ IP giữa AWS và mạng on-premises để bảo đảm khả năng định tuyến.
- Phác thảo sơ đồ kết nối tổng thể giữa mạng doanh nghiệp, thiết bị định tuyến và AWS Cloud.
- Chuẩn bị được các thông tin thiết kế cần thiết để triển khai Amazon VPC, subnet, Internet Gateway và Route Table trong tuần 3.