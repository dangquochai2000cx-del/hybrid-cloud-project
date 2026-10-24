
---
title: "Project Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The following content presents the proposed project direction and implementation plan. Please adjust it to accurately reflect the actual results achieved when completing your report.
{{% /notice %}}

This section presents an overview of the project, the problems to be addressed, the proposed architecture, the implementation plan, the timeline, the estimated budget, potential risks, and expected outcomes.

# Design and Implementation of a Hybrid Cloud System Connecting Multi-Branch Enterprise Networks Using Site-to-Site VPN with Integrated Centralized Monitoring

## 1. Executive Summary

The **Hybrid Cloud System for Multi-Branch Enterprise Networks** project aims to research and implement a connectivity model between an on-premises enterprise network infrastructure and the Amazon Web Services (AWS) cloud platform.

The system adopts a Hybrid Cloud model, in which the enterprise network infrastructure is simulated using EVE-NG with Cisco networking devices, including routers, Cisco ASA firewalls, and LANs representing multiple branches. Connectivity between the on-premises network and AWS is established through AWS Site-to-Site VPN using IPsec, allowing internal networks to exchange data through encrypted tunnels.

In addition to network connectivity, the project integrates a centralized monitoring solution to monitor the operational status of servers, network devices, and system services. Prometheus is used to collect and store time-series monitoring data, Grafana provides visualization dashboards and alerting capabilities, while the ELK Stack supports centralized log collection, searching, and analysis.

The AWS infrastructure uses services such as Amazon VPC, Amazon EC2, Virtual Private Gateway, and Site-to-Site VPN. The architecture is designed to support future expansion to additional branches and to incorporate redundancy mechanisms that improve system availability.

## 2. Problem Statement

### Current Challenges

In a multi-branch enterprise environment, connecting separate LANs and exchanging data with centralized servers introduces requirements for security, manageability, and network reliability.

When branches operate independently, accessing shared resources, managing servers, and troubleshooting network issues can become challenging. Distributed monitoring also increases the time required to detect and resolve incidents.

Furthermore, when an enterprise migrates part of its infrastructure to the cloud, a secure connectivity solution is required between the internal network and cloud resources. The solution must also provide appropriate routing, access control, and connection monitoring.

### Proposed Solution

The project develops a Hybrid Cloud model that connects a multi-branch enterprise network to AWS through Site-to-Site VPN.

The proposed solution consists of the following components:

- **Enterprise Network Infrastructure:** EVE-NG is used to simulate routers, switches, Cisco ASA firewalls, and multiple LANs representing departments or branches.
- **Hybrid Cloud Connectivity:** Amazon VPC provides a private network environment on AWS, while AWS Site-to-Site VPN establishes IPsec connectivity between the enterprise network and a Virtual Private Gateway.
- **Cloud Servers:** Amazon EC2 instances host web applications, network services, or monitoring components as required.
- **Routing and Redundancy:** Routing is configured between internal networks and the VPC. Two VPN tunnels and appropriate failover mechanisms are used to improve connectivity resilience.
- **Centralized Monitoring:** Prometheus and Grafana monitor system metrics, while the ELK Stack centralizes and analyzes log data.
- **Security:** Firewall rules, Security Groups, Network ACLs where appropriate, routing policies, and access controls restrict unnecessary traffic.

The model is implemented in a lab environment to test network connectivity, data exchange, cloud service access, monitoring, and troubleshooting procedures.

### Benefits and Return on Investment (ROI)

The project is expected to provide the following benefits:

- Centrally connect branch networks to AWS resources through encrypted VPN tunnels.
- Support the use of on-premises infrastructure alongside cloud computing resources.
- Improve visibility into the operational status of servers and network devices.
- Reduce incident detection and troubleshooting time through dashboards, alerts, and centralized logs.
- Provide a practical environment for learning enterprise networking, security, cloud computing, and infrastructure monitoring.
- Establish an extensible foundation for additional branches, servers, and monitoring services.

The project's value will be assessed through technical performance, infrastructure reusability, incident response time, and operating costs. As this is a research and lab implementation project, financial benefits should be evaluated using actual results rather than an assumed fixed payback period.

## 3. Solution Architecture

The system adopts a Hybrid Cloud architecture that combines an enterprise network simulated in EVE-NG with cloud resources hosted on AWS.

On the enterprise side, LANs are interconnected through routers and firewalls. Edge routers establish IPsec VPN connections to AWS. On the cloud side, Amazon VPC provides a private network environment containing subnets and EC2 instances configured according to their intended roles.

The main connectivity flow is as follows:

1. Users in enterprise LANs access internal resources or servers hosted on AWS.
2. Traffic destined for cloud networks is routed through the edge routers and firewalls according to the configured network policies.
3. The routers establish IPsec tunnels to AWS Site-to-Site VPN.
4. AWS receives traffic through the Virtual Private Gateway and routes it to the destination subnets.
5. AWS-hosted servers provide services according to their Security Group rules and network configurations.
6. The monitoring system collects data from supported servers and components. Metrics are displayed in Grafana dashboards, while ELK Stack supports log analysis.

![Hybrid Cloud Architecture](../images/2-Proposal/hybrid_cloud_architecture.png)

![Centralized Monitoring Architecture](../images/2-Proposal/monitoring_architecture.png)

### AWS Services and Technologies

- **EVE-NG:** Simulates the enterprise network infrastructure, including routers, switches, firewalls, and multiple LANs.
- **Cisco IOS and Cisco ASA:** Configure routing, firewall policies, NAT, and traffic control.
- **Amazon VPC:** Provides a private network environment on AWS, including subnets and route tables.
- **AWS Site-to-Site VPN:** Establishes IPsec connectivity between the enterprise network and AWS.
- **Virtual Private Gateway:** Provides the AWS-side VPN endpoint attached to the VPC.
- **Amazon EC2:** Hosts application servers and monitoring components.
- **Amazon VPC Route Tables:** Control traffic routing between subnets and enterprise networks connected through the VPN.
- **Prometheus:** Collects performance metrics and status information from configured servers and services.
- **Grafana:** Visualizes metrics through dashboards and supports alert configuration.
- **ELK Stack:** Elasticsearch, Logstash, and Kibana provide log storage, processing, searching, and analysis.
- **AWS CloudWatch:** Monitors metrics and logs from supported AWS services.

### Component Design

**Enterprise Network Infrastructure**

The network model contains LANs representing different departments or branches. Routers and firewalls handle routing, traffic control, and forwarding between networks.

**VPN Connectivity Layer**

AWS Site-to-Site VPN provides IPsec tunnels for secure data transmission between the enterprise network and the VPC. The project examines a two-tunnel configuration and routing failover mechanisms to maintain connectivity when one tunnel becomes unavailable.

**AWS Infrastructure**

Amazon VPC provides a private IP address space. Subnets are organized according to their functions and access policies. Amazon EC2 instances host web services or monitoring components, depending on the implementation phase.

**Monitoring System**

Prometheus collects metrics from compatible exporters or monitoring endpoints. Grafana displays CPU usage, memory utilization, disk capacity, service status, and available network metrics. The ELK Stack centralizes and analyzes logs from servers and devices capable of exporting compatible log data.

**Security Layer**

Firewalls, Security Groups, and routing policies follow the principle of allowing only necessary traffic. Administrative protocols and monitoring interfaces are restricted to appropriate sources to avoid unnecessary exposure to the public Internet.

## 4. Technical Implementation

### Implementation Phases

The project is divided into four main phases.

**Phase 1: Research and Architecture Design**

- Study Hybrid Cloud architecture and multi-branch enterprise connectivity requirements.
- Research the operating principles of IPsec VPN and AWS Site-to-Site VPN.
- Design the EVE-NG network topology, identifying LANs, edge routers, firewalls, and AWS network components.
- Develop the IP addressing plan, routing tables, and redundancy strategy.

**Phase 2: Infrastructure Setup and VPN Configuration**

- Deploy network devices and configure IP addresses in EVE-NG.
- Configure internal routing, default routes, and necessary NAT policies.
- Create the VPC, subnets, Virtual Private Gateway, and VPN connection on AWS.
- Configure routers to establish IPsec tunnels.
- Verify tunnel status, test connectivity to VPN tunnel endpoints, and validate communication between permitted networks.

**Phase 3: Cloud Server and Monitoring Deployment**

- Deploy EC2 instances for web applications or other required services.
- Configure Prometheus to collect metrics from monitoring endpoints.
- Deploy Grafana and build dashboards for system resource monitoring.
- Deploy the ELK Stack when sufficient resources are available, and configure log collection and analysis.
- Verify administrative connectivity and monitoring traffic flows through the VPN according to the architecture.

**Phase 4: Testing, Optimization, and Documentation**

- Test connectivity between LANs and AWS resources.
- Verify service access according to firewall and Security Group policies.
- Simulate VPN tunnel failures to evaluate routing failover.
- Test metric collection, dashboard visualization, and log analysis.
- Optimize network configuration, access permissions, and cloud resources.
- Complete the architecture diagrams, IP addressing tables, device configurations, and test reports.

### Technical Requirements

**Network Infrastructure**

- Use EVE-NG and a virtualization environment to build the network topology.
- Configure routers, Cisco ASA firewalls, LANs, and WAN connectivity.
- Maintain a clear IP addressing plan and avoid overlapping networks.
- Configure bidirectional routing between the enterprise network and the VPC.
- Test routing failover when two VPN tunnels are configured.

**AWS Infrastructure**

- Use Amazon VPC and subnets appropriate to the architecture.
- Create a Virtual Private Gateway and AWS Site-to-Site VPN connection.
- Configure route tables to direct traffic to enterprise networks through the VPN.
- Deploy EC2 instances according to actual requirements and budget constraints.
- Configure Security Groups to allow only the necessary service ports.

**Monitoring System**

- Install Prometheus to collect metrics from servers or compatible exporters.
- Use Grafana to build dashboards and configure alerts.
- Deploy the ELK Stack when resources permit centralized log collection and analysis.
- Monitor CPU, memory, disk capacity, and network utilization.
- Restrict access to administrative interfaces and monitoring dashboards.

## 5. Implementation Timeline and Milestones

The project follows a series of milestones during the internship period from August 10 to December 1.

- **Phase 1 – Research and Design:** Study Hybrid Cloud technologies, design the network topology, plan IP addressing, and develop the AWS connectivity architecture.
- **Phase 2 – Network Infrastructure Setup:** Build the EVE-NG topology, configure routers and firewalls, and verify internal connectivity.
- **Phase 3 – AWS VPN Deployment:** Create the VPC, subnets, Virtual Private Gateway, and VPN connection; configure tunnels and routing between both environments.
- **Phase 4 – Cloud Server Deployment:** Launch EC2 instances and verify service access from permitted networks.
- **Phase 5 – Monitoring Integration:** Deploy Prometheus, Grafana, and the ELK Stack according to available resources; verify metric and log collection.
- **Phase 6 – Testing and Finalization:** Test connectivity, redundancy, security, and performance, then complete the project documentation.

After the internship, the model can be extended to explore configuration automation, advanced alerting, centralized configuration management, and additional cloud security mechanisms.

## 6. Estimated Budget

The project's cost depends on VPN usage duration, the number of EC2 instances, storage capacity, data transfer volume, and the resources allocated to monitoring tools.

The [AWS Pricing Calculator](https://calculator.aws/) can be used to estimate costs based on the actual deployment configuration.

### Cost Components

- **Amazon EC2:** Costs for application servers or monitoring instances, depending on instance type and running time.
- **Amazon EBS:** Costs for storage volumes attached to EC2 instances.
- **AWS Site-to-Site VPN:** VPN connection charges and applicable data transfer costs.
- **Amazon VPC:** Core components such as VPCs, subnets, and route tables generally do not incur separate charges; related resources may incur additional fees.
- **Amazon CloudWatch:** Charges may apply when usage exceeds the applicable free usage allowances for metrics, logs, or alarms.
- **Prometheus and Grafana:** The software can run on EC2, but the underlying compute and storage resources still incur costs.
- **ELK Stack:** CPU, memory, disk capacity, and log storage costs must be considered when deploying on EC2.
- **EVE-NG and Virtualization Environment:** Existing personal computer resources are used; electricity and hardware costs may be considered where applicable.

### Cost Optimization Strategies

- Start EC2 instances only when performing configuration, testing, or demonstrations.
- Select instance types that match the required workload and available resources.
- Monitor AWS Billing and configure budget alerts.
- Remove unused resources after checking for dependencies and resources that may continue to incur charges.
- Deploy monitoring tools incrementally to avoid running multiple resource-intensive services simultaneously.
- Do not assume that costs are zero simply because an instance is covered by a free usage allowance or promotional credits.

The final budget should be validated using the AWS Pricing Calculator and actual billing data. VPN charges and monitoring infrastructure costs should be evaluated separately rather than estimating the project solely from EC2 instance costs.

## 7. Risk Assessment

### Risk Matrix

- **VPN Connectivity Failure:** High impact; may result from incorrect IPsec configuration, routing errors, or network interruptions.
- **Routing Misconfiguration:** High impact; may prevent communication between branch networks and cloud resources.
- **Unauthorized Access:** High impact if firewalls, Security Groups, or administrative interfaces are configured insecurely.
- **Insufficient Monitoring Resources:** Medium to high impact when EC2 instances lack adequate CPU, memory, or storage.
- **AWS Budget Overrun:** Medium to high impact if billable resources remain active beyond the testing period.
- **Log Data Loss:** Medium impact if appropriate retention and backup policies are not implemented.

### Risk Mitigation Strategies

- **VPN:** Verify tunnel status, IKE/IPsec parameters, peer addresses, access control lists, and routing tables. Configure two tunnels and test failover behavior.
- **Routing:** Maintain an IP addressing plan, identify source and destination networks, verify bidirectional paths, and use traceroute or equivalent diagnostic tools.
- **Security:** Restrict SSH, monitoring ports, and administrative interfaces to approved sources. Avoid unnecessarily permissive rules.
- **Resources:** Monitor CPU, memory, disk usage, and adjust configurations according to workload requirements.
- **Costs:** Configure budget alerts, review active resources, and stop or remove resources that are no longer needed.
- **Logs:** Define retention policies, manage storage capacity, and back up important data.

### Contingency Plan

If one VPN tunnel fails, the system will be tested to determine whether traffic can move to the remaining tunnel according to the configured routing mechanism. If the VPN cannot be restored, troubleshooting will proceed through each layer, including WAN connectivity, IPsec status, internal routing, and AWS route tables.

For the monitoring system, Prometheus, Grafana, and ELK configurations should be preserved to support recovery after failures. Network and AWS configurations can be documented or stored as infrastructure code to facilitate redeployment when necessary.

## 8. Expected Outcomes

### Technical Improvements

- Build a Hybrid Cloud model connecting an enterprise network to AWS through Site-to-Site VPN.
- Establish connectivity between internal networks and VPC resources according to routing policies.
- Test two VPN tunnels and routing failover when a failure occurs.
- Deploy EC2 instances for applications or required services.
- Build monitoring dashboards for server resources using Prometheus and Grafana.
- Integrate the ELK Stack for log collection, searching, and analysis when sufficient resources are available.
- Complete network diagrams, IP addressing tables, VPN configurations, security rules, and testing procedures.

### Long-Term Value

The project establishes a practical foundation for studying enterprise network administration, cloud computing, secure connectivity, and centralized monitoring. The architecture can be extended to connect additional branches, deploy more servers, improve redundancy, and introduce infrastructure management automation.

Through this project, the implementer can apply computer networking knowledge to cloud environments and improve practical skills in network device configuration, IPsec VPN deployment, AWS resource management, and infrastructure monitoring.

The final results will be evaluated based on actual connectivity, VPN tunnel status, routing correctness, service accessibility under security policies, and monitoring data collection.
