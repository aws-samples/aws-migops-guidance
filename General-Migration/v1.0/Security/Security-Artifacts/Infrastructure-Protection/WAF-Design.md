  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines a strategy for providing application layer protection using AWS WAF and AWS Firewall Manager.

AWS WAF provides the following protection:

1.  Monitors the HTTP and HTTPs requests that are forwarded to applications.
2.  Controls access to applications content and protects against web attacks using specific conditions. Conditions are defined by using characteristics of web requests such as the following:
    1.  IP addresses that requests originate from.
    2.  Country that requests originate from.
    3.  Values in request headers, for example, values that appear in the User-Agent header.
    4.  Strings that appear in requests, either specific strings or string that match regular expression (regex) patterns.
    5.  Length of requests.
    6.  Presence of SQL code that is likely to be malicious (known as _SQL injection_).
    7.  Presence of a script that is likely to be malicious (known as _cross-site scripting_).

WAF Rules that can allow, block, or count web requests that meet the specified conditions (regular rules). Alternatively, rules can block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5-minute period (rate-based rules).

AWS WAF offers the following additional benefits:

1.  Rules can be reused for multiple web applications.
2.  Provides real-time metrics (published to CloudWatch) and sampled web requests.
3.  Automated administration using the AWS WAF API.
4.  AWS Managed Rules provide protection against common application vulnerabilities or other unwanted traffic, without having to write your own rules. 

AWS Firewall Manager provides the following benefits:

1.  Firewall Manager allows to configure common WAF Rules to be enforced across all application accounts. Once configured, common WAF Rules are automatically applied/updated across all accounts and resources (existing or new).
2.  Common WAF Rules are configured and managed from the Firewall Manager administrator account and can be applied across selected accounts and specific resources.
3.  Common WAF Rules cannot be modified from the member accounts.
4.  Common WAF Rules can be composed of \[Customer\] custom rules and managed rules.
5.  Firewall Manager can be used to subscribe all member accounts in an AWS Organizations organization to AWS Shield Advanced, and automatically subscribes new in-scope accounts that join the organization.

**Implementation**
------------------

\[Customer\] will use AWS WAF to provide for application layer protection. A set of common AWS WAF ACL Rules will be deployed for all applications deployed on Amazon CloudFront, Amazon Application Load Balancer (ALB), or Amazon API Gateway. In order to accelerate AWS WAF configuration and automate protection of new resources across multiple accounts, \[Customer\] will utilize AWS Firewall Manager.

#### WAF Rules Management

\[Customer\] will use a combination of AWS Managed Rule Groups and custom AWS WAF rules for defining and enforcing a set of standard WebACL rules.

*   To provide for a more comprehensive Layer 7 protection and to offload an operational overhead related to the management of the WAF Rules, \[Customer\] will use the following [AWS Managed Rules Groups](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html):

|   **Type**   |   **Rules Group**   |
| --- | --- |
| IP reputation rule groups | Amazon IP Reputation |
|   Baseline rule groups   |   Core Rule Set (CRS)   |

*   To meet Customer requirements which are not covered by the AWS Managed Rules above, Customer will add the following custom rules to the centrally managed WebACL:

| Purpose | Rule # | Rule Name | Rule Condition | Action |
| --- | --- | --- | --- | --- |
|     |     |     |     |     |
|     |     |     |     |     |

*   Customer can also select [AWS Marketplace Rules Groups](https://docs.aws.amazon.com/waf/latest/developerguide/marketplace-managed-rule-groups.html) to subscribe to in addition to AWS Managed Rules Groups in the future.

#### Firewall Manager Implementation

\[Customer\] will use AWS Firewall Manager to manage and enforce a set of common AWS WAF ACL Rules across all application accounts which will host relevant resources. Business justification will have to be presented during an AWS account onboarding process for the account to be excluded from this policy.

*   \[Customer\] Audit account will be designated as the AWS Firewall Manager administrator account. 
*   ‘centrail-it-waf’ tag will be used to indicate resources which should be excluded from the policy - applicable to applications which workflow will be negatively impacted by the common WAF ACL Rules.
*   Since AWS WAF charges are based on the number of web requests received and the number of configured WebACLs/Rules/FW Policies, AWS WAF will be enabled on an as needed basis for accounts which will contain relevant resources to protect.
*   Sandbox account will initially be used for testing purposes.
*   Important security events notifications generated by the AWS Firewall Manager will be forwarded to the audit account’s security contact email distribution list.

#### Pricing Information

1.  [AWS WAF](https://aws.amazon.com/waf/pricing)
2.  [AWS Firewall Manager](https://aws.amazon.com/firewall-manager/pricing)

#### Future State

The following AWS WAF features can be considered for implementation in the future:

1.  [Web ACL traffic logging](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html)
2.  [AWS Firewall Manager to manage AWS Shield Advanced Protection](https://docs.aws.amazon.com/waf/latest/developerguide/getting-started-fms-shield.html)

 **Attachments:** 

