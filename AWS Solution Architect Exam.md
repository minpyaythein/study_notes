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
