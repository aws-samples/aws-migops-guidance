  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes steps to enable federated access to AWS accounts as part of Ozone implementation.

**Procedure**
-------------

### Setup AD Federation for Ozone Core Accounts

The customer must configure their Ozone environment as a Service Provider within their SAML 2.0 Identity Provider to support federation. Likewise, Ozone must configure the customer’s IdP on the Service Provider side. 

To establish the SAML SSO, the customer must provide the IdP XML Metadata file used for configuration as well as their desired name for the Identity Provider name they wish to use

  

|   Input   |   Value   |   Descriptions   |
| --- | --- | --- |
|   **IdP Metadata URL or File**   |   _(Obtain the file or URL)_   |   This is the IdP XML Metadata for the customer’s IdP   |
|   **Identity Provider Name**   |   _(default is customer-saml)_   |   This is the name of the Identity Provider that will be configured and setup within the customer’s AWS accounts.   |

#### Customers with existing AWS Federation

**Microsoft ADFS**

If your customer does have an existing Federation to AWS, and they plan to use ADFS, check to see if they have configured their custom claim rule for Roles in the same manner as the following blog article.

[https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/](https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/)

If the customer wants to reuse their existing Relying Party Trust as is, and only have to specify new security groups to support their Ozone environments, the following must occur:

*   The Identity Provider Name in Table 2: IdP Configuration must be the same as the customer’s existing Identity Provider Name (it should be visible from the existing claim rule for Roles)
*   The customer must be using the format of **AWS-{Account ID}-{AWS Role Name}** for their security groups as described in the blog link above.
*   The customer must be using the custom claim rule for Roles as shown in the blog link above. This claim rule uses a regular expression to pull out the account ID from the security group and build the ARN for the saml-provider and iam role.

**Microsoft AzureAD**

If your customer is using AzureAD to SSO into AWS, they may need to consider creating a new Enterprise Application for AWS SSO. Currently there is a limitation that allows about 1200 entries in the manifest file within AzureAD. These entries are tied to roles for each account. Depending on the customer’s existing scale and plan for future growth, it may be best to encourage them to create a separate Enterprise Application for AWS SSO to support Ozone.

#### **Customers without existing AWS Federation**

If your customer does not have an existing Federation to AWS, and they plan to use ADFS, provide them a link to the following blog article.

[https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/](https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/)

### Setup AD Federation for Customer-Managed Accounts

To maintain a consistent login experience between the Ozone Core accounts and the Customer-Managed accounts, it is recommended to extend the federation solution to also support customer-managed accounts. Customer-managed accounts do not include a set of default IAM Roles. The **Authorization: Human IAM Roles and Policies Design** documents the IAM roles that will be used in the customer-managed application accounts.

### Setup AD Federation for Ozone-Managed Application Accounts

This section applies if the customer is going to leverage any Ozone-Managed Application Accounts

  

Ozone-Managed application accounts must use federation to support logging into the console. It is recommended to extend the federation solution to support application accounts. The **Authorization: Human IAM Roles and Policies Design** documents the IAM roles that will be used in the customer-managed application accounts.

 **Attachments:** 

