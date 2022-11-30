  

  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines Security Groups and Network Access Control Lists which will be deployed in AWS accounts. It is Well-Architected best practice to define network protection requirements, to control traffic at all layers and to limit the exposure of workloads to the internet and internal networks by only allowing the minimum required access. \[Customer\] will use Security Groups as virtual firewalls to control network access to AWS resources. Network Access List will be used to explicitly block malicious traffic. 

AWS SGs/NACLs provide the following capabilities and benefits:

1.  Security Groups act as stateful firewalls and use connection tracking to track information about traffic to and from the instances.
2.  Security group rules are always permissive and allow to control access based on IP, protocol, and port numbers.
3.  Network ACLs are stateless and can either allow or deny traffic.
4.  Network ACLs allow to control access based on IP, protocol, and port numbers.

  

**Implementation**
------------------

#### Naming Convention

SG: <Namespace>-sg-<function>-<semantics> (<semantics> is optional)

NACL: <Namespace>-nacl-<function>-<semantics> (<semantics> is optional)

#### Global Security Groups

Global security groups can be shared among multiple resources and are designed to address most common access requirements.

|   **Purpose**   |   **SG Name**   |   **Source**   |   **Protocol**   |   **Port Range**   |
| --- | --- | --- | --- | --- |
|   SSH access to EC2 instances   |   its-sg-remote-linux   |   \[Customer\] corp space   |   TCP   |   22   |
|   RDP access to EC2 instances   |   its-sg-remote-windows   |   \[Customer\] corp space   |   TCP   |   3389  445  139  5985   |
|   Isolation for contaminated EC2 instances   |   its-sg-isolated   |   N/A   |   N/A   |   N/A   |
|   Common-Windows(CheckMK, WMI,Nessus)   |   its-sg-common-windows   |   \[Customer\] corp space  \[Customer\] Shared-Services account space   |   TCP   |         |
|   Common-Linux(CheckMK,Nessus)   |   its-sg-common-linux   |   \[Customer\] corp space  \[Customer\] Shared-Services account space   |   TCP   |     |
|   Commvault Agent  \*could be part of Common   |   its-sg-commclient   |   Commvault Server SG group or \[Customer\] corp space   |   TCP   |   8400  8403   |

#### Applications Security Groups

Security Groups will be used to control access to all applications and access rules will be developed based on the specific needs of the applications.

Template:

Inbound

|   **Purpose**   |   **SG Name (example)**   |   **Source**   |   **Protocol**   |   **Port Range**   |
| --- | --- | --- | --- | --- |
|   Internet facing load balancer   |   its-sg-banner-weblb   |   0.0.0.0/0   |   TCP   |   443   |
|   its-sg-banner-weblb   |   \[Customer\] internal space   |   TCP   |   80/443   |
|   Internet facing web server (behind LB)   |   its-sg-banner-instance   |   Bastion Host SG  Internet LB SG   |   TCP  TCP   |   22/3389  8080   |
|   Internal load balancer   |   its-sg-banner-applb   |   Web Server SG   |   TCP   |   80/443   |
|   Internal application servers   |   its-sg-app1-instance   |   Bastion Host SG  Internal LB SG   |   TCP  TCP   |   22/3389  8080   |
|   Internal databases   |   its-sg-app1-rds   |   App Servers SG   |   TCP   |   3306   |
|   Internal services   |   its-sg-tenable-instance   |   \[Customer\] internal space   |   TCP   |   443   |
|   its-sg-ldap-instance   |   \[Customer\] internal space   |   TCP   |   389   |
|   its-sg-backup-instance   |   Instance SG   |   TCP   |   8400,8401,8403   |
|   Bastion host   |   its-sg-bastion-instance   |   \[Customer\] public space   |   TCP   |   22/3389   |

By default, SG Outbound rules allow All traffic.

#### Network Access Lists

Initially, NACLs will be used to explicitly block specific traffic on a subnet level in cases such as:

*   \[Customer\] have identified Internet IP addresses or ranges that are unwanted or potentially abusive;
*   \[Customer\] needs to block malicious traffic during an active security incident;
*   \[Customer\] needs to explicitly deny traffic to a sensitive subnet.

Template:

Inbound/Outbound

|   **Purpose**   |   **NACL Name (example)**   |   **Rule #**   |   **Source/Destination**   |   **Protocol**   |   **Port**   |   **Allow/Deny**   |
| --- | --- | --- | --- | --- | --- | --- |
|   Block Known Malicious IPs   |   its-nacl-publicsubnet   |   100   |   Malicious IP   |   All   |   All   |   Deny   |
|   1000   |   0.0.0.0/0   |   All   |   All   |   Allow   |
|   \*   |   0.0.0.0/0   |   All   |   All   |   Deny   |

 **Attachments:** 

