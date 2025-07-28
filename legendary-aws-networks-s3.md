[Main Page](./README.md)
---

---

[⬅ Previous Page: VPC Monitoring with Flow Logs](./legendary-aws-networks-monitoring.md)

[➡️ Next Page: VPC Endpoints](./legendary-aws-networks-endpoints.md)

---

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that helps us create our own networks and configure the security/traffic rules and connectivity with the internet.

### How I used Amazon VPC in this project

We used Amazon VPC in today’s project to create a secure and isolated network environment for our EC2 instance. We launched a custom VPC with a public subnet, configured routing and internet access, and deployed the EC2 instance within this VPC. This setup allowed us to control networking components like IP ranges and route tables, and to ensure that the EC2 instance could securely connect to AWS services—such as Amazon S3—using an IAM role.

### One thing I didn't expect in this project was...

ne thing we didn’t expect in this project was how important IAM roles would be for securely accessing AWS services from the EC2 instance. Initially, we considered using access keys, but assigning an IAM role made the process much easier and more secure. It also eliminated the need to manually configure credentials, which helped us avoid potential security risks and saved time during setup.

### This project took me...

It took me about 1 hours to complete this project

---

## In the first part of my project...

### Step 1 - Architecture set up

We are going to create a VPC from scratch and launch an EC2 instance into it. This will involve defining a custom IP range using a CIDR block, setting up a public subnet, configuring route tables and an internet gateway for external access, and then deploying an EC2 instance into the VPC. This hands-on setup will give us full control over networking and security, and allow the EC2 instance to interact with other AWS services in a secure and isolated environment.

### Step 2 - Connect to my EC2 instance

n this step, we will directly connect to the EC2 instance using SSH from our local machine. This allows us to access the instance’s terminal, run commands, and interact with AWS services like Amazon S3 from within the instance. It’s a crucial step for verifying connectivity, testing permissions, and managing resources securely from within the VPC environment.

### Step 3 - Set up access keys

We are going to give our EC2 instance access to our AWS environment by attaching an IAM role with the necessary permissions. This allows the instance to interact with AWS services—like Amazon S3—securely and without the need to manually configure access keys. By using an IAM role, we ensure that credentials are managed automatically and securely within the AWS environment.

---

## Architecture set up

We started our project by launching a VPC with a public subnet and deploying an EC2 instance within it. This setup provided us with a secure, isolated network environment where the EC2 instance could operate and connect to other AWS services. The VPC gave us full control over networking configurations, such as IP addressing and routing, while the EC2 instance served as our compute resource for interacting with services like Amazon S3.

We also set up an S3 bucket and added 2 files to the bucket.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI is a command-line tool that allows users to interact with AWS services using text-based commands instead of the web console. I have access to AWS CLI because it is pre-installed on the EC2 instance.

The first command we ran was "aws s3 ls". This command is used to list all the Amazon S3 buckets associated with the AWS account that the EC2 instance has access to. It helps confirm that the AWS CLI is properly configured and that the instance has the correct permissions to interact with S3.

The second command I ran was "aws configure". This command is used to set up the AWS CLI with credentials and default settings such as the AWS Access Key ID, Secret Access Key, default region, and output format. It’s essential when an IAM role isn’t attached to the EC2 instance, or when manually configuring the CLI on a local machine to authenticate and interact with AWS services.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up the EC2 instance to interact with the AWS environment, we configured it using the "aws configure" command. This command allowed us to provide the necessary credentials—Access Key ID, Secret Access Key, default region, and output format—so the AWS CLI could authenticate and execute commands like accessing S3 buckets or listing AWS resources.

Access keys are a set of security credentials used to authenticate programmatic access to AWS services. They consist of an Access Key ID and a Secret Access Key. These keys allow the AWS CLI, SDKs, or other tools to make API calls on behalf of a user or application. It’s important to keep them secure, as they provide direct access to your AWS resources—similar to a password.

Secret access keys are confidential security credentials used alongside the Access Key ID to authenticate programmatic access to AWS services. They act like a password and should be kept private and secure.

### Best practice

Although we are using access keys in this project, a best practice alternative is to use IAM roles. IAM roles allow AWS services like EC2 to securely access other AWS resources without storing or managing access keys. Roles provide temporary credentials that are automatically rotated, reducing the risk of credential exposure and improving overall security.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step we will launch a S3 bucket for the project.

### Step 5 - Connecting to my S3 bucket

We are going to head back to our EC2 instance and get it to interact with our S3 bucket.

---

## Connecting to my S3 bucket

The first command we ran was "aws s3 ls". This command is used to list all the Amazon S3 buckets associated with the AWS account that the EC2 instance has access to. It helps confirm that the AWS CLI is properly configured and that the instance has the correct permissions to interact with S3.

When we ran the command aws s3 ls again, the terminal responded with the list of buckets. This indicated that the connection was successful and that the EC2 instance had the proper permissions to access S3 through the AWS CLI.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://nextwork-vpc-project-manish, which returned the list of files in the bucket. This confirmed that the EC2 instance could successfully access and interact with the contents of the specified S3 bucket using the AWS CLI.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to the bucket, we first ran the command:

sudo touch /tmp/test.txt  

This command creates a blank file named test.txt in the /tmp directory.

The second command we ran was:

aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-manish  

This command uploads it to the specified S3 bucket using the aws s3 cp.

The third command we ran was:

aws s3 ls s3://nextwork-vpc-project-manish

This command then lists the contents of the bucket to confirm that the upload was successful.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-s3_3e1e79a2)

---

[➡️ Next Page: VPC Endpoints](./legendary-aws-networks-endpoints.md)

[⬅ Previous Page: VPC Monitoring with Flow Logs](./legendary-aws-networks-monitoring.md)


[Main Page](./README.md)
---

---
