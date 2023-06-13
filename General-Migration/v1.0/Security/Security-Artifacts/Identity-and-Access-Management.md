* * *

#### Design Overview

\[Customer\] will utilize ADFS to enable users within \[Customer\] corporate directory (Microsoft AD) to gain access to specific AWS resources. By adopting this model, \[Customer\] will have a secure and robust IAM approach for accessing AWS resources that is aligned with AWS best practice that further aids control and risk mitigation.  The solution will use AWS Security Token service (STS) to provide temporary credentials (via SAML) for the users to ‘assume’ roles (that they have access to use denoted by AD Groups membership) that have specific permissions associated; as opposed to providing long-term access credentials to the AWS resources.

  

**Diagram 1: SAML-enabled AWS console single sign-on.**

 ![](/.attachments/DK-Security/image2019-11-1_18-37-13.png)

  

**Diagram 2:  SAML-enabled AWS programmatic single sign-on access.**

 ![](/.attachments/DK-Security/image2019-11-1_18-38-25.png)

 **Attachments:** 
