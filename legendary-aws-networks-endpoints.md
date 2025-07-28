<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that helps us create our own networks and configure the security/traffic rules and connectivity with the internet.

### How I used Amazon VPC in this project

We used Amazon VPC in today’s project to create a secure, isolated network environment where we could launch and manage an EC2 instance. We started by creating a custom VPC with a public subnet, configured an internet gateway for external access, and deployed our EC2 instance into this subnet.

Next, we created a VPC endpoint—specifically an S3 Gateway endpoint—to allow our EC2 instance to access an Amazon S3 bucket privately without using the public internet. We then enforced this private access by updating the S3 bucket policy to allow traffic only through our endpoint, and linked the VPC endpoint to our route table to ensure proper routing.

This setup allowed us to securely interact with S3 from within our VPC, demonstrating how VPC, IAM roles, endpoints, and bucket policies work together to control access and protect our resources.

### One thing I didn't expect in this project was...

One thing we didn't expect in this project was that updating the S3 bucket policy to allow access only through the VPC endpoint would block access from the AWS Management Console. Since the console doesn’t route through our VPC endpoint, we immediately saw “Access Denied” warnings after applying the policy. This unexpected behavior highlighted how strictly bucket policies enforce conditions and reminded us to test access from the EC2 instance instead of relying on the console when working with private VPC configurations.

### This project took me...

This project took us approximately 2 hours to complete. The time included setting up the VPC, launching the EC2 instance, configuring IAM roles and policies, creating and testing the S3 bucket and VPC endpoint, updating route tables and bucket policies, and troubleshooting access issues to verify everything worked as expected.

---

## In the first part of my project...

### Step 1 - Architecture set up

We are going to create a VPC from scratch, giving us full control over networking components like IP ranges, subnets, route tables, and internet access.

Next, we’ll launch an EC2 instance into a public subnet within that VPC. Later, we’ll connect to it using EC2 Instance Connect, which allows browser-based SSH access without needing a key pair file.

Finally, we’ll set up an S3 bucket, which we’ll use to store and retrieve files securely. This setup will lay the foundation for securely connecting our compute and storage resources within a custom AWS network environment.

### Step 2 - Connect to EC2 instance

We are going to connect directly to your EC2 instance.

### Step 3 - Set up access keys

In this step, we will give our EC2 instance access to our AWS environment by attaching an IAM role to it. This role will have the necessary permissions—such as access to Amazon S3—so the instance can interact with AWS services securely. 

### Step 4 - Interact with S3 bucket

In this step, we will configure AWS to allow our EC2 instance to access the S3 bucket.

---

## Architecture set up

We started our project by launching a VPC with a public subnet and deploying an EC2 instance within it. This setup provided us with a secure, isolated network environment where the EC2 instance could operate and connect to other AWS services. The VPC gave us full control over networking configurations, such as IP addressing and routing, while the EC2 instance served as our compute resource for interacting with services like Amazon S3.

We set up an S3 bucket and added 2 files to the bucket.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up our EC2 instance to interact with our AWS environment, we configured four key things:

An IAM policy – to define the specific permissions needed to access S3.

An IAM role – to securely grant those permissions to the EC2 instance.

Attached the role to the EC2 instance – so it could assume the permissions defined in the policy.

Used aws configure – to manually set up access credentials on the instance when a role wasn’t used, or to verify the configuration.

Access keys are a pair of security credentials—consisting of an Access Key ID and a Secret Access Key—used to authenticate programmatic access to AWS services. They allow tools like the AWS CLI or SDKs to make API requests on behalf of a user or application. 

Secret access keys are confidential security credentials used alongside the Access Key ID to authenticate programmatic access to AWS services. They act like a password and should be kept private and secure.

### Best practice

Although we are using access keys in this project, a best practice alternative is to use IAM roles. IAM roles allow AWS services like EC2 to securely access other AWS resources without storing or managing access keys. Roles provide temporary credentials that are automatically rotated, reducing the risk of credential exposure and improving overall securit

---

## Connecting to my S3 bucket

The command we ran was "aws s3 ls". This command is used to list all the Amazon S3 buckets associated with the AWS account that the EC2 instance has access to.

When we ran the command aws s3 ls again, the terminal responded with the list of buckets. This indicated that the connection was successful and that the EC2 instance had the proper permissions to access S3 through the AWS CLI.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://nextwork-vpc-project-manish, which returned the list of files in the bucket. This confirmed that the EC2 instance could successfully access and interact with the contents of the specified S3 bucket using the AWS CLI.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_4334d779)

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

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step we will set up a way for our VPC and S3 to communicate direclty.

### Step 6 - Bucket policies

We are going to limit our S3 bucket access to only traffic coming from our VPC endpoint. This means updating the S3 bucket policy to allow access only if the request is made through the specific VPC endpoint we created. This adds an extra layer of security by ensuring that even if credentials are compromised, access to the bucket is blocked unless it comes from within our trusted VPC network.

### Step 7 - Update route tables

We are going to test our VPC endpoint setup by trying to access the S3 bucket from our EC2 instance using the AWS CLI. This will help verify whether the instance can successfully connect to S3 through the private VPC endpoint.

If we encounter any connectivity issues, we’ll troubleshoot by checking the following:

Whether the bucket policy correctly references our VPC endpoint ID.

If the IAM role attached to the EC2 instance has the right permissions for S3.

That the VPC endpoint is properly associated with the route table for our subnet.

And whether DNS resolution is enabled for the VPC.

This step ensures our setup is secure and working as expected.

### Step 8 - Validate endpoint conection

We are going to test our VPC endpoint setup again, but this time with a stronger security control in place.

Specifically, we will restrict our VPC’s access to our AWS environment by updating the endpoint policy.

---

## Setting up a Gateway

We set up an S3 Gateway, which is a type of VPC endpoint that allows private access to Amazon S3 from within our VPC. Instead of routing traffic through the public internet, the S3 Gateway enables our EC2 instance to securely communicate with S3 using the AWS network. This improves both security and performance, ensuring that data transfers between the VPC and S3 stay internal to AWS.

### What are endpoints?

An endpoint is a private connection between your VPC and another AWS service, such as Amazon S3, that allows traffic to flow securely within the AWS network—without using the public internet. Endpoints improve security, reduce latency, and ensure more reliable access to services by keeping data inside the AWS infrastructure. They can be configured using VPC endpoints, such as gateway endpoints for S3.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a resource-based AWS Identity and Access Management (IAM) policy that is attached directly to an S3 bucket. It defines who can access the bucket, what actions they can perform (such as GetObject or PutObject), and under what conditions (like requiring access through a specific VPC endpoint). Bucket policies are written in JSON and provide fine-grained control over access to the bucket and its contents, helping enforce strong security and compliance standards.

Our bucket policy will deny all access to the S3 bucket unless the request comes through a specific VPC endpoint. In this case, access is only allowed if the request uses the VPC endpoint with the ID vpce-0b6a9c9e1e9a10847. This ensures that even if someone has valid credentials, they won't be able to access the bucket from outside the trusted VPC network—enhancing the security of our data by enforcing private, internal access only.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving our bucket policy, our S3 bucket page showed 'denied access' warnings. This was because the policy explicitly denies all access unless the request comes through the specified VPC endpoint. Since the S3 console in the AWS Management Console does not use our VPC endpoint, it was blocked by the policy. This behavior confirms that the policy is working as intended by restricting access to traffic only from our VPC endpoint.

I also had to update my route table because in my VPC endpoint setup, the S3 Gateway endpoint requires an explicit route association with the route table used by the subnet where my EC2 instance is running. Without this association, the EC2 instance wouldn’t be able to route traffic to S3 through the VPC endpoint, and access would fail. Updating the route table ensured that S3 traffic stays within the AWS network and uses the private endpoint instead of the public internet.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

o update my route table, I went to the VPC endpoint section in the VPC console, selected my S3 endpoint, and then clicked on "Route tables". From there, I chose "Manage route tables", checked the box next to the public route table associated with my EC2 instance’s subnet, and selected "Modify route tables". This step ensured that traffic from the EC2 instance to S3 is routed through the VPC endpoint, enabling private and secure access.

After updating our public subnet's route table, our terminal could return the list of files in the S3 bucket using the aws s3 ls s3://nextwork-vpc-project-manish command. This confirmed that our EC2 instance was successfully routing traffic to S3 through the VPC endpoint, and that the bucket policy allowing access only from the endpoint was working correctly.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a resource-based policy attached to a VPC endpoint that controls which AWS services and actions can be accessed through that endpoint. It allows you to define fine-grained access rules—such as limiting access to specific S3 buckets or actions—when traffic flows through the endpoint. An endpoint policy works in combination with IAM policies and bucket policies to enforce secure and controlled access within your VPC.

We updated our endpoint's policy by going to the Endpoints tab in the VPC console, selecting the checkbox next to our VPC endpoint, then clicking on the Policy tab. We chose Edit policy, changed "Effect": "Allow" to "Effect": "Deny", and then saved the changes.

We could see the effect of this right away, because when we tried to access the S3 bucket from our EC2 instance using the AWS CLI, the request was denied. This confirmed that the endpoint policy successfully blocked access, showing how powerful endpoint policies are for controlling traffic through VPC endpoints.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-endpoints_3e1e79a3)

---

---
