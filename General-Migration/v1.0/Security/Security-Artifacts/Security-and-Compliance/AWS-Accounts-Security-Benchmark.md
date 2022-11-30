  

  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

  

This document provides prescriptive guidance for configuring security options for a subset of Amazon Web Services with an emphasis on foundational, testable, and architecture agnostic settings.

**Implementation**
------------------

#### Security Framework

CIS Amazon Web Services Foundations Benchmark will be utilized to define implementation details of the security controls for fortifying AWS accounts and AWS environment foundational architecture security. Deployment of the controls will be performed using IaaC for ease of documentation and configuration consistency through AWS accounts vending machine and accounts baselining for all newly created AWS accounts.

#### Security Controls Implementation

| Category | CIS Requirement | General Applicability | Valid Exceptions | Exceptions Handling | Implementation | NIST 800-53 Control |
| --- | --- | --- | --- | --- | --- | --- |
| IAM | 1.1 Avoid the use of the "root" account (Scored) | Y |     |     | link to Authentication: Root Credentials Management Design |     |
| IAM | 1.2 Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a password (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.3 Ensure credentials unused for 90 days or greater are disabled (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.4 Ensure access keys are rotated every 90 days or less (Scored) | N |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.5 Ensure IAM password policy requires at least one uppercase letter (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.6 Ensure IAM password policy require at least one lowercase letter (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.7 Ensure IAM password policy require at least one symbol (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.8 Ensure IAM password policy require at least one number (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.9 Ensure IAM password policy requires minimum length of 14 or greater (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.10 Ensure IAM password policy prevents password reuse (Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.11 Ensure IAM password policy expires passwords within 90 days or less (Scored) | N |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.12 Ensure no root account access key exists (Scored) | Y |     |     | Authentication: Root Credentials Management Design |     |
| IAM | 1.13 Ensure  MFA is enabled for the "root" account (Scored) | Y |     |     | Authentication: Root Credentials Management Design |     |
| IAM | 1.14 Ensure hardware MFA is enabled for the "root" account (Scored) | Y |     |     | Authentication: Root Credentials Management Design |     |
| IAM | 1.15 Ensure security questions are registered in the AWS account (Not Scored) | Y |     |     | Authentication: Root Credentials Management Design |     |
| IAM | 1.16 Ensure IAM policies are attached only to groups or roles (Scored) | Y |     |     | Authorization: Users IAM Roles and Policies Design |     |
| IAM | 1.17 Maintain Current contact details (Not Scored) | Y |     |     | Landing Zone Account Design |     |
| IAM | 1.18 Ensure Security contact information is registered (Not Scored) | Y |     |     | Landing Zone Account Design |     |
| IAM | 1.19 Ensure IAM instance roles are used for AWS resource access from instances (Not Scored) | Y |     |     | Authorization: Applications IAM Roles and Policies Design |     |
| IAM | 1.20 Ensure a support role has been created to manage incidents with AWS Support (Scored) | N |     |     | Authorization: Users IAM Roles and Policies Design |     |
| IAM | 1.21 Do not setup access keys during initial user setup for all IAM users that have a console password (Not Scored) | Y |     |     | Authentication: IAM Users Credentials Management Design |     |
| IAM | 1.22 Ensure IAM policies that allow full "\*:\*" administrative privileges are not created (Scored) | N |     | Archive | Authentication: IAM Users Credentials Management Design |     |
| Logging | 2.1 Ensure CloudTrail is enabled in all regions (Scored) | Y |     |     | Logging: Log Storage and Retention Design |     |
| Logging | 2.2 Ensure CloudTrail log file validation is enabled (Scored) | Y |     |     | Logging: Log Storage and Retention Design |     |
| Logging | 2.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible (Scored) | Y |     |     | Logging: Log Storage and Retention Design |     |
| Logging | 2.4 Ensure CloudTrail trails are integrated with CloudWatch Logs (Scored) | Y |     |     | Monitoring: Security Monitoring Design |     |
| Logging | 2.5 Ensure AWS Config is enabled in all regions (Scored) | Y |     |     | Logging: Log Storage and Retention Design |     |
| Logging | 2.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket (Scored) | Y |     |     | Logging: Log Storage and Retention Design |     |
| Logging | 2.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs (Scored) | Y |     | Disable | Logging: Log Storage and Retention Design |     |
| Logging | 2.8 Ensure rotation for customer created CMKs is enabled (Scored) | Y |     |     | Logging: Log Storage and Retention Design |     |
| Logging | 2.9 Ensure VPC flow logging is enabled in all VPCs (Scored)  | Y |     |     | Logging: Log Storage and Retention Design |     |
| Monitoring | 3.1 Ensure a log metric filter and alarm exist for unauthorized API calls (Scored) | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.2 Ensure a log metric filter and alarm exist for Management Console sign-in without MFA (Scored) | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.3 Ensure a log metric filter and alarm exist for usage of "root" account  (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.4 Ensure a log metric filter and alarm exist for IAM policy changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.6 Ensure a log metric filter and alarm exist for AWS Management Console authentication failures (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.10 Ensure a log metric filter and alarm exist for security group changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.11 Ensure a log metric filter and alarm exist for changes to Network Access Control Lists (NACL) (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.12 Ensure a log metric filter and alarm exist for changes to network gateways (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.13 Ensure a log metric filter and alarm exist for route table changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Monitoring | 3.14 Ensure a log metric filter and alarm exist for VPC changes (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Networking | 4.1 Ensure no security groups allow ingress from 0.0.0.0/0 to port 22 (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Networking | 4.2 Ensure no security groups allow ingress from 0.0.0.0/0 to port 3389 (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Networking | 4.3 Ensure the default security group of every VPC restricts all traffic (Scored)  | Y |     |     | Monitoring: Detective Controls Design |     |
| Networking | 4.4 Ensure routing tables for VPC peering are "least access" (Not Scored) | N |     |     | Monitoring: Detective Controls Design |     |

  

#### Security Controls and Compliance Validation

The following mechanisms will be utilized for continuous validation of alignment with the CIS Amazon Web Services Foundations Benchmark.

*   *   "CIS AWS Foundations Benchmark" Compliance Standard Controls - AWS SecurityHub console
    *   Custom Detective Controls - AWS Config Aggregator console
    *   [Prowler](https://github.com/toniblyx/prowler)

The following CIS Benchmark checks are not supported by Security Hub and therefore will have to be manually validated: [https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-cis-checks-not-supported.html](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-cis-checks-not-supported.html)

 **Attachments:** 

