
---
title: "Workshop"
date: 2026-10-27
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Design and Implementation of a Hybrid Cloud System Connecting Multi-Branch Enterprise Networks via Site-to-Site VPN Integrated with a Centralized Monitoring Solution

#### Overview

In this workshop, we will learn how to design and implement a Hybrid Cloud system connecting multi-branch enterprise networks via Site-to-Site VPN integrated with a centralized monitoring solution.

The system uses EVE-NG to simulate the on-premises enterprise network infrastructure and Amazon Web Services (AWS) to build the cloud environment. The internal networks at the headquarters and branch offices connect to AWS through IPsec-based Site-to-Site VPN tunnels, enabling secure communication between the two environments.

The system also implements redundant routing to improve network availability. For centralized monitoring, Prometheus and Node Exporter collect server performance metrics, while Grafana visualizes the collected data through dashboards.

Through this workshop, we will build a Hybrid Cloud network infrastructure, establish secure VPN connections, configure routing between networks, test connectivity and failover, and deploy a centralized monitoring solution.

#### Objectives

- **Hybrid Cloud Architecture:** Design connectivity between multi-branch enterprise networks and AWS.
- **AWS Network Infrastructure:** Configure Amazon VPC, subnets, Internet Gateway, Virtual Private Gateway, and route tables.
- **Amazon EC2 and Security:** Deploy an EC2 instance and configure Security Groups.
- **Site-to-Site VPN:** Establish IPsec VPN tunnels between the on-premises network and AWS.
- **Routing and Failover:** Configure routes, test connectivity, and verify VPN redundancy.
- **Centralized Monitoring:** Deploy Prometheus, Node Exporter, and Grafana.
- **System Testing:** Validate connectivity, VPN operation, failover, and monitoring.

#### Contents

1. [Hybrid Cloud Architecture Overview](5.1-Workshop-overview/)
2. [Deployment Environment Preparation](5.2-Prerequisite/)
3. [AWS Network Infrastructure Design and Deployment](5.3-AWS-Network-Infrastructure/)
4. [Amazon EC2 Deployment and Security Group Configuration](5.4-EC2-Security-Groups/)
5. [Site-to-Site VPN Configuration for Multi-Branch Enterprise Networks](5.5-Site-to-Site-VPN/)
6. [Routing Configuration and VPN Failover Mechanisms](5.6-VPN-Routing-Failover/)
7. [Centralized Monitoring with Prometheus and Grafana](5.7-Centralized-Monitoring/)
8. [Hybrid Cloud System Testing and AWS Resource Cleanup](5.8-System-Testing-Cleanup/)
