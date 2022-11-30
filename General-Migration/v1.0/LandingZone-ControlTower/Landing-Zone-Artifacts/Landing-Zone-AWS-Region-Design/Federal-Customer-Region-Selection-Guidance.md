|    |    |    |    |
| --- | --- | --- | --- |

* * *

[[_TOC_]]

* * *

Executive Summary
=================

Amazon Web Services (AWS) offers its federal customers a broad range of fully accredited environments that span common requirements for storing and processing publicly releasable data all the way through Top Secret. However, the majority of agencies are minimizing cost (up to 23% savings) and maximizing value by leveraging AWS' commercial regions (US East and West) to satisfy the needs of FedRAMP Moderate data storage and processing. For FedRAMP High workload needs, GovCloud can be used. This paper offers guidance on choosing the appropriate AWS region; AWS commercial regions and/or AWS GovCloud.

Considerations for choosing between AWS commercial and GovCloud
===============================================================

Choosing the appropriate region(s) should begin with asking the fundamental question of “does my agency's data require FedRAMP Moderate or FedRAMP High?” Examples of data sets generally requiring FedRAMP High are the DOJ’s Criminal Justice Information Systems (CJIS) Security Policy, U.S. International Traffic in Arms Regulations (ITAR), Export Administration Regulations (EAR), and Department of Defense (DoD) Cloud Computing Security Requirements Guide (SRG) for Impact Levels 2, 4 and 5. To accommodate the FedRAMP High baseline, AWS' GovCloud (US) gives vetted government customers and their partners the flexibility to architect secure cloud solutions that comply with aforementioned compliance regimes.

It’s noteworthy that your decision on choosing a region need not be binary. Several agencies in Federal, Department of Defense (DoD), and the Intelligence Community (IC) spaces commonly choose to leverage both AWS Commercial regions and GovCloud, allowing the requirement to drive the decision. Using both regions in some cases may require some duplicative infrastructure such as Active Directory (AD), however the cost impact should be minimal. Operating across both regions may increase technical complexity, as not all services that are available in AWS' commercial regions can be found in GovCloud. Moreover, there are several deployment and automation solutions which are only available in the AWS commercial regions, such as Landing Zone 3.0, which enables automated account creation following AWS best practices.

Examples of agencies who opted to anchor their cloud deployments in the AWS commercial (US East and West) regions include the National Aeronautics and Space Administration (NASA), the U.S. Department of Health and Human Services (HHS), the Centers for Medicare and Medicaid Services (CMS), the National Institutes of Health (NIH), the U.S. Citizenship and Immigration Services (USCIS), the Defense Information Systems Agency Information Assurance Support Environment (DISA IASE) to name a few. If the Customer can comfortably determine that their processing and storage compliance requirements can be satisfied by the FedRAMP Moderate baseline, then AWS commercial regions (US East and West) would be the best choice, as AWS' commercial regions offer some subtle advantages over GovCloud; See Table-1.

  

| Feature | AWS Commercial Regions | AWS GovCloud |
| --- | --- | --- |
| FedRAMP Moderate | Yes | Yes |
| FedRamp High | No | Yes |
| ITAR-compliant | No | Yes |
| Multi-factor authentication | Yes | Yes |
| Cost Differential |     | ~ +23% |
| \# Services available | ~145 | ~58 |
| FIPS 140.2 | Yes | Yes |

_Table-1 - AWS Region Comparison_

  

As the Customer continues to migrate into the public cloud, systems modernization will become something that the Customer will want to pursue. Examples of modernization include taking advantage of AWS' serverless and other fully managed services. To that end, we need to ensure we are aligning the  with AWS commercial regions as new services are typically launched in the commercial regions first, and then GovCloud. GovCloud is typically second to receive new service launches, as complying with ITAR is time consuming and something AWS takes very seriously.

Summary
=======

AWS recommends that the Customer allow requirements, data sensitivity, cost considerations (~23% greater cost in GovCloud), and operational efficiencies to drive the decision on which AWS region(s) should be used. Workloads and systems requiring the FedRAMP High baseline should consider AWS GovCloud as the first choice, however all other workloads and systems should use AWS commercial regions (East and West) under the FedRAMP Moderate baseline. Using the AWS commercial regions will offer the Customer more agility in meeting its modernization objectives – with the same level of security – and will reduce technical complexity. It's important to understand that no one AWS region is more or less secure than any other region. All of AWS’ CONUS regions are subject to annual third party compliance audits across 23 compliance regimes.

Appendix A: AWS FedRAMP Compliance
==================================

Amazon Web Services (AWS) is a Federal Risk and Authorization Management Program (FedRAMP) Compliant Cloud Service Provider. AWS provides two US-based regions to support U.S. government customers with their compliance requirements. At a high-level, these US-based regions and their impact levels are:

1.  AWS US East/West at the FedRAMP Moderate impact level.
    
2.  AWS GovCloud (US) at the FedRAMP High impact level. AWS GovCloud (US) also adheres to U.S. International Traffic in Arms Regulations (ITAR) regulations.
    

AWS US East and US West regions have been granted a Joint Authorization Board Provisional Authority-To-Operate (JAB P-ATO) and multiple Agency Authorizations (A-ATO) for moderate impact level. The services in scope of the AWS US East/West JAB P-ATO boundary at Moderate baseline security categorization can be found within AWS Services-in-Scope by Compliance Program. AWS maintains an up-to-date AWS Services-in-Scope webpage to provide customers a detailed breakdown for determining which AWS Services have been formally authorized within the AWS US East/West and AWS GovCloud (US) regions with their respective impact levels. This resource exists for AWS customers and partners to reference to ensure they build compliant workloads on top of AWS’ service offerings.

AWS has completed the testing performed by a FedRAMP accredited Third-Party Assessment Organization (3PAO) and has been granted two Agency Authority to Operate (ATOs) by the US Department of Health and Human Services (HHS) after demonstrating compliance with FedRAMP requirements at the Moderate impact level. All U.S. government agencies can leverage the AWS Agency ATO packages stored in the FedRAMP repository to evaluate AWS for their applications and workloads, provide authorizations to use AWS, and transition workloads into the AWS environment. The two FedRAMP Agency ATOs encompass all U.S. regions (the AWS US East/West regions and the AWS GovCloud (US) region).

Amazon Web Services (AWS) has been certified by Veris Group, LLC, a FedRAMP-accredited Third Party Assessment Organization (3PAO). AWS’s compliance with FedRAMP/Department of Defense Cloud Computing Security Requirements Guide (DoD SRG) requirements was validated based on testing performed against FedRAMP/DoD SRG requirements. These authorizations validate AWS’s security posture and enables AWS’s Federal customers to store, process, and protect a diverse array of sensitive government data. Please refer to the following URL for more information regarding AWS’s FedRAMP authorizations: [http://www.fedramp.gov/marketplace/compliant-systems/](http://www.fedramp.gov/marketplace/compliant-systems/).

The Federal Information Processing Standard (FIPS) Publication 140-2 is a US government security standard that specifies the security requirements for cryptographic modules protecting sensitive information. To support customers with FIPS 140-2 requirements, SSL terminations in AWS East/West and AWS GovCloud (US) operate using FIPS 140-2 validated hardware. The list of FIPS 140-2 validated endpoints is available on the FIPS Compliance overview webpage.

 **Attachments:** 

