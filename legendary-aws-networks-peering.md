[Main Page](./README.md)
---

---

[⬅ Previous Page: Testing VPC Connectivity](./legendary-aws-networks-connectivity.md)

[➡️ Next Page: VPC Monitoring with Flow Logs](./legendary-aws-networks-monitoring.md)

---

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that helps us create our own networks and configure the security/traffic rules and connectivity with the internet.

### How I used Amazon VPC in this project

n today’s project, we used Amazon VPC to create two separate VPCs, each with their own public subnet and EC2 instance. We then set up a VPC peering connection between them, allowing the two VPCs to communicate securely. After establishing the peering connection, we updated the route tables and security groups so that the EC2 instances in both VPCs could send and receive traffic between each other. This helped us understand how to connect isolated networks using VPC peering.

### One thing I didn't expect in this project was...

One thing we didn't expect in this project was needing to assign Elastic IP addresses to our EC2 instances in order to connect using EC2 Instance Connect. We assumed that the instances would have public IPs by default, but learning to manually assign and associate Elastic IPs was an unexpected but valuable step in understanding network configuration.

### This project took me...

It took us approximately 30 to 60 minutes to complete the project, including time spent troubleshooting and resolving unexpected connectivity issues.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, we're going to create two VPCs from scratch using the visual VPC resource map, which helps us build our VPCs super quickly and easily

### Step 2 - Create a Peering Connection

In this setp we will Set up a connection link between the 2 VPCs.

### Step 3 - Update Route Tables

In this step, we’re going to set up routing so that traffic from VPC 1 can reach VPC 2, and traffic from VPC 2 can reach VPC 1. This means updating the route tables in both VPCs to use the peering connection as the path between them.

### Step 4 - Launch EC2 Instances

In this step, we're going to launch an EC2 instance in each VPC, so we can use them to test our VPC peering connection.

---

## Multi-VPC Architecture

We started our project by launching two VPCs, each with one public subnet.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/24 and 10.2.0.0/24. They must be unique because we’ll be creating a VPC peering connection, and overlapping IP ranges would prevent proper routing between the VPCs.

### I also launched 2 EC2 instances

We didn't set up key pairs for these EC2 instances because AWS manages a key pair for us! There's no need for us to handle key pairs manually. Plus, since we've already practiced setting up key pairs in our last two projects, we didn’t need to repeat that step this time.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a networking link between two VPCs that allows them to communicate with each other as if they were on the same network. It enables resources in one VPC to connect to resources in another using private IP addresses, without needing a VPN, gateway, or internet connection.

VPCs would use peering connections to share resources, services, or data between isolated networks securely. Instead of exposing traffic to the public internet, peering allows private, low-latency, and cost-effective communication between VPCs in the same or different AWS accounts or regions.

The difference between a Requester and an Accepter in a peering connection is who initiates and who approves the connection. The Requester is the VPC that initiates the peering request, while the Accepter is the VPC that must review and accept the request for the peering connection to become active.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, our VPCs' route tables needed to be updated because they didn’t automatically know how to reach each other. By adding new routes that point to the peering connection, we allowed traffic from one VPC to travel to the other through that connection.

Our VPCs' new routes have a destination of 10.2.0.0/24 (for VPC 1) and 10.1.0.0/24 (for VPC 2). The routes' target was the VPC peering connection we created between the two VPCs.








![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, we are going to use EC2 Instance Connect to access our first EC2 instance. This allows us to connect to the instance directly from the AWS Console without needing to manage key pairs ourselves. Once we attempt the connection, we might encounter a connection error, so we’ll also troubleshoot and fix any issues to ensure our instance is accessible and ready for testing the VPC peering setup.

### Step 6 - Connect to EC2 Instance 1

We’re going to use EC2 Instance Connect to connect to Instance 1 one more time and fix another error. Even after assigning an Elastic IP address, we might still face connectivity issues if the security group attached to the instance does not allow inbound SSH traffic (port 22). In this step, we’ll review and update the security group settings to allow SSH access, ensuring we can successfully connect to our instance from the EC2 console.

### Step 7 - Test VPC Peering

We are going to get Instance 1 to send test messages to Instance 2 and work through any connection errors that come up. The goal is to verify that our VPC peering connection is working properly. If the messages don’t go through, we’ll troubleshoot by checking and updating the security groups and network ACLs for both instances to make sure they allow traffic from each other’s IP ranges. We'll continue adjusting the settings until both instances can successfully send and receive messages between each other.

---

## Troubleshooting Instance Connect

Next, we used EC2 Instance Connect to access our EC2 instance directly from the AWS Console without needing to download or manage a key pair. It’s a fast and secure way to connect to the instance and perform any setup or testing tasks, especially useful for verifying VPC peering connectivity.

We were stopped from using EC2 Instance Connect as it didn’t have an IPv4 address assigned — to connect to the server, we need a public IPv4 address. Without it, the instance is unreachable from the internet, which is required for EC2 Instance Connect to work.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, we set up Elastic IP addresses. Elastic IP addresses are static public IPv4 addresses provided by AWS that can be attached to EC2 instances. Unlike regular public IPs that can change when an instance is stopped and started, Elastic IPs remain the same, ensuring consistent connectivity to the instance.

Associating an Elastic IP address resolved the error because it provided a consistent and reachable public IPv4 address for our EC2 instance. This allowed EC2 Instance Connect to successfully establish a connection to the server, which wasn’t possible earlier due to the lack of a public IP.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, we ran the command ping [private IP address] from Instance 1 to Instance 2. This command sends a series of network packets to the specified private IP to check if the instances in the two VPCs can communicate with each other through the peering connection.

A successful ping test would validate the VPC peering connection because it confirms that traffic can travel between the two VPCs over their private IP addresses. This means the peering connection is working, the correct routes are in place, and network rules like security groups and ACLs are allowing the communication between the instances.

We had to update our second EC2 instance's security group because it didn’t allow SMTP IPv4 traffic. We added a new inbound rule that allowed all SMTP IPv4 traffic from the IP range 10.1.0.0/16. This change ensured that our first instance, located in the peered VPC, could successfully send messages to the second instance.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-peering_7a29d352)

---

[➡️ Next Page: VPC Monitoring with Flow Logs](./legendary-aws-networks-monitoring.md)

[⬅ Previous Page: Testing VPC Connectivity](./legendary-aws-networks-connectivity.md)


[Main Page](./README.md)
---

---
