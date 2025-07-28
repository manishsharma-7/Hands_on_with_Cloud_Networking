<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows us to create a logically isolated section of the AWS cloud, acting as our own virtual network. It's useful because it gives us control over our network configuration, security, and resource.

### How I used Amazon VPC in this project

We created our own virtual cloud with subnets and internet gateways.

### One thing I didn't expect in this project was...

We didnt expect AWS by default creates VPC, subnets and internet gateway.

### This project took me...

It took us less then 30 mins to complete this project.

---

## Virtual Private Clouds (VPCs)

VPC are isolated sections of the AWS Cloud that help to keep the AWS resources private and secure.

There was already a default VPC in the account ever since the AWS account was created. This is because AWS has set up default VPC to allow us to deploy resources like EC2 instances or RD databases right away (without having to create my own VPC)

To set up our VPC, we had to define an IPv4 CIDR block, which means a range of IP addresses that our VPC can allocate to the resources deployed into our VPC — 10.0.0.0/16.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets are subsections of our VPC, just like how neighbourhoods are subsections of a city. There are already subnets existing in our account — one for every availability zone in the Region that we’ve set up our VPC in. We have 3 default subnets already.

Once we created our subnet, we enabled auto-assign public IPv4 address. This setting makes sure a public IP is assigned to each resource created in the subnet so that we do not have to manually set up one for each resource. It’s an automatic process.

Public subnets have a route to an internet gateway, allowing resources communicate with internet. Private subnets do not have a direct route to the internet gateway. For a subnet to be considered public, it has to be connected to an intenet gateway

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

Internet gateways are the key VPC components that allow internet access for the resources in our VPC/subnet. An internet gateway is also how users in the public can access our resources in a public subnet.

Attaching an internet gateway means resources in our VPC can now access the internet. The EC2 instances with public IP addresses also become accessible to users, so the applications we host on those servers become public too.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

VPC resources could also be created with CloudShell, which is a browser-based terminal built into the AWS Console that lets us run commands without needing to set up a local environment. CLI (Command Line Interface) is the tool we use within CloudShell to type and execute commands that create, configure, and manage AWS resources like VPCs, subnets, and more.

To set up a VPC or a subnet or internet gateway, we can use the commands below. 

To create VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/24 --query Vpc.VpcId --output text

To name VPC
aws ec2 create-tags --resources=[VPC-ID] --tags Key=Name,Value="NextWork VPC 2"

To create subnet
aws ec2 create-subnet --vpc-id [VPC-ID] --cidr-block [ADD-CIDR-BLOCK-HERE]

To create internet gatway
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text

To attach the gatway to VPC
aws ec2 attach-internet-gateway --vpc-id [VPC-ID] --internet-gateway-id [IG-ID]

Note:Make sure to avoid errors by including CIDR Block

To delete the resource below are the commands. 
To de-attach Gateway and VPC
aws ec2 detach-internet-gateway --vpc-id [VPC-ID] --internet-gateway-id [IG-ID]

To delete gateway
aws ec2 delete-internet-gateway --internet-gateway-id [IG-ID]

To delete subnet
aws ec2 delete-subnet --subnet-id [SUBNET-ID]

To delete VPC
aws ec2 delete-vpc --vpc-id [VPC-ID]


Compared to using the AWS Console, an advantage of using commands is that it's faster and more repeatable — we can automate the setup or reuse commands in future projects. An advantage of using the Console is that it's more visual and beginner-friendly, making it easier to understand how resources connect. Overall, we preferred using commands for speed and automation, once we understood what each command was doing.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-vpc_9b2465411)

---

---
