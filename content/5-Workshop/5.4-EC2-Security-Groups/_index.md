---
title: "Deployment of Amazon EC2 and Security Group Configuration"
date: 2026-10-30
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Overview of Amazon EC2

Amazon Elastic Compute Cloud (Amazon EC2) is an AWS service that provides virtual servers in the cloud. In the Hybrid Cloud model, EC2 is used to deploy essential services, including web servers and system monitoring components.

In this project, an EC2 instance running Ubuntu Server 24.04 is deployed in the public subnet of the `HYBRID-CLOUD-VPC`. This instance is used to run Nginx, Prometheus, Node Exporter, and Grafana for testing and monitoring purposes.

#### Deployment Objectives

- Create an EC2 instance in the AWS public subnet.
- Use Ubuntu Server 24.04 as the operating system.
- Configure Security Groups to control inbound traffic to the instance.
- Connect to the EC2 instance through SSH.
- Install and verify the Nginx service.
- Prepare the environment for deploying centralized monitoring components.

#### EC2 Instance Specifications

| Component | Configuration |
|---|---|
| Instance Name | `HYBRID-CLOUD-WEBSERVER-SG` |
| Operating System | Ubuntu Server 24.04 |
| Instance Type | `t3.micro` |
| VPC | `HYBRID-CLOUD-VPC` |
| Subnet | `AWS-PUBLIC-SUBNET` |
| Private IPv4 Address | `10.100.1.118` |
| Root Volume | 8 GiB gp3 |
| Web Server | Nginx |
| Monitoring Components | Prometheus, Node Exporter, Grafana |

**[Insert image here: EC2 instance details in the AWS Management Console]**

Note: The public IPv4 address of an EC2 instance may change after the instance is stopped and started if an Elastic IP is not assigned. Before accessing the services, check the current public IP address in the AWS Console.

#### Deploying an EC2 Instance

Follow these steps:

1. Access the **AWS Management Console**.
2. Open the **Amazon EC2** service.
3. Select **Instances**, then click **Launch instances**.
4. Enter `HYBRID-CLOUD-WEBSERVER-SG` as the instance name.
5. Select **Ubuntu Server 24.04 LTS** as the operating system.
6. Select the `t3.micro` instance type if it is suitable for the available limits and budget.
7. Create or select a key pair for SSH access.
8. Under **Network settings**, select the VPC `HYBRID-CLOUD-VPC`.
9. Select the subnet `AWS-PUBLIC-SUBNET`.
10. Configure an appropriate Security Group for the services to be deployed.
11. Configure the storage capacity according to the requirements, for example, an 8 GiB gp3 volume.
12. Review the configuration and click **Launch instance**.

**[Insert image here: Launch instance configuration in the AWS Console]**

After launching the instance, verify that its state is **Running** and that the instance status checks have passed before connecting.

#### Configuring Security Groups

A Security Group acts as a virtual firewall at the AWS resource level, controlling inbound and outbound traffic for an EC2 instance.

For this project, inbound rules should follow the principle of allowing only the connections that are actually required.

| Type | Protocol | Port Range | Source | Purpose |
|---|---|---|---|---|
| SSH | TCP | 22 | My IP `/32` | Remote server administration |
| HTTP | TCP | 80 | `0.0.0.0/0` | Access to the Nginx website |
| Custom TCP | TCP | 3000 | My IP `/32` or management network | Access to Grafana when required |
| Custom TCP | TCP | 9090 | My IP `/32` or monitoring network | Access to Prometheus when required |
| Custom TCP | TCP | 9100 | Prometheus server or monitoring network only | Collect metrics from Node Exporter |

**[Insert image here: Security Group inbound rules in the AWS Console]**

Security considerations:

- Do not expose SSH port 22 to the entire Internet unless absolutely necessary.
- Allow access to monitoring ports only from authorized IP addresses or management networks.
- Do not expose port 9100 publicly because Node Exporter provides system monitoring information.
- Inbound rules must match the actual deployment architecture. If services are accessible only through the VPN, restrict their sources to the corresponding internal network ranges.
- Security Groups are stateful, so response traffic for an allowed connection is automatically permitted.

#### Connecting to the EC2 Instance Using SSH

Once the EC2 instance is running properly, use SSH to administer the Ubuntu operating system.

On a Windows computer, open PowerShell and navigate to the directory containing the private key. Run the following command, replacing the key path and IP address with the actual values:

```bash
ssh -i "hybrid-cloud-webserver-key.pem" ubuntu@<PUBLIC_IP>