  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Ozone Build Sheet
=================

The following decisions in the table need to be made and provided to the operations team to build the Ozone environment.

**Build Started on date:**

**Build Completed on date:**

  

| **Account/Service Related** |  |  |  |  |
| --- | --- | --- | --- | --- |
| **Parameter** | **Value** | **Default/Suggested Value** | **Required** | **Comment** |
| **New Account Id (Will be used as Organizations Master Account)** |     |     | Yes | Should not be part of an AWS Organizations |
| **Service Region** |     |     | Yes | The primary region in which AMS multi-account environment will be deployed |
| **Shared Services Account Email** |     | aws-shared-services@{OrgEmailDomain} | Yes | This email is used to create the shared services AMS account. Email domain needs to be the same as Master account email. Also, email name that contains 'sharedservices' is preferred. |
| **Network Account Email** |     | aws-network@{OrgEmailDomain} | Yes | This email is used to create the networking AMS account. Email domain needs to be the same as Master account email. Also, email name that contains 'networking' is preferred. |
| **Logging Account Email** |     | aws-logging@{OrgEmailDomain} | Yes | This email is used to create the logging AMS account. Email domain needs to be the same as Master account email. Also, email name that contains 'logging' is preferred. |
| **Security Account Email** |     | aws-security@{OrgEmailDomain} | Yes | This email is used to create the security AMS account. Email domain needs to be the same as Master account email. Also, email name that contains 'security' is preferred. |
| **AWS Service Type** |     | Business or Enterprise | No (default is Business) | This is the service level of support that will be applied to the core accounts. |
| **Networking Related** |  |  |  |  |
| **Parameter** | **Value** | **Default/Suggested Value** | **Required** | **Comment** |
| **Transit Gateway ASN Number\*** |     |     | Yes | This is the Autonomous System Number (ASN) for the AWS side of a Border Gateway Protocol (BGP) session. The range is 64512 to 65534 (inclusive) for 16-bit ASNs. |
| **Core Infrastructure VPC CIDR Range** |     | x.x.x.x/21 | Yes\* |   We either need the Core Infra CIDR Range (in green) **or** the 3 CIDR ranges in yellow. By providing just the Core Infra CIDR, AMS will subdivide it into the 3 necessary CIDRs.  *   (Required) either the green or yellow CIDR ranges must be specified        |
| **Network VPC CIDR Range** |     | x.x.x.x/24 |     |
| **Shared Services VPC CIDR Range** |     | x.x.x.x/23 |     |
| **DMZ VPC CIDR Range** |     | x.x.x.x/24 |     |
| **VPN ECMP** |     | Yes | Yes | For VPN ECMP support, choose enable if you need Equal Cost Multipath (ECMP) routing support between VPN connections. If connections advertise the same CIDRs, the traffic is distributed equally between them. |
| **Federation** |  |  |  |  |
| **Parameter** | **Value** | **Default/Suggested Value** | **Required** | **Comment** |
| **IdP Name** |     | customer-saml | Yes | The name for the IdP configured within the core accounts. |
| **Control Tower** |  |  |  |  |
| **Parameter** | **Value** | **Default/Suggested Value** | **Required** | **Comment** |
| **Enable Control Tower** |     | True | Yes | True to enable Control Tower, False otherwise. |
| **Audit Account Email** |     | aws-audit@{OrgEmailDomain} | No | This email is used to create the Control Tower Audit Account. Email domain needs ot be the same as Master account email. Also, email name that contains ‘audit’ is preferred. |
| **Log Archive Account Email** |     | aws-log-archive@{OrgEmailDomain} | No | This email is used to create the Control Tower Log Archive AMS account. Email domain needs to be the same as Master account email. Also, email name that contains 'log archive' is preferred. |

 **Attachments:** 

