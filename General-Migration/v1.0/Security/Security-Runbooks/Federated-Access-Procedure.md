  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes steps to take to access AWS Console, AWS CLI, or AWS APIs using federated identities. Granting access through federation or roles is an AWS Well-Architected best practice.

**Procedure**
-------------

#### AWS console federated access procedure

1.  A user browses to Identity Provider (e.g. ADFS, Shibboleth) portal and selects the option to go to the AWS Management Console.
2.  Identity Provider (e.g. ADFS, Shibboleth) verifies and authenticates the user's identity against Directory Store (e.g. Microsoft AD, OpenLDAP) and MFA Provider (e.g Duo Security, RADIUS).
3.  Identity Provider (e.g. ADFS, Shibboleth) generates a SAML authentication response that includes an assertion that identifies the user and includes attributes about the user. Identity Provider (e.g. ADFS, Shibboleth)  then sends this response to the client browser.
4.  The client browser is redirected to the AWS single sign-on endpoint and posts the SAML assertion.
5.  The endpoint requests temporary security credentials on behalf of the user and creates a console sign-in URL that uses those credentials.
6.  AWS sends the sign-in URL back to the client as a redirect.
7.  The client browser is redirected to the AWS Management Console. If the SAML authentication response includes attributes that map to multiple IAM roles, the user is first prompted to select the role to use for access to the console.

  

#### AWS API/CLI federated access procedure

1.  A user launches a client app to request authentication from Identity Provider (e.g. ADFS, Shibboleth).
2.  Identity Provider (e.g. ADFS, Shibboleth) authenticates the user against Directory Store (e.g. Microsoft AD, OpenLDAP) and MFA Provider (e.g Duo Security, RADIUS).
3.  Identity Provider (e.g. ADFS, Shibboleth) constructs a SAML assertion with information about the user and sends the assertion to the client app.
4.  The client app calls the AWS STS AssumeRoleWithSAML API, passing the ARN of the SAML provider, the ARN of the role to assume, and the SAML assertion from Identity Provider (e.g. ADFS, Shibboleth).
5.  The API response to the client app includes temporary security credentials.
6.  The client app saves temporary security credentials in the aws/credentials file.

           Note: alternatively, AWS Cloud9 can be used to execute CLI commands while using federated identities or [awsprocesscreds](https://github.com/awslabs/awsprocesscreds) for supported IdPs.

  

#### API/CLI client app installation procedure (TBD Day2)

 **Attachments:** 

