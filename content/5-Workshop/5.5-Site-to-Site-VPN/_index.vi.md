
---
title: "Cấu hình VPN Site-to-Site kết nối mạng doanh nghiệp đa chi nhánh"
date: 2026-10-30
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Tổng quan

Trong phần này, chúng ta sẽ cấu hình kết nối AWS Site-to-Site VPN nhằm kết nối an toàn mạng doanh nghiệp nội bộ được mô phỏng trên EVE-NG với môi trường điện toán đám mây AWS.

Giải pháp sử dụng Virtual Private Gateway (VGW) trên AWS được gắn với Hybrid Cloud VPC và Customer Gateway đại diện cho thiết bị VPN tại mạng doanh nghiệp. Các đường hầm IPsec VPN cung cấp kết nối được mã hóa giữa hai môi trường.

Mạng doanh nghiệp bao gồm mạng tại trụ sở chính và các chi nhánh. Kết nối VPN cho phép các mạng nội bộ được cấp quyền giao tiếp với tài nguyên được triển khai trong AWS VPC.

#### 1. Chuẩn bị môi trường VPN

Trước khi tạo kết nối VPN, cần kiểm tra và chuẩn bị các tài nguyên, thông tin sau:

- AWS VPC đã được tạo.
- Virtual Private Gateway (VGW) đã được gắn với VPC.
- Địa chỉ IP public có thể được AWS truy cập của thiết bị VPN tại mạng doanh nghiệp.
- Các dải địa chỉ CIDR của mạng nội bộ.
- Dải địa chỉ CIDR của AWS VPC.
- Router hoặc thiết bị VPN tại EVE-NG đang hoạt động.

Trong dự án này, AWS VPC sử dụng dải địa chỉ `10.100.0.0/16`. Các dải mạng nội bộ cần được khai báo theo đúng cấu hình thực tế của hệ thống doanh nghiệp.

**Hình 1: AWS VPC và Virtual Private Gateway**

![AWS VPC và Virtual Private Gateway](/images/5-Workshop/5.5-Site-to-Site-VPN/01-vpc-vgw.png)

#### 2. Tạo Customer Gateway

Customer Gateway đại diện cho thiết bị VPN tại mạng doanh nghiệp trong hệ thống AWS.

1. Truy cập AWS Management Console.
2. Mở dịch vụ **VPC**.
3. Trong thanh điều hướng, chọn **Customer Gateways**.
4. Nhấn **Create customer gateway**.
5. Nhập tên mô tả, ví dụ: `HYBRID-CLOUD-CGW`.
6. Chọn phương thức định tuyến phù hợp. Trong bài thực hành này, chọn định tuyến tĩnh nếu hệ thống sử dụng static routing.
7. Chỉ khai báo BGP ASN nếu sử dụng định tuyến động BGP.
8. Nhập địa chỉ IP public có thể được AWS truy cập của thiết bị VPN tại mạng doanh nghiệp.
9. Nhấn **Create customer gateway** để hoàn tất.

**Lưu ý:** Địa chỉ IP của Customer Gateway phải có khả năng được AWS truy cập qua Internet. Không sử dụng địa chỉ private của VMnet8 như `192.168.80.x` làm địa chỉ VPN public endpoint.

**Hình 2: Tạo Customer Gateway**

![Tạo Customer Gateway](/images/5-Workshop/5.5-Site-to-Site-VPN/02-create-customer-gateway.png)

#### 3. Tạo kết nối Site-to-Site VPN

Sau khi tạo Customer Gateway, tiến hành tạo kết nối VPN.

1. Trong giao diện VPC, chọn **Site-to-Site VPN Connections**.
2. Nhấn **Create VPN connection**.
3. Nhập tên kết nối, ví dụ: `HYBRID-CLOUD-S2S-VPN`.
4. Chọn Virtual Private Gateway đã tạo và gắn với VPC.
5. Chọn Customer Gateway vừa tạo.
6. Chọn phương thức định tuyến phù hợp với cấu hình mạng nội bộ.
7. Nếu sử dụng định tuyến tĩnh, khai báo các dải CIDR của mạng doanh nghiệp.
8. Kiểm tra lại cấu hình và nhấn **Create VPN connection**.

AWS sẽ tạo hai đường hầm IPsec VPN cho kết nối. Hai đường hầm này cung cấp các đường kết nối thay thế giữa mạng nội bộ và AWS.

**Hình 3: Tạo kết nối Site-to-Site VPN**

![Tạo kết nối Site-to-Site VPN](/images/5-Workshop/5.5-Site-to-Site-VPN/03-create-vpn-connection.png)

#### 4. Tải cấu hình VPN từ AWS

AWS cung cấp tệp cấu hình chứa các thông số đường hầm và cấu hình mẫu cho thiết bị VPN tại mạng nội bộ.

1. Chọn kết nối VPN vừa tạo.
2. Nhấn **Download configuration**.
3. Chọn nhà sản xuất và nền tảng thiết bị VPN phù hợp nếu có.
4. Tải tệp cấu hình về máy tính.
5. Kiểm tra các thông tin về địa chỉ IP outside tunnel, inside tunnel, pre-shared key, thuật toán mã hóa và các tham số IPsec khác.

Tệp cấu hình được sử dụng làm tài liệu tham khảo khi cấu hình thiết bị VPN trên EVE-NG.

**Lưu ý bảo mật:** Không công khai pre-shared key trong ảnh chụp màn hình, mã nguồn hoặc kho lưu trữ công khai.

**Hình 4: Tải cấu hình VPN từ AWS**

![Tải cấu hình VPN từ AWS](/images/5-Workshop/5.5-Site-to-Site-VPN/04-download-vpn-configuration.png)

#### 5. Cấu hình VPN Tunnel trên Router mạng nội bộ

Sử dụng tệp cấu hình tải từ AWS làm tài liệu tham khảo để cấu hình router tại EVE-NG.

Cấu hình cần đảm bảo các thông số trùng khớp với thông tin AWS cung cấp, bao gồm:

- Địa chỉ IP outside tunnel.
- Địa chỉ IP inside tunnel.
- Pre-shared key.
- Phiên bản IKE và phương thức xác thực.
- Thuật toán mã hóa và kiểm tra tính toàn vẹn.
- Diffie-Hellman group.
- Thời gian tồn tại của IPsec SA và các tham số liên quan.

Tiến hành cấu hình cả hai đường hầm VPN do AWS cung cấp trên thiết bị VPN mạng nội bộ phù hợp.

**Lưu ý:** Câu lệnh cấu hình cụ thể phụ thuộc vào dòng router và hệ điều hành đang sử dụng. Cần sử dụng thông số được AWS tạo ra thay vì sao chép cấu hình mẫu có thông số tunnel khác.

**Hình 5: Cấu hình IPsec VPN trên Router EVE-NG**

![Cấu hình IPsec VPN trên EVE-NG](/images/5-Workshop/5.5-Site-to-Site-VPN/05-configure-router-vpn.png)

#### 6. Cấu hình định tuyến giữa mạng nội bộ và AWS

Để hai môi trường có thể giao tiếp với nhau, cần cấu hình định tuyến ở cả hai phía.

**Trên AWS:**

1. Mở giao diện VPC.
2. Chọn **Route Tables**.
3. Mở route table gắn với các subnet cần giao tiếp với mạng nội bộ.
4. Chọn **Edit routes**.
5. Thêm các dải CIDR của mạng doanh nghiệp.
6. Chọn Virtual Private Gateway làm target.
7. Lưu cấu hình.

**Trên mạng nội bộ:**

1. Cấu hình route đến dải mạng AWS VPC `10.100.0.0/16`.
2. Chỉ định next hop hoặc tunnel interface theo thiết kế VPN.
3. Kiểm tra các router nội bộ có thể chuyển tiếp lưu lượng đến thiết bị VPN.

Đảm bảo các dải CIDR của mạng nội bộ không bị trùng lặp với dải CIDR của AWS VPC.

**Hình 6: Cấu hình Route Table trên AWS**

![Cấu hình Route Table trên AWS](/images/5-Workshop/5.5-Site-to-Site-VPN/06-configure-route-table.png)

**Hình 7: Cấu hình định tuyến trên Router mạng nội bộ**

![Cấu hình định tuyến mạng nội bộ](/images/5-Workshop/5.5-Site-to-Site-VPN/07-configure-onprem-routes.png)

#### 7. Kiểm tra trạng thái VPN Tunnel

Sau khi hoàn tất cấu hình, tiến hành kiểm tra trạng thái hoạt động của các VPN Tunnel.

1. Mở **Site-to-Site VPN Connections** trong giao diện VPC.
2. Chọn kết nối VPN vừa tạo.
3. Mở tab **Tunnel details**.
4. Kiểm tra trạng thái của cả hai tunnel.
5. Xác nhận tunnel hoạt động có trạng thái **UP**.

Trên router EVE-NG, sử dụng các câu lệnh phù hợp để kiểm tra IKE, IPsec Security Associations và trạng thái tunnel interface.

Ví dụ các câu lệnh kiểm tra trên Cisco IOS:

```bash
show crypto isakmp sa
show crypto ipsec sa
show interface tunnel
show ip route
```

Các câu lệnh cụ thể có thể thay đổi tùy theo nền tảng router và cấu hình VPN.

**Hình 8: Trạng thái VPN Tunnel trên AWS**

![Trạng thái VPN Tunnel trên AWS](/images/5-Workshop/5.5-Site-to-Site-VPN/08-vpn-tunnel-status.png)

**Hình 9: Kiểm tra trạng thái IPsec trên Router**

![Kiểm tra trạng thái IPsec](/images/5-Workshop/5.5-Site-to-Site-VPN/09-verify-ipsec-status.png)

#### Kết luận

Trong phần này, chúng ta đã tạo Customer Gateway và kết nối Site-to-Site VPN trên AWS, cấu hình các đường hầm IPsec trên thiết bị VPN mạng nội bộ và thiết lập định tuyến giữa mạng doanh nghiệp với AWS VPC.

Kết nối VPN cung cấp đường truyền được mã hóa giữa hạ tầng mạng nội bộ và môi trường điện toán đám mây. Trong phần tiếp theo, chúng ta sẽ cấu hình định tuyến và cơ chế dự phòng VPN nhằm nâng cao tính sẵn sàng của kết nối.
