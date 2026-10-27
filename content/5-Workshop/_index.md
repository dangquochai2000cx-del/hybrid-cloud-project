---
title: "Workshop"
date: 2026-10-27
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Design and Implementation of a Hybrid Cloud System Connecting Multi-Branch Enterprise Networks via Site-to-Site VPN Integrated with a Centralized Monitoring Solution

#### Overview

In this workshop, we will learn how to design and implement a **Hybrid Cloud system connecting multi-branch enterprise networks via Site-to-Site VPN integrated with a centralized monitoring solution**.

The model uses EVE-NG to simulate the on-premises enterprise network infrastructure, combined with Amazon Web Services (AWS) to build the cloud computing environment. The internal networks at the headquarters and branch offices are connected to AWS through IPsec-based Site-to-Site VPN tunnels, ensuring secure data exchange between the two environments.

In addition to implementing the Hybrid Cloud connection, the system integrates a redundant routing mechanism to improve network connectivity availability. The centralized monitoring solution uses Prometheus, Node Exporter, and Grafana to collect, monitor, and visualize server performance metrics, helping administrators monitor resources and detect incidents.

Through this workshop, we will practice building a Hybrid Cloud network infrastructure, establishing secure VPN connections, configuring routing between networks, testing network connectivity, and deploying a centralized monitoring system.

The main topics include:

- **Hybrid Cloud Architecture Design:** Building a connectivity model between multi-branch enterprise networks and the AWS environment.
- **AWS Infrastructure Deployment:** Configuring Amazon VPC, Subnets, Internet Gateway, Virtual Private Gateway, and Route Tables.
- **Site-to-Site VPN Configuration:** Establishing IPsec VPN tunnels connecting the on-premises infrastructure to AWS.
- **Routing and Redundancy Configuration:** Configuring routing between internal networks, testing connectivity, and evaluating failover capabilities when a connection fails.
- **Centralized Monitoring Deployment:** Installing Prometheus, Node Exporter, and Grafana to monitor server resources.
- **System Testing and Evaluation:** Testing network connectivity, VPN status, redundancy capabilities, and the operation of the monitoring system.

#### Contents

1. [Hybrid Cloud Architecture Overview](5.1-Workshop-overview/)
2. [Deployment Environment Preparation](5.2-Prerequisite/)
3. [AWS Network Infrastructure Design and Deployment](5.3-AWS-network/)
4. [Configuring Site-to-Site VPN Connections for Multi-Branch Enterprise Networks](5.4-Site-to-Site-VPN/)
5. [Configuring Routing and VPN Failover Mechanisms](5.5-Routing-failover/)
6. [Deploying a Centralized Monitoring System with Prometheus and Grafana](5.6-Monitoring/)
7. [Hybrid Cloud System Testing and Evaluation](5.7-Testing/)
8. [Cleaning Up AWS Resources](5.8-Cleanup/)