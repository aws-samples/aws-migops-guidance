  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines the core IAM roles, and policies that will be used within \[Customer\] accounts by applications (monitoring systems or SaaS solutions with a pull model). This is not a definitive list and may grow as cloud adoption maturity grows. Clearly defining access requirements for automated or programmatic access reduces the risks from unnecessary privileges, aligning to the Well-Architected framework. It is also best practice to allocate unique credentials for each component to help segregation and traceability. For example, use different IAM roles for AWS Lambda functions and EC2 instances.

**Implementation**
------------------

#### IAM Roles and Polices Definition

Each IAM Role need to be defined with required automated tasks and based on those tasks the access permissions are allowed or denied with the help of IAM Policy.  An IAM Policy is a JSON formatted document that provides a list of ‘Allow’ or ‘Deny’ permissions. It consists of one or more statements, each of which describes the set of permissions. The following roles and policies will be deployed in each account.

  

| Role | Purpose | Capabilities | Trust Policy | Access Policy |
| --- | --- | --- | --- | --- |
| <Namespace>-role-azure-sentinel |   Azure Sentinel to pull CloudTrail logs           |   Pull CloudTrail logs using CloudTrail API           |                 |   AWSCloudTrailRead OnlyAccess (AWS managed policy)           |

 **Attachments:** 

