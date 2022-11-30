  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes naming convention used for IAM resources such as IAM User, IAM Roles, and IAM Policies.

**Implementation**
------------------

|   Resource   |   Naming Convention   |   Examples   |
| --- | --- | --- |
| IAM User | <Namespace>-user-<service>/<function>-<privilege> (<privilege> is optional) | baseline-user-breakglass |
| IAM Group | <Namespace>-group-<service>/<function>-<privilege> (<privilege> is optional) | baseline\-group-breakglass |
| IAM Roles | <Namespace>-role-<vendor>/<service>-<privilege> (<privilege> is optional) |   baseline\-role-lambda-securitybaseline  baseline\-role-azure-sentinel  baseline\-role-ec2-s3full   |
| IAM Policy | <Namespace>-policy-<service>/<function>-<privilege> (<privilege> is optional) |   baseline\-policy-poweruser  baseline\-policy-db-admin  baseline\-policy-s3-write   |
| IAM IdP | <Namespace>-idp-<provider> | baseline\-idp-shibboleth |

 **Attachments:** 

