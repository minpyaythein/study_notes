# AWS Solution Architect Exam Study Notes

#### Networking Device suitable for HPC?

Elastic Fabric Adapter > Elastic Network Adapter > Elastic Network Interface (Most basic)

#### Shared Storage Space for windows-based application which is to move from on-premises data center to cloud

Amazon FSx for Windows File Server
Amazon FSx for Lustre, EFS for Linux

#### File Gateway of AWS Storage Gateway for Hybrid Storage (Not suitable for sharing)

#### Clickstream data for a billing application

Amazon Kinesis Data Streams

#### An e-commerce company uses Microsoft Active Directory to provide users and groups with access to resources on the on-premises infrastructure and extended as hybrid cloud. SSO sign on for its users to access resources.

AWS Directory Service for Microsoft Active Directory (AWS Managed Microsoft AD)

#### Given the use-case where the CTO at the company wants to move away from license-based, expensive, legacy commercial database solutions deployed at the on-premises data center to more efficient, open-source, and cost-effective options on AWS Cloud, this is an example of heterogeneous database migrations.

The source and target databases engines are different => AWS Schema Conversion Tool
On-premises DC to AWS Cloud => AWS Database Migration Service

#### AWS Glue

ETL (Extract, transform and load) for analytics and for batch ETL data processing

#### Setting up a consistent resource provisioning process across departments so that each resource follows pre-defined configurations such as using a specific type of Amazon EC2 instances, specific IAM roles for AWS Lambda functions, etc.

Use AWS CloudFormation StackSets to deploy the same template across AWS accounts and regions

#### Too complex with many ALBs, IPs and configs. To reduce IPs

AWS Global Accelerator and create endpoints for all the Regions, connecting to ALBs.

#### ALB cannot be assigned with Elastic IP but NLB can.

#### The application will be accessed by users from different geographic regions of the world to upload and download video files that can reach a maximum size of 10 gigabytes.

(For smaller than 1GB) Use Amazon S3 for hosting the web application and use Amazon S3 Transfer Acceleration (Amazon S3TA) to reduce the latency that geographically dispersed users might face
(For smaller than 1GB) Use Amazon S3 for hosting the web application and use Amazon CloudFront for faster distribution of content to geographically dispersed users

#### A cost-effective serverless solution for its flagship application that has both static and dynamic content

Host the static content on Amazon S3 and use AWS Lambda with Amazon DynamoDB for the serverless web application that handles dynamic content. Amazon CloudFront will sit in front of AWS Lambda for distribution across diverse regions

#### A web log archival solution that only the most frequently accessed logs are available as cached data locally while backing up all logs on Amazon S3.

Use AWS Volume Gateway - Cached Volume - to store the most frequently accessed logs locally for low-latency access while storing the full volume with all logs in its Amazon S3 service
(AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage. The service provides three different types of gateways – Tape Gateway, File Gateway, and Volume Gateway)

#### Automate and accelerate online data transfers to these AWS storage services

Use AWS DataSync

#### Confirm that requests are not sent to the unhealthy or deregistering instances

Connection Draining

#### Correct Configuration for IPSec VPN Connection to move from OP DC to AWS Cloud

Virtual Private Gateway (VGW) on AWS side and Customer Gateway on the on-premises

#### Automatically recover EC2 instances if impaired

A recovered one is identical to the original (instance ID, private and elastic IP, instance metadata) and retains the public IPv4 address.
(The recover action is supported only on instances that have Amazon EBS volumes configured on them, instance store volumes are not supported for automatic recovery by Amazon CloudWatch alarms.)

#### Customers can access Amazon SQS from Amazon VPC using VPC endpoints, without using public IPs, and without needing to traverse the public internet. (VPC endpoints for Amazon SQS are powered by AWS PrivateLink)

#### AWS PrivateLink enables to connect VPC to AWS services.

#### Amazon SQS provides short polling and long polling to receive messages from a queue. By default, queues use short polling. With short polling, Amazon SQS sends the response right away, even if the query found no messages. With long polling, Amazon SQS sends a response after it collects at least one available message, up to the maximum number of messages specified in the request. Amazon SQS sends an empty response only if the polling wait time expires. Long polling makes it inexpensive to retrieve messages from your Amazon SQS queue as soon as the messages are available. Using long polling can reduce the cost of using SQS because you can reduce the number of empty receives.

#### Visibility timeout is a period during which Amazon SQS prevents other consumers from receiving and processing a given message.

#### Use Amazon Kinesis Data Streams to process the data streams as well as decouple the producers and consumers for the real-time data processor

#### Use Amazon GuardDuty to monitor any malicious activity on data stored in Amazon S3. Use Amazon Macie to identify any sensitive data stored on Amazon S3

#### Configure AWS Auto Scaling to scale out the Amazon ECS cluster when the ECS service's CPU utilization rises above a threshold (NOT Cloudwatch)

#### Schedule a weekly Amazon EventBridge event cron expression to invoke an AWS Lambda function that runs the database rollover job

#### Use AWS Config to review resource configurations to meet compliance guidelines and maintain a history of resource configuration changes

#### The orders booked in one AWS Region should be visible to all AWS Regions in a second or less. The database should be able to facilitate failover with a short Recovery Time Objective (RTO).

Amazon Aurora Global Database is cheaper than DynamoDB global tables which also have no failover concept.

#### Service control policy (SCP)

SCP controls over IAM permission policy, affects all users and accounts including root user but not service-linked roles

#### Alias Record for Route 53 for the top node of a DNS namespace

#### Want to use NLB for millions of requests per second

Traffic is routed to instances using primary private IP addresses

#### Create inbound and outbound endpoints for resolving DNS of AWS and on-premises.

#### Sharing a VPC is difficult but subnets by VPC Sharing

#### AWS DMS can also replicate data from a database into Amazon Redshift

#### VPC Gateway endpoints provide reliable connectivity to Amazon S3 without requiring an internet gateway or a NAT device for your VPC.

#### AMI can be shared with another account across regions

#### A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.

#### If you have multiple AWS Site-to-Site VPN connections, you can provide secure communication between sites using the AWS VPN CloudHub. This enables your remote sites to communicate with each other, and not just with the VPC.

#### When you create a Launch Template, the default value for the instance tenancy is shared and the instance tenancy is controlled by the tenancy attribute of the VPC. If you set the Launch Template Tenancy to shared (default) and the VPC Tenancy is set to dedicated, then the instances have dedicated tenancy. If you set the Launch Template Tenancy to dedicated and the VPC Tenancy is set to default, then again the instances have dedicated tenancy.

#### An internet gateway is used to provide internet access for the public subnets.

#### The private subnets require access to the internet to allow Amazon EC2 instances to download software updates. (One public and private subnet in each of 3 AZs)

Set up three NAT gateways, one in each public subnet in each AZ. Create a custom route table for each AZ that forwards non-local traffic to the NAT gateway in its AZ

#### An Internet Gateway serves two purposes: to provide a target in your VPC route tables for internet-routable traffic and to perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.

#### The database backend for a retail company's website is hosted on Amazon RDS for MySQL having a primary instance and three read replicas to support read scalability. The company has mandated that the read replicas should lag no more than 1 second behind the primary instance to provide the best possible user experience

Set up database migration from Amazon RDS MySQL to Amazon Aurora MySQL. Swap out the MySQL read replicas with Aurora Replicas. Configure Aurora Auto Scaling

#### A Spot Instance request is either one-time or persistent. If the spot request is persistent, the request is opened again after your Spot Instance is interrupted. If the request is persistent and you stop your Spot Instance, the request only opens after you start your Spot Instance.

#### To cancel a persistent Spot request and terminate its Spot Instances, you must cancel the Spot request first and then terminate the Spot Instances.

#### Migrating from SQS Standard to FIFO

Make sure that the name of the FIFO (First-In-First-Out) queue ends with the .fifo suffix
Delete the existing standard queue and recreate it as a FIFO (First-In-First-Out) queue
Make sure that the throughput for the target FIFO (First-In-First-Out) queue does not exceed 3,000 messages per second

#### Amazon Aurora Serverless is fully managed and supports full auto-scaling. (NOT Aurora)

#### Security Groups are stateful, so allowing inbound traffic to the necessary ports enables the connection. Network ACLs are stateless, so you must allow both inbound and outbound traffic

#### An e-commerce company runs its web application on Amazon EC2 instances in an Auto Scaling group and it's configured to handle consumer orders in an Amazon Simple Queue Service (Amazon SQS) queue for downstream processing. The DevOps team has observed that the performance of the application goes down in case of a sudden spike in orders received.

Target Tracking Scaling Policy based on a custom Amazon SQS queue metric

#### Dedicated Hosts enable you to use your existing server-bound software licenses like Windows Server and address corporate compliance and regulatory requirements.

#### Security Groups can be associated with a NAT instance

#### NAT instance can be used as a bastion server

#### NAT instance supports port forwarding

#### Even after selecting the same default subnet (us-west-2a) while launching the instances in each of the AWS accounts, the IT consultant notices that the Availability Zones (AZs) are still different.

Use Availability Zone (AZ) ID to uniquely identify the Availability Zones across the two AWS Accounts

#### Looking for cloud file storage offerings that provide full Windows compatibility.

File Gateway Configuration of AWS Storage Gateway
Amazon FSx for Windows File Server

#### With cross-zone load balancing enabled, one instance in Availability Zone A receives 20% traffic and four instances in Availability Zone B receive 20% traffic each. With cross-zone load balancing disabled, one instance in Availability Zone A receives 50% traffic and four instances in Availability Zone B receive 12.5% traffic each.

#### Use Amazon DynamoDB point in time recovery to restore the table to the state just before corrupted data was written

#### When you enable PITR, DynamoDB backs up your table data automatically with per-second granularity. Thus, it helps with accidental writes and deletes.

#### Amazon DynamoDB Streams captures a time-ordered sequence of item-level modifications in any Amazon DynamoDB table and stores this information in a log for up to 24 hours.

#### Amazon CloudFront provides two ways to send authenticated requests to an Amazon S3 origin: origin access control (OAC) and origin access identity (OAI).

Configure Amazon CloudFront to send authenticated requests to Amazon S3, and configure Amazon S3 to only allow access to authenticated requests from Amazon CloudFront.

Create an AWS WAF ACL and use an IP match condition to allow traffic only from those IPs that are allowed in the Amazon EC2 security group. Associate this new AWS WAF ACL with the Amazon CloudFront distribution

#### Use AWS Global Accelerator to provide a low latency way to distribute live sports results for UDP connection. (For HTTP connection, CloudFront may be better.)

#### The app is very slow when the business reports are run on RDS DB.

Create a read replica and connect the report generation tool or app to it

#### Read cannot be done from the standby DB.

#### CNAME records can be used to map one domain name to another but not for the top node of a DNS namespace.

#### Route 53 charges CNAME records but alias records.

#### Amazon SQS lets you decouple application components so that they run and fail independently, increasing the overall fault tolerance of the system.
