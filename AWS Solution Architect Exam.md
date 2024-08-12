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
