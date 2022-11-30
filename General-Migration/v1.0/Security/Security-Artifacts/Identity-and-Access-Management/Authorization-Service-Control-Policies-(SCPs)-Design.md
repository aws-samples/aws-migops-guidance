  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines AWS Organizations Service Control Policies(SCPs) which will be implemented across AWS Accounts.

**Implementation**
------------------

#### Naming Convention

  

|   ControlTower Managed SCP   |  |   Custom SCP   |  |
| --- | --- | --- | --- |
| Name  | Description | Name  | Description |
| aws-guardrails-<......> | Guardrails applied to an organization |   <NameSpace>-guardrails-all  <NameSpace>\-guardrails-<special-ou>   |   Custom guardrails applicable to all OUs  Custom guardrails applicable to individual OUs   |

  

#### ControlTower Mandatory SCPs for all OUs

The following SCPs will be created and enforced by Control Tower for all accounts under all AWS Organizations' OUs.

|   **Service Control Policy Name**   |   **Effect**   |   **Conditions**   |  |   **Actions**   |  |  |  |   **Resource**   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|   **1**   |   **2**   |   **1**   |   **2**   |   **3**   |   **4**    |
|   **CloudTrail Enabled**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Update or Delete Cloudtrail   |   Put Event Selectors   |   Stop Logging   |     |   Any   |
|   Config Enabled   | Deny |   Applies for all except for principal ARNs matching "arn: aws:iam::\*:role /AWSControlTowerExecution   |     |   Delete / Put / Stop Config Configuration recorder   |   Delete / Put Config Delivery Channel   |   Delete / Put Config Retention Configuration   |     |   Any   |
| Config Rule Policy | Deny | Applies for all except for principal ARNs matching "arn: aws:iam::\*:role /AWSControlTowerExecution | Applies for all where string for tag matching "aws:ResourceTag /aws-control-tower": "managed- by-control-tower" | Put / Delete Config Rule | Put / Delete Config Configuration Aggregator | Delete Evaluation results |     | Any |
| **Config Rule Tags Policy** | Deny | Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution | Applies for all values where string for tag key matching "aws-control-tower" | Tag / Untag Config Resource |     |     |     | Any |
|   **CloudWatch Event Policy**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Put / Delete / Disable CloudWatch Rule   |   Put / Remove Targets of CloudWatch    |     |     |   Any resources matching:   "arn:aws:events:\*:\*:rule/aws-controltower-\*"   |
|   **Lambda Function Policy**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Create / Delete / Update Lambda Event Source Mapping   |   Create / Delete / Update Code / Update Configuration  Lambda Function   |   Delete / Put Lambda Function Concurrency    |   Add / Remove Lambda Function Permission   |   Any resources matching:   "arn:aws:lambda:\*:\*:function:aws-controltower-\*"   |
|   **SNS Subscription Policy**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution   |     |   Subscribe / Unsubscribe SNS topic   |     |     |     |   Any resource matching:   "arn:aws:sns:\*:\*:aws-controltower-SecurityNotifications"   |
|   **SNS Topic Policy**    |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution   |     |   Create / Delete SNS Topic   |   Add / Remove SNS Permissions    |   Set SNS Topic Attributes   |     |   Any resource matching:   "arn:aws:sns:\*:\*:aws-controltower-\*"   |
|   **IAM Role Policy**    |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution   |     |   Attach / Delete / Detach / Put IAM Role Policy    |   Create / Delete / Update / Update Description of IAM Role   |   Delete / Put IAM Role Permission Boundary   |   Update IAM Assume Role Policy    |   Any resource matching:   "arn:aws:iam::\*:role/aws-controltower-\*" or  "arn:aws:iam::\*:role/\*AWSControlTower\*"   |

  

#### ControlTower Mandatory SCPs for Core OU

The following SCPs are create and enforced by Control Tower for all accounts under all AWS Organizations' Core OU.

|   **Service Control Policy Name**   |   **Effect**   |   **Conditions**   |  |   **Actions**   |  |  |  |   **Resource**   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|   **1**   |   **2**   |   **1**   |   **2**   |   **3**   |   **4**    |
|   **Log Archive Bucket Encryption Enabled**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Put Encryption Configuration for S3   |     |     |     |   Any   |
|   ****Log Archive** Bucket Logging Enabled**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Put Bucket Logging for S3   |     |     |     |   Any   |
|   ****Log Archive** Bucket Policy Changes Prohibited**   |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Put Bucket Policy for S3   |     |     |     |   Any   |
|   ****Log Archive** Bucket Retention Policy**    |   Deny   |   Applies for all except for principal ARNs matching "arn:aws:iam::\*:role/AWSControlTowerExecution"   |     |   Put Lifecycle Configuration for S3   |     |     |     |   Any   |

#### Custom SCPs for All OUs 

**NotVisibletoControlTower**

Any of the custom Service Control Policies are not visible to the Control Tower but are viewable in the AWS Organizations Service Page.

  

|   **Service Control Policy Name**   |   **Effect**   |   **Conditions**   |  |   **Actions**         |   **Resource**   |
| --- | --- | --- | --- | --- | --- |
| **1** |   **2**   |   **1**   |
|   **IAM User Creation**   |   Deny   |     |   Except for principal ARNs matching:   "arn:aws:iam::\*:role/AWSControlTowerExecution"   |   CreateUser   |   Any   |
|   **Allowed Regions**   |   Deny   | Except for us-west-2 |   Except for principal ARNs matching:   "arn:aws:iam::\*:role/AWSControlTowerExecution"   "arn:aws:iam::\*:role/service-role/AWSControlTowerAdmin"   "arn:aws:iam::\*:role/<Namespace>\-role-lambda-delete-default-vpc"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"     |   All \*   |   Any   |
| **GuardDuty Enabled** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   "arn:aws:iam::\*:role/<Namespace>-role-crossaccount-securitybaseline"   |   DeleteDetector  UpdateDetector  StopMonitoringMembers  DeleteMembers  DisassociateMembers  DisassociateFromMasterAccount   | Any |
| **SecurityHub Enabled** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>-role-crossaccount-securitybaseline"   |   DisableSecurityHub  DeleteMembers  DisassociateMembers  DisassociateFromMasterAccount   | Any |
|   **Access Analyzer Enabled**   | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   | DeleteAnalyzer |   Any resources matching:  "arn:aws:access-analyzer:\*:\*:analyzer/<Namespace>-\*"   |
| **Custom CloudWatch Events **Persist**** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   |   Put / Delete / Disable CloudWatch Rule  Put / Remove Targets of CloudWatch   |   Any resources matching:  "arn:aws:events:\*:\*:rule/<Namespace>-\*"   |
| **Custom CloudWatch Alarms **Persist**** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   |   DeleteAlarms  EnableAlarmActions  DisableAlarmActions  PutMetricAlarm  SetAlarmState   |   Any resources matching:  "arn:aws:cloudwatch:\*:\*: alarm :<Namespace>-\*"   |
| **Custom Confg Rules **Persist**** | Deny |   Applies for all where string for tag matching "aws: ResourceTag/baseline":"managed-resource"   |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/aws-controltower-\*"   |   Put / Delete Config Rule  Delete Evaluation results   |   Any   |
| **Custom Confg Rules Tags Persist** | Deny |   Applies for all values where string for tag key matching  "baseline"   |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-lambda-\-configruletagging-\*"   |   TagResource  UnTagResource   |   Any   |
|   **Centrally managed Lambda Functions Persist**   | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-service-catalog"   |   Create / Delete /  Update Lambda Event Source Mapping  Create / Delete / Update Code / Update Configuration Lambda Function  Delete / Put Lambda Function Concurrency  Add / Remove Lambda Function Permission   |   Any resources matching:  "arn:aws:lambda:\*:\*: function:<Namespace>-\*"   |
|   **Centrally managed application IAM Roles Persist**   | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/aws-controltower-\*"  "arn:aws:iam::\*:role/<Namespace>\-role-breakglass"   "arn:aws:iam::\*:role/<Namespace>\-role-service-catalog"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"   |   AttachRolePolicy  DetachRolePolicy  UpdateAssumeRolePolicy  DeleteRole  UpdateRole  UpdateRoleDescription  DeleteRolePolicy  PutRolePolicy   |   Any resources matching:  "arn:aws:iam::\*:\*/<Namespace>-\*"   |
| **IAM Password Policy Persist** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   "arn:aws:iam::\*:role/<Namespace>\-role-lambda-iampasswordpolicy"  "arn:aws:iam::\*:role/<Namespace>\-role-crossaccount-securitybaseline"     | Delete/Update IAM password Policy | Any |
| **IAM IdP Persists** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/aws-controltower-\*"  "arn:aws:iam::\*:role/<Namespace>\-role-breakglass"   "arn:aws:iam::\*:role/<Namespace>\-role-service-catalog"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"   |   CreateSAMLProvider  DeleteSAMLProvider  UpdateSAMLProvider           |   Any resources matching:  "arn:aws:iam::\*:\*/<Namespace>-\*"   |
| **Centrally managed CloudFormation Stacks Persist** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"  "arn:aws:iam::\*:role/<Namespace>\-role-service-catalog"   |   Create\*  Delete\*  Update\*  SetStackPolicy   |   Any resources matching:   "arn:aws:cloudformation:\*:\*:stack/<Namespace>\*",   "arn:aws:cloudformation:\*:\*:stack/CustomControlTower-\*",   "arn:aws:cloudformation:\*:\*:stack/StackSet-CustomControlTower-\*"   |
| **Centrally managed SSM Parameters Persist** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   | Delete parameters |   Any resources matching:   "arn:aws:ssm:\*:\*:parameter/<Namespace>/\*"   |
| **Default SG configurations Persist** | Deny | Applies for all where string for tag matching "aws: ResourceTag/baseline":"managed-resource" |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-securityresponse"  "arn:aws:iam::\*:role/<Namespace>\-role-lambda-cleanupdefaultsg-\*"  arn:aws:iam::\*:role/<Namespace>\-role-service-catalog"         |   AuthorizeSecurityGroupEgress  AuthorizeSecurityGroupIngress  DeleteSecurityGroup   | Any |
| **Automation tags configurations Persist** | Deny |   Applies for all values where string for tag key matching  "baseline", "Associate-with", "Propagate-to", "Attach-to-tgw",  "backup","patch","availability\_zone"     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"  "arn:aws:iam::\*:role/<Namespace>\-role-lambda-configruletagging-\*"  "arn:aws:iam::\*:role/<Namespace>\-role-lambda-cleanupdefaultsg-\*"  "arn:aws:iam::\*:role/<Namespace>\-role-service-catalog"         |   CreateTags  DeleteTags   | Any |
| **WAF Logs Kinesis Firehose Persist** | Deny |     |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"   |   DeleteDeliveryStream  StopDeliveryStreamEncryption  UpdateDestination           | Any resources matching:   "arn:aws:firehose:\*:\*:deliverystream/aws-waf-logs-kinesis-baseline" |
| **WAF Firewall Manager Policy Persists** | Deny | Applies for all where string for tag matching "aws: ResourceTag/baseline":"managed-resource" |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"  "arn:aws:iam::\*:role/<Namespace>\-role-saml-administrator"   |   DeletePolicy  PutPolicy       | Any |
| **WAF Firewall Manager Policy Tag Persists** | Deny |   Applies for all values where string for tag key matching  "baseline"   |   Except for principal ARNs matching:  "arn:aws:iam::\*:role/AWSControlTowerExecution"   |   TagResource  UnTagResource   | Any |

\*some AWS services do not have [endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html) in the us-east-1 region, therefore, if \[CUSTOMER\] plans on using these services in the future, they should be added to the "NotAction" element of the "GRALLOWEDREGIONS" statement. 

#### Ozone Mandatory SCPs 

  

This section is applicable to Ozone implementation only.

  

**NotVisibletoControlTower**

Any of the custom Service Control Policies are not visible to the Control Tower but are viewable in the AWS Organizations Service Page.

  

  

| Scope | Functionality |
| --- | --- |
| Entire Organization             | Restricts Root User access in all accounts (except Master) and prevents anyone creating new Root Access Keys. |
| Restricts SAML Provider CRUD to only AMS internal Admin Roles in any account. |
| Protects AMS Infrastructure Logging and Monitoring Lambdas used for AMS Change Management system, CW Events, SNS and EC2 Instance Profiles etc. |
| Restricts s3 actions of CreateBucket and Delete on AMS buckets to only AMS Change Management system, CFN StackSets and AMS Infrastructure S3 Bucket Management Lambda. |
| Allows only VPC service to write to VPC Flow Logs CW LogGroup. |
| Core OU (including Master)          | Allows creation/deletion of VPC, DHCP Options, Internet Gateway, NAT Gateway, Route, Route Table, Subnet, Security Group, TGW Resources only to AMS internal automation roles. Allows Route and Route Table replacement and Updating SG Ingress/Egress descriptions only to AMS internal automation roles. |
| Allows TGW-VPC Attachment create/delete only to TGW Lambda and AMS Change Management system. |
| Allows TGW Attachment Lambda update/delete/invoke only to CFN StackSets and AMS Change Management system. |
| Allows IAM Actions only to CFN StackSets, BreakGlass Roles and AMS Change Management system. |
| Allows CFN operations only to CFN StackSets and AMS Change Management system. |
| Restricts s3 actions on cf-templates-\* bucket to CFN StackSets and AMS Change Management system. |
| Allows s3 delete operations on AMS buckets only to AMS Change Management system. |
| Denies AWS MarketPlace unsubscribe operations |
| Denies SNS delete topic and unsubscribe to anyone except CFN StackSets and AMS Change Management system. |
| Denies Secrets Manager delete secret to anyone except AMS Change Management system. |
| Denies SSM put/delete parameter for /org/member/local\_sns\_arn to anyone except CFN StackSets and AMS Change Management system. |
| Denies SSM put/delete parameter for /ams/\* to anyone except CFN StackSets, AMS Change Management system and EPS Lambdas. |
| Allows STS Actions on BreakGlass Roles only to CSC team. |
| Logging Account | Allows s3 PutEncryptionConfiguration, PutBucketLogging, PutBucketPolicy and PutLifecycleConfiguration actions on any bucket in the Logging account only to CFN StackSets and AMS Change Management system. |
| Networking Account | Allows delete of DXGW and DXGW-Association only to DXGW Lambdas and AMS Change Management system. |
| Allows DXGW Lambdas' update/delete/invoke only to AMS Change Management system. |
| Shared Services Account | Protects RDP, EPS and Onboarding Lambdas by segregating them in groups based on Principals/Services allowed to invoke them (AMS Change Management system, CW Events, SNS and Management Host Instance Profiles). |
| Allows certain EPS Lambdas to only be invoked by certain other specific Lambdas. |
| Allows secretsmanager:updatesecret on any secret in the Shared Services Account only to management host and AMS Change Management system. |
| Allows ds:delete actions only to AMS Change Management system. |
| Allows kms:updateAlias and kms:deleteAlias only to management host and AMS Change Management system. |

 **Attachments:** 

