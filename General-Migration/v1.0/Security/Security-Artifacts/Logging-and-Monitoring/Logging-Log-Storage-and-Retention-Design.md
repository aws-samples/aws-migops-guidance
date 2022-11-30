  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines AWS logging services which will be enabled in each AWS account and which will emit their respective logs to the consolidated logging (Log Archive) account. This document also outlines a strategy for AWS logs retention and access. Configuring service and application logging, and analyzing logs centrally follow AWS Well-Architected Framework best practices.

**Implementation**
------------------

#### **Logging Sources**

| Log Source | Description | Implementation Details | Location |
| --- | --- | --- | --- |
| [CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) | Provides event history of AWS accounts activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. |   CloudTrail will be enabled in each region for each account and will send the logs to the consolidated Log Archive account S3 bucket. Additionally, CloudTrail logs will be streamed to CloudWatch Log Groups in local accounts to ensure that application administrators can utilize them for their day-to-day operations.   |   S3 bucket (Log Archive account)  CloudWatch Log Group (local accounts)   |
| [VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) | Captures information about the IP traffic going to and from network interfaces in AWS VPCs. |   VPC Flow Logs will be enabled for VPCs in each account and will send network logs to the consolidated Log Archive account S3 bucket. Additionally, VPC Flow Logs will be streamed to CloudWatch Log Groups in local accounts to ensure that application administrators can utilize them for their day-to-day operations.   |   S3 bucket (Log Archive account)  CloudWatch Log Group (local accounts)   |
| [Config](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html) | Continuously monitors and records AWS resources configurations and allows to automate the evaluation of recorded configurations against desired configurations. |   Config will be enabled in each account and will send configuration history logs to the consolidated Log Archive account S3 bucket. Additionally, configuration history will be accessible through the local and Log Archive account Config Console/API.    |   S3 bucket (Log Archive account)  Config Console (local accounts)   |

Other logging sources may optionally include the following logs based on an account provisioning configuration and workload specifics:

*   AWS services logs (e.g. ALB logs);
*   Operating system logs;
*   Application logs (e.g. authentication logs, firewall logs).

#### Logs **Retention Policy**

| Storage Type | Transition | Expiration |
| --- | --- | --- |
| S3 bucket (Log Archive account) |   Transition to Glacier after 90 days after the creation of an object   | Expire after 365 days after the creation of an object |
| CloudWatch Log Group (local accounts) | N/A | Expire after 30 days |

#### Logs Storage Security Controls

S3 bucket located in the Log Archive account will be used to consolidate logs from all member accounts. This bucket will have the following security controls enabled:

1.  S3 server-side encryption (SSE-S3) with the industry standard AES-256 encryption algorithm - to encrypt all log files.
2.  S3 service access logging - to track requests for access to logs files.
3.  Versioning - to recover objects from accidental deletion or overwrites.
4.  Bucket Policy – to only allow logging services to upload objects to the bucket.

Access to the Log Archive account and the S3 bucket will be regulated by the federated IAM Roles. Additionally, cross-account IAM Roles can be used to access the bucket from the Audit account. IAM Roles mapping can found here (link to IAM Roles and Policies Design artifact).

#### Pricing Information

1.  [AWS CloudTrail](https://aws.amazon.com/cloudtrail/pricing/)
2.  [AWS Config](https://aws.amazon.com/config/pricing)
3.  [AWS VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html)
4.  [AWS S3](https://aws.amazon.com/s3/pricing/)
5.  [AWS CloudWatch](https://aws.amazon.com/cloudwatch/pricing)

 **Attachments:** 

