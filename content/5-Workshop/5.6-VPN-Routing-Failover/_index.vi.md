
---
title: "Cấu hình định tuyến và cơ chế dự phòng VPN"
date: 2026-10-30
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Tổng quan

Trong phần này, chúng ta sẽ cấu hình định tuyến và cơ chế dự phòng VPN nhằm nâng cao tính sẵn sàng cho hệ thống Hybrid Cloud.

Mô hình mạng sử dụng hai router tại doanh nghiệp kết nối đến AWS thông qua các kết nối Site-to-Site VPN riêng biệt. Router15 đóng vai trò router chính, trong khi Router16 đảm nhiệm vai trò router dự phòng.

Trong điều kiện hoạt động bình thường, lưu lượng được ưu tiên đi qua đường VPN chính. Khi đường kết nối chính gặp sự cố, lưu lượng sẽ chuyển sang đường VPN dự phòng. Thiết kế này giúp duy trì khả năng giao tiếp giữa mạng doanh nghiệp và AWS khi tunnel VPN hoặc router chính gặp lỗi.

#### 1. Kiểm tra mô hình mạng

Trước khi cấu hình định tuyến, cần kiểm tra lại sơ đồ Hybrid Cloud và xác định các đường kết nối chính, dự phòng.

Mô hình bao gồm:

- **Router15:** Router VPN chính tại mạng doanh nghiệp.
- **Router16:** Router VPN dự phòng.
- **AWS Virtual Private Gateway:** Thiết bị kết cuối các kết nối Site-to-Site VPN trên AWS.
- **VPN chính:** Kết nối Router15 với AWS.
- **VPN dự phòng:** Kết nối Router16 với AWS.
- **Mạng nội bộ doanh nghiệp:** Bao gồm mạng trụ sở chính và các chi nhánh.
- **AWS VPC:** Mạng Cloud sử dụng dải địa chỉ `10.100.0.0/16`.

Mỗi Customer Gateway phải đại diện cho đúng địa chỉ public endpoint của thiết bị VPN tương ứng tại mạng nội bộ.

**Hình 1: Sơ đồ kết nối VPN chính và dự phòng của hệ thống Hybrid Cloud**

![Sơ đồ VPN chính và dự phòng](/images/5-Workshop/5.6-VPN-Routing-Failover/01-vpn-topology.png)

#### 2. Cấu hình định tuyến VPN chính

Cấu hình Router15 làm đường kết nối được ưu tiên sử dụng để đi đến AWS VPC.

Thiết kế định tuyến cần đảm bảo lưu lượng có đích đến `10.100.0.0/16` sử dụng đường VPN chính trong điều kiện hoạt động bình thường.

Đối với router Cisco sử dụng định tuyến tĩnh, có thể cấu hình route kết hợp với tracking object:

```bash
ip route 10.100.0.0 255.255.0.0 Tunnel1 track 100
```

Tracking object cần giám sát một địa chỉ đích có thể truy cập thông qua đường VPN chính. Cấu hình cơ chế tracking phải phù hợp với tunnel interface và sơ đồ mạng thực tế.

**Hình 2: Cấu hình định tuyến VPN chính**

![Cấu hình định tuyến VPN chính](/images/5-Workshop/5.6-VPN-Routing-Failover/02-primary-routing.png)

#### 3. Cấu hình định tuyến VPN dự phòng

Router16 cung cấp đường kết nối thay thế đến AWS khi đường VPN chính gặp sự cố.

Cấu hình route dự phòng với Administrative Distance cao hơn để route này không được ưu tiên khi đường chính vẫn hoạt động.

Ví dụ:

```bash
ip route 10.100.0.0 255.255.0.0 <BACKUP_NEXT_HOP> 10
```

Thay `<BACKUP_NEXT_HOP>` bằng địa chỉ next-hop hoặc interface phù hợp với đường VPN dự phòng.

Nếu hai router cùng tham gia một miền định tuyến nội bộ, cần đảm bảo việc quảng bá route và lựa chọn đường đi được cấu hình thống nhất. Đường dự phòng phải có khả năng được sử dụng khi route chính bị rút khỏi bảng định tuyến.

**Hình 3: Cấu hình định tuyến VPN dự phòng**

![Cấu hình định tuyến VPN dự phòng](/images/5-Workshop/5.6-VPN-Routing-Failover/03-backup-routing.png)

#### 4. Cấu hình Route Tracking và cơ chế chuyển đổi dự phòng

Route Tracking cho phép router phát hiện đường kết nối chính còn hoạt động hay không.

Trên Cisco IOS, có thể sử dụng IP SLA kết hợp với Object Tracking để giám sát khả năng kết nối thông qua đường chính.

Ví dụ cấu hình:

```bash
ip sla 1
 icmp-echo <REACHABLE_DESTINATION> source-interface <SOURCE_INTERFACE>
 frequency 5
exit

ip sla schedule 1 life forever start-time now

track 100 ip sla 1 reachability
```

Địa chỉ đích và source interface cần được lựa chọn theo sơ đồ mạng thực tế. Địa chỉ giám sát phải được truy cập thông qua đường chính và không nên được truy cập qua một đường định tuyến khác không liên quan, vì điều đó có thể khiến router không phát hiện được lỗi VPN chính.

Liên kết tracking object với route tĩnh chính. Khi đường kết nối được giám sát gặp sự cố, route chính sẽ bị loại khỏi bảng định tuyến, cho phép route dự phòng được sử dụng.

**Hình 4: Cấu hình IP SLA và Object Tracking**

![Cấu hình IP SLA và Tracking](/images/5-Workshop/5.6-VPN-Routing-Failover/04-ip-sla-tracking.png)

#### 5. Kiểm tra bảng định tuyến

Sau khi cấu hình các route chính và dự phòng, tiến hành kiểm tra đường đi hiện đang được lựa chọn.

Trên router Cisco, sử dụng các câu lệnh:

```bash
show ip route 10.100.0.0
show track 100
show ip sla statistics
```

Trong điều kiện hoạt động bình thường, xác nhận route đến `10.100.0.0/16` đang sử dụng đường VPN chính.

Đồng thời, kiểm tra route dự phòng đã được cấu hình và có thể được đưa vào bảng định tuyến khi route chính bị rút khỏi hệ thống.

**Hình 5: Kiểm tra route chính trong bảng định tuyến**

![Kiểm tra route chính](/images/5-Workshop/5.6-VPN-Routing-Failover/05-primary-route-verification.png)

#### 6. Kiểm tra cơ chế chuyển đổi VPN dự phòng

Tiến hành kiểm tra có kiểm soát để xác nhận đường VPN dự phòng hoạt động chính xác.

1. Xác nhận kết nối VPN chính đang hoạt động.
2. Kiểm tra khả năng kết nối từ máy tính trong mạng nội bộ đến tài nguyên AWS.
3. Ghi nhận bảng định tuyến hiện tại.
4. Tạm thời vô hiệu hóa đường VPN chính trong môi trường lab.
5. Chờ cơ chế tracking phát hiện sự cố.
6. Kiểm tra route chính đã bị loại khỏi bảng định tuyến.
7. Xác nhận lưu lượng được chuyển sang đường VPN dự phòng.
8. Kiểm tra lại khả năng kết nối đến tài nguyên AWS.
9. Khôi phục đường VPN chính và kiểm tra lại mức độ ưu tiên định tuyến ban đầu.

Sử dụng các câu lệnh sau để kiểm tra:

```bash
show ip route 10.100.0.0
show track 100
show crypto ipsec sa
ping <AWS_PRIVATE_IP>
```

Kết quả kiểm tra cần chứng minh lưu lượng có thể sử dụng đường VPN dự phòng khi đường chính không còn hoạt động.

**Hình 6: Kiểm tra khi VPN chính gặp sự cố**

![Kiểm tra lỗi VPN chính](/images/5-Workshop/5.6-VPN-Routing-Failover/06-primary-failure-test.png)

**Hình 7: Đường VPN dự phòng sau khi chuyển đổi**

![Đường VPN dự phòng](/images/5-Workshop/5.6-VPN-Routing-Failover/07-backup-path.png)

#### 7. Khôi phục đường VPN chính và kiểm tra hoạt động

Sau khi hoàn thành kiểm tra chuyển đổi dự phòng, tiến hành khôi phục đường VPN chính:

1. Kích hoạt lại đường VPN chính.
2. Chờ VPN Tunnel và tracking object khôi phục trạng thái hoạt động.
3. Kiểm tra lại bảng định tuyến.
4. Xác nhận route chính được ưu tiên sử dụng.
5. Kiểm tra kết nối giữa mạng nội bộ và AWS.

Bước này giúp xác nhận hệ thống có thể khôi phục hoạt động bình thường sau khi sự cố tạm thời được xử lý.

**Hình 8: Khôi phục đường VPN chính**

![Khôi phục VPN chính](/images/5-Workshop/5.6-VPN-Routing-Failover/08-primary-recovery.png)

#### Kết luận

Trong phần này, chúng ta đã cấu hình định tuyến VPN chính và dự phòng, triển khai cơ chế Route Tracking, đồng thời kiểm tra quá trình chuyển đổi và khôi phục kết nối giữa mạng doanh nghiệp và AWS.

Router15 đảm nhiệm đường VPN chính, trong khi Router16 đóng vai trò đường dự phòng. Cơ chế chuyển đổi dự phòng giúp nâng cao tính sẵn sàng của hệ thống bằng cách cho phép lưu lượng sử dụng kết nối thay thế khi đường chính gặp sự cố.

Trong phần tiếp theo, chúng ta sẽ triển khai hệ thống giám sát tập trung sử dụng Prometheus, Node Exporter và Grafana.
