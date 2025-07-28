<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that helps us create our own networks and configure the security/traffic rules and connectivity with the internet.

### How I used Amazon VPC in this project

We used Amazon VPC to create our own VPC with different resources and components (e.g. security groups, network ACLs, private resources like private subnets, and EC2 instances in both our public and private subnets).

### One thing I didn't expect in this project was...

We didn't expect the resource map to be so visual and interactive! It was such a convenient and speedy way to set up an entire VPC architecture.

### This project took me...

This project took us 1 hr to complete

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means "logging into" the EC2 instance, rather than just managing it at a higher level using the AWS Management Console. This allows us to perform operations like installing software, running commands, and changing our EC2 instance's configuration directly from the command line.

### SSH is a key method for directly accessing a VM

SSH means Secure Shell, and it is both a protocol and a traffic type. It is the protocol that matches key pairs, and once a connection is set up, it is a traffic type that encrypts communication/data being transferred.

### To enable direct access, I set up key pairs

Key Pairs are tools that help engineers authenticate themselves when trying to gain direct access to a virtual machine (e.g. an EC2 instance). Key pairs work using two keys: a public key, which is stored on the virtual machine, and a private key, which is kept securely by the user. When the user tries to connect, AWS verifies that the private key matches the public key, allowing secure access.

A private key's file format refers to the type of file our key is stored in. Our private key's file format was .pem, which is a widely accepted format that most servers can read and use for authentication.

---

## Launching a public server

We had to change our EC2 instance's networking settings by updating the VPC and the subnet it would be launched in. We selected our NextWork VPC and our public subnet. We also used our existing public security group.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

Our private server has its own dedicated security group because the NextWork public security group allows all HTTP traffic — which would leave our private server more vulnerable to security risks and attacks.

Our private server's security group has its source set to the NextWork Public Security Group, which means only traffic coming from resources associated with that group will be allowed.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

We used an alternative way to set up an Amazon VPC! This time, we used the “VPC and more” option, which provides a VPC resource map to help us create the VPC and all its components — e.g., security groups, route tables, and internet gateways.

A VPC resource map is a visual diagram that maps our my VPC's components and the relationships/connection between them. A resource map is interactive i.e. it will highlight the connection relevant to a resource that I highlight/hover over.

Our new VPC has a CIDR block of 10.0.0.0/16. It’s technically possible for our new VPC to have the same IPv4 CIDR block as an existing VPC because VPCs are already isolated from each other. However, this is not considered best practice—especially if we plan to use VPC peering, which requires unique, non-overlapping IP ranges.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in our VPC, we only had two options: either none or one in each Availability Zone in our VPC. This is because it’s best practice to have at least one subnet per Availability Zone to improve redundancy and high availability.

The setup page also offered to create NAT gateways, which are connectors that let resources in our private subnets access the internet (e.g. for security updates) while still blocking incoming traffic from the internet.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-ec2_8ee57662)

---

---
