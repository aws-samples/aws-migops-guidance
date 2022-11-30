  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines standard technical and business controls that \[Customer\] has established to support an effective incident response and security operations in the AWS cloud. It outlines incident response best practices aligned to the Well-Architected Framework including: defining an investigation process, identifying key personnel and external resources, tooling, and forensics capabilities.

The initial phase of an Incident Response process involves establishing and training an incident response team, and acquiring the necessary tools and resources. During preparation, the organization also attempts to limit the number of incidents that will occur by selecting and implementing a set of controls based on the results of risk assessments.

The following processes and procedures should be in place for an effective incident response:

1.  24×7 security monitoring to ensure that security events are detected and addressed in a timely manner.
2.  Security awareness training to ensure all stakeholders cooperate and escalate to maintain an agile, high-responsive security posture.
3.  Defined roles and responsibilities and escalation procedures to ensure all responsible, accountable, consulted, or kept informed parties are involved at proper stages of an incident.
4.  Incident response procedures and runbooks to ensure reliable and consistent responses.
5.  Incident response training and simulations to reduce dependency and decrease response time.

The following technical capabilities should be in place for an effective incident response:

1.  Account onboarding and readiness - each account is required to meet a baseline consisting of the minimum set of parameters that will allow \[Customer\] security team to effectively respond to potential incidents. The team responsible for accounts provisioning ensures that the following is in place:
    1.  Designated security contact (Email distribution list) to ensure that AWS security notification emails reach appropriate teams within the company;
    2.  Access to AWS accounts and services for \[Customer\] security teams to be able to investigate and respond to incidents;
    3.  Logging capabilities to ensure successful investigation, eradication, recovery, and root cause analysis;
    4.  Detective capabilities to automatically identify deviations from the established baseline and to detect security incidents.
2.  Incident Response Toolkit - some of incident response activities might include analysis of disk images , file systems, RAM dumps, or other artifacts that are involved in an incident. \[Customer\] security team is responsible for readiness from a tooling perspective to be able to quickly and effectively deal with any incident report:
    1.  Forensics workstation AMI and deployment template to ensure fast investigation and response;
    2.  Mechanisms that programmatically triage and respond to common situations to minimize human interaction and decrease time between detection and response.

Security incident detection and notification can come from a variety of sources:

1.  AWS Outreach.

AWS Abuse or DRT (DDoS Response) teams can use AWS Premium Support team as a communication channel with customers if abusive or malicious activity is observed.

Abuse activities are externally observed behaviors of AWS customers' instances or other resources that are malicious, offensive, illegal, or could harm other internet sites. AWS detects abuse activities in customers' resources using mechanisms such as AWS internal event monitoring, external security intelligence against AWS network space, Internet abuse complaints against AWS resources.

AWS abuse response team aggressively monitors and shuts down unauthorized activity running on AWS. AWS will provide all relevant information to \[Customer\] within the notification sent for the security incident. It is very important to communicate and keep AWS informed of the investigation findings, even if \[Customer\] decides to take no action on a false alarm report. This way AWS can work to continuously fine tune the alerting process and minimize false positives.

     2. \[Customer\] monitoring and threat detection systems.

AWS resource logs, AWS security monitoring services such as CloudTrail, CloudWatch, GuardDuty, and 3rd party services can be used to detect malicious activity and deviations for an established security baseline. Some of incident indicators include:

*   Unusual IAM activity
*   Unusual billing activity
*   CloudWatch alarms
*   CloudTrail logs

   3. \[Customer\] personal.

   4. \[Customer\] staff will use clear procedures for opening a security ticket or reporting a security issue to \[Customer\] security team which are described in the _\[Customer\] IT Security Incident Reporting and Response Policy(or another doc)_.

   5. A third-party organization, or an Internet security blacklisting service.

**Implementation**
------------------

#### Controls

To support efficient incident response across multiple accounts, \[Customer\] will deploy the following technical capabilities:

Designated Security Contact

Each AWS account will be configured with a security contact which represents an email distribution list with \[Customer\] network and security team members included. Distribution lists are documented _here(link to LZ Account Design page)._

\[Customer\] Security Team access to AWS accounts

Each AWS account will have federated security IAM Roles deployed for manual security auditing and incident response activities.

|   **IAM Role**   |   **Trusted Entity**   |   **IAM Permissions**   |   **Purpose**   |   **Account**   |
| --- | --- | --- | --- | --- |
|   <Namespace>-saml-securityaudit   |   Shibboleth IdP   |   SecurityAudit (AWS Managed Policy)   |   Manual security audit and investigation   |   All Accounts   |
|   <Namespace>-saml-securityresponse   |   Shibboleth IdP   |   AdministratorAccess (AWS Managed Policy)   |   Manual security response and policy enforcement   |   All Accounts   |

  

Additionally, several IAM Roles will be deployed to support automated security tasks.

|   **IAM Role**   |   **Trusted Entity**   |   **IAM Permissions**   |   **Purpose**   |   **Account**   |
| --- | --- | --- | --- | --- |
|   aws-controltower-AuditReadOnlyRole   |   Lambda   |   AWSLambdaExecute (AWS Managed Policy)  +  permissions to AssumeRole for _aws-controltower-ReadOnlyExecutionRole_ in any account   |   Lambda execution role for automated security audit and investigation   |   Audit Account   |
|   aws-controltower-AuditAdministratorRole   |   Lambda   |   AWSLambdaExecute (AWS Managed Policy)  +  permissions to AssumeRole for _aws-controltower-AdministratorExecutionRole_ in any account   |   Lambda execution role for automated security response   |   Audit Account   |
|   aws-controltower-ReadOnlyExecutionRole   |   arn:aws:iam::AuditAccountID:role/aws-controltower-AuditReadOnlyRole   |   ReadOnlyAccess (AWS Managed Policy)   |   Automated security audit and investigation role to be used by central Lambda   |   All Accounts (except master)   |
|   aws-controltower-AdministratorExecutionRole   |   arn:aws:iam::AuditAccountID:role/aws-controltower-AuditAdministratorRole   |   AdministratorAccess (AWS Managed Policy)   |   Automated security response role to be used by central Lambda   |   All Accounts (except master)   |

If \[Customer\] decides to encrypt EBS volumes and perform offline forensics from the Audit account, then KMS Customer managed CMK will have to be used to allow for cross-account sharing of encrypted volumes .

Contaminated resources and owners identification

The following tags will be used to quickly identify operational owners of affected applications and to consistently mark artifacts collected during an incident investigation for reporting and post-incident analysis.

|   **Tag Name**   |   **Tag Value (example)**   |   **Purpose**   |
| --- | --- | --- |
|   notification   |   aws-operations@\[Customer\].edu   |   Indicates a notification contact for the resource. This will be a point of contact (Email DL) for incidents or issues.   |
|   incident-response   |   quarantine:ticket-id   |   Identifies a contaminated instance and any related artifacts (disk snapshots, metadata stored in S3)   |

Logging and Monitoring

\[Customer\] will automatically benefit from AWS Shield Standard protection against Distributed Denial of Service (DDoS) while using applicable AWS services. \[Customer\] can further improve the resiliency of their applications running on AWS against DDoS attacks by implementing [DDoS-resilient reference architecture](https://aws.amazon.com/answers/networking/aws-ddos-attack-mitigation). AWS may notify \[Customer\] about abusive activities originating from \[Customer\] accounts and take responsive actions if they violate AWS Acceptable Use Policy. AWS may also notify \[Customer\] if it discovers \[Customer\] AWS accounts' credentials posted in public code repositories such as GitHub. In both scenarios, AWS will provide guidance for mitigation steps.

\[Customer\] will implement a solution to consolidate account and network logs as well as resources configuration history in the centralized Log Archive account. This capability will be automatically deployed to all new accounts as part of the account creation process. Logs collection and retention design can be found here (link to Log Storage and Retention Design page).

\[Customer\] will also deploy a set of monitoring capabilities across all application accounts. Security monitoring design can be found here (link to Security Monitoring Design). All security events and notifications will be streamed to the Audit account for centralized processing.

Containment

\[Customer\] will pre-deploy an isolation security group in all AWS accounts to be used to isolate a compromised EC2 instance in a timely manner.

#### Future State

1.  \[Customer\] will select_(if not yet)_ a SIEM platform for visualization and logs/event correlation capability in the future.
2.  \[Customer\] should build a base AMI (link to Forensics AMI Creation Procedure page) which will contain a set of pre-installed tools to perform forensics in the cloud. This AMI can be created in the \[Customer\] Audit account and can be used to launch a forensics workstation for offline and online forensics activities during each incident.
    
3.  \[Customer\] should create a CloudFormation template that describes a forensics environment (including the forensics workstation) and which will be used to launch the environment during an incident to facilitate fast incident response. The forensics CloudFormation template may perform the following actions once launched in a stack:
    1.  Creates a forensics instance security group:
        1.  Forensics security group should have ingress and egress rules allowing its communication with the compromised instance;
        2.  CloudFormation Forensics template can take the compromised instance isolation security group as a parameter to configure proper ingress/egress rules for the forensics instance security group.
    2.  Launches a forensics instance into the pre-deployed subnet with preconfigured AMI which has all required forensics tools installed;
    3.  Associates the forensics instance with the forensics security group.

In order to be certain that when needed, the IR environment will be ready to launch without any issues, the template should be tested to confirm that all resources are launched properly.

      4. The isolation security group can be set to allow communication with the forensic workstation’s subnet which is preconfigured in the Audit account. This way, the \[Customer\] Security team can connect to the compromised instance from the response workstation in order to perform a memory dump or collect additional evidence and artifacts as necessary. The security group should permit necessary ports used by the \[Customer\] forensics tools (e.g. TCP 4445 for Encase).

      5. \[Customer\] should execute incident response game days at least every 12 months for \[Customer\] security team to develop familiarity with the tools, processes, and technology described in this document, and have an opportunity to exercise this knowledge.

      6. \[Customer\] should improve manual incident remediation processes by programmatically automating steps in the process. After having defined the remediation pattern to an event, \[Customer\] can decompose that pattern into actionable logic, and write the code to perform the logic. Responders can then execute that code to remediate the issue. Over time, \[Customer\] can automate more and more steps, and ultimately automatically handle whole classes of common incidents. Automating containment capability aligns to Well-Architected best practices.

7. \[Customer\] should use a threat model to identify and maintain an up to date register of potential threats. This will allow Customer to prioritize their threats and adjust their security posture to respond. Customer can subscribe to threat intelligence sources, and regularly review threat intelligence information from multiple sources that are relevant to the technologies used in their workloads.

 **Attachments:** 

