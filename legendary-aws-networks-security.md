<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated section of the AWS cloud where you can launch and manage AWS resources—like EC2 instances, databases, and containers—in a virtual network you define.

Why is it useful?
Control: You have full control over network settings like IP ranges, subnets, route tables, and gateways.

Security: It lets you define security groups and network ACLs to tightly control traffic in and out of your resources.

Customization: You can design your network architecture to fit your application needs, including public and private subnets.

Scalability: VPCs are highly scalable and integrate with other AWS services like Load Balancers, Auto Scaling, and VPNs.

Isolation: Your VPC is logically isolated from other AWS customers, offering an extra layer of security

### How I used Amazon VPC in this project

We used Amazon VPC in today’s project to set up the foundational network environment for our resources. Specifically, we:

Created a custom VPC with a defined IPv4 CIDR block (e.g. 10.0.0.0/16) to control the IP range

Created subnets within that VPC to segment our network

Enabled auto‑assign public IPs so resources in our subnet could be accessible from the internet

Attached an Internet Gateway to allow public internet access

Configured a route table with a route to direct outbound traffic (e.g. 0.0.0.0/0) to the Internet Gateway

Set up security groups to allow HTTP traffic inbound and all traffic outbound at the resource level

### One thing I didn't expect in this project was...

configured for it to work properly—like subnets, route tables, internet gateways, security groups, and ACLs. We thought setting up a VPC would be a single step, but it actually involved coordinating many resources to make the network functional and secure.

### This project took me...

I took us about 30 mins to complete this project.

---

## Route tables

Route tables are like the GPS that directs traffic within our VPC to the correct destination.

Routes tables are needed to make a subnet public because a subnet needs to have a route to an internet gateway in order to be considered public. A route table is the only way to establish this connection.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

The destination is the range of IP addresses that traffic in our VPC is trying to reach. 
The target is the road/path that the traffic will use to get to their destination

The route in our route table that directed internet-bound traffic to our internet gateway had a destination of 0.0.0.0/0 and a target of NextWork (Internet Gateway -IGW).

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are like security guards that monitor both inbound and outbound network traffic at the resource level—meaning every single resource in a subnet or VPC has its own security group.

### Inbound vs Outbound rules

Inbound rules are the rules that monitor/restrict/control incoming traffic—for example, users visiting a web app we're hosting. We configured an inbound rule that allows all inbound HTTP traffic (port 80) from any IP address.

Outbound rules are the rules that monitor/restrict/control the outbound traffic leaving our resources—for example, when our web app requests data from a public API. By default, outbound rules allow all outbound traffic.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACL are like community watchment that secure our network at the subnet level.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is their scope. A security group controls traffic at the resource level (e.g., an EC2 instance), while a network ACL (Access Control List) controls traffic at the subnet level. Every subnet in a VPC is automatically associated with a network ACL.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules allow all traffic. However, unlike security groups, network ACLs are stateless—meaning you must explicitly allow both inbound and outbound traffic for two-way communication.

In contrast, a custom network ACL's inbound and outbound rules are automatically set to deny all traffic by default. This means you must explicitly add rules to allow specific types of traffic.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---
