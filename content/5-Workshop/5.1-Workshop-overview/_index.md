---
title: "Introduction"
date: 2026-10-29
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Introduction to the Hybrid Cloud System

- **Hybrid Cloud** is a model that combines on-premises enterprise network infrastructure with the AWS cloud computing environment. This model allows enterprises to leverage their existing network infrastructure while using cloud services to scale resources and deploy applications.

- **Site-to-Site VPN** provides a secure connection between multi-branch enterprise networks and AWS through encrypted IPsec tunnels. This solution allows internal networks to exchange data with the cloud environment without exposing internal resources directly to the Internet.

- **Centralized Monitoring** uses Prometheus, Node Exporter, and Grafana to collect, monitor, and visualize server performance metrics. This enables administrators to monitor resource utilization, detect anomalies, and support troubleshooting.

#### Workshop Overview

In this workshop, you will build a Hybrid Cloud model consisting of a multi-branch enterprise network simulated using EVE-NG and an AWS environment using Amazon VPC.

- **"On-premises Enterprise Network"** simulates the network infrastructure at the headquarters and branch offices. Routers are configured to connect internal networks and establish Site-to-Site VPN connections with AWS.

- **"AWS Cloud Environment"** uses Amazon VPC to deploy cloud network infrastructure, including subnets, an Internet Gateway, a Virtual Private Gateway, and route tables. Amazon EC2 instances are deployed to provide services and test connectivity between the two environments.

- **"Site-to-Site VPN Connectivity"** uses IPsec tunnels to connect the enterprise network to AWS. Two VPN tunnels are configured to test connectivity and establish a backup mechanism in case of a connection failure.

- **"Centralized Monitoring System"** is deployed on Amazon EC2, using Prometheus to collect metrics, Node Exporter to provide system resource information, and Grafana to display data through dashboards.

Through this workshop, you will practice designing a Hybrid Cloud architecture, deploying Site-to-Site VPN connectivity, configuring routing between networks, testing redundancy capabilities, and building a centralized monitoring system.

![Hybrid Cloud Overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)
![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)