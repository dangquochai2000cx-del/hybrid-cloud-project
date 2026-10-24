
---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Nội dung dưới đây trình bày định hướng và kế hoạch triển khai dự án. Khi hoàn thiện báo cáo, cần điều chỉnh để phản ánh chính xác kết quả thực tế đã thực hiện.
{{% /notice %}}

Tại phần này, trình bày tổng quan dự án, các vấn đề cần giải quyết, kiến trúc hệ thống, phương án triển khai, lộ trình thực hiện, ngân sách dự kiến, rủi ro và kết quả kỳ vọng.

# Thiết kế và triển khai hệ thống Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh bằng VPN Site-to-Site tích hợp giải pháp giám sát tập trung

## 1. Tóm tắt điều hành

Dự án **Hybrid Cloud cho hệ thống mạng doanh nghiệp đa chi nhánh** được xây dựng nhằm nghiên cứu và triển khai mô hình kết nối giữa hạ tầng mạng doanh nghiệp tại chỗ (On-premises) với nền tảng điện toán đám mây Amazon Web Services (AWS).

Hệ thống sử dụng mô hình Hybrid Cloud, trong đó hạ tầng mạng doanh nghiệp được mô phỏng bằng EVE-NG với các thiết bị mạng Cisco, bao gồm router, firewall Cisco ASA và các mạng LAN tại nhiều chi nhánh. Kết nối giữa hệ thống mạng tại chỗ và AWS được thiết lập thông qua AWS Site-to-Site VPN sử dụng IPsec, cho phép các mạng nội bộ trao đổi dữ liệu qua kết nối được mã hóa.

Bên cạnh giải pháp kết nối mạng, dự án tích hợp hệ thống giám sát tập trung nhằm theo dõi tình trạng hoạt động của máy chủ, thiết bị mạng và các thành phần dịch vụ. Prometheus được sử dụng để thu thập và lưu trữ dữ liệu giám sát dạng chuỗi thời gian, Grafana cung cấp giao diện trực quan hóa và cảnh báo, trong khi ELK Stack hỗ trợ thu thập, tìm kiếm và phân tích nhật ký hệ thống.

Hạ tầng AWS được triển khai với các dịch vụ như Amazon VPC, EC2, Virtual Private Gateway và Site-to-Site VPN. Mô hình được thiết kế theo hướng có khả năng mở rộng, hỗ trợ nhiều chi nhánh và có thể bổ sung các cơ chế dự phòng nhằm nâng cao tính sẵn sàng của hệ thống.

## 2. Tuyên bố vấn đề

### Vấn đề hiện tại

Trong môi trường doanh nghiệp có nhiều chi nhánh, việc kết nối các mạng LAN riêng biệt và trao đổi dữ liệu với hệ thống máy chủ tập trung đặt ra các yêu cầu về bảo mật, khả năng quản trị và tính ổn định.

Nếu các chi nhánh hoạt động độc lập, việc truy cập tài nguyên dùng chung, quản lý máy chủ và xử lý sự cố mạng có thể gặp nhiều khó khăn. Việc giám sát thiết bị phân tán cũng làm tăng thời gian phát hiện và khắc phục sự cố.

Ngoài ra, khi doanh nghiệp chuyển một phần hạ tầng lên nền tảng đám mây, cần có giải pháp kết nối an toàn giữa mạng nội bộ và tài nguyên cloud, đồng thời đảm bảo định tuyến phù hợp, kiểm soát truy cập và theo dõi trạng thái kết nối.

### Giải pháp đề xuất

Dự án xây dựng mô hình Hybrid Cloud kết nối mạng doanh nghiệp đa chi nhánh với AWS thông qua VPN Site-to-Site.

Giải pháp gồm các thành phần chính:

- **Hạ tầng mạng doanh nghiệp:** Sử dụng EVE-NG để mô phỏng hệ thống mạng gồm các router, switch, firewall Cisco ASA và nhiều mạng LAN đại diện cho các phòng ban hoặc chi nhánh.
- **Kết nối Hybrid Cloud:** Sử dụng Amazon VPC để xây dựng mạng riêng trên AWS và AWS Site-to-Site VPN để thiết lập kết nối IPsec giữa mạng doanh nghiệp với Virtual Private Gateway.
- **Máy chủ cloud:** Sử dụng Amazon EC2 để triển khai máy chủ dịch vụ, máy chủ web hoặc các thành phần giám sát cần thiết.
- **Định tuyến và dự phòng:** Cấu hình định tuyến giữa các mạng nội bộ và VPC; sử dụng hai đường hầm VPN và cơ chế chuyển đổi đường đi khi kết nối chính gặp sự cố.
- **Giám sát tập trung:** Sử dụng Prometheus và Grafana để theo dõi các chỉ số hệ thống, kết hợp ELK Stack để tập trung hóa và phân tích log.
- **Bảo mật:** Áp dụng các quy tắc firewall, Security Group, Network ACL khi phù hợp, cùng với chính sách định tuyến và phân quyền truy cập nhằm hạn chế lưu lượng không cần thiết.

Mô hình được triển khai trong môi trường lab để kiểm thử khả năng kết nối, trao đổi dữ liệu, truy cập dịch vụ cloud, giám sát và xử lý sự cố.

### Lợi ích và hiệu quả đầu tư (ROI)

Dự án mang lại các lợi ích dự kiến sau:

- Kết nối tập trung các chi nhánh với tài nguyên trên AWS thông qua đường truyền VPN được mã hóa.
- Hỗ trợ doanh nghiệp sử dụng kết hợp hạ tầng tại chỗ và tài nguyên điện toán đám mây.
- Cải thiện khả năng giám sát tình trạng hoạt động của máy chủ và thiết bị mạng.
- Rút ngắn thời gian phát hiện, phân tích và xử lý sự cố thông qua dashboard, cảnh báo và hệ thống log tập trung.
- Tạo môi trường thực hành về mạng doanh nghiệp, bảo mật, điện toán đám mây và giám sát hạ tầng.
- Xây dựng nền tảng có thể mở rộng thêm chi nhánh, máy chủ và các dịch vụ giám sát khi có nhu cầu.

Hiệu quả đầu tư được đánh giá thông qua mức độ đáp ứng yêu cầu kỹ thuật, khả năng tái sử dụng hạ tầng, thời gian xử lý sự cố và chi phí vận hành. Do đây là mô hình nghiên cứu và triển khai trong môi trường lab, lợi ích tài chính cần được đánh giá dựa trên kết quả thực tế.

## 3. Kiến trúc giải pháp

Hệ thống áp dụng mô hình Hybrid Cloud, kết hợp hạ tầng mạng doanh nghiệp được mô phỏng trên EVE-NG với tài nguyên cloud trên AWS.

Tại phía doanh nghiệp, các mạng LAN được kết nối thông qua các thiết bị định tuyến và firewall. Router biên đảm nhiệm việc thiết lập VPN IPsec với AWS. Tại phía cloud, Amazon VPC cung cấp không gian mạng riêng, trong đó các subnet và EC2 được cấu hình theo mục đích sử dụng.

Luồng kết nối chính được thiết kế như sau:

1. Người dùng tại các mạng LAN truy cập tài nguyên nội bộ hoặc máy chủ trên AWS.
2. Lưu lượng đến mạng cloud được định tuyến qua router biên và firewall theo cấu hình của hệ thống.
3. Router thiết lập đường hầm IPsec tới AWS Site-to-Site VPN.
4. AWS tiếp nhận lưu lượng tại Virtual Private Gateway và định tuyến tới các subnet đích.
5. Các máy chủ trên AWS cung cấp dịch vụ theo chính sách Security Group và cấu hình mạng tương ứng.
6. Hệ thống giám sát thu thập dữ liệu từ máy chủ và các thành phần được hỗ trợ, sau đó hiển thị thông tin trên dashboard Grafana và hỗ trợ phân tích log bằng ELK Stack.

![Kiến trúc Hybrid Cloud](../images/2-Proposal/hybrid_cloud_architecture.png)

![Kiến trúc giám sát tập trung](../images/2-Proposal/monitoring_architecture.png)

### Dịch vụ và công nghệ sử dụng

- **EVE-NG:** Mô phỏng hạ tầng mạng doanh nghiệp, router, switch, firewall và nhiều mạng LAN.
- **Cisco IOS và Cisco ASA:** Cấu hình định tuyến, firewall, NAT và các chính sách kiểm soát lưu lượng.
- **Amazon VPC:** Xây dựng mạng riêng trên AWS, bao gồm các subnet và bảng định tuyến.
- **AWS Site-to-Site VPN:** Thiết lập kết nối IPsec giữa mạng doanh nghiệp và AWS.
- **Virtual Private Gateway:** Cổng kết nối VPN phía AWS, gắn với VPC.
- **Amazon EC2:** Triển khai máy chủ ứng dụng và các thành phần giám sát.
- **Amazon VPC Route Tables:** Quản lý đường đi của lưu lượng giữa các subnet và mạng kết nối VPN.
- **Prometheus:** Thu thập các chỉ số hiệu năng và trạng thái của máy chủ, dịch vụ được cấu hình giám sát.
- **Grafana:** Trực quan hóa số liệu trên dashboard và hỗ trợ cấu hình cảnh báo.
- **ELK Stack:** Elasticsearch, Logstash và Kibana phục vụ lưu trữ, xử lý, tìm kiếm và phân tích log.
- **AWS CloudWatch:** Theo dõi các chỉ số và nhật ký của những dịch vụ AWS được hỗ trợ.

### Thiết kế thành phần

**Hạ tầng mạng doanh nghiệp**

Mô hình mạng bao gồm các mạng LAN đại diện cho nhiều phòng ban hoặc chi nhánh. Các thiết bị router và firewall chịu trách nhiệm định tuyến, kiểm soát lưu lượng và chuyển tiếp dữ liệu giữa các mạng.

**Lớp kết nối VPN**

AWS Site-to-Site VPN cung cấp các đường hầm IPsec để truyền dữ liệu an toàn giữa mạng doanh nghiệp và VPC. Dự án nghiên cứu cấu hình hai đường hầm và cơ chế định tuyến dự phòng, đồng thời kiểm tra khả năng duy trì kết nối khi một đường hầm gặp sự cố.

**Hạ tầng AWS**

Amazon VPC cung cấp không gian địa chỉ IP riêng. Các subnet được phân chia theo chức năng và chính sách truy cập. Amazon EC2 được sử dụng để triển khai máy chủ web hoặc máy chủ giám sát tùy theo giai đoạn thực hiện.

**Hệ thống giám sát**

Prometheus thu thập chỉ số từ các exporter hoặc endpoint tương thích. Grafana hiển thị CPU, RAM, dung lượng ổ đĩa, trạng thái dịch vụ và các chỉ số mạng có thể thu thập được. ELK Stack hỗ trợ tổng hợp và phân tích nhật ký từ các máy chủ hoặc thiết bị có khả năng xuất log phù hợp.

**Lớp bảo mật**

Firewall, Security Group và chính sách định tuyến được cấu hình theo nguyên tắc chỉ cho phép lưu lượng cần thiết. Các giao thức quản trị và giao diện giám sát cần được giới hạn theo nguồn truy cập phù hợp, tránh mở trực tiếp các cổng quản trị ra Internet.

## 4. Triển khai kỹ thuật

### Các giai đoạn triển khai

Dự án được chia thành bốn giai đoạn chính.

**Giai đoạn 1: Khảo sát và thiết kế kiến trúc**

- Tìm hiểu mô hình Hybrid Cloud và yêu cầu kết nối mạng doanh nghiệp đa chi nhánh.
- Nghiên cứu nguyên lý hoạt động của VPN IPsec và AWS Site-to-Site VPN.
- Thiết kế sơ đồ mạng trên EVE-NG, xác định các mạng LAN, router biên, firewall và vùng mạng AWS.
- Xác định kế hoạch địa chỉ IP, bảng định tuyến và phương án dự phòng.

**Giai đoạn 2: Xây dựng hạ tầng và thiết lập VPN**

- Triển khai các thiết bị mạng và cấu hình địa chỉ IP trong EVE-NG.
- Cấu hình định tuyến nội bộ, định tuyến mặc định và các chính sách NAT cần thiết.
- Tạo VPC, subnet, Virtual Private Gateway và VPN Connection trên AWS.
- Cấu hình router để thiết lập đường hầm IPsec.
- Kiểm tra trạng thái tunnel, khả năng ping các địa chỉ đầu cuối VPN và kết nối giữa các mạng được phép.

**Giai đoạn 3: Triển khai máy chủ và giải pháp giám sát**

- Triển khai EC2 phục vụ ứng dụng web hoặc các dịch vụ cần thiết.
- Cấu hình Prometheus để thu thập số liệu từ các endpoint giám sát.
- Triển khai Grafana và xây dựng dashboard theo dõi tài nguyên hệ thống.
- Triển khai ELK Stack khi đủ tài nguyên, cấu hình thu thập và phân tích log.
- Kiểm tra kết nối quản trị và luồng dữ liệu giám sát qua VPN theo kiến trúc đã thiết kế.

**Giai đoạn 4: Kiểm thử, tối ưu và hoàn thiện tài liệu**

- Kiểm tra khả năng kết nối giữa các mạng LAN và tài nguyên AWS.
- Kiểm thử truy cập dịch vụ theo chính sách firewall và Security Group.
- Mô phỏng sự cố đường hầm VPN để đánh giá khả năng chuyển đổi tuyến.
- Kiểm tra khả năng thu thập số liệu, hiển thị dashboard và phân tích log.
- Tối ưu cấu hình mạng, quyền truy cập và tài nguyên cloud.
- Hoàn thiện sơ đồ kiến trúc, bảng địa chỉ IP, cấu hình thiết bị và báo cáo kết quả.

### Yêu cầu kỹ thuật

**Hạ tầng mạng**

- Sử dụng EVE-NG và môi trường ảo hóa để xây dựng mô hình mạng.
- Cấu hình router, firewall Cisco ASA, các mạng LAN và kết nối WAN.
- Xây dựng bảng địa chỉ IP rõ ràng, hạn chế trùng lặp giữa các mạng.
- Cấu hình định tuyến hai chiều giữa mạng doanh nghiệp và VPC.
- Kiểm thử định tuyến dự phòng khi sử dụng hai đường hầm VPN.

**Hạ tầng AWS**

- Sử dụng Amazon VPC và các subnet phù hợp với thiết kế.
- Tạo Virtual Private Gateway và AWS Site-to-Site VPN.
- Cấu hình route table để chuyển lưu lượng tới các mạng doanh nghiệp qua VPN.
- Triển khai EC2 theo nhu cầu thực tế và giới hạn tài nguyên để tiết kiệm chi phí.
- Thiết lập Security Group chỉ cho phép các cổng dịch vụ cần thiết.

**Hệ thống giám sát**

- Cài đặt Prometheus để thu thập số liệu từ các máy chủ hoặc exporter tương thích.
- Sử dụng Grafana để xây dựng dashboard và cấu hình cảnh báo.
- Triển khai ELK Stack nếu tài nguyên cho phép để thu thập và phân tích log.
- Đánh giá tài nguyên CPU, RAM, dung lượng ổ đĩa và lưu lượng mạng.
- Giới hạn quyền truy cập vào các giao diện quản trị và giám sát.

## 5. Lộ trình và mốc triển khai

Dự án được triển khai theo các mốc công việc chính trong thời gian thực tập từ ngày 10/08 đến ngày 01/12.

- **Giai đoạn 1 – Khảo sát và thiết kế:** Nghiên cứu công nghệ Hybrid Cloud, thiết kế sơ đồ mạng, quy hoạch IP và xây dựng kiến trúc kết nối AWS.
- **Giai đoạn 2 – Xây dựng hạ tầng mạng:** Triển khai mô hình trên EVE-NG, cấu hình router, firewall và kiểm tra khả năng kết nối nội bộ.
- **Giai đoạn 3 – Triển khai AWS VPN:** Tạo VPC, subnet, Virtual Private Gateway và VPN Connection; cấu hình tunnel và định tuyến giữa hai phía.
- **Giai đoạn 4 – Triển khai máy chủ cloud:** Tạo EC2 và kiểm tra khả năng truy cập dịch vụ từ các mạng được phép.
- **Giai đoạn 5 – Tích hợp giám sát:** Triển khai Prometheus, Grafana và ELK Stack theo khả năng tài nguyên; kiểm tra việc thu thập chỉ số và log.
- **Giai đoạn 6 – Kiểm thử và hoàn thiện:** Kiểm tra kết nối, dự phòng, bảo mật, hiệu năng và hoàn thiện báo cáo.

Sau giai đoạn thực tập, mô hình có thể tiếp tục được mở rộng để nghiên cứu thêm về tự động hóa cấu hình, cảnh báo nâng cao, quản lý cấu hình tập trung và các cơ chế bảo mật cloud.

## 6. Ước tính ngân sách

Chi phí của dự án phụ thuộc vào thời gian sử dụng VPN, số lượng EC2, dung lượng lưu trữ, lưu lượng dữ liệu và tài nguyên dành cho các công cụ giám sát.

Có thể tham khảo công cụ [AWS Pricing Calculator](https://calculator.aws/) để ước tính chi phí theo cấu hình triển khai thực tế.

### Các hạng mục chi phí

- **Amazon EC2:** Chi phí máy chủ chạy ứng dụng hoặc hệ thống giám sát, phụ thuộc vào loại instance và thời gian hoạt động.
- **Amazon EBS:** Chi phí ổ đĩa lưu trữ gắn với EC2.
- **AWS Site-to-Site VPN:** Chi phí sử dụng kết nối VPN và các khoản phí truyền dữ liệu liên quan.
- **Amazon VPC:** Các thành phần mạng cơ bản như VPC, subnet và route table thường không phát sinh phí riêng; các tài nguyên liên quan có thể phát sinh phí.
- **Amazon CloudWatch:** Có thể phát sinh phí khi vượt các mức sử dụng miễn phí đối với chỉ số, log hoặc cảnh báo.
- **Prometheus và Grafana:** Phần mềm có thể triển khai trên EC2, nhưng tài nguyên máy chủ và lưu trữ vẫn phát sinh chi phí.
- **ELK Stack:** Cần dự trù CPU, RAM, dung lượng ổ đĩa và chi phí lưu trữ log nếu triển khai trên EC2.
- **EVE-NG và môi trường ảo hóa:** Sử dụng hạ tầng máy tính cá nhân hiện có; chi phí điện và tài nguyên phần cứng được xem xét nếu cần.

### Biện pháp tối ưu chi phí

- Chỉ khởi chạy EC2 khi thực hiện cấu hình, kiểm thử hoặc trình diễn.
- Sử dụng loại instance phù hợp với yêu cầu tài nguyên và khả năng cấp phát.
- Theo dõi chi phí phát sinh trong AWS Billing và thiết lập cảnh báo ngân sách.
- Xóa các tài nguyên không còn sử dụng, đồng thời kiểm tra các thành phần có tính phí riêng trước khi xóa.
- Ưu tiên triển khai từng công cụ giám sát theo giai đoạn để tránh chạy đồng thời nhiều dịch vụ tiêu tốn RAM.
- Không mặc định chi phí bằng 0 chỉ vì instance thuộc chương trình dùng thử hoặc có credits.

Chi phí cuối cùng cần được xác nhận từ AWS Pricing Calculator và hóa đơn sử dụng thực tế. Đặc biệt, chi phí VPN và các tài nguyên giám sát cần được tính riêng thay vì chỉ tính chi phí máy chủ EC2.

## 7. Đánh giá rủi ro

### Ma trận rủi ro

- **Mất kết nối VPN:** Ảnh hưởng cao, có thể xảy ra do sai cấu hình IPsec, lỗi định tuyến hoặc gián đoạn mạng.
- **Định tuyến sai:** Ảnh hưởng cao, có thể làm mất kết nối giữa các chi nhánh và tài nguyên cloud.
- **Truy cập trái phép:** Ảnh hưởng cao nếu firewall, Security Group hoặc giao diện quản trị được cấu hình không an toàn.
- **Thiếu tài nguyên giám sát:** Ảnh hưởng trung bình đến cao khi EC2 không đủ CPU, RAM hoặc dung lượng lưu trữ.
- **Vượt ngân sách AWS:** Ảnh hưởng trung bình đến cao nếu các tài nguyên tính phí tiếp tục hoạt động ngoài thời gian kiểm thử.
- **Mất dữ liệu log:** Ảnh hưởng trung bình nếu không có chính sách lưu trữ và sao lưu phù hợp.

### Chiến lược giảm thiểu rủi ro

- **Đối với VPN:** Kiểm tra trạng thái tunnel, thông số IKE/IPsec, địa chỉ peer, ACL và bảng định tuyến; triển khai hai đường hầm và kiểm thử phương án dự phòng.
- **Đối với định tuyến:** Lập bảng địa chỉ IP, xác định rõ mạng nguồn và mạng đích, kiểm tra đường đi hai chiều và sử dụng traceroute hoặc công cụ tương đương.
- **Đối với bảo mật:** Giới hạn nguồn truy cập SSH, các cổng giám sát và giao diện quản trị; tránh sử dụng quy tắc mở rộng không cần thiết.
- **Đối với tài nguyên:** Theo dõi mức sử dụng CPU, RAM, dung lượng đĩa và điều chỉnh cấu hình phù hợp.
- **Đối với chi phí:** Thiết lập cảnh báo ngân sách, kiểm tra các tài nguyên đang chạy và dừng hoặc xóa tài nguyên không còn cần thiết.
- **Đối với log:** Xây dựng chính sách lưu trữ, giới hạn dung lượng và sao lưu các dữ liệu quan trọng.

### Kế hoạch dự phòng

Khi một đường hầm VPN gặp sự cố, hệ thống được kiểm tra khả năng chuyển lưu lượng sang đường hầm còn lại theo cơ chế định tuyến đã cấu hình. Nếu VPN không thể khôi phục, có thể kiểm tra từng lớp từ kết nối WAN, trạng thái IPsec, định tuyến nội bộ đến route table AWS.

Đối với hệ thống giám sát, cần lưu giữ cấu hình Prometheus, Grafana và ELK để có thể khôi phục sau sự cố. Các cấu hình mạng và tài nguyên AWS có thể được lưu lại dưới dạng tài liệu hoặc mã hạ tầng nhằm hỗ trợ triển khai lại khi cần.

## 8. Kết quả kỳ vọng

### Cải tiến kỹ thuật

- Xây dựng mô hình Hybrid Cloud kết nối mạng doanh nghiệp với AWS thông qua VPN Site-to-Site.
- Thiết lập kết nối giữa các mạng nội bộ và tài nguyên trong VPC theo đúng chính sách định tuyến.
- Kiểm thử hoạt động của hai đường hầm VPN và khả năng chuyển đổi tuyến khi xảy ra sự cố.
- Triển khai máy chủ EC2 phục vụ ứng dụng hoặc dịch vụ cần thiết.
- Xây dựng dashboard giám sát tài nguyên máy chủ bằng Prometheus và Grafana.
- Tích hợp ELK Stack để hỗ trợ thu thập, tìm kiếm và phân tích log khi đủ tài nguyên.
- Hoàn thiện sơ đồ mạng, bảng địa chỉ IP, cấu hình VPN, quy tắc bảo mật và quy trình kiểm thử.

### Giá trị dài hạn

Dự án tạo nền tảng thực hành và nghiên cứu về quản trị mạng doanh nghiệp, điện toán đám mây, bảo mật kết nối và giám sát tập trung. Kiến trúc có thể được mở rộng để kết nối thêm chi nhánh, bổ sung máy chủ, tăng khả năng dự phòng và triển khai các công cụ tự động hóa quản trị.

Thông qua dự án, người thực hiện có cơ hội vận dụng kiến thức mạng máy tính vào môi trường cloud, nâng cao kỹ năng cấu hình thiết bị mạng, triển khai VPN IPsec, quản lý tài nguyên AWS và xây dựng hệ thống giám sát hạ tầng.

Kết quả cuối cùng được đánh giá dựa trên khả năng kết nối thực tế, trạng thái hoạt động của VPN, tính đúng đắn của định tuyến, khả năng truy cập dịch vụ theo chính sách bảo mật và kết quả thu thập dữ liệu giám sát.
