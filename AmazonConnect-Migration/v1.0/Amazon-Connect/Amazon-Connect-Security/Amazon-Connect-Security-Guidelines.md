  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Amazon Connect Security Guidelines**
======================================

Amazon Connect is a self-service, cloud-based contact center service that enables businesses of any size to deliver engaging, dynamic, and personal customer service experiences. This document provides the guidelines and describes the data handled by Amazon Connect including the security controls that safeguard this data. AWS follows a shared responsibility model, where AWS manages security of the cloud itself and customers retain control of what security is implemented to protect their own data. The first step is understanding the 
[AWS Shared Responsibility Model](https://myitportal.atlassian.net/wiki/download/attachments/927727749/image2020-12-17_0-16-36.png?version=1&modificationDate=1608182197642&cacheVersion=1&api=v2) followed by how this applies to Amazon Connect.  

The following diagrams and guidelines are in accordance with [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc) 
with a lens for Amazon Connect:

### **AWS Shared Responsibility Model for Amazon Connect**

 ![](/.attachments/DK-MobilizeforConnect/image2020-12-17_1-12-13.png)

### **Amazon Connect Security Journey**

 ![](/.attachments/DK-MobilizeforConnect/image2020-12-17_0-16-36.png)

### **Compliance Foundations**

Third-party auditors assess the security and compliance of Amazon Connect as part of multiple AWS compliance programs. These include SOC, PCI, HIPAA, C5 (Frankfurt), and HITRUST CSF.

For a list of AWS services in scope of specific compliance programs, see [AWS Services in Scope by Compliance Program](http://aws.amazon.com/compliance/services-in-scope/). For general information, see [AWS Compliance Programs](http://aws.amazon.com/compliance/programs/).

### **Region Selection**

[Region selection](https://docs.aws.amazon.com/connect/latest/adminguide/ccp-networking.html#ccp-region-selection) 
to host the Amazon Connect instance depends on data sovereignty restrictions and where the contacts and agents are based. Once that decision is made, customers will need to review 
[network requirements](https://docs.aws.amazon.com/connect/latest/adminguide/ccp-networking.html) 
for Amazon Connect and 
[ports and protocols](https://docs.aws.amazon.com/connect/latest/adminguide/ccp-networking.html#port-considerations) 
that customers would need to allow. Additionally, customers looking to reduce the blast radius can do so by using the 
[domain allow list](https://docs.aws.amazon.com/connect/latest/adminguide/ccp-networking.html#option1)  or 
[whitelist IP address ranges](https://docs.aws.amazon.com/connect/latest/adminguide/ccp-networking.html#option2) 
for their Amazon Connect instance.

### **AWS Services Integration**

Customers will need to review each AWS service in their solution against the security requirements of their organization. Security information about AWS services commonly integrated with Amazon Connect can be found below.

*   [Security in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-security.html)
*   [Security and Compliance in Dynamo DB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/security.html)
*   [Security in AWS Lex](https://docs.aws.amazon.com/lex/latest/dg/security.html)

### **Data Security within Amazon Connect**

During your security journey, your security teams may require a deeper understanding of 
[how data is handled in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/security.html). You may refer to the 
[Detailed Network Paths for Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/detailed-network-paths.html), 
[Infrastructure Security in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/infrastructure-security.html), 
[Data Protection in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/data-protection.html), and 
[Compliance Validation](https://docs.aws.amazon.com/connect/latest/adminguide/compliance-validation.html) 
documentation for more information.

### **Workload Diagram**

Customers should review their workload diagram and architect an optimum solution on AWS. This would include analyzing and deciding which additional AWS services would be included in the solution and any third party and on-premises applications that would need to be integrated.

As an example, a workload for 
[automatically distributing scheduled reports for Amazon Connect](https://aws.amazon.com/blogs/contact-center/automatically-distribute-scheduled-reports-for-amazon-connect/) 
stores the scheduled reports in an S3 bucket. A CloudWatch event triggers an AWS Lambda function when a new report is added the S3 bucket and sends an email with the report attached. The workload diagram below for this workload shows Amazon Connect along with AWS Lambda, Amazon S3, Amazon CloudWatch and Amazon SES.

 ![](/.attachments/DK-MobilizeforConnect/image2020-12-17_1-26-45.png)

  

### **Definition**

There are five best practice areas for security in the cloud:

*   Identity and access management
*   Detective controls
*   Infrastructure protection
*   Data protection
*   Incident response

### **Identity and Access Management**

#### **Types of Amazon Connect Personas**

There are four types of Amazon Connect personas which differ, depending on the activities being performed.

**
 [IAM%20Connect%20Personas.pptx](/.attachments/DK-MobilizeforConnect/IAM%20Connect%20Personas.pptx)
**
=========================================================================================================

1.  **IAM administrator**– IAM administrators create or modify Amazon Connect resources and may also delegate administrative access to other principals. The scope of this persona is Amazon Connect instance creation and administration.
2.  **Connect Service administrator**– Service administrators determine which Amazon Connect features and resources employees should access within the Connect Console. The service administrator assigns 
    [Security profiles](https://docs.aws.amazon.com/connect/latest/adminguide/connect-security-profiles.html) 
    to determine who can access the connect console and what tasks they can perform. The scope of this persona is Amazon Connect contact center creation and administration.
3.  **Connect Service agent**– Service users interact with the Amazon Connect service to perform their job duties. Service users may be contact center agents or supervisors.
4.  **Connect Service contact**– The external customer or end user of the Connect contact center services.

### **IAM Administrator Best Practices**

IAM Administrative access should be limited to approved personnel within your organization. IAM administrators should also understand what IAM features are available to use with Amazon Connect. Additional information on IAM best practices is available in the 
[IAM documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#use-roles-with-ec2) 
and in the 
[Amazon Connect policy examples](https://docs.aws.amazon.com/connect/latest/adminguide/security_iam_id-based-policy-examples.html)

### **Connect Service Administrator Best Practices**

Service administrators are responsible for managing Amazon Connect users, including adding users to Amazon Connect give them their credentials, and assign the appropriate permissions so they can access the features needed to do their job. Administrators should start with a minimum set of permissions and grant additional permissions as necessary.

[Security profiles](https://docs.aws.amazon.com/connect/latest/adminguide/connect-security-profiles.html) 
help you manage who can access the Amazon Connect dashboard and Contact Control Panel, and who can perform specific tasks. Customers should review the granular permissions granted within the default security profiles available natively. Custom security profiles can be set up to meet specific requirements. For example, a power agent who can take calls but also has access to reports. Once this is finalized, users should be assigned to the correct security profiles.

### **Multi-Factor Authentication**

For extra security, we recommend that you require multi-factor authentication (MFA) for all AWS IAM users in your account. Multi-factor authentication (MFA) 
[can be set up through AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) 
or your SAML 2.0 identity provider, or Radius server, if that's more applicable for your use case. After MFA is set up, a third text box becomes visible on the Amazon Connect login page to provide the second factor.

### **Identity Federation**

In addition to storing users in Amazon Connect, you can 
[enable single sign-on (SSO) to Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/configure-saml.html) 
by using identity federation. Federation is a recommended practice to allow for employee lifecycle events to be reflected in Amazon Connect when they are made in the source identity provider.

### **Access to Integrated Applications**

Steps within your Contact flows may need credentials in order to access information in external applications and systems. To provide credentials to access other AWS services in a secure way, use 
[IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html). An IAM role is an entity that has its own set of permissions, but that isn't a user or group. Roles also don't have their own permanent set of credentials and are automatically rotated.

Credentials such as API keys should be stored outside of your contact flow application code, where they can be retrieved programmatically. To accomplish this, you can use 
[AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) 
or an existing third-party solution. Secrets Manager enables you to replace hardcoded credentials in your code, including passwords, with an API call to Secrets Manager to retrieve the secret programmatically.

### **Detective Controls**

Logging and monitoring are important for the availability, reliability and, performance of contact center. Customers should log relevant information from Amazon Connect contact flows to CloudWatch and build alerts and notifications based on the same.

Customers should define log retention requirements and lifecycle policies early on, and plan to move log files to cost-efficient storage locations as soon as practical. Amazon Connect public APIs log to Cloud Trail. Customers should review and automate actions set up based on Cloud Trail logs.

[Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html) 
is the best choice for long-term retention and archiving of log data, especially for organizations with compliance programs that require log data to be auditable in its native format. Once log data is in an Amazon S3 bucket, define lifecycle rules to automatically enforce retention policies and move these objects to other, cost-effective storage classes, such as Amazon S3 Standard - Infrequent Access (Standard - IA) or Amazon Glacier.

The AWS Cloud provides flexible infrastructure and tools to support both sophisticated partner offerings and self-managed centralized-logging solutions. This includes solutions such as 
[Amazon Elasticsearch Service](https://aws.amazon.com/elasticsearch-service/) 
and 
[Amazon CloudWatch Logs](https://aws.amazon.com/cloudwatch/details/).

Fraud detection and prevention for incoming contacts can be implemented by customizing Amazon Connect contact flows per the customer requirements. As an example, customers can check incoming contacts against previous contact activity in Dynamo DB and then take actions such as disconnecting a contact for black listed contacts.

### **Infrastructure Protection**

Although there is no infrastructure to manage in Amazon Connect, there

could be scenarios where your Amazon Connect instance needs to interact with

other components or applications deployed in infrastructure residing on-premises. Consequently, it is important to ensure networking boundaries are considered under this assumption. Specific 
[Amazon Connect infrastructure security](https://docs.aws.amazon.com/connect/latest/adminguide/infrastructure-security.html) 
considerations should be reviewed and implemented. Contact center agent and supervisor desktops or VDI solutions should be reviewed for security considerations as well.

You can 
[configure a Lambda function](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html) 
to connect to private subnets in a virtual private cloud (VPC) in your account. Use Amazon Virtual Private Cloud (Amazon VPC) to create a private network for resources such as databases, cache instances, or internal services. Connect your function to the VPC to access private resources during execution.

### **Data Protection**

Customers should analyze the data traversing through and interacting with the contact center solution.

*   Third party and external data
*   On-premises data in hybrid Amazon Connect architectures

After analyzing the scope of the data, data classifications should be performed paying attention to identifying sensitive data. Connect Application conforms to the AWS shared security model. 
[Data protection for Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/data-protection.html) 
includes best practices like using MFA and TLS and the use of other AWS services, including 
[Amazon Macie](https://aws.amazon.com/macie/).

Amazon Connect handles variety of 
[data related to contact centers](https://docs.aws.amazon.com/connect/latest/adminguide/data-handled-by-connect.html). This includes phone call media, call recordings, chat transcripts, contact metadata as well as contact flows, routing profiles and queues. Amazon Connect handles 
[data at rest](https://docs.aws.amazon.com/connect/latest/adminguide/encryption-at-rest.html) 
by segregating data by account ID and instance ID. All data exchanged with Amazon Connect is protected 
[in transit](https://docs.aws.amazon.com/connect/latest/adminguide/encryption-in-transit.html) 
b­etween the users’ web browser and Amazon Connect using industry standard TLS encryption.

Customers can specify KMS keys to be used for 
[encryption](https://docs.aws.amazon.com/connect/latest/adminguide/key-management.html) 
including BYOK. Additionally, they can use key management options within S3.

### **Protecting Data Using Client-Side Encryption**

Your use case may require encryption of sensitive data that is collected by contact flows. For example, to gather appropriate personal information to customize the customer experience when they interact with their IVR. To do this you can use public-key cryptography with the 
[AWS Encryption SDK](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/introduction.html). The AWS Encryption SDK is a client-side encryption library designed to make it easy for everyone to encrypt and decrypt data using industry standards and best practices. For more information, see the 
[Connect documentation](https://docs.aws.amazon.com/connect/latest/adminguide/contact-flow-keys.html).

### **Input Validation**

Input validation should be performed to ensure only properly formed data is entering the Contact flow. Input validation should happen as early as possible in the Contact flow.

### **Amazon Connect Security Vectors**

Amazon Connect security can be broken down into three logical layers as illustrated in the diagram below:

 [Amazon%20Connect%20Security%20Vectors.pptx](/.attachments/DK-MobilizeforConnect/Amazon%20Connect%20Security%20Vectors.pptx)

*   **Agent Workstation Layer**. The agent workstation layer is not managed by AWS and consists of any physical equipment and third-party technologies, services, and endpoints that facilitate your agent’s voice, data, and access the Connect interface layer.
*   **AWS Layer**: The AWS layer includes Amazon Connect and AWS integrations including AWS Lambda, Amazon DynamoDB, Amazon API Gateway, and Amazon S3.

*   **External Layer**: The External Layer includes contact points including chat, click-to-call endpoints, and the PSTN for voice calls, integrations you may have with legacy contact center solutions in a Hybrid contact center architecture, and integrations you may have with other third-party solutions. Any entry point or exit point for a third party in your workload is considered the external layer.

  

**Agent Workstation:** 
Follow your security best practices for this layer with special attention to the following:

*   Plan 
    [identity management](https://docs.aws.amazon.com/connect/latest/adminguide/directory-service.html) 
    keeping in mind best practices noted in 
    [single sign-on and MFA](https://docs.aws.amazon.com/connect/latest/adminguide/best-practices.html).
*   Mitigate insider threat and compliance risk associated with workloads that handle sensitive information by 
    [creating a Secure IVR solution](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/) 
    that allows you to bypass agent access to sensitive information. By 
    [encrypting contact input in your contact flows](https://docs.aws.amazon.com/connect/latest/adminguide/contact-flow-keys.html), you’re able to capture information securely without exposing it to your agents, their workstations, or their operating environments.
*   You are responsible for maintaining the 
    [whitelisting](https://docs.aws.amazon.com/connect/latest/adminguide/ccp-networking.html) 
    of AWS IP addresses, ports, and protocols needed to use Amazon Connect.

**AWS**: The AWS layer includes Amazon Connect and AWS integrations including Lambda, DynamoDB, API Gateway, S3 and other services. Customers should follow the security pillar guidelines for AWS services that they integrate with special attention to the following:

*   Plan 
    [identity management](https://docs.aws.amazon.com/connect/latest/adminguide/directory-service.html) 
    keeping in mind best practices noted in 
    [single sign-on and MFA](https://docs.aws.amazon.com/connect/latest/adminguide/best-practices.html).
*   Integrations with other AWS services: Identify each AWS service in the use case as well as any third-party integration points applicable for this use case.
*   Amazon Connect can integrate with AWS lambda functions that run inside of a customer VPC through the 
    [VPC endpoints for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html).

**External**: The External Layer includes integrations that the customers may have with their on-premises infrastructure in a hybrid Amazon Connect model. This layer also covers integrations customers may have with other third-party solutions and applications such as CRM systems, WFM and reporting and visualization tools and applications such as Tableau and Kibana. You should consider the following areas when securing the external layer:

*   You can create contact filters for repeat and fraudulent contacts using AWS Lambda to write contact details to DynamoDB from within your Contact flow, including ANI, IP address for click-to-dial and chat endpoints, and any other identifying information to track how many contact requests occur during a given period of time. This allows you to query and add contacts to black-lists, automatically disconnecting them if they exceed reasonable levels. You can also prevent contacts from ever reaching your instance by implementing these filter controls at the micro-service and/or web server levels.
*   ANI Fraud detection solutions using 
    [Amazon Connect telephony metadata](https://docs.aws.amazon.com/connect/latest/adminguide/connect-attrib-list.html#telephony-call-metadata-attributes) 
    and 
    [partner solutions](https://aws.amazon.com/connect/partners/) 
    can be used to protect against Caller ID spoofing.
*   Voice biometric 
    [partner solutions](https://aws.amazon.com/connect/partners/) 
    can be used to enhance and streamline the authentication process. Active voice biometric authentication allows contacts the option to speak specific phrases and use those for voice signature authentication. Passive voice biometrics allow contacts to register their unique voiceprint and use their voiceprint to authenticate with any voice input that meets sufficient length requirements for authentication.
*   Maintain the 
    [application integration](https://docs.aws.amazon.com/connect/latest/adminguide/app-integration.html) 
    section in the Amazon Connect console for whitelisting any third-party application or integration points and remove unused endpoints.

Send only the data necessary to meet minimum requirements to external systems that handle sensitive data. For example, if you only have one business unit using your call recording analytics solution, you can set an AWS Lambda trigger in your Amazon S3 bucket to 
[process Contact Trace Records](https://aws.amazon.com/quickstart/connect/data-streaming/), check for the business unit’s specific queues in the 
[CTR data](https://docs.aws.amazon.com/connect/latest/adminguide/ctr-data-model.html), and if it is a queue that belongs to the unit, send only that call recording to the external solution. With this approach, you only send the data necessary and avoid the cost and overhead associated with processing unnecessary recordings.  
  

* * *

 **Attachments:** 


[Amazon%20Connect%20Security%20Vectors.pptx](/.attachments/DK-MobilizeforConnect/Amazon%20Connect%20Security%20Vectors.pptx)

[IAM%20Connect%20Personas.pptx](/.attachments/DK-MobilizeforConnect/IAM%20Connect%20Personas.pptx)

[image2020-12-17_0-16-36.png](/.attachments/DK-MobilizeforConnect/image2020-12-17_0-16-36.png)

[image2020-12-17_1-12-13.png](/.attachments/DK-MobilizeforConnect/image2020-12-17_1-12-13.png)

[image2020-12-17_1-26-45.png](/.attachments/DK-MobilizeforConnect/image2020-12-17_1-26-45.png)

[image2020-12-17_1-28-32.png](/.attachments/DK-MobilizeforConnect/image2020-12-17_1-28-32.png)
