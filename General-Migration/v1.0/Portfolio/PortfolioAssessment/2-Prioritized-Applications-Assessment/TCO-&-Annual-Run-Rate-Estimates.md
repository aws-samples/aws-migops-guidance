  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Infrastructure, AWS assumptions, and tooling for TCO
====================================================

This document defines the set of assumptions that will be used by AWS Professional Services team as input into the creation of Annual Run Rate estimates for applications. There are several partner discovery tools that include financial analysis, if one of those tools are being used please follow the tool user guide. In all cases, verify that the assumptions used by the tool are correct. Customers can obtain a directional business case which includes TCO via [Migration Evaluator](https://aws.amazon.com/migration-evaluator/) tool. AWS Employees and Partners can use the [MPA tool](http://mpa-proserve.amazonaws.com/).

Working with customers, consultants need to identify broad solutions that may be applicable to each situation primarily in high impact categories such as Compute, Storage, Databases, Licensing and Networking.  These could include but not be limited to:

*   Categories of servers (such as "t" series)
*   Type of storage or storage solutions (such as EFS, Netapp Cloud Appliance, backup storage options, etc.)
*   Database options (such as AWS native solutions, RDS, etc.)
*   Licensing options (such as BYOL, RHEL to Amazon Linux, .net conversion to .net core, etc.)
*   Networking configurations (such as VPN, Direct Connect, redundancy, etc.). 

  

Some useful recommendations are listed below:

Well-Architected Guidance for Selecting Infrastructure
======================================================

Compute Solutions
-----------------

**Evaluate the available compute options**: Look at and understand the performance characteristics of the compute-related options available to you. Know how instances, containers, and functions work and what advantages, or disadvantages, they bring to your workloads.

**Understand the available compute configuration options**: Understand how various options complement your workload and which configuration options are best for your system. Examples of these options include instance family, sizes, features (GPU, I/O), function sizes, container instances, single versus multi-tenancy, and so on.

**Collect compute-related metrics**: One of the best ways to understand how your systems are performing is to record and track the true utilization of various resources. This data can then be fed back into making more accurate determinations of resource requirements.

**Determine the required configuration by right-sizing**: Analyze the various performance characteristics of your workload and how these characteristics relate to memory, network, and CPU usage. Use this data when choosing resources that best match your workload's profile. For example, a memory\-intensive workload, such as a database, could be served best by the r-family of instances, while a bursting workload may benefit more from an elastic container system such as Amazon Elastic Container Service.

**Use the available 
elasticity 
of resources**: AWS provides the flexibility to expand or reduce your resources dynamically through a variety of mechanisms (for example: [AWS Auto Scaling](https://wa.aws.amazon.com/wat.concept.awsautoscaling.en.html "A fully managed service that enables you to quickly discover the scalable AWS resources that are part of your application and configure dynamic scaling."), [Amazon Elastic Container Service](https://wa.aws.amazon.com/wat.concept.ecs.en.html "A highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containers on a cluster of EC2 instances."), and [AWS Lambda](https://wa.aws.amazon.com/wat.concept.lambda.en.html "A web service that lets you run code without provisioning or managing servers. You can run code for virtually any type of application or back-end service with zero administration. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.")) to meet changes in demand. Combined with compute-related metrics, a workload can automatically respond to these changes and utilize the optimal set of resources to achieve its goal.

**Re-evaluate compute needs based on metrics**: Use system-level metrics to identify the behavior and requirements of your workload over time. Evaluate your workload's needs by comparing the available resources with these requirements and make changes to your compute environment to best match your workload's profile. For example, over time a system may be observed to be more memory\-intensive than initially thought, so moving to a different instance family or size may improve both performance and efficiency.

Storage Solutions
-----------------

**Understand storage characteristics and requirements**: Understand the different characteristics (for example, shareable, file size, cache size, access patterns, latency, throughput, and persistence of data) that are required to select the services that best fit your workloads, such as [Amazon S3](https://wa.aws.amazon.com/wat.concept.amazonsimplestorageservice.en.html "Storage for the internet. You can use it to store and retrieve any amount of data at any time, from anywhere on the web."), [Amazon EBS](https://wa.aws.amazon.com/wat.concept.ebs.en.html "A service that provides block level storage volumes for use with EC2 instances."), [Amazon Elastic File System](https://wa.aws.amazon.com/wat.concept.efs.en.html "A file storage service for EC2instances. Amazon EFS is easy to use and provides a simple interface with which you can create and configure file systems. Amazon EFS storage capacity grows and shrinks automatically as you add and remove files.") ([Amazon EFS](https://wa.aws.amazon.com/wat.concept.efs.en.html "A file storage service for EC2instances. Amazon EFS is easy to use and provides a simple interface with which you can create and configure file systems. Amazon EFS storage capacity grows and shrinks automatically as you add and remove files.")), and [Amazon EC2 instance store](https://wa.aws.amazon.com/wat.concept.ec2-instance-store.en.html "Storage is located on disks that are physically attached to the host computer.").

**Evaluate available configuration options**: Evaluate the various characteristics and configuration options and how they relate to storage. Understand where and how to use [PIOPS](https://wa.aws.amazon.com/wat.concept.piops.en.html "For EBS volumes you can specify a consistent IOPS rate when you create the volume."), [SSDs](https://wa.aws.amazon.com/wat.concept.ssd.en.html "Solid-state drives are a storage device that uses memory to store data."), magnetic storage, [Amazon S3](https://wa.aws.amazon.com/wat.concept.amazonsimplestorageservice.en.html "Storage for the internet. You can use it to store and retrieve any amount of data at any time, from anywhere on the web."), [Amazon Glacier](https://wa.aws.amazon.com/wat.concept.glacier.en.html "A secure, durable, and low-cost storage service for data archiving and long-term backup. You can reliably store large or small amounts of data for significantly less than on-premises solutions. Amazon Glacier is optimized for infrequently accessed data, where a retrieval time of several hours is suitable."), or ephemeral storage to optimize storage space and performance for your workloads.

**Make decisions based on access patterns and metrics**: Choose storage systems and configure them by considering how the workload accesses data. Make performance improvements, such as choosing caching services or instances that best match your access patterns, utilizing optimal key distributions when storing data in Amazon S3 or DynamoDB, striping storage volumes, or partitioning data based on system measurements. Increase storage efficiency by choosing object storage, such as Amazon S3, or block storage, such as Amazon Elastic Block Store. Configure the storage options you choose to match your data access patterns.

Database Solutions
------------------

**Understand data characteristics**: Understand the different characteristics of data in your workloads. Determine if the workload requires transactions, how it interacts with data, what its performance demands are, and so on. Use this data to select the best performing database approach for your workload (for example, [relational databases](https://wa.aws.amazon.com/wat.concept.relational.en.html "A relational database is a collection of data items with pre-defined relationships between them."), [NoSQL](https://wa.aws.amazon.com/wat.concept.nosql.en.html "NoSQL databases are purpose built for specific data models and have flexible schemas for building modern applications."), [data warehouses](https://wa.aws.amazon.com/wat.concept.data-warehouse.en.html "A central repository of information that can be analyzed to make better informed decisions."), or [in-memory](https://wa.aws.amazon.com/wat.concept.in-memory.en.html "The state of being stored in volatile system RAM rather than on stable storage, such as flash or disk.") storage).

**Evaluate the available options**: Evaluate the services and storage options that are available as part of the selection process for your workload's storage mechanisms. Understand how, and when, to use a given service or system for data storage. Learn about available configuration options that can further optimize database performance or efficiency, such as PIOPs, memory and compute resources, caching, and so on.

**Collect and record database 
performance 
metrics**: Use tools, libraries, and systems that record performance measurements related to database performance. For example, measure transactions per second, slow queries, or system latency introduced when accessing the database. Use this data to understand the performance of your database systems.

**Choose data storage based on access patterns**: Use the access patterns of the workload to decide which services and technologies to use. For example, utilize a [relational database](https://wa.aws.amazon.com/wat.concept.relational.en.html "A relational database is a collection of data items with pre-defined relationships between them.") for workloads that require transactions, or a key-value store that provides higher throughput but is eventually consistent where applicable.

**Optimize data storage based on access patterns and metrics**: Use performance characteristics and access patterns that optimize how data is stored or queried to achieve the best possible performance. Measure how optimizations such as indexing, [key distribution](https://wa.aws.amazon.com/wat.concept.key-distribution.en.html "The relative probability that a given key to access data is spread out across storage."), [data warehouse](https://wa.aws.amazon.com/wat.concept.data-warehouse.en.html "A central repository of information that can be analyzed to make better informed decisions.") design, or caching strategies affect system performance or overall efficiency.

* * *

 **Attachments:** 

