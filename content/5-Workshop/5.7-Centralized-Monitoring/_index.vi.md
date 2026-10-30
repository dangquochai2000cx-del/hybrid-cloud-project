
---
title: "Triển khai hệ thống giám sát tập trung Prometheus và Grafana"
date: 2026-10-30
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Tổng quan

Trong phần này, chúng ta sẽ triển khai giải pháp giám sát tập trung nhằm theo dõi hiệu suất và mức độ sử dụng tài nguyên của máy chủ Cloud trong hệ thống Hybrid Cloud.

Hệ thống giám sát được triển khai trên máy chủ EC2 sử dụng Ubuntu 24.04 và bao gồm ba thành phần chính:

- **Prometheus:** Thu thập và lưu trữ dữ liệu giám sát dạng chuỗi thời gian.
- **Node Exporter:** Thu thập thông tin tài nguyên máy chủ Linux, bao gồm CPU, RAM, ổ đĩa và mạng.
- **Grafana:** Trực quan hóa dữ liệu giám sát thông qua Dashboard và biểu đồ.

Các thành phần phối hợp với nhau giúp quản trị viên theo dõi hiệu suất máy chủ, phân tích xu hướng sử dụng tài nguyên và phát hiện các vấn đề tiềm ẩn của hạ tầng.

#### 1. Chuẩn bị môi trường giám sát

Trước khi cài đặt các thành phần giám sát, tiến hành kết nối SSH đến máy chủ EC2.

Sử dụng câu lệnh sau trên máy tính cá nhân:

```bash
ssh -i "hybrid-cloud-webserver-key.pem" ubuntu@<EC2_PUBLIC_IP>
```

Thay `<EC2_PUBLIC_IP>` bằng địa chỉ IPv4 Public hiện tại của máy chủ EC2.

Cập nhật danh sách gói phần mềm Ubuntu:

```bash
sudo apt update
sudo apt upgrade -y
```

Kiểm tra phiên bản hệ điều hành:

```bash
lsb_release -a
```

Xác nhận máy chủ đang sử dụng Ubuntu 24.04.

**Hình 1: Kết nối SSH đến máy chủ EC2**

![Kết nối SSH đến EC2](/images/5-Workshop/5.7-Centralized-Monitoring/01-ec2-ssh.png)

#### 2. Cài đặt Node Exporter

Node Exporter có nhiệm vụ thu thập các thông số phần cứng và hệ điều hành Linux, sau đó cung cấp dữ liệu để Prometheus truy vấn.

Tạo tài khoản hệ thống riêng:

```bash
sudo useradd --no-create-home --shell /usr/sbin/nologin node_exporter
```

Tải và giải nén Node Exporter:

```bash
cd /tmp

wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz

tar xvf node_exporter-1.7.0.linux-amd64.tar.gz
```

Sao chép chương trình thực thi vào thư mục hệ thống:

```bash
sudo cp node_exporter-1.7.0.linux-amd64/node_exporter /usr/local/bin/

sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
```

Tạo file cấu hình dịch vụ systemd:

```bash
sudo nano /etc/systemd/system/node_exporter.service
```

Thêm nội dung sau:

```ini
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

Lưu file và khởi động dịch vụ:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now node_exporter
```

Kiểm tra trạng thái dịch vụ:

```bash
sudo systemctl status node_exporter
```

Node Exporter mặc định sử dụng cổng TCP `9100`.

**Hình 2: Cài đặt Node Exporter và kiểm tra trạng thái dịch vụ**

![Node Exporter](/images/5-Workshop/5.7-Centralized-Monitoring/02-node-exporter.png)

#### 3. Cài đặt Prometheus

Prometheus chịu trách nhiệm thu thập và lưu trữ dữ liệu giám sát từ Node Exporter.

Tạo tài khoản hệ thống và các thư mục cần thiết:

```bash
sudo useradd --no-create-home --shell /usr/sbin/nologin prometheus

sudo mkdir -p /etc/prometheus

sudo mkdir -p /var/lib/prometheus
```

Tải và giải nén Prometheus:

```bash
cd /tmp

wget https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz

tar xvf prometheus-2.54.1.linux-amd64.tar.gz
```

Sao chép các file cần thiết:

```bash
sudo cp prometheus-2.54.1.linux-amd64/prometheus /usr/local/bin/

sudo cp prometheus-2.54.1.linux-amd64/promtool /usr/local/bin/

sudo cp -r prometheus-2.54.1.linux-amd64/consoles /etc/prometheus/

sudo cp -r prometheus-2.54.1.linux-amd64/console_libraries /etc/prometheus/
```

Thiết lập quyền sở hữu:

```bash
sudo chown prometheus:prometheus /usr/local/bin/prometheus

sudo chown prometheus:prometheus /usr/local/bin/promtool

sudo chown -R prometheus:prometheus /etc/prometheus

sudo chown -R prometheus:prometheus /var/lib/prometheus
```

**Hình 3: Cài đặt Prometheus**

![Cài đặt Prometheus](/images/5-Workshop/5.7-Centralized-Monitoring/03-prometheus-installation.png)

#### 4. Cấu hình Prometheus

Tạo file cấu hình Prometheus:

```bash
sudo nano /etc/prometheus/prometheus.yml
```

Thêm nội dung sau:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["localhost:9100"]
```

Cấu hình trên khai báo hai đối tượng giám sát:

- `localhost:9090`: Prometheus tự giám sát các thông số hoạt động của chính nó.
- `localhost:9100`: Prometheus thu thập thông tin tài nguyên máy chủ Linux từ Node Exporter.

Thiết lập quyền sở hữu file cấu hình:

```bash
sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml
```

Tạo file dịch vụ systemd:

```bash
sudo nano /etc/systemd/system/prometheus.service
```

Thêm nội dung:

```ini
[Unit]
Description=Prometheus Monitoring
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus/ \
  --web.listen-address=0.0.0.0:9090

[Install]
WantedBy=multi-user.target
```

Khởi động và kích hoạt Prometheus:

```bash
sudo systemctl daemon-reload

sudo systemctl enable --now prometheus
```

Kiểm tra trạng thái dịch vụ:

```bash
sudo systemctl status prometheus
```

**Hình 4: Cấu hình Prometheus**

![Cấu hình Prometheus](/images/5-Workshop/5.7-Centralized-Monitoring/04-prometheus-configuration.png)

**Hình 5: Kiểm tra trạng thái dịch vụ Prometheus**

![Trạng thái Prometheus](/images/5-Workshop/5.7-Centralized-Monitoring/05-prometheus-status.png)

#### 5. Kiểm tra các Prometheus Targets

Mở trình duyệt và truy cập địa chỉ:

```text
http://<EC2_PUBLIC_IP>:9090/targets
```

Thay `<EC2_PUBLIC_IP>` bằng địa chỉ IPv4 Public hiện tại của máy chủ EC2.

Trang Targets hiển thị các endpoint giám sát đã được cấu hình.

Kiểm tra cả hai đối tượng có trạng thái **UP**:

- `prometheus`
- `node_exporter`

Nếu một target có trạng thái DOWN, cần kiểm tra dịch vụ tương ứng và file cấu hình Prometheus.

**Hình 6: Kiểm tra trạng thái Prometheus Targets**

![Prometheus Targets](/images/5-Workshop/5.7-Centralized-Monitoring/06-prometheus-targets.png)

#### 6. Cài đặt Grafana

Grafana cung cấp giao diện Dashboard để trực quan hóa dữ liệu giám sát được Prometheus thu thập.

Cài đặt các gói phần mềm cần thiết:

```bash
sudo apt-get install -y apt-transport-https software-properties-common wget
```

Tạo thư mục lưu trữ khóa:

```bash
sudo mkdir -p /etc/apt/keyrings
```

Thêm khóa xác thực repository của Grafana:

```bash
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

Thêm Grafana repository:

```bash
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

Cập nhật danh sách gói và cài đặt Grafana:

```bash
sudo apt-get update

sudo apt-get install -y grafana
```

Kích hoạt và khởi động Grafana:

```bash
sudo systemctl enable --now grafana-server
```

Kiểm tra trạng thái dịch vụ:

```bash
sudo systemctl status grafana-server
```

Grafana mặc định sử dụng cổng TCP `3000`.

**Hình 7: Cài đặt Grafana và kiểm tra trạng thái dịch vụ**

![Cài đặt Grafana](/images/5-Workshop/5.7-Centralized-Monitoring/07-grafana-installation.png)

#### 7. Truy cập Grafana và thêm Prometheus Data Source

Mở trình duyệt và truy cập Grafana:

```text
http://<EC2_PUBLIC_IP>:3000
```

Đăng nhập bằng tài khoản quản trị đã cấu hình. Với cài đặt mới, thông tin đăng nhập mặc định là:

- Username: `admin`
- Password: `admin`

Grafana thường yêu cầu thay đổi mật khẩu mặc định sau lần đăng nhập đầu tiên.

Tiến hành thêm Prometheus làm nguồn dữ liệu:

1. Mở **Connections**.
2. Chọn **Data sources**.
3. Nhấn **Add data source**.
4. Chọn **Prometheus**.
5. Nhập địa chỉ máy chủ Prometheus:

```text
http://localhost:9090
```

6. Nhấn **Save & test**.

Xác nhận Grafana có thể kết nối thành công đến Prometheus.

**Hình 8: Thêm Prometheus Data Source trong Grafana**

![Grafana Prometheus Data Source](/images/5-Workshop/5.7-Centralized-Monitoring/08-grafana-datasource.png)

#### 8. Tạo Dashboard giám sát hệ thống

Sau khi thêm Prometheus Data Source, tiến hành tạo Dashboard để trực quan hóa hiệu suất máy chủ.

1. Mở **Dashboards**.
2. Chọn **New**.
3. Nhấn **New dashboard**.
4. Thêm một visualization.
5. Chọn Prometheus làm nguồn dữ liệu.
6. Nhập truy vấn PromQL.
7. Lưu Dashboard.

Một số truy vấn PromQL tham khảo:

**Giám sát CPU:**

```promql
100 * (1 - avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])))
```

**Giám sát RAM:**

```promql
100 * (1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)
```

**Giám sát dung lượng ổ đĩa:**

```promql
100 * (1 - node_filesystem_avail_bytes{mountpoint="/",fstype!="tmpfs"} / node_filesystem_size_bytes{mountpoint="/",fstype!="tmpfs"})
```

**Giám sát lưu lượng mạng nhận vào:**

```promql
rate(node_network_receive_bytes_total{device!="lo"}[5m])
```

Dashboard có thể hiển thị các thông số CPU, RAM, dung lượng ổ đĩa và lưu lượng mạng của máy chủ.

**Hình 9: Dashboard giám sát trên Grafana**

![Grafana Dashboard](/images/5-Workshop/5.7-Centralized-Monitoring/09-grafana-dashboard.png)

#### 9. Kiểm tra hoạt động của hệ thống giám sát

Để xác nhận hệ thống có thể thu thập dữ liệu theo thời gian thực, tiến hành tạo tải CPU tạm thời trên máy chủ EC2.

Cài đặt stress-ng nếu máy chủ chưa có:

```bash
sudo apt update

sudo apt install -y stress-ng
```

Tạo tải CPU trong khoảng thời gian ngắn:

```bash
stress-ng --cpu 2 --timeout 60s
```

Trong khi bài kiểm tra đang chạy:

1. Mở Dashboard Grafana.
2. Quan sát biểu đồ CPU Utilization.
3. Kiểm tra mức sử dụng CPU có tăng trong quá trình kiểm tra hay không.
4. Chờ quá trình tạo tải kết thúc.
5. Xác nhận mức sử dụng CPU giảm dần về trạng thái bình thường.

Sau khi kiểm tra, xác nhận Prometheus vẫn hiển thị cả hai monitoring target ở trạng thái UP.

**Hình 10: Tạo tải CPU để kiểm tra giám sát**

![Kiểm tra tải CPU](/images/5-Workshop/5.7-Centralized-Monitoring/10-cpu-stress-test.png)

**Hình 11: Theo dõi CPU trên Grafana**

![Giám sát CPU trên Grafana](/images/5-Workshop/5.7-Centralized-Monitoring/11-grafana-cpu-monitoring.png)

#### Kết luận

Trong phần này, chúng ta đã triển khai hệ thống giám sát tập trung sử dụng Prometheus, Node Exporter và Grafana trên máy chủ AWS EC2.

Node Exporter thu thập các thông số của máy chủ Linux, Prometheus lưu trữ và xử lý dữ liệu giám sát, còn Grafana trực quan hóa dữ liệu thông qua các Dashboard.

Giải pháp giám sát giúp quản trị viên theo dõi mức độ sử dụng tài nguyên máy chủ, phát hiện hiệu suất bất thường và đánh giá trạng thái hoạt động của hạ tầng Cloud.

Trong phần tiếp theo, chúng ta sẽ tiến hành kiểm tra toàn bộ hệ thống Hybrid Cloud và dọn dẹp các tài nguyên AWS.
