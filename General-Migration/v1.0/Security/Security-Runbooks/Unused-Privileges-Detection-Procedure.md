  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes manual procedures which can be used to detect IAM Unused Credentials and Permissions or to assist with internal/external auditing efforts. Removing insecure configurations, by removing unnecessary and unused credentials or permissions is a Well-Architected best practice.

**Procedure**
-------------

For AWS Console interactive IAM Users:

1.  IAM Console: “Console last sign-in” column of the IAM Users console will indicate when a password was last used to log into AWS.
2.  [Credential Report](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html): “password\_last\_used” column of the report will indicate when a password was last used.
3.  API: [ListUsers](https://docs.aws.amazon.com/IAM/latest/APIReference/API_ListUsers.html) API will return “PasswordLastUsed” value for each IAM User in the account.

For AWS CLI/API IAM Users:

1.  IAM Console: “Access key last used” column of the IAM Users console will indicate when an access key was last used to sign API calls.
2.  Credential Report: “access\_key\_1\_last\_used\_date” and “access\_key\_2\_last\_used\_date” columns of the report will indicate when access keys were last used to sign API calls.
3.  API: [ListAccessKeys](https://docs.aws.amazon.com/IAM/latest/APIReference/API_ListAccessKeys.html) API will return information about access keys enabled for a user; [GetAccessKeyLastUsed](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetAccessKeyLastUsed.html) will return “LastUsedDate” value for an access key.

For IAM Roles:

1.  Use [IAM Access Advisor console](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor-view-data.html#access_policies_access-advisor-viewing) page to look up services recently accessed by an IAM Role.
2.  Use [IAM Access Advisor APIs](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor-view-data.html#access_policies_access-advisor-viewing-cli) to programmatically collect information about all non-active IAM Roles.
3.  Parse CloudTrail logs for AssumeRole, AssumeRoleWithSAML, and AssumeRoleWithWebIdentity events.

  

IAM Access Advisor Console page and APIs can also be utilized to detect and delete unused permissions to enforce least privileges. This process can be automated by periodically running a Lambda function which would notify \[Customer\] if any unused credentials are detected.

 **Attachments:** 

