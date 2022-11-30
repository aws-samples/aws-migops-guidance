  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

Periodic tests should be executed to validate the responsive controls in at least a sandbox account to ensure that the controls are active, that notifications have been configured correctly, and that actual results match the expected results. This document outlines procedures to test these controls.

**Implementation**
------------------

The following procedures can initially be used to test the responsive controls. \[Customer\] should constantly revise the list to include all relevant and critical controls and test procedures.

|   **Test Name**   |   **Description**   |   **Control**   |   **Steps**   |   **Expected Result**   |   **Test Date**   |   **Actual Result**   |
| --- | --- | --- | --- | --- | --- | --- |
|   Detect SSH ingress rule   |   Detect presence of open SSH access in security groups ingress rules.   |   Config Rule:  securityhub-restricted-ssh-…   |   1.     Log in to a test account.  2.     Create a new test security group.  3.     Add ingress rule for port 22 from 0.0.0.0/0.   |   1.     An email should be received on the appropriate email distribution list.  2.     The Confg Rule securityhub-restricted-ssh-… should be marked as non-compliant.   |     |     |
|   Detect Root login   |   Detect Root login attempts.   |   CloudWatch Alarm:  \[NameSpace\]-cwalarm-cis-root-activity   |   1.     Access the AWS console.  2.     Log in using Root credentials.   |   An email should be received on the appropriate email distribution list.   |     |     |
|   Detect IAM policy attachment   |   Detect changes to IAM resources.   |   CloudWatch Alarm:  \[NameSpace\]-cwalarm-cis-iam-policy-change   |   1.     Log in to a test account.  2.     Select an Administrator role (we'll use an administrator role so that in reality we're not assigning permissions that the role doesn't already have).  3.     Attach the ReadOnlyAccess managed policy to the Administrator role.   |   An email should be received on the appropriate email distribution list.   |     |     |
|   Detect instances not managed by SSM   |   Detect instances which are not currently managed by AWS System Manager.   |   Config Rule:  securityhub-ec2-instance-managed-by-ssm-.....   |   1.     Log in to a test account.  2.     Spin up a new EC2 instance without an appropriate IAM instance profile attachment.   |   1.     An email should be received on the appropriate email distribution list.  2.     The Confg Rule securityhub-ec2-instance-managed-by-ssm-..... should be marked as non-compliant.   |     |     |

 **Attachments:** 

