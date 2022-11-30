  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Purpose
=======

This page captures the design details for the Customer's Primary and DR AWS Regions. 

AWS Regions
===========

The Customer is required to locate disaster recovery facilities at least 50 miles from the primary location. To meet this requirement, two AWS commercial regions will be used.

Initial Operational State
-------------------------

The initial operational state will include the initial Landing Zone implementation through the decommissioning of the targeted colocation facilities. AWS us-east-1 and us-west-2 regions will be used for all AWS FISMA Moderate workloads.

| Role | AWS Region | Region Selection Rationale | Degraded Modes of Operation (Failure Scenarios) |
| --- | --- | --- | --- |
| Primary Region | us-east-1 |   *   One of lowest cost regions (us-east-1, us-east-2, and us-west-2 have cost parity as of 9/3/2018) *   Current FedRAMP ATO *   ~90ms apart from us-west-2, so there is no need to split primary application operations across both regions (e.g. app1 primary us-east-1, app2 primary us-east-2, etc.) *   Includes the most services and typically one of the first regions to get new services   |   *   Server failures will be resolved in the primary region     *   Recovery Time Objective (RTO) - best effort     *   Recovery Point Objective (RPO) - 24 hours *   Application-wide failures will be resolved in the primary region with a specific:     *   Recovery Time Objective (RTO) - best effort     *   Recovery Point Objective (RPO) -   |
| DR Region | us-west-2 |   *   One of lowest cost regions (us-east-1, us-east-2, and us-west-1 have cost parity as of 9/3/2018)     *   us-west-1 is ~15% more expensive for core services like EC2 & S3 *   Current FedRAMP ATO *   ~90ms apart from us-east-1 *   Includes the most services and typically one of the first regions to get new services   |   *   AWS Region level sustained failures will be resolved in the DR region with a different set of:     *   *   Recovery Time Objective (RTO) - best effort         *   Recovery Point Objective (RPO) - 24 hours   |

References:

*    How to chose your AWS Region Wisely - [https://www.concurrencylabs.com/blog/choose-your-aws-region-wisely/](https://www.concurrencylabs.com/blog/choose-your-aws-region-wisely/)
*   AWS Inter-Region Latency - [https://www.cloudping.co/](https://www.cloudping.co/)

Long Term Operational State
---------------------------

The long-term approach will be to continue with the approach used during the Initial Operational State. This will be revisited as the Customer gets closer to completing the shutdown of both colocations.

Rationale: The two regions are ~90ms apart, so there is no need to split primary application operations across both regions (e.g. app1 primary us-east-1, app2 primary us-east-2, etc.) since ~90ms delay should not impact end user experience.

| Role | AWS Region | Region Selection Rationale | Degraded Modes of Operation (Failure Scenarios) |
| --- | --- | --- | --- |
| Primary Region | us-east-1 |   *   One of lowest cost regions (us-east-1, us-east-2, and us-west-2 have cost parity as of 9/3/2018) *   Current FedRAMP ATO *   ~90ms apart from us-west-2, so there is no need to split primary application operations across both regions (e.g. app1 primary us-east-1, app2 primary us-east-2, etc.) *   Includes the most services and typically one of the first regions to get new services   |   *   Server failures will be resolved in the primary region *   Application-wide failures will be resolved in the primary region with a specific:     *   RTO     *   RPO   |
|   DR Region  Choose one of the two regions   | us-west-2 |   *   One of lowest cost regions (us-east-1, us-east-2, and us-west-2 have cost parity as of 9/3/2018)     *   us-west-1 is ~15% more expensive for core services like EC2 & S3 *   Current FedRAMP ATO *   ~90ms apart from us-east-1 *   Includes the most services and typically one of the first regions to get new services   |   *   AWS Region level sustained failures will be resolved in the DR region with a different set of:     *   RTO     *   RPO   |
|     | or us-east-2 |   *   One of lowest cost regions (us-east-1, us-east-2, and us-west-2 have cost parity as of 9/3/2018)     *   us-west-1 is ~15% more expensive for core services like EC2 & S3 *   Under FedRAMP ATO Review *   ~16 ms apart from us-east-1 *   Cross region data transfer between us-east-1 and us-east-2 is ~50% less than between any other two regions. This with the ~16ms latency makes us-east-2 an ideal DR location that is over the 50 mile minimum limit   |     |

  

An alternative would be to separate the primary region based on the the location that is closest to the users. Since the Customer has a large number of geographically distributed facilities, and the two AWS regions are only ~90ms apart, it will be harder to justify maintaining primary operations in two regions since it will most likely not make a noticeable improvement for end users accessing the applications.

Primary region:   
—— us-east-1 for Enterprise wide applications and individual Enterprise east coast customers/facilities   
—— us-west-2 for Enterprise wide applications and individual Enterprise west coast customers/facilities   
DR region:  
—— us-west-2 for Enterprise wide applications and individual Enterprise west coast customers/facilities   
—— us-east-1 for Enterprise wide applications and individual Enterprise east coast customers/facilities

Managing Service Limits
-----------------------

Default service limits exist to prevent accidental provisioning of more resources than you need. There are also limits on how often you can call API operations to protect services from abuse. If you are using AWS Direct Connect, you have limits on the amount of data you can transfer on each connection. If you are using AWS Marketplace applications, you need to understand the limitations of the applications. If you are using third-party web services or software as a service, you also need to be aware of the limits of those services. Well-Architected best practices in reliability to consider include:

**Monitoring and managing limits:** Evaluate your potential usage, increase your regional limits appropriately, and allow planned growth in usage.

**Use automated monitoring and management of limits:** Implement tools to alert you when thresholds are being approached. You will want to use a distribution mechanism to alert a responsible group until the limit increase request can be automated.

**Accommodate fixed service limits through architecture:** Be aware of unchangeable service limits and architect around these.

**Ensure a sufficient gap between the current service limit and the maximum usage to accommodate failover:** When a resource fails it may still be counted against limits until it is successfully terminated. Ensure your limits cover the overlap of all failed resources with replacements before the failed resources are terminated. You should consider an Availability Zone failure when calculating this gap.

**Manage service limits across all relevant account and regions:** If you are using multiple AWS accounts or AWS Regions, ensure you request the same limits in all environments in which you run your production workloads.

 **Attachments:** 

