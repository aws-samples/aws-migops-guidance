  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines best practices and considerations for protecting your compute resources. Compute resources in your workloads require multiple layers of defense to help protect from external and internal threats. Compute resources include EC2 instances, containers, AWS Lambda functions, database services, IoT devices and more.

General recommendations:

1.  Define compute protection requirements: Define the protection controls for your compute resources to meet your organizational, legal, and compliance requirements. It will also help to identify AWS compliance resources, some of which can be found here: 
    [AWS cloud compliance](https://aws.amazon.com/compliance/?ref=wellarchitected). Research security hardening guides, settings, and tools applicable to your workload, including operating systems (Linux and Microsoft Windows), and execution environments, such as AWS Lambda. 
    _Additional resources:_ 
    [CIS Benchmark](https://www.cisecurity.org/cis-benchmarks/?ref=wellarchitected), 
    [Security category in AWS Marketplace](https://aws.amazon.com/marketplace/b/2649363011?ref_=header_nav_category_2649363011&ref=wellarchitected).
2.  Scan for and patch vulnerabilities: Frequently scan for and patch vulnerabilities in your code base and in your infrastructure to help protect against new threats. Implement file integrity controls to reduce the risk of malicious software or adversaries modifying files.
3.  Reduce attack surface: Reduce the attack surface, including hardening EC2 operating systems and configuring container and serverless resources, to help limit exposure. 
    _Additional resources:_ 
    [Securing Amazon Linux](https://www.cisecurity.org/benchmark/amazon_linux/?ref=wellarchitected), 
    [Securing Microsoft Windows Server](https://www.cisecurity.org/benchmark/microsoft_windows_server/?ref=wellarchitected), 
    [Docker Bench](https://github.com/docker/docker-bench-security?ref=wellarchitected)
4.  Implement managed services: Implement services that manage resources, such as [Amazon RDS](https://wa.aws.amazon.com/wat.concept.amazonrelationaldatabaseservice.en.html "A web service that makes it easier to set up, operate, and scale a relational database in the cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks."), [AWS Lambda](https://wa.aws.amazon.com/wat.concept.lambda.en.html "A web service that lets you run code without provisioning or managing servers. You can run code for virtually any type of application or back-end service with zero administration. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app."), and [Amazon ECS](https://wa.aws.amazon.com/wat.concept.ecs.en.html "A highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containers on a cluster of EC2 instances."), to reduce security maintenance tasks.

General Resources: 
[Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_introduction.html?ref=wellarchitected), [Securing Amazon EC2 Instances](https://aws.amazon.com/answers/security/aws-securing-ec2-instances/?ref=wellarchitected), 
[AWS Systems Manager](https://aws.amazon.com/systems-manager/?ref=wellarchitected)

AWS SSM Session Manager provides the following capabilities and benefits:

1.  Provides EC2 instances management capability through an interactive one-click browser-based shell or through the AWS CLI without the need to open inbound ports, maintain bastion hosts, or manage SSH keys.
2.  Allows to define the operation system user account that an interactive shell uses on an instance through IAM Roles tagging.
3.  Provides fully auditable logs for instance access details with AWS CloudWatch and S3.
4.  Traffic between a client and a managed instance is encrypted using TLS 1.2.
5.  Supports VPC Endpoints to limit administrative traffic to the Amazon network.

**Implementation**

#### Vulnerability scanning

Amazon Inspector will be used as a default solution for regular vulnerability scanning of AWS resources unless individual departments have already adopted other partner solutions (e.g. Qualys, Tenable, Rapid7) and have developed expertise managing those.

#### Administrative access

AWS SSM Session Manager will be used for administrative access to EC2 instances. All EC2 instances will have SSM agent installed and IAM profile associated which would have 
[required permissions](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-getting-started-instance-profile.html).

  

Other operational aspects will be covered in the Operations Workstream documentation.

#### Pricing Information

1.  [Inspector](https://aws.amazon.com/inspector/pricing/)
2.  [AWS EC2 Connect](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-connect-methods.html)
3.  [AWS Session Manager](https://aws.amazon.com/systems-manager/pricing/)

 **Attachments:** 

