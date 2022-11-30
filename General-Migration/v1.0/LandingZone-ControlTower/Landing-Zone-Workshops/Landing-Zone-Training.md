The AWS Control Tower and Ozone are Landing Zone solutions that helps customers quickly set up a baseline AWS environment with multi-account architecture, identity and access management, governance, data security, network design, and logging. These solutions can save customers time by automating the set-up of their environment in line with AWS best practice recommendations. 

Presentation
============

This Tech Talk we will review the account best practices and explain what the AWS Landing Zone solution can set up for customers within just a few hours.

Slides
======

 [AWS%20Control%20Tower%20First%20Call%20Deck%20-%20Mar2020.pdf](/.attachments/DK-LandingZone-ControlTower/AWS%20Control%20Tower%20First%20Call%20Deck%20-%20Mar2020.pdf)

  

Ozone Landing Zone Overview
===========================

Before starting the onboarding process, it is important to understand the baseline architecture, or landing zone, that the Ozone AWS Landing Zone creates on your behalf, and its components and functions. Ozone multi-account landing zone is a multi-account architecture that is built on top of AWS Control Tower. It is pre-configured with the infrastructure to facilitate authentication, security, networking, and logging where the core infrastructure is fully managed by AWS. A typical Ozone multi-account landing zone's architecture resembles the following diagram. Customer workloads will be deployed into customer-managed accounts under a separate OU structure than the core set of account.

[ozone-core-lz](/.attachments/DK-LandingZone-ControlTower/ozone-core-lz.drawio)
[ozone-core-lz](/.attachments/DK-LandingZone-ControlTower/ozone-core-lz.drawio)

  

AWS Control Tower compared to AWS Ozone
=======================================

The chart below provides a high-level comparison between AWS Control Tower and AWS Ozone.

|   **Foundational Architecture**   |   **AWS Control Tower**   |   **AWS Ozone**   |
| --- | --- | --- |
|   **Multi-Account structure - Pre-defined foundational multi-account structure following best practices**   |   Y   |   Y   |
|   **Automated deployment - automate the creation of the multi-account environment**   |   Y   |   Y   |
|   **Management Account - provides the ability to create and financially manage member accounts**   |   Y   |   Y   |
|   **Preventative & Detective Guardrails - prepackaged governance rules for security, operations, and compliance**   |   Y   |   Y   |
|   **Logging - centralized copies of log files from all accounts**   |   Y   |   Y   |
|   **Cross-account access - provide least-privilege, individual access to accounts**   |   Y   |   Y   |
|   **Fully automated change pipeline tooling - pipeline to build, test, and deploy changes in the foundational components**   |   Y   |   Y   |
|   **Multiple OUs - support OUs to organize and apply policies**   |   Y   |   Y   |
|   **Nested OUs**   |   |   Y   |
|   **Networking - preconfigured centralized networking hub between VPCs, WAN, and egress**   |   |   Y   |
|   **Tooling - ability to leverage customer toolchains (chef, puppet, Ansiible, …)**   |   Y   |   Y   |
|   **Fully-operated core accounts - operational management of the core set of accounts (non-workload accounts) (patch, backup, monitoring, incident mgmt)**   |   |   Y   |

 **Attachments:** 


[AWS%20Control%20Tower%20First%20Call%20Deck%20-%20Mar2020.pdf](/.attachments/DK-LandingZone-ControlTower/AWS%20Control%20Tower%20First%20Call%20Deck%20-%20Mar2020.pdf)

[AWS-ControlTower_Overview.pdf](/.attachments/DK-LandingZone-ControlTower/AWS-ControlTower_Overview.pdf)

[ozone-core-lz.drawio](/.attachments/DK-LandingZone-ControlTower/ozone-core-lz.drawio)

[ozone-core-lz.drawio.png](/.attachments/DK-LandingZone-ControlTower/ozone-core-lz.drawio.png)

[~drawio~5db8728fa766000da47cc72d~ozone-core-lz.drawio.tmp](/.attachments/DK-LandingZone-ControlTower/~drawio~5db8728fa766000da47cc72d~ozone-core-lz.drawio.tmp)
