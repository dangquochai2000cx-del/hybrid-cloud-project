
---
title: "Worklog Week 10"
date: 2026-10-17
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

- Perform overall testing of the Hybrid Cloud model connecting the enterprise network to AWS through Site-to-Site VPN.
- Verify routing and data exchange between the internal network and the VPC on AWS.
- Evaluate the operation of the web server and the centralized monitoring system using Prometheus, Node Exporter, and Grafana.
- Review security configurations related to Security Groups, VPN, and AWS resource access permissions.
- Evaluate AWS service costs and propose measures to optimize resource usage.

### Tasks to Be Implemented This Week:

| Day | Tasks | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| 2 | - Review the overall architecture of the deployed Hybrid Cloud system.<br>- Check the status of the VPC, Subnet, Route Table, Virtual Private Gateway, and Site-to-Site VPN connection.<br>- Check routing configurations between the enterprise network and the AWS network.<br>- Identify the components that need to be tested across the entire system. | 17/10/2026 | 17/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Test connectivity between the internal network and resources in the AWS VPC.<br>- Use ping and network diagnostic tools to verify data transmission.<br>- Check VPN tunnel status and routing configurations when connectivity issues occur.<br>- Record test results and any issues encountered. | 18/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Check access to the Nginx web server on EC2.<br>- Verify the operation of Prometheus, Node Exporter, and Grafana.<br>- Evaluate the collection, querying, and visualization of CPU, RAM, and disk capacity metrics.<br>- Review Security Groups, service ports, and access rules to restrict unnecessary traffic. | 20/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Review usage information and costs for AWS services during deployment.<br>- Identify resources that may incur charges when not in use, such as EC2, EBS, and related networking components.<br>- Propose cost optimization measures by stopping or releasing unnecessary resources after testing is complete.<br>- Summarize the results, evaluate the strengths and limitations of the Hybrid Cloud model, and propose improvements. | 22/10/2026 | 23/10/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 10 Results:

- Tested and evaluated the overall architecture of the Hybrid Cloud model connecting the enterprise network to AWS.
- Tested connectivity, routing, and data exchange between the internal network and the AWS VPC.
- Checked the operational status of Site-to-Site VPN and evaluated its ability to handle connectivity issues.
- Verified the operation of the Nginx web server and the monitoring system using Prometheus, Node Exporter, and Grafana.
- Reviewed basic security configurations, including Security Groups, service ports, and resource access permissions.
- Learned how to monitor AWS costs and identify resources that may cause unexpected charges.
- Proposed resource optimization measures, summarized the deployment results, and evaluated the strengths and limitations of the Hybrid Cloud model.
