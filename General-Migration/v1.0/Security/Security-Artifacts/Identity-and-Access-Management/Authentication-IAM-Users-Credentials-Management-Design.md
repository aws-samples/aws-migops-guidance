  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes controls which will be implemented to protect AWS Accounts IAM Users.

**Implementation**
------------------

\[Customer\] will use Break the Glass IAM User for emergency access during SAML federation environment failures. IAM Users with access keys but without console passwords will be permitted in limited use cases if a business justification is provided and explicit approval is received. Any other IAM users with console passwords will not be permitted.

  

BreakGlass IAM User will be configured in the Master account. Break the Glass user will have to assume BreakGlass IAM Role (link to Human IAM Roles design page) in an account before being able to perform any actions.

| User | Purpose | Capabilities | Access Policy |
| --- | --- | --- | --- |
| <Namespace>-user- breakglass | Emergency access in case SAML is down |   Ability to assume breakglass IAM Role in all accounts           |       {   "Version": "2012-10-17",   "Statement": \[   {   "Effect": "Allow",   "Action": "sts:AssumeRole",   "Resource": "arn:aws:iam::\*:role/<Namespace>-role-breakglass"   }   \]   }          |

#### **  
IAM Users Security Preventative Guardrails**

\[Customer\] will enforce a set of preventative and detective security controls to protect AWS accounts credentials and prevent deviations from the developed IAM credentials management baseline. 

\[Customer\] will implement the following security measures to properly protect the password associated with the Break the Glass user:

1.  Strong password policy will be configured for all AWS Accounts which will:
    1.  Require a minimum password length of 14;
    2.  Require at least one uppercase latter;
    3.  Require at least one lowercase letter;
    4.  Require at least one number;
    5.  Require at least one non-alphanumeric character;
    6.  Prevent password reuse (number of passwords to remember – 24);
    7.  Enable password expiration (90 days);
    8.  Allow users to change their own passwords.
2.  Break the Glass password will be generated using a random number generator provided by \[Customer\] Secrets Management platform (e.g. LastPass, CyberArk).
3.  Break the Glass password will be stored in \[Customer\] Secrets Management platform (e.g. LastPass, CyberArk) and will only be accessible by a limited group of people responsible for AWS accounts administration.
4.  No access key will be generated for the Break the Glass user.
5.  Virtual MFA will be used for the Break the Glass user to provide for two-factor authentication.
6.  Virtual MFA QR code or secret configuration key will be stored in \[Customer\] Secrets Management platform (e.g. LastPass, CyberArk).
7.  A process will be created to enforce deletion of the virtual MFA from personal devices after the use.
8.  Additional preventative controls will be implemented using AWS Organizations Service Control Policies (SCPs) (link to Service Control Policies (SCPs) Design artifact).

There might be other use cases when \[Customer\] would have to create IAM Users for programmatic access (e.g. for applications which do not support temporary credentials). \[Customer\] will implement the following security measures to properly protect the access keys associated with these users:

1.  Access Keys will be rotated at least every 90 days.

In addition, a process for requesting a creation of IAM Users using standard change request procedures will be implemented to strictly regulate the amount of permanent credentials present in AWS accounts.

#### **IAM Users Security Detective Guardrails**

1.  Detective controls will be implemented using a combination of AWS Config Rules and AWS CloudWatch Alarms (link to Detective Controls Design artifact). In order to detect unused credentials, \[Customer\] will implement an AWS managed Config Rule (“Detect unused credentials”) which will periodically evaluate AWS accounts and detect any passwords or access keys which have not been used within 90 days. 
2.  \[Customer\] will also use a set of manual procedures (link to Unused Privileges Detection Procedure runbook) to detect unused privileges which can be automated in the future.

 **Attachments:** 

