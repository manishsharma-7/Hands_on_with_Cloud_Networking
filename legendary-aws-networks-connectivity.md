[Main Page](./README.md)
---

---

[⬅ Previous Page: Launching VPC Resources](./legendary-aws-networks-ec2.md)

[➡️ Next Page: Testing VPC Connectivity](./legendary-aws-networks-connectivity.md)

---

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that helps us create our own networks and configure the security/traffic rules and connectivity with the internet.

### How I used Amazon VPC in this project

In today’s project, we tested the connectivity between the public and private servers and the internet. We troubleshooted issues by allowing the correct traffic types and enabling SSH access through the security group and network ACL settings.

### One thing I didn't expect in this project was...

One thing we didn't expect in this project was how many different settings needed to be updated just to allow basic connectivity—especially needing to allow specific traffic types like ICMP and SSH in both the security groups and network ACLs. It was a good reminder of how strict AWS is with security by default.

### This project took me...

It took us about 1 hour to test and troubleshoot this project, including updating security group rules, modifying network ACLs, and verifying connectivity between the public and private servers as well as the internet.

---

## Connecting to an EC2 Instance

SSH connectivity error means there's a connectivity issue — for example, missing or misconfigured security group rules, incorrect key pair, wrong IP address, or the instance not having a public IP or internet access.

Our first connectivity test was whether we could connect to the Public server

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

We connected to our EC2 instance using EC2 Instance Connect, which is a browser-based SSH client provided by AWS. It lets us securely connect to our EC2 instances without needing to manage or store a private key locally. It’s a fast and easy way to access our instance directly from the AWS Console.

Our first attempt at getting direct access to our public server resulted in an error, because the security group for the public subnet didn’t allow SSH connections.

We fixed this error by updating the inbound rules to allow traffic on port 22 (SSH) so we could connect successfully.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network utility that checks if one device can reach another over a network by sending small data packets and measuring the response time. We used ping to test the connectivity between our public and private server to ensure they could communicate with each other inside the VPC.

The ping command I ran was
ping [ip address of private server]

The first ping returned with "unreachable." This meant that our private server could not be reached from the public server, likely due to missing or incorrect routing rules, security group settings, or network ACLs blocking the traffic.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

We troubleshooted this by allowing ICMP in the network ACL for the private subnet and allowing ICMP in the security group. This enabled the private server to respond to ping requests, confirming connectivity between the public and private servers.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command-line tool used to transfer data to or from a server using various protocols, most commonly HTTP or HTTPS. 

We used curl to send a request from our public server to the internet (NextWork website) to check if we could connect to the internet and confirm that it was reachable.

### Ping vs Curl

Ping and curl are different because ping checks basic network connectivity between two devices by sending ICMP packets, while curl is used to make requests to web servers (typically using HTTP or HTTPS) and retrieve data. Ping tells us if a host is reachable, whereas curl checks if a service like a website is responding properly.

---

## Connectivity to the Internet

The successful curl command we ran is below

curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3



![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-connectivity_8ee57662)

---

[➡️ Next Page: Testing VPC Connectivity](./legendary-aws-networks-connectivity.md)

[⬅ Previous Page: Launching VPC Resources](./legendary-aws-networks-ec2.md)


[Main Page](./README.md)
---

---
