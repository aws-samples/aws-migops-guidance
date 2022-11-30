  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines details about detective controls which will be enabled in AWS accounts.

**Implementation**
------------------

#### Control Tower Mandatory Config Rules

|   **Config Rule**   |   **Organizational Unit (OU)**    |   **Description**   |   **Implementation Details**   |
| --- | --- | --- | --- |
|   **Disallow public read access to log archive**    |   Core OU (mandatory)   |   Checks that your log archive's S3 bucket does not allow public read access. If an S3 bucket policy or bucket ACL allows public read access, the bucket is noncompliant. Rule will run on configuration change.   |   ControlTower (Config Rule)   |
|   **Disallow public write access to log archive**   |   Core OU (mandatory)   |   Checks that your log archive's S3 bucket does not allow public write access. If an S3 bucket policy or bucket ACL allows public write access, the bucket is noncompliant. Rule will run on configuration change.   |   ControlTower (Config Rule)   |

  

#### Additional AWS Config Rules 

  

NotVisibletoControlTower

Custom Config Rules compliance status is not trackable by Control Tower but is viewable in the AWS Config Aggregator dashboard.

  

| **Config Rule** | **Organizational Unit (OU)**  | **Description** | **Implementation **Details**** |
| --- | --- | --- | --- |
| CIS AWS Foundations Benchmark |  |  |  |
| CIS 1.1 Avoid the use of the "root" account (Scored) | All | Detects usage of Root account. Rule will run periodically (every 12 hours). | SecurityHub CIS (native) |
| CIS 1.2 Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a password (Scored) | All | Checks whether AWS Multi-Factor Authentication (MFA) is enabled for all AWS Identity and Access Management (IAM) users that use a console password. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
| CIS 1.3 Ensure credentials unused for 90 days or greater are disabled (Scored) | All |   Checks whether the account password policy for IAM users meets the specified requirements. Rule will run periodically (every 12 hours).  \*Exception: BreakGlass   | SecurityHub CIS (Config Rule) |
| CIS 1.4 Ensure access keys are rotated every 90 days or less (Scored) |   All   |   Checks whether the account password policy for IAM users meets the specified requirements. Rule will run periodically (every 12 hours).   |   SecurityHub CIS (Config Rule)   |
| CIS 1.12 Ensure no root account access key exists (Scored) |   All   |   Checks whether the root user access key is available. The rule is compliant if the user access key does not exist. Rule will run periodically (every 12 hours).   |   SecurityHub CIS (Config Rule)   |
| CIS 1.13 Ensure  MFA is enabled for the "root" account (Scored) |   All    |   Checks whether the root user of your AWS account requires multi-factor authentication for console sign-in. Rule will run periodically (every 12 hours).   |   SecurityHub CIS (Config Rule)   |
| CIS 1.14 Ensure hardware MFA is enabled for the "root" account (Scored) |   All   |   Checks whether your AWS account is enabled to use multi-factor authentication (MFA) hardware device to sign in with root credentials. Rule will run periodically (every 12 hours).   |   SecurityHub CIS (Config Rule)   |
| CIS 1.16 Ensure IAM policies are attached only to groups or roles (Scored) |   All   | Checks whether IAM polices are attached to IAM Groups for granting permissions to IAM Users. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
| CIS 1.22 Ensure IAM policies that allow full "\*:\*" administrative privileges are not created (Scored) | All |   Checks  whether IAM policies allow full administrative privileges and whether the policies follow the principle of least privilege.Rule is triggered on configuration change.  \*Exception   | SecurityHub CIS (Config Rule) |
| CIS 2.1 Ensure CloudTrail is enabled in all regions (Scored) |   All   |   Checks whether AWS CloudTrail is enabled in your AWS account. Rule will run periodically (every 12 hours).   |   SecurityHub CIS (Config Rule)   |
| CIS 2.2 Ensure CloudTrail log file validation is enabled (Scored) | All | Checks whether CloudTrail log file validation is enabled. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
| CIS 2.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible (Scored) | All | Checks whether any S3 bucket is publicly accessible(read and write). Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
| CIS 2.4 Ensure CloudTrail trails are integrated with CloudWatch Logs (Scored) | All | Checks whether CloudTrail trails are integrated with CloudWatch Logs. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
| CIS 2.5 Ensure AWS Config is enabled in all regions (Scored) | All | Checks whether AWS Config is enabled in all regions. Rule will run periodically (every 12 hours). | SecurityHub CIS (native) |
| CIS 2.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket (Scored) | All | Checks whether S3 bucket access logging is enabled on the CloudTrail S3 bucket. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
| CIS 2.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs (Scored) | All |   Checks whether CloudTrail logs are encrypted at rest using KMS CMKs. Rule will run periodically (every 12 hours).  \*Exception   | SecurityHub CIS (Config Rule) |
| CIS 2.8 Ensure rotation for customer created CMKs is enabled (Scored) | All | Checks whether rotation for customer created CMKs is enabled. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
| CIS 2.9 Ensure VPC flow logging is enabled in all VPCs (Scored)  |   All   |   Checks whether Amazon Virtual Private Cloud flow logs are found and enabled for Amazon VPC. Rule will run periodically (every 12 hours).   |   SecurityHub CIS (Config Rule)   |
| CIS 4.1 Ensure no security groups allow ingress from 0.0.0.0/0 to port 22 (Scored)  |   All   |   Checks whether security groups that are in use disallow unrestricted incoming SSH traffic. Rule is triggered on configuration change.   |   SecurityHub CIS (Config Rule)   |
| CIS 4.2 Ensure no security groups allow ingress from 0.0.0.0/0 to port 3389 (Scored)  |   All   |   Checks whether security groups that are in use disallow unrestricted incoming RDP traffic. Rule is triggered on configuration change.   |   SecurityHub CIS (Config Rule)   |
| CIS 4.3 Ensure the default security group of every VPC restricts all traffic (Scored)  | All | Checks whether the default security group of every VPC restricts all traffic. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   **AWS Foundational Security Best Practices**   |  |  |  |
|   \[ACM.1\] Imported ACM certificates should be renewed within 90 days of expiration   | All | Checks whether ACM certificates in your account are marked for expiration within 90 days. Rule is triggered on configuration change and periodically. | SecurityHub CIS (Config Rule) |
| \[CloudTrail.1\] CloudTrail should be enabled and configured with at least one multi-Region trail |     |   Implemented by CIS 2.1 Ensure CloudTrail is enabled in all regions (Scored)       |     |
|   \[CloudTrail.2\] CloudTrail should have encryption at-rest enabled   |     |   Implemented by CIS 2.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs (Scored)       |     |
| \[CodeBuild.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth | All | Checks whether the GitHub or Bitbucket source repository URL contains either personal access tokens or a user name and password. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
| \[CodeBuild.2\] CodeBuild project environment variables should not contain clear text credentials | All | Checks whether the project contains the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
| \[Config.1\] AWS Config should be enabled |     |   Implemented by CIS 2.5 Ensure AWS Config is enabled in all regions (Scored)       |     |
| \[EC2.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone | All | Checks that Amazon Elastic Block Store snapshots are not public, determined by the ability to be restorable by anyone. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
|   \[EC2.2\] The VPC default security group should not allow inbound and outbound traffic   |     |   Implemented by CIS 4.3 Ensure the default security group of every VPC restricts all traffic (Scored)        |     |
|   \[EC2.3\] Attached EBS volumes should be encrypted at-rest   | All | Checks whether the EBS volumes that are in an attached state are encrypted.  Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[EFS.1\] Amazon EFS should be configured to encrypt file data at-rest using AWS KMS   | All | Checks whether Amazon Elastic File System is configured to encrypt the file data using AWS KMS.  Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
|   \[ELBv2.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS   | All | Checks whether HTTP to HTTPS redirection is configured on all HTTP listeners of Application Load Balancers.  Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
|   \[ES.1\] Elasticsearch domains should have encryption at-rest enabled   | All | Checks whether Amazon Elasticsearch Service (Amazon ES) domains have encryption at rest configuration enabled.  Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
|   \[GuardDuty.1\] GuardDuty should be enabled   | All | Checks whether Amazon GuardDuty is enabled in your GuardDuty account and Region. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
|   \[IAM.1\] IAM policies should not allow full "\*" administrative privileges   |     |   Implemented by CIS 1.22 Ensure IAM policies that allow full "\*:\*" administrative privileges are not created (Scored)       |     |
|   \[IAM.2\] IAM users should not have IAM policies attached   |     |   Implemented by CIS 1.16 Ensure IAM policies are attached only to groups or roles (Scored)       |     |
|   \[IAM.3\] IAM users access keys should be rotated every 90 days or less   |     |   Implemented by CIS 1.4 Ensure access keys are rotated every 90 days or less (Scored)       |     |
|   \[IAM.4\] IAM root user access key should not exist   |     |   Implemented by CIS 1.12 Ensure no root account access key exists (Scored)       |     |
|   \[IAM.5\] MFA should be enabled for all IAM users that have a console password   |         |   Implemented by CIS 1.2 Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a password (Scored)       |     |
|   \[IAM.6\] Hardware MFA should be enabled for the root user   |     |   Implemented by CIS 1.14 Ensure hardware MFA is enabled for the "root" account (Scored)       |     |
|   \[IAM.7\] Password policies for IAM users should have strong configurations   | All | Checks whether the account password policy for IAM users uses the recommended configurations. Rule will run periodically (every 12 hours). | SecurityHub CIS (Config Rule) |
|   \[Lambda.1\] Lambda functions should prohibit public access by other accounts   | All | Checks whether the Lambda function resource-based policy prohibits public access outside of your account. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[Lambda.2\] Lambda functions should use latest runtimes   | All | Checks that the Lambda function settings for runtimes match the expected values set for the latest runtimes for each supported language. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[RDS.1\] RDS snapshots should be private   | All | Checks whether RDS snapshots are public. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[RDS.2\] RDS DB instances should prohibit public access, determined by the PubliclyAccessible configuration   | All | Checks whether RDS instances are publicly accessible by evaluating the`PubliclyAccessible`field in the instance configuration item. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[RDS.3\] RDS DB instances should have encryption at-rest enabled   | All | Checks whether storage encryption is enabled for your RDS DB instances. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[S3.1\] S3 Block Public Access setting should be enabled   | All |   Checks whether S3 Block Public Access is configured at the account level. Rule is triggered on configuration change.   | SecurityHub CIS (Config Rule) |
|   \[S3.2\] S3 buckets should prohibit public read access   |     |   Implemented by CIS 2.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible (Scored)       |     |
|   \[S3.3\] S3 buckets should prohibit public write access   |     |   Implemented by CIS 2.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible (Scored)       |     |
|   \[S3.4\] S3 buckets should have server-side encryption enabled   | All | Checks that your S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put-object requests without server side encryption. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[SSM.1\] EC2 instances should be managed by AWS Systems Manager   | All | Checks whether the EC2 instances in your account are managed by AWS Systems Manager. Systems Manager is an AWS service that you can use to view and control your AWS infrastructure. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
|   \[SSM.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements   | All | Checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is `COMPLIANT` or `NON_COMPLIANT` after the patch installation on the instance. Rule is triggered on configuration change. | SecurityHub CIS (Config Rule) |
| Custom |  |  |  |
| Ensure resources are tagged with required tags | All | Checks whether your resources have the tags that you specify. Rule is triggered on configuration change. | StackSets (Config Rule) |
|     |     |     |     |
|     |     |     |     |
| Ozone (This section is applicable to Ozone implementation only) |  |  |  |
| AMSCheckSGManagementPorts | All | Checks that AWS Security Groups do not allow unrestricted incoming TCP traffic to ports 3389, 5985, or 5986 (Windows RDP and management ports). Rule is triggered on configuration change. | Ozone |
| [AMSCheckGuardDutyEnabled](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html) | All | Checks that AWS GuardDuty is enabled on the AWS Account. Rule is triggered on configuration change. | Ozone |
| AMSCheckIAMUsersPasswords | All | Checks that no IAM users have passwords (A user with a password would not be using your federated identity system). Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckEC2InstanceSSHKeysAll | All | Checks that no EC2 Instances have key pairs (An EC2 instance with a key pair would allow for access outside of the AMS Access Management System).  Rule is triggered on configuration change. | Ozone |
| AMSCheckSGLaunchWizard | All | Checks that no Security Groups were created using the AWS Launch Wizard (A Security Group created using the Launch Wizard would have been created outside of the AMS Change Management System).  Rule is triggered on configuration change. | Ozone |
| AMSCheckIAMOnboardingRole | All | Checks that the AMS Onboarding IAM role is no longer present in your AWS Account.  Rule is triggered on configuration change. | Ozone |
| AMSCheckCloudTrailMultiRegion | All | Checks that AWS CloudTrail is enabled for all AWS Regions in your AWS Account. Rule will run periodically (every 24 hours). | Ozone |
| [AMSCheckCloudTrailLogValidation](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html) | All | Checks that AWS CloudTrail log file validation is enabled in your AWS Account. Rule will run periodically (every 24 hours). | Ozone |
| [AMSCheckCloudTrailCloudWatchLogs](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html) | All | Checks that AWS CloudTrail trails are integrated with CloudWatch Logs in your AWS Account.  Rule will run periodically (every 24 hours). | Ozone |
| [AMSCheckCloudTrailEncryption](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html) | All | Checks that AWS CloudTrail logs are encrypted at rest using KMS Customer Master Keys in your AWS Account. Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckEBSVolumesEncrypted | All | Checks that EBS volumes are encrypted. Rule is triggered on configuration change. | Ozone |
| AMSCheckPublicAMIs | All | Checks that no AWS EC2 Amazon Machine Images are shared publically with All AWS Accounts from within your AWS Account. Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckIAMGroups | All | Checks that there are no AWS IAM Groups within your AWS Account. Rule is triggered on configuration change. | Ozone |
| [AMSCheckPublicRDSInstances](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html) | All | Checks that there are no AWS RDS Instances that are exposed to the public internet (Publically exposed RDS instances are against AWS Security Practices). Rule is triggered on configuration change. | Ozone |
| AMSCheckRDSUnencryptedSnapshots | All | Checks that there are no AWS RDS Snapshots that are unencrypted within your AWS Account. Rule is triggered on configuration change. | Ozone |
| AMSCheckUnencryptedSQSQueues | All | Checks that there are no AWS SQS Queues that are unencrypted within your AWS Account. Rule will run periodically (every 24 hours). | Ozone |
| [AMSCheckVPCFlowLogs](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html) | All | Checks that AWS VPC Flow Logging is enabled on VPCs in your AWS Account. Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckElastiCacheAMSSecurityGroup | All | Checks that AWS Elasticache clusters do not have AMS Security Groups. Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckAMSMandatoryTags | All | Checks that mandatory AMS tags are present on applicable AWS resources. Rule is triggered on configuration change. | Ozone |
| AMSCheckMMSTopic | All | Checks MMS topic exist and has a subscription. Rule will run periodically (every 1 hour). | Ozone |
| AMSCheckCorrectCoreStacks | All | Checks that multi-account landing zone Core accounts have the correct Cloud Formation stacks present. Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckKMSKeyPolicy | All | Checks if the KMS key policy gets modified. Rule will run periodically (every 1 hour). | Ozone |
| AMSCheckIAMUserMfaEnable | All | Checks whether AWS Multi-Factor Authentication (MFA) is enabled for all AWS Identity and Access Management (IAM) users that use a console password. Rule will run periodically (every 24 hours). | Ozone |
| AMSCheckSSMAgentHealth | All | Checks if SSM agent is successfully communicating to SSM service. Rule will run periodically (every 24 hours).  | Ozone |
| AMSCheckS3PublicWrite | All | Checks that your S3 buckets do not allow public write access. Rule is triggered on configuration change. | Ozone |
| AMSCheckS3PublicRead | All | Checks that your S3 buckets do not allow public read access. Rule is triggered on configuration change.  | Ozone |
| AMSCheckIAMRootKeys | All | Checks whether users of your AWS account require a multi-factor authentication (MFA) device to sign in with root credentials. Rule will run periodically (every 24 hours).  | Ozone |
| [AMSCheckIAMPasswordPolicy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) | All | Checks whether the account password policy for IAM users meets the specified requirements. Rule will run periodically (every 24 hours).  | Ozone |
| [AMSCheckRDSEncryption](https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html) | All | Checks whether storage encryption is enabled for your RDS DB instances. Rule is triggered on configuration change.  | Ozone |
| [AMSCheckS3ServerSideEncryption](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html) | All | Checks for explicit denies on put-object requests without server side encryption. Rule is triggered on configuration change.   | Ozone |
| AMSCheckSGCommonPorts | All | Checks that AWS Security Groups do not allow unrestricted incoming TCP traffic to ports 20, 21, 3306, 3389, 4333, 5985, or 5986. | Ozone |
| [AMSCheckSGRestrictedSSHRule](https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html) | All | Checks whether the incoming SSH traffic for the security groups is accessible. The rule is COMPLIANT when IP addresses of the incoming SSH traffic in the security groups are restricted. This rule applies only to IPv4. Rule is triggered on configuration change.  | Ozone |

  

#### CloudWatch Alarms

|   **CloudWatch Alarm**   | **Organizational Unit (OU)** | **Description** | **Implementation Details** |
| --- | --- | --- | --- |
| CIS AWS Foundations Benchmark |  |  |  |
| CIS 3.1 Ensure a log metric filter and alarm exist for unauthorized API calls (Scored) | All | Monitor unauthorized API calls which will help reveal application errors and may reduce time to detect malicious activity. | StackSets (CloudWatch Alarm) |
| CIS 3.2 Ensure a log metric filter and alarm exist for Management Console sign-in without MFA (Scored) | All | Monitor for single-factor console logins. This will increase visibility into accounts that are not protected by MFA. | StackSets (CloudWatch Alarm) |
| CIS 3.3 Ensure a log metric filter and alarm exist for usage of "root" account  (Scored)  | All | Monitor for root account logins which will provide visibility into the use of a fully privileged account and an opportunity to reduce the use of it. | StackSets (CloudWatch Alarm) |
| CIS 3.4 Ensure a log metric filter and alarm exist for IAM policy changes (Scored)  | All | Monitor changes to IAM policies which will help ensure authentication and authorization controls remain intact. | StackSets (CloudWatch Alarm) |
| CIS 3.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes (Scored)  | All | Monitor changes to CloudTrail's configuration which will help ensure sustained visibility to activities performed in the AWS account. | StackSets (CloudWatch Alarm) |
| CIS 3.6 Ensure a log metric filter and alarm exist for AWS Management Console authentication failures (Scored)  | All | Monitor failed console logins. This may decrease lead time to detect an attempt to brute force a credential, which may provide an indicator, such as source IP, that can be used in other event correlation. | StackSets (CloudWatch Alarm) |
| CIS 3.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs (Scored)  | All | Monitor deletion or disabling of CMKs. Data encrypted with disabled or deleted keys will no longer be accessible. | StackSets (CloudWatch Alarm) |
| CIS 3.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes (Scored)  | All | Monitor changes to S3 bucket policies to reduce time to detect and correct permissive policies on sensitive S3 buckets. | StackSets (CloudWatch Alarm) |
| CIS 3.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes (Scored)  | All | Monitor changes to AWS Config configuration which will help ensure sustained visibility of configuration items within the AWS account. | StackSets (CloudWatch Alarm) |
| CIS 3.10 Ensure a log metric filter and alarm exist for security group changes (Scored)  | All | Monitor changes to security group which will help ensure that resources and services are not unintentionally exposed. | StackSets (CloudWatch Alarm) |
| CIS 3.11 Ensure a log metric filter and alarm exist for changes to Network Access Control Lists (NACL) (Scored)  | All | Monitor changes to NACLs to help ensure that AWS resources and services are not unintentionally exposed. | StackSets (CloudWatch Alarm) |
| CIS 3.12 Ensure a log metric filter and alarm exist for changes to network gateways (Scored)  | All | Monitor changes to network gateways which will help ensure that all ingress/egress traffic traverses the VPC border via a controlled path.       | StackSets (CloudWatch Alarm) |
| CIS 3.13 Ensure a log metric filter and alarm exist for route table changes (Scored)  | All | Monitor changes to route tables which will help ensure that all VPC traffic flows through an expected path. | StackSets (CloudWatch Alarm) |
| CIS 3.14 Ensure a log metric filter and alarm exist for VPC changes (Scored)  | All | Monitor changes to VPC configuration which will help ensure that all VPCs remain intact. | StackSets (CloudWatch Alarm) |
| Custom |  |  |  |
|   Ensure a log metric filter and alarm exist for using customer created CMKs which is in Pending Deletion state   | All | Monitors usage of CMKs which are in Pending Deletion state. | StackSets (CloudWatch Alarm) |
|     |     |     |     |

  

#### CloudWatch Events

|   **CloudWatch Event**   |   **Organizational Unit (OU)**    |   **Description**   |   **Implementation Details**   |
| --- | --- | --- | --- |
| ControlTower Mandatory |  |  |  |
|   Config Rules Compliance Status (mandatory)   | All | Notifies about changes in Config Rule compliance status. | ControlTower (CloudWatch Event) |
| Custom |  |  |  |
| **SecurityHub Findings** | Audit account | Notifies about SecurityHub Findings. | StackSets (CloudWatch Event) |
| Trusted Advisor Exposed Keys | All | Checks popular code repositories for access keys that have been exposed to the public.  | StackSets (CloudWatch Event) |
| **Break The Glass user sign-in** | Master account | Notifies about the usage of Break The Glass user. | StackSets (CloudWatch Event) |
| Account creation | Master account | Notifies about account creation  | StackSets (CloudWatch Event) |
| SCP changes | Master account | Notifies if an SCP is modified, attached, detached, or deleted | StackSets (CloudWatch Event) |

  

  

Additional security alerts deployed as part of Ozone implementation can found [here](http://amsdocs.aka.corp.amazon.com/documentation/managedservices/latest/userguide-ma/monitoring-default-metrics.html).

  

Notifications generated by the detective controls will be forwarded to the security contact email distribution list setup for all AWS accounts.

 **Attachments:** 

