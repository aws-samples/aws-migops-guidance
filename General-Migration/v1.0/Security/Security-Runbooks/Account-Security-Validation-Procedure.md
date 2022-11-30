  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes configuration validation steps which should be taken after the initial deployment and can also be used each time a new AWS account is created and fully configured through the pipeline.

**Procedure**
-------------

#### Account and IAM Baseline

-  Verify that all Manual Account Bootstrapping steps are complete -  Verify that the account alias is created -  Verify that IAM Password Policy is configured in accordance with the developed baseline -  Verify that Human IAM Roles and Applications IAM Roles have been created -  Verify that AWS federation is working as expected -  Verify that SCPs function as expected

#### Logging and Monitoring Baseline

-  Verify that CloudTrail, Config, and VPC FlowLogs are enabled and centralized into the Log Archive account S3 Bucket -  Verify that CloudTrail and VPC FlowLogs are forwarded to each account's CloudWatch Log group -  Verify that S3 bucket and CloudWatch Log group retention policy are configured in accordance with the developed baseline -  Verify that integration with SIEM (e.g. LogRhythm) is configured in accordance with the design -  Verify that custom AWS Config Rules and AWS CloudWatch Events/Alarms are created and notifications are properly configured (check SNS topic configurations) -  Verify that GuardDuty is enabled and centralized into the Audit account -  Verify that Security Hub is enabled and centralized into the Audit account -  Verify that Security Hub security standards checks are enabled -  Verify that account and organization Access Analyzer are created

#### Infrastructure Security Baseline

-  Verify that the default VPC is deleted -  Verify that Firewall Manager policies exist and are applied to appropriate resources

#### Data Protection Baseline

-  Verify that default EBS encryption is enabled -  Verify that S3 Block Public account is enabled for applicable accounts

 **Attachments:** 

