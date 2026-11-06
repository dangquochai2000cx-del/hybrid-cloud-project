
---
title: "Worklog Week 4"
date: 2026-09-07
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Learn about Amazon EC2 and its role in deploying servers for the Hybrid Cloud system.
- Understand EC2 instance types, Amazon Machine Images (AMIs), and Amazon EBS storage.
- Launch and configure an EC2 instance in the VPC created in Week 3.
- Configure Security Groups to control inbound and outbound traffic and protect the EC2 instance.
- Learn how to connect to an EC2 instance via SSH and perform basic system checks.
- Understand basic EC2 instance management operations to help control AWS costs.

### Tasks to Be Implemented This Week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Study Amazon EC2, instance types, AMIs, and EBS.<br>- Learn how to select an appropriate instance type and Ubuntu Server AMI for the project.<br>- Review the basic configuration options required when launching an EC2 instance. | 07/09/2026 | 07/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Launch an EC2 instance in the VPC created in Week 3.<br>- Select the AMI, instance type, subnet, and storage capacity.<br>- Create and select a key pair for secure access.<br>- Check the instance status and assigned IP address. | 08/09/2026 | 09/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Create and configure a Security Group for the EC2 instance.<br>- Configure an inbound SSH rule using TCP port 22 and restrict access to the administrator's IP address.<br>- Configure an HTTP rule using TCP port 80 if the instance will host a web server.<br>- Review outbound rules and apply the principle of least privilege. | 09/09/2026 | 10/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Connect to the EC2 instance via SSH.<br>- Inspect the operating system, network configuration, and basic system resources.<br>- Verify connectivity and Security Group settings.<br>- Learn how to stop and start the EC2 instance to help manage AWS costs. | 11/09/2026 | 12/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 4 Results:

- Understanding the role of Amazon EC2 in providing server resources for a Hybrid Cloud system.
- Understand the basic components when initializing an EC2 instance:
  - **AMI:** Provides the initial operating system and software configuration for the instance.
  - **Instance Type:** Specifies computing resources such as CPU and memory.
  - **Amazon EBS:** Provides block-based storage capacity for instances.
  - **Key Pair:** Supports authentication when connecting to a server via SSH.
- Create and configure EC2 instances according to practical needs.
- Understand how to create and apply Security Groups to control network traffic to and from your server.
- Understand the role of inbound and outbound rules in protecting AWS resources.
- Understand how to connect to a Linux server via SSH using key pair.
- Learn how to check EC2 status, IP address, and basic configuration information.
- Recognizing the importance of limiting SSH access sources, opening only necessary service ports, and managing the EC2 lifecycle to control costs.
- Completed the basic server setup and security steps, laying the groundwork for configuring AWS Site-to-Site VPN and Virtual Private Gateway in week 5.