  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines a strategy for managing secrets in AWS.

AWS Secrets Manager and AWS SSM Parameter Store improve the security posture by removing hard-coded credentials from applications’ source code, by not storing credentials on the instances, and by replacing them with a runtime call to the service, so that the credentials are retrieved dynamically when needed. Dynamic retrieval of the credentials also simplify their rotation.

AWS Secrets Manager provides the following capabilities and benefits:

1.  Provides scalable, hosted secrets management service with no servers to manage.
2.  Stores key-value pairs with versioning enabled.
3.  Stores values with up to 10KB in size.
4.  Enforces encryption of all values at rest with KMS and in transit with TLS.
5.  Enforces recovery window for secrets deletion.
6.  Provides native support for automatic passwords rotation for AWS RDS, DocumentDB, Redshift databases.
7.  Supports granular access control using IAM policies and Secrets resource-based policies with secrets tagging capability.

AWS SSM Parameter Store provides the following capabilities and benefits:

1.  Provides scalable, hosted secrets management service with no servers to manage.
2.  Stores configuration data and secure strings in hierarchies with versioning enabled.
3.  Stores values with up to 8KB in size (advanced tier).
4.  Protects secure strings with KMS encryption and enforces TLS for all transfers.
5.  Supports granular access control using IAM policies with parameters pathing and tagging capability.
6.  Supports parameters expiration and notification polices (advanced tier).
7.  Allows to reference AWS Secrets Manager secrets by using Parameter Store parameters.
8.  Supports integration with other Systems Manager capabilities and AWS services to retrieve secrets and configuration data from a central store.

**Implementation**
------------------

#### Services

\[Customer\] will use AWS Secrets Manager to store and protect secrets values such as database passwords, system credentials, license codes, and other values that are subject to encryption and more rigorous access controls. \[Customer\] may also utilize AWS SSM Parameter Store to store frequently referenced strings of data such as deployment configuration data, golden AMI ID, and instances bootstrapping parameters.

\[Customer\] will manage configuration parameters and secrets in accordance with their protection requirements and the size of the values to store. The decision on which service to use will be made on a case-by-case basis. The following common use cases will be present.

\[Customer\] will utilize AWS Secrets Manager for storing:

1.  AWS RDS passwords.
2.  Databases running on EC2 instances.

\[Customer\] will utilize AWS SSM Parameter Store for storing:

1.  Golden AMI ID.
2.  Configuration parameters used by CloudFormation or automation platforms.
3.  Application bootstrapping parameters.

#### Pricing Information

1.  [AWS SSM Parameter Store](https://aws.amazon.com/systems-manager/pricing)
2.  [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/pricing)

#### Future State

The following features can be considered for implementation in the future:

1.  [AWS Secrets Manager secrets rotation](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html).
2.  [Referencing AWS Secrets Manager secrets from Parameter Store parameters.](https://docs.aws.amazon.com/systems-manager/latest/userguide/integration-ps-secretsmanager.html)

 **Attachments:** 

