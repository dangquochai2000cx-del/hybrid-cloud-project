
---
title: "Centralized Monitoring Deployment with Prometheus and Grafana"
date: 2026-10-30
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Overview

In this section, we will deploy a centralized monitoring solution to monitor the performance and resource utilization of the cloud server in the Hybrid Cloud environment.

The monitoring system is deployed on an Ubuntu 24.04 EC2 instance and consists of three main components:

- **Prometheus:** Collects and stores time-series monitoring metrics.
- **Node Exporter:** Exposes Linux server metrics, including CPU, memory, disk, and network information.
- **Grafana:** Visualizes monitoring data through dashboards and charts.

The components work together to help administrators observe server performance, identify resource usage trends, and detect potential infrastructure issues.

#### 1. Prepare the Monitoring Environment

Before installing the monitoring components, connect to the EC2 instance using SSH.

Use the following command from your local terminal:

```bash
ssh -i "hybrid-cloud-webserver-key.pem" ubuntu@<EC2_PUBLIC_IP>
```

Replace `<EC2_PUBLIC_IP>` with the current public IPv4 address of the EC2 instance.

Update the Ubuntu package index:

```bash
sudo apt update
sudo apt upgrade -y
```

Check the operating system version:

```bash
lsb_release -a
```

Confirm that the instance is running Ubuntu 24.04.

**Image 1: Connect to the EC2 Instance**

![Connect to EC2](/images/5-Workshop/5.7-Centralized-Monitoring/01-ec2-ssh.png)

#### 2. Install Node Exporter

Node Exporter collects hardware and operating system metrics from Linux servers and exposes them for Prometheus to scrape.

Create a dedicated system user:

```bash
sudo useradd --no-create-home --shell /usr/sbin/nologin node_exporter
```

Download and extract Node Exporter:

```bash
cd /tmp

wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz

tar xvf node_exporter-1.7.0.linux-amd64.tar.gz
```

Install the executable:

```bash
sudo cp node_exporter-1.7.0.linux-amd64/node_exporter /usr/local/bin/

sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
```

Create a systemd service:

```bash
sudo nano /etc/systemd/system/node_exporter.service
```

Add the following configuration:

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

Save the file and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now node_exporter
```

Check the service status:

```bash
sudo systemctl status node_exporter
```

Node Exporter uses TCP port `9100` by default.

**Image 2: Node Exporter Installation and Service Status**

![Node Exporter Service](/images/5-Workshop/5.7-Centralized-Monitoring/02-node-exporter.png)

#### 3. Install Prometheus

Prometheus is responsible for collecting and storing monitoring metrics from Node Exporter.

Create a dedicated system user and required directories:

```bash
sudo useradd --no-create-home --shell /usr/sbin/nologin prometheus

sudo mkdir -p /etc/prometheus

sudo mkdir -p /var/lib/prometheus
```

Download and extract Prometheus:

```bash
cd /tmp

wget https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz

tar xvf prometheus-2.54.1.linux-amd64.tar.gz
```

Copy the required files:

```bash
sudo cp prometheus-2.54.1.linux-amd64/prometheus /usr/local/bin/

sudo cp prometheus-2.54.1.linux-amd64/promtool /usr/local/bin/

sudo cp -r prometheus-2.54.1.linux-amd64/consoles /etc/prometheus/

sudo cp -r prometheus-2.54.1.linux-amd64/console_libraries /etc/prometheus/
```

Set the appropriate ownership:

```bash
sudo chown prometheus:prometheus /usr/local/bin/prometheus

sudo chown prometheus:prometheus /usr/local/bin/promtool

sudo chown -R prometheus:prometheus /etc/prometheus

sudo chown -R prometheus:prometheus /var/lib/prometheus
```

**Image 3: Prometheus Installation**

![Prometheus Installation](/images/5-Workshop/5.7-Centralized-Monitoring/03-prometheus-installation.png)

#### 4. Configure Prometheus

Create the Prometheus configuration file:

```bash
sudo nano /etc/prometheus/prometheus.yml
```

Add the following configuration:

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

This configuration defines two monitoring targets:

- `localhost:9090`: Prometheus monitors its own metrics.
- `localhost:9100`: Prometheus collects Linux server metrics from Node Exporter.

Set the configuration file ownership:

```bash
sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml
```

Create a systemd service:

```bash
sudo nano /etc/systemd/system/prometheus.service
```

Add:

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

Start and enable Prometheus:

```bash
sudo systemctl daemon-reload

sudo systemctl enable --now prometheus
```

Check the service:

```bash
sudo systemctl status prometheus
```

**Image 4: Prometheus Configuration**

![Prometheus Configuration](/images/5-Workshop/5.7-Centralized-Monitoring/04-prometheus-configuration.png)

**Image 5: Prometheus Service Status**

![Prometheus Service Status](/images/5-Workshop/5.7-Centralized-Monitoring/05-prometheus-status.png)

#### 5. Verify Prometheus Targets

Open the following address in a web browser:

```text
http://<EC2_PUBLIC_IP>:9090/targets
```

Replace `<EC2_PUBLIC_IP>` with the public IPv4 address of the EC2 instance.

The Targets page should display the configured monitoring endpoints.

Verify that both targets have the status **UP**:

- `prometheus`
- `node_exporter`

If a target is DOWN, check the corresponding service and Prometheus configuration.

**Image 6: Prometheus Targets Status**

![Prometheus Targets](/images/5-Workshop/5.7-Centralized-Monitoring/06-prometheus-targets.png)

#### 6. Install Grafana

Grafana provides dashboards for visualizing the metrics collected by Prometheus.

Install the required packages:

```bash
sudo apt-get install -y apt-transport-https software-properties-common wget
```

Create the keyrings directory:

```bash
sudo mkdir -p /etc/apt/keyrings
```

Add the Grafana package signing key:

```bash
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

Add the Grafana repository:

```bash
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

Update the package index and install Grafana:

```bash
sudo apt-get update

sudo apt-get install -y grafana
```

Enable and start Grafana:

```bash
sudo systemctl enable --now grafana-server
```

Check the service status:

```bash
sudo systemctl status grafana-server
```

Grafana uses TCP port `3000` by default.

**Image 7: Grafana Installation and Service Status**

![Grafana Installation](/images/5-Workshop/5.7-Centralized-Monitoring/07-grafana-installation.png)

#### 7. Access Grafana and Add Prometheus as a Data Source

Open Grafana in a web browser:

```text
http://<EC2_PUBLIC_IP>:3000
```

Log in using the configured administrator credentials. On a fresh installation, the default credentials are:

- Username: `admin`
- Password: `admin`

Grafana will normally require changing the default password after the first login.

To add Prometheus as a data source:

1. Open **Connections**.
2. Select **Data sources**.
3. Choose **Add data source**.
4. Select **Prometheus**.
5. Enter the Prometheus server URL:

```text
http://localhost:9090
```

6. Choose **Save & test**.

Confirm that Grafana can successfully connect to Prometheus.

**Image 8: Add Prometheus Data Source in Grafana**

![Grafana Prometheus Data Source](/images/5-Workshop/5.7-Centralized-Monitoring/08-grafana-datasource.png)

#### 8. Create a Monitoring Dashboard

After adding Prometheus as a data source, create a dashboard to visualize server performance.

1. Open **Dashboards**.
2. Select **New**.
3. Choose **New dashboard**.
4. Add a visualization.
5. Select Prometheus as the data source.
6. Enter a PromQL query.
7. Save the dashboard.

Example PromQL queries:

**CPU Usage:**

```promql
100 * (1 - avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])))
```

**Memory Usage:**

```promql
100 * (1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)
```

**Disk Usage:**

```promql
100 * (1 - node_filesystem_avail_bytes{mountpoint="/",fstype!="tmpfs"} / node_filesystem_size_bytes{mountpoint="/",fstype!="tmpfs"})
```

**Network Receive Traffic:**

```promql
rate(node_network_receive_bytes_total{device!="lo"}[5m])
```

The dashboard can display CPU utilization, memory consumption, disk usage, and network traffic.

**Image 9: Grafana Monitoring Dashboard**

![Grafana Dashboard](/images/5-Workshop/5.7-Centralized-Monitoring/09-grafana-dashboard.png)

#### 9. Test the Monitoring System

To verify that the monitoring system collects real-time metrics, generate a temporary CPU workload on the EC2 instance.

Install stress-ng if it is not already installed:

```bash
sudo apt update

sudo apt install -y stress-ng
```

Generate CPU load for a short period:

```bash
stress-ng --cpu 2 --timeout 60s
```

While the test is running:

1. Open the Grafana dashboard.
2. Observe the CPU utilization graph.
3. Check whether CPU usage increases during the test.
4. Wait for the workload to finish.
5. Verify that CPU usage returns toward its normal level.

After the test, check that Prometheus continues to report both monitoring targets as UP.

**Image 10: Generate CPU Load for Monitoring**

![CPU Stress Test](/images/5-Workshop/5.7-Centralized-Monitoring/10-cpu-stress-test.png)

**Image 11: Monitor CPU Usage in Grafana**

![Grafana CPU Monitoring](/images/5-Workshop/5.7-Centralized-Monitoring/11-grafana-cpu-monitoring.png)

#### Conclusion

In this section, we deployed a centralized monitoring solution using Prometheus, Node Exporter, and Grafana on an AWS EC2 instance.

Node Exporter collects Linux server metrics, Prometheus stores and processes the metrics, and Grafana visualizes the monitoring data through dashboards.

The monitoring solution helps administrators observe server resource utilization, identify abnormal performance, and evaluate the operational status of the cloud infrastructure.

In the next section, we will test the Hybrid Cloud system and clean up AWS resources.
