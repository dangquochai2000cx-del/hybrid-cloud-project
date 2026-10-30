
---
title: "Kiểm tra hệ thống Hybrid Cloud và dọn dẹp tài nguyên AWS"
date: 2026-10-30
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Tổng quan

Trong phần cuối cùng này, chúng ta sẽ kiểm tra hoạt động của hệ thống Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh được mô phỏng trên EVE-NG với môi trường điện toán đám mây AWS.

Quá trình kiểm tra bao gồm khả năng kết nối mạng, trạng thái các VPN Tunnel Site-to-Site, cơ chế định tuyến và chuyển đổi dự phòng, khả năng hoạt động của máy chủ EC2 và hệ thống giám sát tập trung sử dụng Prometheus, Node Exporter và Grafana.

Sau khi hoàn thành các bài kiểm tra, chúng ta sẽ rà soát tài nguyên AWS và dọn dẹp những tài nguyên không còn cần thiết nhằm hạn chế các chi phí phát sinh.

#### 1. Kiểm tra tổng thể kiến trúc Hybrid Cloud

Trước khi tiến hành kiểm tra, cần rà soát kiến trúc tổng thể và xác nhận các thành phần cần thiết đã được triển khai.

Hệ thống bao gồm:

- **Hạ tầng mạng nội bộ:** Mạng doanh nghiệp được mô phỏng bằng EVE-NG, bao gồm mạng trụ sở chính và các chi nhánh.
- **AWS VPC:** Mạng Cloud sử dụng dải địa chỉ `10.100.0.0/16`.
- **Virtual Private Gateway:** Cung cấp điểm kết cuối VPN phía AWS.
- **Customer Gateways:** Đại diện cho các thiết bị VPN tại mạng nội bộ.
- **VPN Connections:** Cung cấp kết nối được mã hóa giữa mạng doanh nghiệp và AWS.
- **EC2 Instance:** Máy chủ triển khai Web Server và các thành phần giám sát.
- **Hệ thống giám sát:** Sử dụng Prometheus, Node Exporter và Grafana để theo dõi hiệu suất máy chủ.

**Hình 1: Kiến trúc tổng thể hệ thống Hybrid Cloud**

![Kiến trúc Hybrid Cloud](/images/5-Workshop/5.8-System-Testing-Cleanup/01-hybrid-cloud-architecture.png)

#### 2. Kiểm tra khả năng kết nối mạng

Tiến hành kiểm tra khả năng giao tiếp giữa mạng doanh nghiệp nội bộ và AWS VPC.

Từ một máy tính hoặc router được cấp quyền trong mạng nội bộ, kiểm tra kết nối đến địa chỉ IP private của máy chủ EC2.

Ví dụ:

```bash
ping <EC2_PRIVATE_IP>
```

Thay `<EC2_PRIVATE_IP>` bằng địa chỉ IP private thực tế của máy chủ EC2.

Kiểm tra bảng định tuyến để xác nhận route đến AWS VPC:

```bash
show ip route 10.100.0.0
```

Đảm bảo lưu lượng được chuyển tiếp thông qua đường VPN theo thiết kế.

Nếu kết nối không thành công, cần kiểm tra:

- Các route trong AWS Route Table.
- Cấu hình định tuyến tại mạng nội bộ.
- Trạng thái VPN Tunnel.
- Các quy tắc inbound của Security Group.
- Network ACL nếu đã tùy chỉnh.
- Cấu hình Firewall trên máy chủ.

**Hình 2: Kiểm tra kết nối từ mạng doanh nghiệp đến AWS**

![Kiểm tra kết nối mạng](/images/5-Workshop/5.8-System-Testing-Cleanup/02-network-connectivity.png)

#### 3. Kiểm tra kết nối Site-to-Site VPN

Truy cập AWS VPC Console và mở mục **Site-to-Site VPN Connections**.

Chọn từng kết nối VPN và kiểm tra tab **Tunnel details**.

Xác nhận các VPN Tunnel theo thiết kế đang hoạt động và có trạng thái **UP**.

Trên các router mạng nội bộ, sử dụng các câu lệnh Cisco IOS sau:

```bash
show crypto isakmp sa
show crypto ipsec sa
show interface tunnel
```

Kiểm tra các IPsec Security Association đã được thiết lập và bộ đếm lưu lượng tăng khi có hoạt động giao tiếp giữa mạng doanh nghiệp và AWS.

**Hình 3: Kiểm tra trạng thái VPN Tunnel trên AWS**

![Trạng thái VPN Tunnel AWS](/images/5-Workshop/5.8-System-Testing-Cleanup/03-vpn-status.png)

#### 4. Kiểm tra định tuyến và cơ chế dự phòng VPN

Kiểm tra hoạt động của đường VPN chính và dự phòng theo thiết kế định tuyến.

Kết quả mong đợi:

- Router15 đảm nhiệm đường VPN chính được ưu tiên.
- Router16 đảm nhiệm đường VPN dự phòng.
- Đường dự phòng được sử dụng khi đường chính gặp sự cố.
- Đường chính được ưu tiên trở lại sau khi khôi phục.

Kiểm tra trạng thái định tuyến và tracking:

```bash
show ip route 10.100.0.0
show track 100
show ip sla statistics
```

Thực hiện kiểm tra chuyển đổi dự phòng có kiểm soát:

1. Xác nhận đường VPN chính đang hoạt động.
2. Ghi nhận bảng định tuyến hiện tại.
3. Tạm thời vô hiệu hóa đường chính trong môi trường lab.
4. Kiểm tra cơ chế tracking có phát hiện sự cố hay không.
5. Xác nhận lưu lượng được chuyển sang đường dự phòng.
6. Khôi phục đường VPN chính.
7. Kiểm tra lại mức độ ưu tiên của route ban đầu.

Không thực hiện kiểm tra này trên hệ thống đang vận hành thực tế nếu chưa có kế hoạch bảo trì được phê duyệt.

**Hình 4: Kiểm tra định tuyến VPN chính và dự phòng**

![Kiểm tra VPN Failover](/images/5-Workshop/5.8-System-Testing-Cleanup/04-vpn-failover.png)

#### 5. Kiểm tra máy chủ Web trên EC2

Kiểm tra trạng thái hoạt động của EC2 Instance và Web Server.

Trên Ubuntu, kiểm tra dịch vụ Nginx:

```bash
sudo systemctl status nginx
```

Nếu Nginx chưa hoạt động, khởi động dịch vụ:

```bash
sudo systemctl start nginx
```

Kiểm tra Web Server đang lắng nghe trên cổng `80`:

```bash
sudo ss -tulpn | grep :80
```

Từ trình duyệt được cấp quyền truy cập, mở địa chỉ:

```text
http://<EC2_PUBLIC_IP>
```

Xác nhận trang Web được hiển thị thành công.

Đồng thời, kiểm tra EC2 Instance đang ở trạng thái **Running** trong AWS EC2 Console.

**Hình 5: Kiểm tra trạng thái EC2 Instance**

![Trạng thái EC2 Instance](/images/5-Workshop/5.8-System-Testing-Cleanup/05-ec2-status.png)

**Hình 6: Truy cập Web Server Nginx**

![Web Server Nginx](/images/5-Workshop/5.8-System-Testing-Cleanup/06-nginx-web-server.png)

#### 6. Kiểm tra hệ thống giám sát tập trung

Kiểm tra trạng thái hoạt động của Node Exporter, Prometheus và Grafana trên máy chủ EC2.

Thực hiện các câu lệnh:

```bash
sudo systemctl status node_exporter
sudo systemctl status prometheus
sudo systemctl status grafana-server
```

Truy cập trang Prometheus Targets:

```text
http://<EC2_PUBLIC_IP>:9090/targets
```

Xác nhận hai target `prometheus` và `node_exporter` có trạng thái **UP**.

Tiếp theo, truy cập Grafana:

```text
http://<EC2_PUBLIC_IP>:3000
```

Kiểm tra Dashboard hiển thị các thông số tài nguyên máy chủ như:

- Mức sử dụng CPU.
- Mức sử dụng RAM.
- Dung lượng ổ đĩa.
- Lưu lượng mạng.

Xác nhận các biểu đồ nhận được dữ liệu cập nhật từ Prometheus.

**Hình 7: Kiểm tra Prometheus Targets**

![Prometheus Targets](/images/5-Workshop/5.8-System-Testing-Cleanup/07-prometheus-targets.png)

**Hình 8: Dashboard giám sát tập trung**

![Grafana Monitoring Dashboard](/images/5-Workshop/5.8-System-Testing-Cleanup/08-grafana-dashboard.png)

#### 7. Kiểm tra tài nguyên và chi phí AWS

Trước khi dọn dẹp môi trường, cần rà soát các tài nguyên có khả năng phát sinh chi phí.

Truy cập AWS Management Console và kiểm tra các dịch vụ sau:

- **EC2:** Kiểm tra các instance đang chạy và dung lượng lưu trữ đi kèm.
- **Elastic IP Addresses:** Kiểm tra các địa chỉ được cấp phát nhưng không còn gắn với tài nguyên cần thiết.
- **EBS Volumes:** Kiểm tra các volume không còn sử dụng.
- **Snapshots:** Rà soát các bản snapshot không còn cần thiết.
- **VPN Connections:** Kiểm tra các kết nối Site-to-Site VPN đang hoạt động.
- **NAT Gateway:** Kiểm tra xem có NAT Gateway nào được triển khai hay không.
- **CloudWatch:** Rà soát các tài nguyên giám sát có thể phát sinh thêm chi phí.

Ngoài ra, có thể kiểm tra mức chi tiêu ước tính trong mục **Billing and Cost Management**.

**Lưu ý quan trọng:** Dừng EC2 Instance không đồng nghĩa với việc dừng toàn bộ chi phí liên quan. EBS Volume và một số tài nguyên được giữ lại vẫn có thể phát sinh phí. Địa chỉ IPv4 Public và VPN Connection cũng có thể có chi phí riêng.

**Hình 9: Rà soát tài nguyên AWS**

![Rà soát tài nguyên AWS](/images/5-Workshop/5.8-System-Testing-Cleanup/09-aws-resource-review.png)

#### 8. Dọn dẹp các tài nguyên AWS không cần thiết

Chỉ xóa những tài nguyên không còn cần thiết cho workshop.

Trước khi xóa, cần lưu lại các file cấu hình, ảnh chụp màn hình và kết quả kiểm tra cần thiết.

Quá trình dọn dẹp có thể bao gồm:

**EC2 Instance**

Nếu không còn cần sử dụng máy chủ:

1. Truy cập EC2 Console.
2. Chọn **Instances**.
3. Chọn EC2 Instance sử dụng trong workshop.
4. Chọn **Instance state**.
5. Chọn **Terminate instance** nếu chắc chắn không còn cần sử dụng máy chủ.

**EBS Volumes và Snapshots**

1. Mở mục **Volumes** trong EC2 Console.
2. Kiểm tra các volume chưa được gắn với instance.
3. Chỉ xóa những volume không còn cần thiết và đã được sao lưu nếu cần.
4. Kiểm tra các snapshot và xóa những bản không còn sử dụng.

**Site-to-Site VPN Resources**

Nếu không còn cần sử dụng môi trường VPN:

1. Mở **Site-to-Site VPN Connections**.
2. Xóa các kết nối VPN không còn cần thiết.
3. Kiểm tra và xóa các Customer Gateway không còn sử dụng.
4. Kiểm tra Virtual Private Gateway trước khi thực hiện thao tác detach hoặc delete.

**Các tài nguyên khác**

Rà soát Elastic IP, NAT Gateway và các tài nguyên khác trước khi xóa.

**Lưu ý quan trọng:** Không xóa tài nguyên dùng chung hoặc tài nguyên vẫn được sử dụng bởi các phần khác của dự án. Việc terminate EC2 Instance không thể khôi phục dữ liệu trên instance storage; các tài nguyên liên quan cũng có thể cần được dọn dẹp riêng.

**Hình 10: Dọn dẹp tài nguyên AWS**

![Dọn dẹp tài nguyên AWS](/images/5-Workshop/5.8-System-Testing-Cleanup/10-aws-cleanup.png)

#### 9. Đánh giá tổng thể hệ thống

Sau khi hoàn thành các bài kiểm tra, tiến hành đánh giá hoạt động tổng thể của hệ thống Hybrid Cloud.

Các nội dung đánh giá bao gồm:

- Khả năng kết nối giữa mạng nội bộ và AWS.
- Khả năng thiết lập và hoạt động của các VPN Tunnel Site-to-Site.
- Khả năng lựa chọn route chính và route dự phòng.
- Quá trình chuyển đổi và khôi phục kết nối VPN.
- Khả năng hoạt động của Web Server trên EC2.
- Khả năng thu thập dữ liệu máy chủ của Prometheus.
- Khả năng trực quan hóa dữ liệu giám sát trên Grafana.
- Quá trình rà soát và dọn dẹp các tài nguyên AWS không cần thiết.

Các kết quả cần được ghi nhận bằng ảnh chụp màn hình và minh chứng kiểm tra để đưa vào báo cáo dự án.

**Hình 11: Kiểm tra hoàn thiện hệ thống Hybrid Cloud**

![Kiểm tra hệ thống Hybrid Cloud](/images/5-Workshop/5.8-System-Testing-Cleanup/11-final-system-verification.png)

#### Kết luận

Trong phần cuối cùng này, chúng ta đã kiểm tra hoạt động của hệ thống Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh được mô phỏng trên EVE-NG với môi trường điện toán đám mây AWS.

Các bài kiểm tra bao gồm khả năng kết nối mạng, hoạt động của Site-to-Site VPN, định tuyến và chuyển đổi dự phòng, khả năng hoạt động của Web Server EC2 và hệ thống giám sát tập trung sử dụng Prometheus, Node Exporter và Grafana.

Đồng thời, chúng ta đã rà soát tài nguyên AWS và xác định những tài nguyên có thể dọn dẹp nhằm hạn chế chi phí không cần thiết.

Thông qua workshop này, chúng ta đã hoàn thành quá trình thiết kế, triển khai, giám sát và đánh giá giải pháp Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh với AWS.
