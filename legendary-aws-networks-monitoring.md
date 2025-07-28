[Main Page](./README.md)
---

---

[⬅ Previous Page: VPC Peering](./legendary-aws-networks-peering.md)

[➡️ Next Page: Access S3 from a VPC](./legendary-aws-networks-s3.md)

---

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated section of the AWS cloud where you can launch and manage AWS resources—like EC2 instances, databases, and containers—in a virtual network you define.

### How I used Amazon VPC in this project

We used Amazon VPC in today’s project to create two isolated virtual networks, each with a unique CIDR block—10.1.0.0/24 and 10.2.0.0/24. Each VPC included one public subnet. This setup allowed us to simulate a multi-VPC architecture and configure a VPC peering connection between them, enabling secure communication while maintaining network isolation.

We launched EC2 instances (@EC2) in each public subnet to simulate traffic between the VPCs. To monitor and analyze this traffic, we enabled VPC Flow Logs and used Amazon CloudWatch for log storage and visualization. With CloudWatch Logs Insights, we ran queries to gain insights into the network traffic patterns, helping us troubleshoot and validate connectivity between the peered VPCs.

### One thing I didn't expect in this project was...

One thing we didn't expect in this project was the need to manually update the route tables in each VPC to enable communication after setting up the VPC peering connection. While the peering connection was successfully established, traffic between EC2 instances didn’t work until we added the appropriate routes.

Another unexpected aspect was how essential it was to capture and monitor traffic using VPC Flow Logs in CloudWatch. Setting up flow logs allowed us to verify whether packets were reaching their destination, helping us troubleshoot connectivity issues more effectively using CloudWatch Logs Insights.

### This project took me...

It took me about 1 hour to complete this project. 

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step we will  set up two VPCs and test their peering connection to ensure that resources in both VPCs can communicate with each other.

### Step 2 - Launch EC2 instances

We are going to launch an EC2 instance in each VPC, so we can use them to test our VPC peering connection later. These instances will act as endpoints in each VPC, allowing us to run connectivity tests like ping to verify that traffic can flow between the two VPCs successfully.

### Step 3 - Set up Logs

We’re going to set up a way to track all inbound and outbound network traffic using VPC Flow Logs. These logs will capture information about the IP traffic going to and from network interfaces in our VPCs. We’ll also set up a storage space—a CloudWatch Log Group—to store and analyze these flow log records for monitoring, troubleshooting, and security auditing.

### Step 4 - Set IAM permissions for Logs

We’re going to give VPC Flow Logs the necessary permissions to write log data and send it to Amazon CloudWatch. This involves assigning an IAM role that allows the logs to be delivered to a CloudWatch Logs group. Once permissions are in place, we’ll complete the setup of the subnet’s flow log so that all network traffic data—both inbound and outbound—is captured and stored for analysis.

---

## Multi-VPC Architecture

In this step, we launched two separate VPCs, each with one public subnet. This setup gave us two total subnets—one for each VPC—to use later for testing VPC peering and monitoring network traffic.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because overlapping IP ranges would prevent proper routing between the VPCs. Since we’re creating a peering connection, each VPC must have a distinct IP range so that traffic knows exactly where to go without confusion or conflict.

### I also launched EC2 instances in each subnet

Our EC2 instances' security groups allow all SMTP IPv4 traffic for all IPv4. This is because we needed to ensure that traffic between the two EC2 instances in different VPCs could flow freely for testing the VPC peering connection. Allowing SMTP traffic helped us simulate communication and verify connectivity between the instances.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are detailed records of events and actions that happen within a system, network, or application. In the context of AWS, logs help track things like network traffic, user activity, and system performance. They’re essential for monitoring, troubleshooting issues, analyzing security, and understanding how resources are being used.

Log groups are containers in Amazon CloudWatch Logs that organize and store logs from one or more sources. Each log group typically represents a specific application, resource, or service. Within a log group, you can have multiple log streams, which are sequences of log events from individual sources like EC2 instances or VPC Flow Logs. Log groups help keep logs structured and easy to manage, search, and analyze.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

We created an IAM policy because we needed to define the specific permissions that allow VPC Flow Logs to write log data to CloudWatch Logs. This policy gives the necessary access to actions like logs:CreateLogGroup, logs:CreateLogStream, and logs:PutLogEvents, so that the flow logs can be successfully captured and stored in the designated log group.

We also created an IAM role because VPC Flow Logs need permission to send network traffic data to CloudWatch Logs. The IAM role grants the necessary access so that logs from our subnet can be securely delivered and stored in the designated log group for monitoring and analysis.

A custom trust policy is a set of rules that defines which AWS services or accounts are allowed to assume a specific IAM role. It acts as a way to grant trusted entities permission to use the role. In our case, the custom trust policy allows the VPC Flow Logs service to assume the role and send log data to CloudWatch Logs on our behalf.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

We are going to get Instance 1 to send test messages to Instance 2 to confirm that our VPC peering connection is working properly. This involves using commands like ping or curl from Instance 1 to reach Instance 2’s private IP address. If successful, it means both VPCs are correctly configured to communicate through the peering connection. Additionally, this network traffic will be captured by VPC Flow Logs and sent to CloudWatch, allowing us to analyze and verify the communication between the instances.

### Step 6 - Set up a peering connection

We are going to set up a connection link between our VPCs by creating and configuring a VPC peering connection. This link will allow the two VPCs to communicate with each other as if they were part of the same network. Once the peering connection is established and properly routed, we’ll be able to send traffic between resources in both VPCs securely and efficiently.

### Step 7 - Analyze flow logs

We are going to review the flow logs recorded about VPC 1's public subnet and analyse the logs to gain valuable insights into the network traffic. These flow logs will show us details like the source and destination IP addresses, traffic direction, protocol used, and whether the traffic was accepted or rejected—helping us understand what's happening inside our VPC at a deeper level.

---

## Connectivity troubleshooting

Our first ping test between my EC2 instances had no replies, which means the network traffic was not getting through—likely due to missing or misconfigured security group rules, network ACLs, or route table entries that were blocking the connection between the two VPCs.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_99d4ba42)

We could receive ping replies if I ran the ping test using the other instance's public IP address, which means the connection was working over the internet, but not through the private VPC peering connection. This indicated that while the instances were reachable publicly, the private connectivity between the VPCs still had configuration issues such as missing route entries or security group rules.

---

## Connectivity troubleshooting

ooking at VPC 1's route table, we identified that the ping test with Instance 2's private address failed because there was no route pointing to the CIDR block of VPC 2 through the peering connection. Without this route, traffic from VPC 1 didn’t know how to reach the private IP range of VPC 2, causing the ping test to fail.

### To solve this, I set up a peering connection between my VPCs

We also updated both VPCs' route tables so that traffic could flow between them through the VPC peering connection. In addition to that, we allowed ICMP IPv4 traffic by updating the security group rules—this was essential to enable successful ping tests and verify connectivity between the EC2 instances in each VPC.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

We received ping replies from Instance 2's private IP address! This means our VPC peering connection was successfully established, and the routing and security configurations between both VPCs are correctly set up—allowing network traffic to flow privately between the two instances.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about different aspects of network traffic, including the source and destination IP addresses, source and destination ports, protocol used (like TCP or UDP), the action taken (accepted or rejected), traffic direction (inbound or outbound), number of packets, number of bytes transferred, and the timestamp of the traffic flow. These parts help us monitor, troubleshoot, and analyse the behavior of our network.

For example, the flow log we have captured tells us that most traffic from external IP addresses (like 147.185.133.190 and 92.118.39.237) trying to reach our instance at 10.1.0.116 was rejected, which is good—it shows our security groups or NACLs are blocking unwanted traffic. However, the traffic between 10.1.0.116 and 10.2.0.111 (our two instances in peered VPCs) was accepted, showing that VPC peering is working and the connection between our instances is successful.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is an interactive log analytics service provided by AWS CloudWatch that allows you to search, analyze, and visualize log data in real time. It helps you quickly identify operational and application issues by running queries on logs from sources like AWS Lambda, EC2, and CloudTrail. With its powerful query language, you can extract meaningful patterns, filter specific events, and create dashboards for monitoring system performance and troubleshooting problems efficiently.

We ran the query below.

stats sum(bytes) as bytesTransferred by srcAddr, dstAddr
| sort bytesTransferred desc
| limit 10

This query analyzes network traffic by calculating the total number of bytes transferred (sum(bytes)) between each source address (srcAddr) and destination address (dstAddr). It then sorts the results in descending order based on the amount of data transferred and displays the top 10 pairs with the highest traffic. This helps identify the most active network connections

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-monitoring_3e1e79a1)

---

[➡️ Next Page: Access S3 from a VPC](./legendary-aws-networks-s3.md)

[⬅ Previous Page: VPC Peering](./legendary-aws-networks-peering.md)


[Main Page](./README.md)
---

---
