[Main Page](./README.md)
---

---

[⬅ Previous Page: VPC Traffic Flow and Security](./legendary-aws-networks-security.md) 

[➡️ Creating a Private Subnet](./legendary-aws-networks-private.md)

---

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated section of the AWS cloud where you can launch and manage AWS resources—like EC2 instances, databases, and containers—in a virtual network you define.

### How I used Amazon VPC in this project

In this project, we set up a private subnet and created a new ACL for it to help isolate the resources. This ensures tighter security by restricting both inbound and outbound traffic, limiting exposure to the internet and other subnets.

### One thing I didn't expect in this project was...

Needing to create a new ACL was the one thing we didn’t expect. We assumed the default ACL would be enough, but quickly learned that customizing an ACL was necessary to properly secure and control traffic for our private subnet.

### This project took me...

It took me about 15 mins to complete this project and about 20 mins to document it.

---

## Private vs Public Subnets

The difference between public and private subnets is that public subnets are accessible from the internet and can access the internet, while private subnets are isolated from the internet by default. Public subnets typically contain resources like web servers, whereas private subnets are used for internal resources like databases.

Having private subnets is useful because keeping resources away from the internet is extremely important for securing confidential data and internal systems. This isolation helps reduce the risk of unauthorized access, data breaches, and external attacks, especially for sensitive components like databases or internal services.

My private and public subnets cannot have the same IPv4 CIDR block—that is, each subnet must have a unique range of IP addresses. CIDR blocks cannot overlap because AWS needs to know exactly which IP addresses belong to which subnet to properly route traffic and avoid conflicts.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, our private subnet is associated with default route table i.e. route table that has a route to an internet

We had to set up a new route table because our subnet can't have a route to an internet gateway.

Our private subnet's dedicated route table only has one route — for internal communication — with a destination that points to another resource within our VPC (e.g., 10.0.0.0/16). This ensures that traffic stays within the VPC and does not reach the internet, which is what makes the subnet private.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, our private subnet is associated with its VPC's default ACL thats's set up for every VPC crreated in my ASW account

Setting up a route without an internet gateway would already prevent direct internet access to and from my subnet. It is still important to set up a dedicated network for private subnet coz ACL becomes crucial in the event of security breaches.

Our new network ACL has two simple rules - deny all inbound and deny all outbound traffic

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-private_1ed2cb07)

---

[➡️ Next Page: Creating a Private Subnet](./legendary-aws-networks-private.md)

[⬅ VPC Traffic Flow and Security](./legendary-aws-networks-security.md)


[Main Page](./README.md)
---

---
