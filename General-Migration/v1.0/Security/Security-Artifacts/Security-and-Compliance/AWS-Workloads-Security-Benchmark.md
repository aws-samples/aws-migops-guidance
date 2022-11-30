  

  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

  

This document provides prescriptive guidance for establishing a secure operational posture for workloads deployed to the Amazon Web Services environment.

**Implementation**
------------------

#### Security Framework

AWS Foundational Security Best Practices Benchmark will be utilized to define implementation details of the security controls for fortifying application security in the AWS cloud. The implementation of the controls will be tracked via backlog created for each application to be migrated or created on AWS. Deployment of the controls will be performed using IaaC for ease of documentation and configuration consistency.

Security Controls Implementation

| Category | Subcategory | Security Best Practices controls | General Applicability | Valid Exceptions | Exception Handling | Notes | Implementation |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Identify | Inventory | \[Config.1\] AWS Config should be enabled | Y |     |     |     | Logging: Log Storage and Retention Design |
| Identify | Inventory |   \[SSM.1\] EC2 instances should be managed by AWS Systems Manager   | Y |     |     |     | Compute Resource Protection Design |
| Identify | Logging |   \[CloudTrail.1\] CloudTrail should be enabled and configured with at least one multi-Region trail   | Y |     |     |     | Logging: Log Storage and Retention Design |
| Protect | Data Protection | \[ACM.1\] Imported ACM certificates should be renewed within 90 days of expiration | Y |     |     |     | Encryption In Transit Design |
| Protect | Data Protection |   \[CloudTrail.2\] CloudTrail should have encryption at-rest enabled   | N |     | Disable SecHub control | Using SSE- S3 to save on cost | Logging: Log Storage and Retention Design |
| Protect | Data Protection |   \[EC2.3\] Attached EBS volumes should be encrypted at-rest   | Y |     |     |     | Encryption At Rest Design |
| Protect | Data Protection |   \[EFS.1\] Amazon EFS should be configured to encrypt file data at-rest using AWS KMS   | Y |     |     |     | Encryption At Rest Design |
| Protect | Data Protection |   \[ELBv2.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS   | Y |     |     |     | Encryption At Rest Design |
| Protect | Data Protection |   \[ES.1\] Elasticsearch domains should have encryption at-rest enabled   | Y |     |     |     | Encryption At Rest Design |
| Protect | Data Protection |   \[RDS.3\] RDS DB instances should have encryption at-rest enabled   | Y |     |     |     | Encryption At Rest Design |
| Protect | Data Protection |   \[S3.4\] S3 buckets should have server-side encryption enabled   | Y |     |     |     | Encryption At Rest Design |
| Protect | Secure Development  |   \[CodeBuild.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth   | Y |     |     |     |     |
| Protect | Secure Development  |   \[CodeBuild.2\] CodeBuild project environment variables should not contain clear text credentials   | Y |     |     |     |     |
| Protect | Secure Development  |   \[Lambda.2\] Lambda functions should use latest runtimes   | Y |     |     |     |     |
| Protect | Secure network configuration |   \[EC2.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone   | Y |     |     |     |     |
| Protect | Secure network configuration |   \[EC2.2\] The VPC default security group should not allow inbound and outbound traffic   | Y |     |     |     | Security Groups and NACLs Design |
| Protect | Secure network configuration | \[Lambda.1\] Lambda functions should prohibit public access by other accounts | Y |     |     |     |     |
| Protect | Secure network configuration | \[RDS.1\] RDS snapshots should be private | Y |     |     |     |     |
| Protect | Secure network configuration | \[RDS.2\] RDS DB instances should prohibit public access, determined by the PubliclyAccessible configuration | Y |     |     |     |     |
| Protect | Secure network configuration | \[S3.1\] S3 Block Public Access setting should be enabled | Y | static website hosting | Archive finding |     |     |
| Protect | Secure network configuration | \[S3.3\] S3 buckets should prohibit public write access | Y |     |     |     |     |
| Protect | Secure network configuration | \[S3.2\] S3 buckets should prohibit public read access | Y | static website hosting | Archive finding |     |     |
| Protect | Secure access management | \[IAM.1\] IAM policies should not allow full "\*" administrative privileges | Y |     |     |     | Authorization: Human IAM Roles and Policies Design |
| Protect | Secure access management | \[IAM.2\] IAM users should not have IAM policies attached | Y |     |     |     | Authentication: IAM Users Credentials Management Design |
| Protect | Secure access management | \[IAM.3\] IAM users access keys should be rotated every 90 days or less | Y |     |     |     | Authentication: IAM Users Credentials Management Design |
| Protect | Secure access management | \[IAM.4\] IAM root user access key should not exist | Y |     |     |     | Authentication: Root Credentials Management Design |
| Protect | Secure access management | \[IAM.5\] MFA should be enabled for all IAM users that have a console password | Y |     |     |     | Authentication: IAM Users Credentials Management Design |
| Protect | Secure access management | \[IAM.6\] Hardware MFA should be enabled for the root user | Y |     |     |     | Authentication: Root Credentials Management Design |
| Protect | Secure access management | \[IAM.7\] Password policies for IAM users should have strong configurations | Y |     |     |     | Authentication: IAM Users Credentials Management Design |
| Detect | Detection services | \[GuardDuty.1\] GuardDuty should be enabled | Y |     |     |     | Monitoring: Security Monitoring Design |
| Detect | Detection services | \[SSM.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements | Y |     |     |     | Patch Management Design |

#### Security Controls and Compliance Validation

The following mechanisms will be utilizing for continuous validation of alignment with the 
AWS 
Foundational Security Best Practices Benchmark.

*   SecurityHub "AWS Foundational Security Best Practices" security standard
*   [Prowler](https://github.com/toniblyx/prowler)

#### Data Classification Validation

Classification provides a way to categorize data, based on levels of sensitivity, to help you determine appropriate protective and retention controls. The following Well-Architected best practices can help you achieve this:

Define data classification requirements: Define data classification requirements to meet your organizational, legal, and compliance requirements.

*   Identify AWS compliance resources, including [AWS cloud compliance](https://aws.amazon.com/compliance/?ref=wellarchitected) to assist.
*   Define your data identification and classification schema- identification and classification of your data is performed to assess the potential impact and type of data your store, and who can access it.

Define data protection controls: Protect data according to its classification level; for example, secure publicly accessible data by using best practices while protecting sensitive data with additional controls.

Implement data identification and classification: Classify data with easily identifiable indicators; for example, use tags for Amazon S3 buckets and objects that classify the data in the buckets.

Automate identification and classification: Automate identification and classification of data to reduce the risk of human error.

Identify the types of data: Be aware of the types of data in your various workload to help you implement controls to meet organizational, legal, and compliance requirements.

 **Attachments:** 

