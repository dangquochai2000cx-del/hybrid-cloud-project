
---
title: "Worklog Week 6"
date: 2026-09-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

- Implement an AWS Site-to-Site VPN connection between the simulated enterprise network and the AWS VPC.
- Configure the VPN components required to establish a secure connection between the internal network and AWS.
- Configure routing to allow the enterprise internal networks to communicate with the AWS VPC network.
- Check the VPN tunnel status and verify data transmission between the two network environments.
- Evaluate connection redundancy and prepare the environment for web server deployment in the following week.

### Tasks to Be Implemented This Week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Check the VPC, Virtual Private Gateway, and VPN information prepared in Week 5.<br>- Check the public IP address of the router in the simulated enterprise network and the network ranges that need to be connected.<br>- Compare the internal network information with the AWS configuration to avoid overlapping CIDR ranges.<br>- Prepare the necessary parameters before configuring the VPN. | 19/09/2026 | 19/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Configure the Customer Gateway and AWS Site-to-Site VPN connection according to the established design.<br>- Download and review the VPN configuration file provided by AWS.<br>- Configure IPsec parameters, pre-shared keys, and tunnel endpoint addresses on the router.<br>- Check the establishment status of the VPN tunnels. | 20/09/2026 | 21/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Configure routing between the enterprise network and the AWS VPC.<br>- Check the VPC Route Table and add routes to the internal network when necessary.<br>- Configure network routes on the router to forward traffic to AWS through the VPN tunnels.<br>- Check the routing table and verify network traffic paths. | 22/09/2026 | 23/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Check the operational status of the VPN tunnels and the ability to exchange data between the two network environments.<br>- Test connectivity using the ping command and appropriate routing diagnostic commands.<br>- Review the redundancy configuration and determine whether failover occurs when the primary tunnel fails, if the environment allows.<br>- Summarize the implementation results, record errors, and prepare for web server deployment in Week 7. | 24/09/2026 | 25/09/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 6 Results:

- Checked and finalized the network information required to implement a Site-to-Site VPN connection between the simulated enterprise network and AWS.
- Learned and performed the configuration of the Customer Gateway, VPN connection, and IPsec parameters according to the design.
- Understood how to check VPN tunnel status and identify the parameters required for troubleshooting connectivity issues.
- Configured or reviewed routing between the enterprise internal network and the AWS VPC.
- Tested connectivity and network traffic paths using appropriate tools.
- Evaluated the VPN tunnel redundancy configuration within the test environment.
- Prepared the Hybrid Cloud network infrastructure for web server deployment and monitoring in the following weeks.
