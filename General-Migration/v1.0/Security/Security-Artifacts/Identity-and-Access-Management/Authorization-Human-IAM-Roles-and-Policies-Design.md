  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines the core federated IAM roles, and policies which will be used within \[Customer\] accounts. This is not a definitive list and may grow as cloud adoption maturity grows. Defining human identity and access management requirements aligns to Well-Architected best practices. It is important to define requirements that will help control human access with appropriate defined, limited and segregated access. This requires the identification of compliance requirements, compliance resources, and defining roles and responsibilities.

**Implementation**
------------------

#### IAM Roles and Polices Definition

Each IAM Role need to be defined with responsibilities and based on those responsibilities the access permissions are allowed or denied with the help of IAM Policy.  An IAM Policy is a JSON formatted document that provides a list of ‘Allow’ or ‘Deny’ permissions. It consists of one or more statements, each of which describes the set of permissions. The following roles and policies will be deployed in each account.

##### Federated Roles

| Role | Purpose | Capabilities | Access Policy |
| --- | --- | --- | --- |
| <Namespace>-saml-administrator |   Perform administration tasks including IAM   | Full access to AWS services and resources | AdministratorAccess (AWS managed policy) |
| <Namespace>-saml-readonly | Perform monitoring tasks | Read-only access to AWS services and resources (no data read) | ReadOnly(AWS managed policy ) |
| <Namespace>-saml-billing | Perform billing and cost management tasks | Full access to account usage and viewing and modifying budgets and payment methods | Billing (AWS managed policy)  |
| <Namespace>-saml-poweruser | Perform application administration tasks | Full access to AWS services and resources, except for Accounts, Orgs, and VPCs |       {   "Version": "2012-10-17",   "Statement": \[   {   "Effect": "Allow",   "NotAction": \[   "organizations:\*",   "account:\*"   \],   "Resource": "\*"   },   {   "Effect": "Allow",   "Action": \[   "organizations:DescribeOrganization",   "account:ListRegions"   \],   "Resource": "\*"   }   \]   }      {   "Version": "2012-10-17",   "Statement": \[   {   "Effect": "Deny",   "Action": \[   "ec2:RejectVpc\*",   "ec2:CreateVpc\*",   "ec2:ModifyVpc\*",   "ec2:Accept\*",   "ec2:AttachClassicLinkVpc\*",   "ec2:CreateDefaultVpc",   "ec2:DeleteVpc\*",   "ec2:AssociateVpc\*",   "ec2:DisassociateVpc\*",   "ec2:AdvertiseByoipCidr",   "ec2:DeprovisionByoipCidr",   "ec2:DescribeByoipCidrs",   "ec2:ProvisionByoipCidr",   "ec2:WithdrawByoipCidr",   "ec2:AssociateSubnetCidrBlock",   "ec2:DisassociateSubnetCidrBlock",   "ec2:CreateTransitGatewayRouteTable",   "ec2:CreateNatGateway",   "ec2:AttachInternetGateway",   "ec2:AcceptTransitGatewayVpcAttachment",   "ec2:CreateTransitGateway",   "ec2:ReplaceTransitGatewayRoute",   "ec2:DeleteTransitGatewayVpcAttachment",   "ec2:DeleteVpnGateway",   "ec2:CreateInternetGateway",   "ec2:CreateVpnGateway",   "ec2:AssociateTransitGatewayRouteTable",   "ec2:DeleteInternetGateway",   "ec2:RejectTransitGatewayVpcAttachment",   "ec2:DisassociateTransitGatewayRouteTable",   "ec2:ModifyTransitGatewayVpcAttachment",   "ec2:DisableTransitGatewayRouteTablePropagation",   "ec2:DeleteEgressOnlyInternetGateway",   "ec2:AttachVpnGateway",   "ec2:DetachInternetGateway",   "ec2:CreateCustomerGateway",   "ec2:DeleteTransitGatewayRouteTable",   "ec2:CreateTransitGatewayRoute",   "ec2:DetachVpnGateway",   "ec2:DeleteTransitGatewayRoute",   "ec2:CreateTransitGatewayVpcAttachment",   "ec2:DeleteCustomerGateway",   "ec2:DeleteNatGateway",   "ec2:CreateEgressOnlyInternetGateway",   "ec2:EnableTransitGatewayRouteTablePropagation",   "ec2:DeleteTransitGateway"   \],   "Resource": \[   "\*"   \]   }   \]   }          |
| <Namespace>-saml-systemadministrator | Application and development operations    |   Permissions to create and maintain resources across a large variety of AWS services, including AWS CloudTrail, Amazon CloudWatch, AWS CodeCommit, AWS CodeDeploy, AWS Config, AWS Directory Service, Amazon EC2, AWS Identity and Access Management (viewing ) , AWS Key Management Service, AWS Lambda, Amazon RDS, Route 53, Amazon S3, Amazon SES, Amazon SQS, AWS Trusted Advisor, and Amazon VPC.   | SystemAdministrator (AWS managed policy) |
| <Namespace>-saml-securityaudit |   Conduct account auditing and compliance assessments   |   Read-only access to AWS services and resources   | SecurityAudit (AWS managed policy ) |
| <Namespace>-saml-securityresponse |   Conduct security incidents investigation and mitigation   | Full access to AWS services | AdministratorAccess (AWS managed policy) |

  

##### Non-federated Roles

  

|   Role     |   Purpose     |   Capabilities     |   Trust Policy     |   Access Policy     |
| --- | --- | --- | --- | --- |
|   <Namespace>-role-breakglass        | Emergency access in case SAML is down | Full access to AWS services and resources |       "Version": "2012-10-17",   "Statement": \[   {   "Effect": "Allow",   "Principal": {   "AWS": "arn:aws:iam::<MasterAccountID>:user/<Namespace>-user-breakglass"   },   "Action": "sts:AssumeRole",   "Condition": {   "Bool": {   "aws:MultiFactorAuthPresent": "true"   }   }   }   \]   }              | AdministratorAccess (AWS managed policy) |

  

#### IAM Roles and \[Customer\] Directory Store Groups/Users Matrix

The following IAM Roles and \[Customer\] Directory Store Groups mapping will be used to construct SAML assertion.

| AWS Account | IAM Role | Directory Store Group |
| --- | --- | --- |
| All | <Namespace>-saml-administrator | AWS-AccountID-administrator |
| All | <Namespace>-saml-readonly | AWS-AccountID-readonly |
| All | <Namespace>-saml-billing | AWS-AccountID-billing |
| All | <Namespace>-saml-poweruser | AWS-AccountID-poweruser |
| All | <Namespace>-saml-systemadministrator | AWS-AccountID-systemadministrator |
| All | <Namespace>-saml-securityaudit | AWS-AccountID-securityaudit |
| All | <Namespace>-saml-securityresponse | AWS-AccountID-securityresponse |

#### IdP Metadata

The following IdP metadata will be used to configure trust between \[Customer\] IdP and AWS accounts.  

*   To download an up-to-data metadata file,  the following public URL will be used: 
*   Current Metadata file(If not public URL is available):
*   Identity Provider name that will be configured and setup within the customer’s AWS accounts: 

**Ozone Implementation**
------------------------

  

This section applies to Ozone implementations only

#### **Ozone Default Federated Roles Definition**

|   Roles    |   Permissions   |
| --- | --- |
| CustomerDefaultAssumeRole | Facilitates the first login to a newly created customer-managed account. Log into this role from the Master account and Switch Role to a role named CustomerDefaultAdminRole for a newly created Customer-Managed account. |
| AWSManagedServicesSecurityOpsRole | Allows you to view the AMS infrastructure in the application accounts, manage Secrets Manager secrets, manage Web Application Firewall rules, manage certificates, and file AWS Support tickets. |
| AWSManagedServicesReadOnlyRole | Allows you to view the resources in your new application account. |
| AWSManagedServicesChangeManagementRole | Allows you to view the AMS infrastructure in the application accounts, file RFCs, file AWS Support tickets, write to S3 buckets, manage Secrets Manager secrets, and manage Reserved Amazon Elastic Compute Cloud (Amazon EC2) instances. |
| AWSManagedServicesCaseRole | Allows you to view the resources in your new application account and file AWS Support tickets. |
| AWSManagedServicesBillingRole | Allows your accounting department to view and change billing information or account settings in the Master account. |
| AWSManagedServicesAdminRole | Allows you to view the AMS infrastructure in the application accounts, manage Marketplace subscriptions, manage Secrets Manager secrets, manage Web Application Firewall rules, manage certificates, create RFCs, manage Reserved Amazon EC2 instances, write to S3 buckets, file AWS Support tickets, and manage AWS Artifacts agreements. |

#### Core Accounts Federated Roles

  

|   AWS Account   |   IAM Role Name   |   Directory Store Group   |
| --- | --- | --- |
| **Master** | AWSManagedServicesReadOnlyRole |     |
|     | AWSManagedServicesCaseRole |     |
|     | AWSManagedServicesChangeManagementRole |     |
|     | AWSManagedServicesBillingRole |     |
|     | CustomerDefaultAssumeRole |     |
| **Shared Services** | AWSManagedServicesReadOnlyRole |     |
|     | AWSManagedServicesCaseRole |     |
|     | AWSManagedServicesChangeManagementRole |     |
| **Security** | AWSManagedServicesReadOnlyRole |     |
|     | AWSManagedServicesCaseRole |     |
|     | AWSManagedServicesChangeManagementRole |     |
| **Networking** | AWSManagedServicesReadOnlyRole |     |
|     | AWSManagedServicesCaseRole |     |
|     | AWSManagedServicesChangeManagementRole |     |
| **Log Archive** | AWSManagedServicesReadOnlyRole |     |
|     | AWSManagedServicesCaseRole |     |
|     | AWSManagedServicesChangeManagementRole |     |

  

#### Member Accounts Federated Roles

|   AWS Account   | IAM Role Name | Directory Store Group |
| --- | --- | --- |
| **Account A** | AWSManagedServicesReadOnlyRole |     |
|     | AWSManagedServicesCaseRole |     |
|     | AWSManagedServicesChangeManagementRole |     |
|     | AWSManagedServicesSecurityOpsRole |     |
|     | AWSManagedServicesAdminRole |     |
| **Account B**  |     |     |

 **Attachments:** 

