  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes minimum configuration steps which should be taken each time a new AWS account is created in order to apply and enforce an established security baseline for protecting access to AWS accounts.

**Procedure**
-------------

1.  [Reset Root password](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys_retrieve.html#reset-root-password) - can only be performed by Root.
2.  [Enable MFA for the Root account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_mfa) - can only be performed by Root.
3.  [Configure support plan](https://aws.amazon.com/premiumsupport/knowledge-center/change-support-plan/) \- can only be performed by Root.
4.  [Grant access to billing information for IAM users/roles if required](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/control-access-billing.html) - can only be performed by Root.
5.  Store Root password in a Secrets Management platform and MFA in the physical vault.
6.  Configure account Security Challenge Questions and store them in the Secrets Management platform.
7.  [Configure alternative contact information for Security, Billing, and Operations](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-account-payment.html#manage-account-payment-alternate-contacts).

 **Attachments:** 

