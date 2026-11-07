
---
title: "Worklog Week 8"
date: 2026-10-19
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

- Learn about server resource monitoring solutions using Prometheus and Node Exporter.
- Install and configure Prometheus on an EC2 instance running Ubuntu Server.
- Install Node Exporter to collect data on CPU, RAM, disk usage, and system metrics.
- Configure Prometheus to collect data from Node Exporter and verify its operational status.
- Learn about and implement a backup storage solution using Amazon S3.
- Configure IAM Roles and IAM Policies to allow the EC2 instance to access S3 and perform data backups.
- Back up Prometheus, Node Exporter, and Grafana configuration files to S3, and verify the ability to download backup data back to EC2.
- Prepare monitoring data for integration with Grafana in the following week.

### Tasks to Be Implemented This Week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Learn about the architecture and operating principles of Prometheus.<br>- Learn about the role of Node Exporter in collecting Linux system metrics.<br>- Identify the metrics to be monitored, including CPU, RAM, disk capacity, and system status.<br>- Check the status of the EC2 instance deployed in Week 7. | 19/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Update the software package list on Ubuntu Server.<br>- Download and install Prometheus on the EC2 instance.<br>- Configure Prometheus and validate the configuration file before starting the service.<br>- Start Prometheus and check the service status. | 20/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Install Node Exporter to collect resource metrics on Ubuntu Server.<br>- Configure Node Exporter to run as a system service.<br>- Check its operational status and ability to provide metrics on port 9100.<br>- Configure Prometheus to collect data from Node Exporter through the appropriate monitoring target. | 22/10/2026 | 23/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Access the Prometheus web interface and check the system status.<br>- Check the Node Exporter monitoring target and verify that data is being collected successfully.<br>- Test queries for basic server resource metrics.<br>- Learn about and create an Amazon S3 Bucket for storing backup data.<br>- Create an IAM Policy and IAM Role, and configure S3 access permissions for the EC2 instance.<br>- Install and configure AWS CLI on Ubuntu Server to interact with S3.<br>- Back up Prometheus, Node Exporter, and Grafana configuration files, then upload the backups to S3.<br>- Test downloading backup files from S3 to EC2 and verify their contents. | 24/10/2026 | 25/10/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 8 Results:

- Understood the operating principles of Prometheus and the role of Node Exporter in the monitoring system.
- Learned about and installed Prometheus on an EC2 instance running Ubuntu Server.
- Configured and verified the Prometheus service to ensure that the system could start and operate properly.
- Installed Node Exporter to collect CPU, RAM, disk usage, and other Linux system metrics.
- Configured Prometheus to collect data from Node Exporter and checked the status of monitoring targets.
- Learned how to query basic resource metrics through the Prometheus interface.
- Learned about and implemented Amazon S3 to store backup files for the monitoring system.
- Created an S3 Bucket and configured IAM Policies and IAM Roles to grant the EC2 instance access to S3.
- Installed and used AWS CLI to transfer backup data from EC2 to S3 and vice versa.
- Backed up Prometheus, Node Exporter, and Grafana configuration files to S3.
- Tested downloading backup files from S3 to EC2 and verified the integrity of the backup file structure.
- Prepared the Prometheus data source for integration with Grafana and the development of monitoring dashboards in Week 9.