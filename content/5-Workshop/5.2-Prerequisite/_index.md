---
title: "Prerequisites"
date: 2026-10-29
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Overview of the Deployment Environment

To deploy a Hybrid Cloud system that connects a multi-branch enterprise network using Site-to-Site VPN and integrates a centralized monitoring solution, we need to prepare both the on-premises network environment and the AWS cloud environment.

The on-premises environment is simulated using EVE-NG, which allows us to build an enterprise network consisting of multiple routers and internal networks at the headquarters and branch offices. AWS is used to deploy the cloud network infrastructure, establish VPN connectivity, and run servers that support centralized monitoring.

#### Required Components

- **EVE-NG:** Used to simulate the multi-branch enterprise network infrastructure, including routers, network devices, and internal LANs.

- **Amazon Web Services (AWS):** Used to deploy the Hybrid Cloud infrastructure, including Amazon VPC, subnets, Internet Gateway, Virtual Private Gateway, route tables, and related resources.

- **AWS Site-to-Site VPN:** Used to establish IPsec VPN tunnels connecting the on-premises network to AWS, ensuring secure data exchange between the two environments.

- **Amazon EC2:** Used to deploy servers running web services and system monitoring components.

- **Prometheus and Node Exporter:** Used to collect performance metrics and server resource utilization data.

- **Grafana:** Used to visualize monitoring data through dashboards, enabling administrators to monitor system status.

- **Administration Computer:** Used to configure network devices in EVE-NG, manage AWS resources, and access the monitoring interface through a web browser.

#### Images of the Deployment Environment

Figure 5.2.1: Enterprise network topology simulated in EVE-NG.

![EVE-NG Network Topology](/images/5-Workshop/5.2-Prerequisite/eve-ng-topology.png)

Figure 5.2.2: Amazon VPC environment on AWS.

![AWS VPC Environment](/images/5-Workshop/5.2-Prerequisite/aws-vpc-fixed.png)

#### Prerequisites Before Deployment

Before starting the workshop, ensure that the following requirements are met:

1. An AWS account with permissions to create and configure the required resources.
2. EVE-NG is installed and accessible for enterprise network simulation.
3. Routers and a network topology for the headquarters and branch offices have been prepared.
4. An IP addressing plan for the internal networks and AWS environment has been developed, ensuring that the address ranges do not overlap.
5. An Internet connection is available to establish Site-to-Site VPN tunnels between the on-premises environment and AWS.
6. An Amazon EC2 environment is ready for deploying Prometheus, Node Exporter, and Grafana.

#### Expected Outcome

After completing the preparation stage, we will have a multi-branch enterprise network simulation environment in EVE-NG, an AWS account ready for use, and an appropriate IP addressing plan.

This provides the foundation for deploying Amazon VPC, configuring AWS networking components, establishing Site-to-Site VPN connectivity, and building a centralized monitoring system in the following sections.