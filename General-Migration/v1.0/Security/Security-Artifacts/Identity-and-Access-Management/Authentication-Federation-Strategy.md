  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes a strategy for the AWS Accounts federated access. Granting access through federation or roles is an AWS Well-Architected best practice, as is implementing dynamic authentication.

**Implementation**
------------------

#### **Federation**

To follow AWS Well-Architected best practices for granting least privileges and to ensure that access to AWS resources is controlled using existing identity and access management infrastructure, the strategy of using federated access to manage and utilize AWS resources will be adopted. Below are the main components of the developed strategy:

1.   Directory Store (e.g. Microsoft AD, OpenLDAP) will be used as the directory store.
2.  Identity Provider (e.g. ADFS, Shibboleth) will be used as the Identity Provider.
3.  Identity Provider (e.g. ADFS, Shibboleth) is integrated with \[Customer\] MFA Provider (e.g Duo Security, RADIUS) to provide for two-factor authentication for the federated users.
4.  A set of predefined IAM Roles and Policies (link to Users Roles design page)will be deployed in all AWS accounts to provide for a unified accounts management solution. These roles will define what users authenticated by Identity Provider (e.g. ADFS, Shibboleth)/\[Customer\] Directory Store (e.g. Microsoft AD, OpenLDAP) will be allowed to do in AWS based on \[Customer\] Directory Store (e.g. Microsoft AD, OpenLDAP) groups membership.

 **Attachments:** 

