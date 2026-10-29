---
title: "Design and Deployment of AWS Network Infrastructure"
date: 2026-10-30
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Overview of AWS Network Infrastructure

In the Hybrid Cloud model, Amazon Web Services (AWS) provides a cloud computing environment that connects to the enterprise network simulated in EVE-NG. The AWS network infrastructure is designed to provide connectivity between cloud-based servers and internal networks at the headquarters and branch offices.

The main network components include Amazon VPC, subnets, Internet Gateway, and route tables. In addition, a Virtual Private Gateway is used to establish a Site-to-Site VPN connection between AWS and the on-premises network.

#### Deployment Objectives

- Create and configure an Amazon VPC with an appropriate IP address range.
- Build a public subnet to deploy Amazon EC2 instances.
- Connect the VPC to the Internet through an Internet Gateway.
- Configure route tables to control network traffic between AWS, the Internet, and the enterprise network.
- Prepare a Virtual Private Gateway for the Site-to-Site VPN connection.

#### IP Addressing Design

The AWS network infrastructure uses the private IP address range `10.100.0.0/16`. This range is selected to avoid overlapping with the internal networks in the on-premises environment.

| Component | Resource Name | IP Range / Configuration |
|---|---|---|
| Amazon VPC | HYBRID-CLOUD-VPC | `10.100.0.0/16` |
| Public Subnet | AWS-PUBLIC-SUBNET | `10.100.1.0/24` |
| Internet Gateway | HYBRID-CLOUD-IGW | Connects the VPC to the Internet |
| Virtual Private Gateway | VGW | Supports the Site-to-Site VPN connection |
| Route Table | AWS-PUBLIC-RT | Controls routing for the public subnet |

#### Deploying Amazon VPC

Amazon VPC is a logically isolated virtual network in AWS that allows administrators to control IP address ranges, subnets, routing, and network connectivity.

Follow these steps:

1. Access the AWS Management Console.
2. Open the **Amazon VPC** service.
3. Select **Your VPCs**, then click **Create VPC**.
4. Create a VPC and enter `HYBRID-CLOUD-VPC` as the name.
5. Enter `10.100.0.0/16` as the IPv4 CIDR block.
6. Keep the other settings according to the lab requirements.
7. Click **Create VPC** to complete the process.

**[Insert image here: AWS console interface for creating an Amazon VPC]**

After the VPC is created successfully, verify its name and IPv4 address range in the **Your VPCs** list.

#### Creating a Public Subnet

A public subnet is used to deploy servers that require Internet connectivity, such as a web server and a monitoring server.

Follow these steps:

1. In the Amazon VPC console, select **Subnets**.
2. Click **Create subnet**.
3. Select the VPC `HYBRID-CLOUD-VPC`.
4. Set the subnet name to `AWS-PUBLIC-SUBNET`.
5. Select an appropriate Availability Zone, such as `us-east-1b`.
6. Enter `10.100.1.0/24` as the IPv4 subnet CIDR block.
7. Click **Create subnet**.
8. Select the newly created subnet, open **Actions**, and enable **Enable auto-assign public IPv4 address** if new EC2 instances should automatically receive public IPv4 addresses.

**[Insert image here: AWS console configuration for creating the public subnet]**

Note: Enabling automatic public IPv4 address assignment does not replace the need to configure an Internet Gateway and route table.

#### Creating and Attaching an Internet Gateway

An Internet Gateway allows resources in a VPC to communicate with the Internet when the appropriate routing and security configurations are in place.

Follow these steps:

1. In the Amazon VPC console, select **Internet gateways**.
2. Click **Create internet gateway**.
3. Set the name to `HYBRID-CLOUD-IGW`.
4. Click **Create internet gateway**.
5. Select the newly created Internet Gateway.
6. Open **Actions** and select **Attach to a VPC**.
7. Select `HYBRID-CLOUD-VPC` and confirm the attachment.

**[Insert image here: Internet Gateway successfully created and attached to the VPC]**

After completing these steps, verify that the Internet Gateway is attached to the VPC.

#### Configuring the Route Table

A route table determines where network traffic is directed. In this model, the public route table is used to route Internet traffic and traffic destined for enterprise networks through the VPN.

Follow these steps:

1. In the Amazon VPC console, select **Route tables**.
2. Create or select the route table named `AWS-PUBLIC-RT`.
3. Ensure that the route table belongs to `HYBRID-CLOUD-VPC`.
4. Open the **Routes** tab and select **Edit routes**.
5. Add the route `0.0.0.0/0` with `HYBRID-CLOUD-IGW` as the target.
6. Add routes to the enterprise networks through the Virtual Private Gateway after the VPN has been created and configured, using the actual network ranges in the lab.
7. Save the changes and open the **Subnet associations** tab.
8. Associate `AWS-PUBLIC-SUBNET` with `AWS-PUBLIC-RT`.

**[Insert image here: AWS-PUBLIC-RT route table with the default route pointing to the Internet Gateway]**

Routes to on-premises networks will work only after the VPN and the corresponding routing configuration are ready. Do not add network ranges that are not used in the actual environment.

#### Verifying the Deployment

After completing the configuration, verify the following:

- The Amazon VPC uses the CIDR block `10.100.0.0/16`.
- The public subnet uses the CIDR block `10.100.1.0/24`.
- The Internet Gateway is attached to the VPC.
- The route table contains the default route `0.0.0.0/0` pointing to the Internet Gateway.
- The public subnet is associated with the appropriate route table.
- Routes to enterprise networks are added when the Site-to-Site VPN has been configured.

**[Insert image here: Overview of the configured VPC, subnet, Internet Gateway, and route table]**

#### Expected Results

After completing this section, the basic AWS network infrastructure will be ready for deploying EC2 instances and integrating with the enterprise network. Amazon VPC, the public subnet, the Internet Gateway, and the route table provide the foundation for deploying cloud services.

In the next section, we will configure an Amazon EC2 instance and its Security Groups to deploy the services required for the Hybrid Cloud system.