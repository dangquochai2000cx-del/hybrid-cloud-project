---
title: "Worklog Week 2"
date: 2026-08-17
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- Study the existing multi-branch enterprise network architecture and the requirements for connecting it to AWS Cloud.
- Identify a suitable Hybrid Cloud architecture for the internship project.
- Plan IP addresses for the AWS network and the enterprise internal networks, ensuring that the network ranges do not overlap.
- Identify the network components required to establish a Site-to-Site VPN connection between the enterprise and AWS.
- Prepare an architecture diagram and an IP addressing plan as the basis for implementation in the following weeks.

### Tasks to Be Implemented This Week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Analyze the requirements of the Hybrid Cloud project.<br>- Identify the system components: enterprise networks at multiple branches, routing devices, AWS Cloud, and planned servers.<br>- Determine the data communication requirements between the internal networks and resources on AWS.<br>- Draft an overall connectivity model between the on-premises environment and AWS. | 17/08/2026 | 17/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Study the network components used in a Hybrid Cloud architecture.<br>- Analyze the roles of Amazon VPC, Subnet, Route Table, Internet Gateway, and Virtual Private Gateway.<br>- Learn the principles of connecting enterprise networks to AWS through Site-to-Site VPN.<br>- Identify the planned traffic flows between the internal networks and the AWS network. | 18/08/2026 | 19/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Develop an IP addressing plan for the AWS network and enterprise internal networks.<br>- Determine the CIDR range for the VPC and the subnets to be used.<br>- Allocate IP addresses to VLANs or LANs at each branch based on the existing network diagram.<br>- Check for overlapping IP address ranges between the internal networks and the AWS network. | 20/08/2026 | 20/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Finalize the Hybrid Cloud architecture diagram connecting the multi-branch enterprise network to AWS.<br>- Consolidate the IP addressing table and identify the components to be implemented in Week 3.<br>- Review the suitability of the architecture and IP addressing plan before actual implementation. | 21/08/2026 | 21/08/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 2 Results:

- Identified the objectives and connectivity requirements between the multi-branch enterprise network and AWS Cloud.
- Developed a preliminary Hybrid Cloud architecture design to serve as the basis for system implementation.
- Gained a better understanding of the roles of AWS networking components:
  - **Amazon VPC:** Provides a private network on AWS.
  - **Subnet:** Divides a VPC into smaller networks for different deployment purposes.
  - **Route Table:** Determines the paths taken by network traffic.
  - **Internet Gateway:** Enables eligible resources in a VPC to communicate with the Internet.
  - **Virtual Private Gateway:** Acts as the AWS-side VPN endpoint for connecting to an external network through Site-to-Site VPN.
- Developed an IP address allocation plan for the VPC, subnets, and enterprise internal networks.
- Identified the importance of avoiding overlapping IP address ranges between AWS and the on-premises network to ensure proper routing.
- Drafted an overall connectivity diagram between the enterprise network, routing devices, and AWS Cloud.
- Prepared the necessary design information for implementing Amazon VPC, subnets, Internet Gateway, and Route Table in Week 3.