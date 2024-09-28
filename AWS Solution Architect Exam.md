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

(For larger than 1GB) Use Amazon S3 for hosting the web application and use Amazon S3 Transfer Acceleration (Amazon S3TA) to reduce the latency that geographically dispersed users might face
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

#### To run its applications on single-tenant hardware to meet compliance guidelines.

The most cost-effective way of isolating the Amazon EC2 instances to a single tenant is using Dedicated Instances

#### Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances.

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

#### CNAME records can be used to map one domain name to another but not for the top node of a DNS namespace such as acme.example.com, to another domain (example.com or example.net) or subdomain (acme.example.com or zenith.example.org). For example, if you register the DNS name example.com, the zone apex is example.com. You cannot create a CNAME record for example.com, but you can create CNAME records for www.example.com, newproduct.example.com, and so on.

#### Route 53 charges CNAME records but alias records.

#### CNAME and NS record cannot be used for the top node of the DNS namespace but can be used for other such as from app.covid19survey.com to app.covid19survey.net.

#### Alias record can be used for the top node such as from covid19survey.com to www.covid19survey.com and can only redirect queries to selected AWS resources.

#### An A record is used to point a domain or subdomain to an IP address and a PTR record is just opposite.

#### Looking for cloud file storage offerings that provide full Windows compatibility.

File Gateway Configuration of AWS Storage Gateway
Amazon FSx for Windows File Server

#### Amazon SQS lets you decouple application components so that they run and fail independently, increasing the overall fault tolerance of the system.

#### DynamoDB has two read/write capacity modes: on-demand and provisioned.

#### ELB can be configured for host-based routing to support multiple subdomains and different top-level domains.

#### AWS Site-to-Site VPN connections are used for secure connectivity to its AWS cloud resources from its on-premises DC.

If users are experiencing slower VPN connectivity, AWS Transit Gateway with equal cost multipath routing and add additional VPN tunnels

#### Access control lists (ACLs) are service policies that allow you to control which principals in another account can access a resource.

#### A permissions boundary is an advanced feature for using a managed policy to set the maximum permissions that an identity-based policy can grant to an IAM entity.

#### SCPs are JSON policies that specify the maximum permissions for an organization or organizational unit (OU). The SCP limits permissions for entities in member accounts, including each AWS account root user. An explicit deny in any of these policies overrides the allow.

#### Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket.

#### The IAM service supports only one type of resource-based policy called a role trust policy, which is attached to an IAM role.

#### Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies.

#### AWS CloudFormation allows you to keep your infrastructure as code and re-use the best practices around your company for configuration parameters.

#### Amazon ElastiCache Redis is used and a disaster recovery strategy for its caching layer that gives minimal downtime and data loss is necessary.

Opt for Multi-AZ configuration with automatic failover functionality to help mitigate failure

#### To facilitate the hosting of Docker containers, the company is looking at various orchestration services.

Amazon EKS and ECS with Fargate for serverless orchestration of the containerized services

#### Select a cluster placement group while launching EC2 instances for high network throughput and low-latency network performance with tightly coupled node-to-node communication.

#### When you create an AWS Elastic Beanstalk environment, you can specify an Amazon Machine Image (AMI) to use instead of the standard Elastic Beanstalk AMI included in your platform version.

Create a Golden Amazon Machine Image (AMI) with the static installation components already setup
Use Amazon EC2 user data to customize the dynamic installation parts at boot time

#### Disaster Recovery Strategy leveraging AWS Cloud

Multi-Site > Warm Standby > Pilot Light > Backup and Restore
Backup and Restore: In most traditional environments, data is backed up to tape and sent off-site regularly. If you use this method, it can take a long time to restore your system in the event of a disruption or disaster.
Pilot Light: The term pilot light is often used to describe a DR scenario in which a minimal version of an environment is always running in the cloud. With AWS you can maintain a pilot light by configuring and running the most critical core elements of your system in AWS.
Warm Standby: The term warm standby is used to describe a DR scenario in which a scaled-down version of a fully functional environment is always running in the cloud. A warm standby solution extends the pilot light elements and preparation.
Multi-Site: A multi-site solution runs in AWS as well as on your existing on-site infrastructure, in an active-active configuration.

#### To reduce costs and for read-heavy operations of an app using API Gateway, Lambda and Aurora DB.

You can enable Amazon API caching in Amazon API Gateway to cache your endpoint's responses. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of requests to your API. When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds.

#### To copy a petabyte of data from on-premises DC to a S3 bucket

Copy data from the source bucket to the destination bucket using the aws S3 sync command
Set up Amazon S3 batch replication to copy objects across Amazon S3 buckets in another Region using S3 console and then delete the replication configuration

#### Migrating the application consisting of application servers and a Microsoft SQL Server database from on-premises to AWS.

Migrate the data to Amazon RDS for SQL Server database in a Multi-AZ deployment

#### Costs are too high for startup app using EC2 instances, RDS instances and S3.

Use AWS Cost Explorer Resource Optimization to get a report of Amazon EC2 instances that are either idle or have low utilization and use AWS Compute Optimizer to look at instance type recommendations

#### Decoupling the architecture of a SaaS app with in-house and 3rd-party apps.

Use Amazon EventBridge to decouple the system architecture.
Amazon SQS cannot be integrated with 3rd-party SaaS services.

#### Adding read replicas would further add to the database costs and will not help in reducing latency when compared to a caching solution. Caching is the solution.

#### Across regions have multiple ALBs and it is necessary to allow IP addresses of the ALBs in on-premises.

Use Global Accelerator. Register the Application Load Balancers in different Regions to the AWS Global Accelerator. Configure the on-premises firewall's rule to allow static IP addresses associated with the AWS Global Accelerator

#### Amazon MQ is a managed message broker service for Apache ActiveMQ that makes it easy to set up and operate message brokers in the cloud. Message brokers allow different software systems–often using different programming languages, and on different platforms–to communicate and exchange information.

Connecting your current applications to Amazon MQ is easy because it uses industry-standard APIs and protocols for messaging, including JMS, NMS, AMQP, STOMP, MQTT, and WebSocket.

#### There are two types of VPC endpoints: Interface Endpoints and Gateway Endpoints.

An Interface Endpoint is an Elastic Network Interface with a private IP address from the IP address range of your subnet that serves as an entry point for traffic destined to a supported service.

A Gateway Endpoint is a gateway that you specify as a target for a route in your route table for traffic destined to a supported AWS service. The following AWS services are supported: Amazon S3 and Amazon DynamoDB.

#### Wants a capability to dynamically alter the size of a geographic area from which traffic is routed to a specific server resource.

Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

#### The CTO wants to re-engineer a monolithic app towards microservices architecture and expose their application from the same load balancer, linked to different target groups with different URLs: checkout.mycorp.com, www.mycorp.com, yourcorp.com/profile and yourcorp.com/search. The CTO would like to expose all these URLs as HTTPS endpoints for security purposes.

Use Secure Sockets Layer certificate (SSL certificate) with SNI
SNI supports the use of more than one certificate with the same ALB.

#### A music-sharing company uses a Network Load Balancer to direct traffic to 5 Amazon EC2 instances managed by an Auto Scaling group. When a very popular song is released, the Auto Scaling Group scales to 100 instances and the company incurs high network and compute fees.

#### Amazon CloudFront

Amazon CloudFront can route to multiple origins based on the content type
Use an origin group with primary and secondary origins to configure Amazon CloudFront for high-availability and failover
Use field level encryption in Amazon CloudFront to protect sensitive data for specific content

#### The company wants a dedicated private connection between the on-premise data center and AWS. In case of failures though, the company needs to guarantee uptime and is willing to use the public internet for an encrypted connection.

Use AWS Direct Connect connection as a primary connection and AWS Site-to-Site VPN as a backup connection.

#### IAM database authentication works with MySQL and PostgreSQL. With this authentication method, you don't need to use a password when you connect to a database instance. Instead, you use an authentication token.

#### The bucket policies are for managing permissions for users in their own AWS account and users in other AWS accounts.

#### The user policies are for managing permissions for users in their own AWS account and NOT for users in other AWS accounts.

#### AWS Secrets Manager enables you to easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle

#### The database uses AWS Key Management Service (AWS KMS) for encrypting data at rest. SSL is used for data in transit.

#### If you intend to reuse code in more than one AWS Lambda function, you should consider creating an AWS Lambda Layer for the reusable code

#### Since AWS Lambda functions can scale extremely quickly, it's a good idea to deploy a Amazon CloudWatch Alarm that notifies your team when function metrics such as ConcurrentExecutions or Invocations exceeds the expected threshold

#### By default, AWS Lambda functions always operate from an AWS-owned VPC and hence have access to any public internet address or public AWS APIs. Once an AWS Lambda function is VPC-enabled, it will need a route through a Network Address Translation gateway (NAT gateway) in a public subnet to access public resources.

#### A Lambda function should only be VPC-enabled when necessary to interact with a private resource or subnet.

#### Amazon EBS

SSD-backed volumes optimized for transactional workloads involving frequent read/write operations with small I/O size, where the dominant performance attribute is IOPS.
HDD-backed volumes optimized for large streaming workloads where throughput (measured in MiB/s) is a better performance measure than IOPS.
Provisioned IOPS SSD (io1) volumes are designed to meet the needs of I/O-intensive workloads, particularly database workloads, that are sensitive to storage performance and consistency.

#### AWS Transit Gateway can be used to connect the Amazon VPCs to the on-premises networks.

#### What is better than saving log files on EC2

Installing CloudWatch Logs agents on EC2 to send logs to CloudWatch

#### Amazon Memcached, a high-performance distributed memory cache service, is designed for simplicity while Redis offers a rich set of features that make it effective for a wide range of use cases. Memcached does not offer support for geospatial data.

#### Use AWS DataSync to migrate existing data to Amazon S3 and then use File Gateway to retain access to the migrated data for ongoing updates from the on-premises applications

#### Enable Amazon S3 Transfer Acceleration (Amazon S3TA) for the Amazon S3 bucket. This would speed up uploads as well as downloads for the video files.

#### Use Amazon CloudFront distribution with origin as the Amazon S3 bucket. This would speed up uploads as well as downloads for the video files

#### The Application Load Balancer removes an instance from its pool of healthy instances whenever it is detected as unhealthy but the Auto Scaling group provisions the replacement instance.

It is recommended to use ALB based health checks for both Auto Scaling group and Application Load Balancer.

#### Internet Gateway (IGW) allows instances with public IPs to access the internet. NAT Gateway (NGW) allows instances with no public IPs to access the internet.

#### An encrypted Amazon EBS volume

Data moving between the volume and the instance is encrypted
Data at rest inside the volume is encrypted
Any snapshot created from the volume is encrypted

#### Upon inspecting application logs, the team notices several "could not connect to server: connection timed out" error messages.

The security group configuration for the database instance does not have the correct rules to allow inbound connections from the application servers

#### A process replaces an existing object and immediately tries to read it. Amazon S3 always returns the latest version of the object

#### Amazon EBS volumes are Availability Zone (AZ) locked

#### Use a dead-letter queue of SQS to handle message processing failures

Dead-letter queues can be used by other queues (source queues) as a target for messages that can't be processed (consumed) successfully. Dead-letter queues are useful for debugging your application or messaging system because they let you isolate problematic messages to determine why their processing doesn't succeed. Sometimes, messages can’t be processed because of a variety of possible issues, such as when a user comments on a story but it remains unprocessed because the original story itself is deleted by the author while the comments were being posted. In such a case, the dead-letter queue can be used to handle message processing failures.

#### AWS Trusted Advisor is an online tool that draws upon best practices learned from AWS’s aggregated operational history of serving hundreds of thousands of AWS customers.

#### For disaster recovery of the read-heavy database

Use cross-Region Read Replicas and enable the automated backup feature of Amazon RDS in a multi-AZ deployment that creates backups across multiple Regions

#### When you use AWS WAF with Amazon CloudFront, you can protect your applications running on any HTTP webserver

#### Only Standard Amazon SQS queue is allowed as an Amazon S3 event notification destination, whereas FIFO SQS queue is not allowed

#### The development team has updated the Amazon Route 53 simple record to point "myapp.mydomain.com" from the old Load Balancer to the new one. The users are still not redirected to the new Load Balancer.

The Time To Live (TTL) is still in effect.

#### A healthcare company is evaluating storage options on Amazon S3 to meet regulatory guidelines. The data should be stored in such a way on Amazon S3 that it cannot be deleted until the regulatory time period has expired.

Use Amazon S3 Object Lock
Amazon S3 Object Lock is an Amazon S3 feature that allows you to store objects using a write once, read many (WORM) model. You can use WORM protection for scenarios where it is imperative that data is not changed or deleted after it has been written.

#### Amazon S3 Glacier Vault Lock

A vault is a container for storing archives on Glacier. When you create a vault, you specify a vault name and the AWS Region in which you want to create the vault. Since Vault Lock is only for Glacier and not for Amazon S3, so it cannot be used for the given use-case.
It is for data backup and archival.

#### To whitelist an IP, NLB is useful. To whitelist a DNS or URL, ALB can be used.

#### To transition objects of certain group to S3, a prefix can be used.

#### Both AWS Snowball Edge Storage Optimized and AWS Snowball Edge Compute Optimized offer the storage clustering feature.

#### Amazon EC2 user data cannot be used to install the app.

#### AWS DMS enables you to seamlessly migrate data from supported sources to relational databases, data warehouses, streaming platforms, and other data stores in AWS cloud. It allows to stream the existing data files as well as any ongoing file updates from Amazon S3 to Amazon Kinesis Data Streams.

#### Amazon DynamoDB Streams will contain a stream of all the changes that happen to an Amazon DynamoDB table. It can be chained with an AWS Lambda function that will be triggered to react to these changes, one of which is the developer's milestone.

#### By default, cross-zone load balancing is enabled for Application Load Balancer and disabled for Network Load Balancer

#### Amazon Redshift is a fully-managed petabyte-scale cloud-based data warehouse product designed for large scale data set storage and analysis.

Using Amazon Redshift Spectrum, you can efficiently query and retrieve structured and semistructured data from files in Amazon S3 without having to load the data into Amazon Redshift tables.

#### Allowing some connections without blocking all in a country

Use AWS WAF geo match statement listing the countries that you want to block
Use AWS WAF IP set statement that specifies the IP addresses that you want to allow through

#### Amazon S3 cannot encrypt object metadata by using Server-Side Encryption

#### AWS WAF (w/o Amazon CloudFront) can prevent SQL injection and cross-site scripting attacks.

#### Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon S3 using standard SQL.

#### Use AWS transit gateway to interconnect the VPCs

#### Instance store is ideal for the temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

#### You can quickly create clones of an Aurora DB by using the database cloning feature. In addition, database cloning uses a copy-on-write protocol, in which data is copied only at the time the data changes, either on the source database or the clone database. Cloning is much faster than a manual snapshot of the DB cluster.

#### DynamoDB can handle any changes in data attributes over time.

#### By default, all Amazon DynamoDB tables are encrypted using AWS owned keys, which do not write to AWS CloudTrail logs

#### HIPAA compliant in-memory database that supports caching results of SQL queries is ElastiCache for Redis/Memcached.

#### DAX does not support SQL query caching.

#### When you use server-side encryption with AWS KMS (SSE-KMS), you can specify a customer-managed CMK that you have already created. SSE-KMS provides you with an audit trail that shows when your CMK was used and by whom.

#### When you use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3), each object is encrypted with a unique key.

#### With Server-Side Encryption with Customer-Provided Keys (SSE-C), you manage the encryption keys and Amazon S3 manages the encryption

#### Network Load Balancer is best suited for use-cases involving low latency and high throughput workloads that involve scaling to millions of requests per second.

#### The CNAME record will be updated to point to the standby database when the primary instance of the Multi-AZ configuration goes down.

#### Internet Gateway to establish internet connectivity

The network access control list (network ACL) associated with the subnet must have rules to allow inbound and outbound traffic

The route table in the instance’s subnet should have a route to an Internet Gateway

#### http://169.254.169.254/latest/meta-data/public-ipv4 to retrieve the instance public IP from within a shell script

#### The company wants a solution where users will be directed to a static error page, configured as a backup, in case of unavailability of the primary website.

Set up Amazon Route 53 active-passive type of failover routing policy. If Amazon Route 53 health check determines the Application Load Balancer endpoint as unhealthy, the traffic will be diverted to a static error page, hosted on Amazon S3 bucket

#### An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for the temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

You can specify instance store volumes for an instance only when you launch it. You can't detach an instance store volume from one instance and attach it to a different instance.

#### Moving the data to Amazon S3 glacier will prevent us from being able to query it.

#### S3 Intelligent-Tiering storage class works by storing objects in two access tiers: one tier that is optimized for frequent access and another lower-cost tier that is optimized for infrequent access.

#### Service control policy (SCP) is a type of organization policy that you can use to manage permissions in your organization. SCPs offer central control over the maximum available permissions for all accounts in your organization. SCPs help you to ensure your accounts stay within your organization’s access control guidelines.

#### AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics.

#### Amazon EMR is the industry-leading cloud big data platform for processing vast amounts of data using open source tools such as Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto.

#### Client-side encryption is the act of encrypting your data locally to help ensure its security in transit and at rest.

#### ElastiCache for Memcached does not support replication and archival snapshots where redis does.

#### To accomplish this, the engineering team has designed the VPC with a public subnet and a private subnet. The team also wants Transport Layer Security (TLS) termination to be offloaded from the Amazon EC2 instances.

Set up a Network Load Balancer in the public subnet. Create an Auto Scaling group in the private subnet and associate it with the Network Load Balancer

NLB has to be accessible over the internet and hence has to be in a public subnet and will act as a single point-of-contact for all incoming traffic.

ALB and NLB also support Transport Layer Security (TLS) offloading. CLB supports SSL offloading.

#### Updates to your DB Instance are synchronously replicated across the Availability Zone to the standby in order to keep both in sync and protect your latest database updates against DB instance failure.

#### Amazon RDS applies operating system updates by performing maintenance on the standby, then promoting the standby to primary and finally performing maintenance on the old primary, which becomes the new standby

#### A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.

Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.

VPC Endpoints are not used on top of Amazon EC2 instances. They're a way to access AWS services privately within your VPC (without using the public internet).

There are two types of VPC endpoints: interface endpoints and gateway endpoints. An interface endpoint is an elastic network interface with a private IP address from the IP address range of your subnet that serves as an entry point for traffic destined to a supported service.

A gateway endpoint is a gateway that you specify as a target for a route in your route table for traffic destined to a supported AWS service. The following AWS services are supported: Amazon S3, Amazon DynamoDB

#### Amazon DynamoDB supports both interface endpoints as well as gateway endpoints. However, to use the interface endpoints, you need to connect to the given services using the private IP address, instead of creating an entry as a target in the route table of the custom VPC.

#### Spot instances are spare Amazon EC2 capacity that can save you up 90% off of On-Demand prices. Spot instances can be interrupted by Amazon EC2 for capacity requirements with a 2-minute notification

#### A Spot fleet can consist of a set of Spot Instances and optionally On-Demand Instances that are launched to meet your target capacity

#### Upgrades to the database engine level require downtime. Even if your Amazon RDS DB instance uses a Multi-AZ deployment, both the primary and standby DB instances are upgraded at the same time. This causes downtime until the upgrade is complete, and the duration of the downtime varies based on the size of your database instance.

#### Your e-commerce application is using an Amazon RDS PostgreSQL database and an analytics workload also runs on the same database. When the analytics workload is run, your e-commerce application slows down which further affects your sales.

Create a Read Replica in the same Region as the Master database and point the analytics workload there

#### An elastic IP address (EIP) can only be attached to one Amazon EC2 instance at a time

#### Create a public Network Load Balancer that links to Amazon EC2 instances that are bastion hosts managed by an Auto Scaling Group

SSH protocol is based on TCP and is layer 4.

#### Amazon S3 Select is a new Amazon S3 capability designed to pull out only the data you need from an object, which can dramatically improve the performance and reduce the cost of applications that need to access data in Amazon S3.

#### To build this index, it is necessary to read the first 250 bytes of each object in Amazon S3, which contains some metadata about the content of the file itself.

Create an application that will traverse the S3 bucket, issue a Byte Range Fetch for the first 250 bytes, and store that information in Amazon RDS

Using the Range HTTP header in a GET Object request, you can fetch a byte-range from an object, transferring only the specified portion.

#### AWS Web Application Firewall (AWS WAF) is a web application firewall that helps protect your web applications or APIs against common web exploits that may affect availability, compromise security, or consume excessive resources. AWS WAF (which has integration on top of your ALB) gives you control over how traffic reaches your applications by enabling you to create security rules that block common attack patterns, such as SQL injection or cross-site scripting, and rules that filter out specific traffic patterns you define.

#### AWS Lambda functions can be configured to run up to 15 minutes per execution. You can set the timeout to any value between 1 second and 15 minutes.

#### Change enableDnsHostnames, enableDnsSupport settings of the private hosted zones feature of Route 53 to true for custom domain for internal usage.

A private hosted zone is a container for records for a domain that you host in one or more Amazon virtual private clouds (VPCs).

#### Amazon FSx for ONTAP instance supports SMB and NFS protocols. FSx for OpenZFS does not support SMB.

#### A company is transferring a significant volume of data from on-site storage to AWS, where it will be accessed by Windows, Mac, and Linux-based Amazon EC2 instances within the same AWS region using both SMB and NFS protocols.

Set up an Amazon FSx for ONTAP instance. Configure an FSx for ONTAP file system on the root volume and migrate the data to the FSx for ONTAP volume

#### AD Connector is a directory gateway with which you can redirect directory requests to your on-premises Microsoft Active Directory without caching any information in the cloud. AD Connector is your best choice when you want to use your existing on-premises directory with compatible AWS services.

#### The instances under the ASG span two Availability Zones (AZ) within the us-east-1 region. All the incoming requests are handled by an Application Load Balancer (ALB) that routes the requests to the Amazon EC2 instances under the Auto Scaling Group. As part of a test run, two instances (instance 1 and 2, belonging to AZ A) were manually terminated by the DevOps team causing the Availability Zones (AZ) to have unbalanced resources. Later that day, another instance (belonging to AZ B) was detected as unhealthy by the Application Load Balancer's health check.

Within these AZs related to each other,
As the resources are unbalanced in the Availability Zones, Amazon EC2 Auto Scaling will compensate by rebalancing the Availability Zones. When rebalancing, Amazon EC2 Auto Scaling launches new instances before terminating the old ones, so that rebalancing does not compromise the performance or availability of your application

Within only an AZ,
Amazon EC2 Auto Scaling creates a new scaling activity for terminating the unhealthy instance and then terminates it. Later, another scaling activity launches a new instance to replace the terminated instance

#### An application running on an Amazon EC2 instance needs to access a Amazon DynamoDB table in the same AWS account.

Set up an IAM service role with the appropriate permissions to allow access to the Amazon DynamoDB table. Configure an instance profile to assign this IAM role to the Amazon EC2 instance

A service role is an IAM role that a service assumes to perform actions on your behalf. Service roles provide access only within your account and cannot be used to grant access to services in other accounts. An IAM administrator can create, modify, and delete a service role from within IAM. When you create the service role, you define the trusted entity in the definition.

#### Amazon ElastiCache for Memcached supports multi-threading architecture for caching.

#### SSE-S3 and SSE-KMS provide you with an audit trail of when your key was used and by whom. KMS is more expensive.

#### Storage class analysis only provides recommendations for Standard to Standard IA classes

By using Amazon S3 analytics Storage Class Analysis you can analyze storage access patterns to help you decide when to transition the right data to the right storage class.

#### AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery), while Global Accelerator improves performance for a wide range of applications over TCP or UDP.

#### AWS Lambda currently supports 1000 concurrent executions per AWS account per region. If your Amazon SNS message deliveries to AWS Lambda contribute to crossing these concurrency quotas, your Amazon SNS message deliveries will be throttled. You need to contact AWS support to raise the account limit.

#### By default, FIFO queues support up to 300 messages per second per batch.

#### Amazon CloudFront does not work in a Amazon Virtual Private Cloud (Amazon VPC)

#### Cost of test file storage on Amazon S3 Standard < Cost of test file storage on Amazon EFS < Cost of test file storage on Amazon EBS

#### VPC Flow Logs, DNS logs, CloudTrail Logs can be identified as data sources supported by Amazon GuardDuty.

#### A gaming company uses Amazon Aurora as its primary database service. The company has now deployed 5 multi-AZ read replicas to increase the read throughput and for use as failover target. The replicas have been assigned the following failover priority tiers and corresponding instance sizes are given in parentheses: tier-1 (16 terabytes), tier-1 (32 terabytes), tier-10 (16 terabytes), tier-15 (16 terabytes), tier-15 (32 terabytes).

Tier-1 (32-gigs)

#### Cold Hard disk drive (sc1) and Throughput Optimized Hard disk drive (st1) CANNOT be used as boot volumes while creating the instances

#### A development team wants to ensure that all objects uploaded to an Amazon S3 bucket are encrypted?

Configure the bucket policy to deny if the PutObject does not have an x-amz-server-side-encryption header set

#### Amazon SQS temporary queues gives a high-throughput request-response message pattern.

#### To run distributed and replicated workloads, partition placement groups of EC2 instances help.

#### Use the Amazon EC2 instances private IP for the affordable replication cost.

#### Increasing the IOPS on the EBS volume results in bigger space and thus, throughput.

#### Amazon EFS with Provisioned Throughput mode does not increase storage size but Bursting Throughput mode does.

#### Use Amazon CloudFront signed URLs and cookies to distribute content only to its service subscribers.

#### Provisioned IOPS SSD EBS volumes allow to set up shared data access for EC2 instances.

#### Snowmobile should be used for 10 petabytes unit.

#### Snowball is for under 10 terabytes.

#### DR strategy for monolith app

An autoscaling group that spans across 2 AZs which min=1, max=1, desired=1
Use EIP and EC2 user data script to attach
Assign an EC2 Instance Role to perform API calls

#### Create an OAI and update S3 bucket policy to let users access to S3 only through CloudFront

#### When your object size reaches 100 megabytes, you should consider using multipart uploads instead of uploading the object in a single operation.

#### Ingest the data in Amazon Kinesis Data Firehose and use an intermediary AWS Lambda function to filter and transform the incoming stream before the output is dumped on Amazon S3

#### FSx for Lustre provides the ability to both process the 'hot data' in a parallel and distributed fashion as well as easily store the 'cold data' on Amazon S3.

#### Kinesis Data Firehose cannot directly write into a DynamoDB table.

#### Kinesis Data Streams cannot directly write the output to Amazon S3 but Firehose can.

#### AWS DMS enables you to seamlessly migrate data from supported sources to relational databases, data warehouses, streaming platforms, and other data stores in AWS cloud.

Leverage AWS Database Migration Service (AWS DMS) as a bridge between Amazon S3 and Amazon Kinesis Data Streams

#### If you need to scale your AWS Site-to-Site VPN connection beyond 1.25 Gbps while managing traffic between multiple VPCs and your on-premises network, AWS Transit Gateway with ECMP is a scalable and manageable solution.

#### Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and AWS Lambda functions.

#### The S3 Glacier Instant Retrieval storage class delivers milliseconds retrieval for archives that need immediate access, such as medical images or news media assets. S3 Glacier Flexible Retrieval provides three retrieval options: expedited retrievals that typically complete in 1–5 minutes, standard retrievals that typically complete in 3–5 hours and start within minutes when initiated using S3 Batch Operations, and free bulk retrievals that return large amounts of data typically in 5–12 hours. The Amazon S3 Glacier Deep Archive storage class provides two retrieval options ranging from 12-48 hours.

If your application is composed of several individual services, an Application Load Balancer can route a request to a service based on the content of the request. Here are the different types -

Host-based Routing:

You can route a client request based on the Host field of the HTTP header allowing you to route to multiple domains from the same load balancer.

Path-based Routing:

You can route a client request based on the URL path of the HTTP header.

HTTP header-based routing:

You can route a client request based on the value of any standard or custom HTTP header.

HTTP method-based routing:

You can route a client request based on any standard or custom HTTP method.

Query string parameter-based routing:

You can route a client request based on the query string or query parameters.

Source IP address CIDR-based routing:

You can route a client request based on source IP address CIDR from where the request originates.

#### Common Port Numbers

There are 65,535 possible port numbers, although not all are in common use. Some of the most commonly used ports, along with their associated networking protocol, are:

Ports 20 and 21: File Transfer Protocol (FTP). FTP is for transferring files between a client and a server.
Port 22: Secure Shell (SSH). SSH is one of many tunneling protocols that create secure network connections.
Port 25: Historically, Simple Mail Transfer Protocol (SMTP). SMTP is used for email.
Port 53: Domain Name System (DNS). DNS is an essential process for the modern Internet; it matches human-readable domain names to machine-readable IP addresses, enabling users to load websites and applications without memorizing a long list of IP addresses.
Port 80: Hypertext Transfer Protocol (HTTP). HTTP is the protocol that makes the World Wide Web possible.
Port 123: Network Time Protocol (NTP). NTP allows computer clocks to sync with each other, a process that is essential for encryption.
Port 179: Border Gateway Protocol (BGP). BGP is essential for establishing efficient routes between the large networks that make up the Internet (these large networks are called autonomous systems). Autonomous systems use BGP to broadcast which IP addresses they control.
Port 443: HTTP Secure (HTTPS). HTTPS is the secure and encrypted version of HTTP. All HTTPS web traffic goes to port 443. Network services that use HTTPS for encryption, such as DNS over HTTPS, also connect at this port.
Port 500: Internet Security Association and Key Management Protocol (ISAKMP), which is part of the process of setting up secure IPsec connections.
Port 587: Modern, secure SMTP that uses encryption.
Port 3389: Remote Desktop Protocol (RDP). RDP enables users to remotely connect to their desktop computers from another device.
The Internet Assigned Numbers Authority (IANA) maintains the full list of port numbers and protocols assigned to them.
