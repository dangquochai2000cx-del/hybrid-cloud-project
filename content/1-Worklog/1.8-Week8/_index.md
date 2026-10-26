
---
title: "Worklog Week 8"
date: 2026-10-03
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

- Learn about server resource monitoring solutions using Prometheus and Node Exporter.
- Install and configure Prometheus on an EC2 instance running Ubuntu Server.
- Install Node Exporter to collect data on CPU, RAM, disk storage, and system metrics.
- Configure Prometheus to collect data from Node Exporter and check its operational status.
- Prepare monitoring data for integration with Grafana in the following week.

### Tasks to Be Implemented This Week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Learn about the architecture and operating principles of Prometheus.<br>- Learn about the role of Node Exporter in collecting Linux system metrics.<br>- Identify the metrics to monitor, including CPU, RAM, disk capacity, and system status.<br>- Check the EC2 instance deployed in Week 7. | 03/10/2026 | 03/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Update the software package list on Ubuntu Server.<br>- Download and install Prometheus on the EC2 instance.<br>- Configure Prometheus and validate the configuration file before starting the service.<br>- Start Prometheus and check the service status. | 04/10/2026 | 05/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Install Node Exporter to collect resource metrics on Ubuntu Server.<br>- Configure Node Exporter to run as a system service.<br>- Check its operational status and verify that metrics are available on port 9100.<br>- Configure Prometheus to collect data from Node Exporter through an appropriate monitoring target. | 06/10/2026 | 07/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Access the Prometheus web interface and check the system status.<br>- Check the Node Exporter monitoring target and confirm that data is being collected successfully.<br>- Query several basic server resource metrics.<br>- Summarize the results and prepare to integrate Prometheus with Grafana in Week 9. | 08/10/2026 | 09/10/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 8 Results:

- Understood the operating principles of Prometheus and the role of Node Exporter in a monitoring system.
- Learned about and performed the installation of Prometheus on an EC2 instance running Ubuntu Server.
- Configured and checked the Prometheus service to ensure that it could start and operate properly.
- Installed Node Exporter to collect CPU, RAM, disk, and other Linux system metrics.
- Configured Prometheus to collect data from Node Exporter and checked the monitoring target status.
- Learned how to query basic resource metrics through the Prometheus interface.
- Prepared the Prometheus data source for integration with Grafana and the creation of a monitoring dashboard in Week 9.
