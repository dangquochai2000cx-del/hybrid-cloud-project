
---
title: "Hybrid Cloud System Testing and AWS Resource Cleanup"
date: 2026-10-30
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Overview

In this final section, we will verify the operation of the Hybrid Cloud system connecting the multi-branch enterprise network simulated in EVE-NG with the AWS cloud environment.

The testing process covers network connectivity, Site-to-Site VPN tunnels, routing and failover mechanisms, EC2 server availability, and the centralized monitoring solution using Prometheus, Node Exporter, and Grafana.

After completing the tests, we will review the AWS resources and clean up resources that are no longer required to reduce unnecessary costs.

#### 1. Review the Hybrid Cloud Architecture

Before testing, review the overall system architecture and confirm that all required components have been deployed.

The system consists of:

- **On-premises infrastructure:** Enterprise network simulated using EVE-NG, including headquarters and branch office networks.
- **AWS VPC:** Cloud network using CIDR `10.100.0.0/16`.
- **Virtual Private Gateway:** Provides the AWS endpoint for Site-to-Site VPN connections.
- **Customer Gateways:** Represent the on-premises VPN devices.
- **VPN connections:** Provide encrypted connectivity between the enterprise network and AWS.
- **EC2 instance:** Hosts the web server and monitoring components.
- **Monitoring system:** Uses Prometheus, Node Exporter, and Grafana to monitor server performance.

**Image 1: Overall Hybrid Cloud Architecture**

![Hybrid Cloud Architecture](/images/5-Workshop/5.8-System-Testing-Cleanup/01-hybrid-cloud-architecture.png)

#### 2. Test Network Connectivity

Verify communication between the on-premises enterprise network and the AWS VPC.

From an authorized on-premises host or router, test connectivity to the private IP address of the EC2 instance.

Example:

```bash
ping <EC2_PRIVATE_IP>
```

Replace `<EC2_PRIVATE_IP>` with the actual private IP address of the EC2 instance.

Also verify that the routing table contains the expected routes to the AWS VPC:

```bash
show ip route 10.100.0.0
```

Check that the traffic is forwarded through the intended VPN path.

If connectivity fails, review the following:

- AWS route table entries.
- On-premises routing configuration.
- VPN tunnel status.
- Security Group inbound rules.
- Network ACL rules, if customized.
- Host firewall configuration.

**Image 2: Test Connectivity from the Enterprise Network to AWS**

![Network Connectivity Test](/images/5-Workshop/5.8-System-Testing-Cleanup/02-network-connectivity.png)

#### 3. Verify Site-to-Site VPN Connections

Open the AWS VPC console and navigate to **Site-to-Site VPN Connections**.

Select each VPN connection and inspect the **Tunnel details** tab.

Verify that the expected VPN tunnels are operational and that the status is **UP**.

On the on-premises routers, use the following Cisco IOS commands:

```bash
show crypto isakmp sa
show crypto ipsec sa
show interface tunnel
```

Check that the IPsec security associations are established and that traffic counters increase when communication occurs between the enterprise network and AWS.

**Image 3: AWS Site-to-Site VPN Tunnel Status**

![AWS VPN Tunnel Status](/images/5-Workshop/5.8-System-Testing-Cleanup/03-vpn-status.png)

#### 4. Test Routing and VPN Failover

Verify that the primary and backup VPN paths operate according to the routing design.

The expected behavior is:

- Router15 provides the preferred primary VPN path.
- Router16 provides the backup path.
- The backup path is used when the primary path becomes unavailable.
- The primary path is preferred again after it recovers.

Check the routing and tracking status:

```bash
show ip route 10.100.0.0
show track 100
show ip sla statistics
```

Perform a controlled failover test:

1. Confirm that the primary VPN path is operational.
2. Record the current routing table.
3. Temporarily disable the primary path in the lab.
4. Verify that the tracking mechanism detects the failure.
5. Confirm that traffic uses the backup path.
6. Restore the primary path.
7. Verify that the original route preference is recovered.

Do not perform this test during normal production operation without an approved maintenance window.

**Image 4: Verify Primary and Backup VPN Routing**

![VPN Routing Failover](/images/5-Workshop/5.8-System-Testing-Cleanup/04-vpn-failover.png)

#### 5. Test the EC2 Web Server

Verify that the EC2 instance and its web server are operating correctly.

Check the Nginx service on Ubuntu:

```bash
sudo systemctl status nginx
```

If Nginx is not running, start the service:

```bash
sudo systemctl start nginx
```

Check that the web server is listening on port `80`:

```bash
sudo ss -tulpn | grep :80
```

From an authorized browser, access:

```text
http://<EC2_PUBLIC_IP>
```

Confirm that the web page is displayed successfully.

Also verify that the EC2 instance is in the **Running** state in the AWS EC2 console.

**Image 5: Verify EC2 Instance Status**

![EC2 Instance Status](/images/5-Workshop/5.8-System-Testing-Cleanup/05-ec2-status.png)

**Image 6: Access the Nginx Web Server**

![Nginx Web Server](/images/5-Workshop/5.8-System-Testing-Cleanup/06-nginx-web-server.png)

#### 6. Verify the Centralized Monitoring System

Check the status of Node Exporter, Prometheus, and Grafana on the EC2 instance.

Run:

```bash
sudo systemctl status node_exporter
sudo systemctl status prometheus
sudo systemctl status grafana-server
```

Open the Prometheus Targets page:

```text
http://<EC2_PUBLIC_IP>:9090/targets
```

Confirm that the `prometheus` and `node_exporter` targets are **UP**.

Then open Grafana:

```text
http://<EC2_PUBLIC_IP>:3000
```

Verify that the monitoring dashboard displays server metrics such as:

- CPU utilization.
- Memory utilization.
- Disk usage.
- Network traffic.

Confirm that the graphs are receiving updated data from Prometheus.

**Image 7: Prometheus Targets Verification**

![Prometheus Targets](/images/5-Workshop/5.8-System-Testing-Cleanup/07-prometheus-targets.png)

**Image 8: Centralized Monitoring Dashboard**

![Grafana Monitoring Dashboard](/images/5-Workshop/5.8-System-Testing-Cleanup/08-grafana-dashboard.png)

#### 7. Review AWS Resource Usage and Costs

Before cleaning up the environment, review the resources that may generate charges.

Open the AWS Management Console and check the following services:

- **EC2:** Check running instances and attached storage volumes.
- **Elastic IP addresses:** Check allocated addresses that are not associated with running resources.
- **EBS Volumes:** Check volumes that are no longer required.
- **Snapshots:** Review snapshots that are no longer needed.
- **VPN Connections:** Review active Site-to-Site VPN connections.
- **NAT Gateway:** Check whether any NAT Gateway is deployed.
- **CloudWatch:** Review any monitoring resources that may incur additional charges.

You can also review estimated spending through **Billing and Cost Management**.

**Important:** Stopping an EC2 instance does not stop all related charges. EBS volumes and other retained resources may continue to incur costs. Public IPv4 addresses and VPN connections may also have separate charges.

**Image 9: Review AWS Resources**

![AWS Resource Review](/images/5-Workshop/5.8-System-Testing-Cleanup/09-aws-resource-review.png)

#### 8. Clean Up Unnecessary AWS Resources

Only delete resources that are no longer required for the workshop.

Before deleting anything, save the required configuration files, screenshots, and test results.

The cleanup process may include:

**EC2 Instance**

If the instance is no longer needed:

1. Open the EC2 console.
2. Select **Instances**.
3. Select the workshop EC2 instance.
4. Choose **Instance state**.
5. Select **Terminate instance** only if the instance is no longer required.

**EBS Volumes and Snapshots**

1. Open **Volumes** in the EC2 console.
2. Review unattached volumes.
3. Delete only volumes that are no longer required and have been backed up if necessary.
4. Review snapshots and delete only unnecessary snapshots.

**Site-to-Site VPN Resources**

If the VPN environment is no longer needed:

1. Open **Site-to-Site VPN Connections**.
2. Delete the VPN connections that are no longer required.
3. Review and delete unused Customer Gateways.
4. Review the Virtual Private Gateway before detaching or deleting it.

**Other Resources**

Review unused Elastic IP addresses, NAT Gateways, and other resources before deleting them.

**Important:** Do not delete shared resources or resources still used by another part of the project. Terminating an EC2 instance is irreversible for its instance storage, and associated resources may require separate cleanup.

**Image 10: AWS Resource Cleanup**

![AWS Resource Cleanup](/images/5-Workshop/5.8-System-Testing-Cleanup/10-aws-cleanup.png)

#### 9. Final System Evaluation

After completing the tests, evaluate the overall operation of the Hybrid Cloud system.

The evaluation should cover:

- Connectivity between the on-premises network and AWS.
- Establishment and operation of Site-to-Site VPN tunnels.
- Correct route selection between primary and backup paths.
- Successful failover and recovery.
- Availability of the EC2 web server.
- Successful collection of server metrics by Prometheus.
- Visualization of monitoring data in Grafana.
- Review and cleanup of unnecessary AWS resources.

The results should be recorded with screenshots and test evidence for the project report.

**Image 11: Final Hybrid Cloud System Verification**

![Final Hybrid Cloud Verification](/images/5-Workshop/5.8-System-Testing-Cleanup/11-final-system-verification.png)

#### Conclusion

In this final section, we verified the operation of the Hybrid Cloud system connecting the multi-branch enterprise network simulated in EVE-NG with the AWS cloud environment.

The tests covered network connectivity, Site-to-Site VPN operation, routing and failover, EC2 web server availability, and centralized monitoring using Prometheus, Node Exporter, and Grafana.

We also reviewed AWS resource usage and identified resources that could be cleaned up to reduce unnecessary costs.

Through this workshop, we completed the design, deployment, monitoring, and evaluation of a Hybrid Cloud solution for connecting multi-branch enterprise networks to AWS.
