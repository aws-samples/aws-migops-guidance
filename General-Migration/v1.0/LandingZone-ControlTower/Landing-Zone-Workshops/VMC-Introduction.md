  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

Agenda
------

*   VMware Cloud on AWS Overview
*   Account Structure
*   On-premises to SDDC connectivity
*   Cloud migration options
*   Demo of HCX Migration
*   Disaster Recovery
*   Pricing and Billing
*   Q&A

VMware Coud on AWS Overview
---------------------------

VMware and AWS offer organizations a faster, secure path to the cloud in a jointly engineered seamless customer experience. With VMware Cloud on AWS you can migrate data centers to the cloud for rapid datacenter evacuation, disaster recovery, and application modernization.

Account Structure
-----------------

The way the account structure is setup:

*   **VMware on AWS Shadow account:** This a dedicated AWS account to run (Software Defined Datacenter) SDDC resources which is owned and managed by VMware
*   **Customer owned AWS account:** This is owned and paid for by the customer and it provides private connectivity to the SDDC and integration to AWS services

On-premises to SDDC connectivity
--------------------------------

*   **On-premises to SDDC:** SDDC supports integration with AWS Direct Connect service to provide persistent, reliable, and low latency connection to customers’ on-premises environments. 
*   **SDDC to Connected account:** VMware Cloud on AWS enables customers to seamlessly integrate their SDDC cluster to AWS services. This is achieved by connecting the SDDC cluster to the customer’s VPC of choice. During the onboarding process, customers have the ability to choose a VPC and the subnets they want to connect to their SDDC cluster. Customers will also run an [AWS CloudFormation](https://aws.amazon.com/cloudformation/) template, which grants VMware Cloud Management Services across account roles with a managed policy.

Cloud Migration Options
-----------------------

*   **NSX Live migration with vMotion:** Can be used to migrate virtual machines in running state without downtime which can also be used for reverse migration back to on-premises. However, there are certain key requirements such as the version for the on-premises vSphere should be 6.5P03/6.7U2 (or later)
*   **VMware HCX migration:** Most commonly used migration type for bulk migration which requires the extension of networks from on-premises to VMware on Cloud. It provides an abstraction of underlying infrastructure and can also be used for reverse migration. This option is most useful to consolidate heterogeneous environments and migrate large scale workloads with lower bandwidth requirements than NSX vMotion while supporting older vSphere versions. This requires a VM power cycle.
*   **Backup and restore with partner solutions**: These options are usually for cold migration of virtual machines and have longer downtime.

Disaster Recovery
-----------------

*   **Backup and restore:** This for workloads that are not business critical. Launch another SDDC in response to a Disaster Recovery (DR) event
*   **Pilot Light:** These are for workloads that meet lower RTO and RPO requirements. Launch SDDC resources in response to a DR event
*   **Warm Standby:** These are for applications that require RTO and RPO in the order of minutes. Scale SDDC resources in response to a DR event
*   **Hot standby Active/Active:** These are for applications that require immediate and automatic failover of in SDDC. Active standby SDDC

Pricing and billing
-------------------

*   **Cost:** VMware Cloud on AWS service provides simple yet flexible options to consume VMware’s powerful software capabilities and AWS’s elastic, bare-metal infrastructure as a combined offering with support included. This offering can be purchased on-demand, or as 1-year or 3-year subscription. If you choose on-demand option, you will be billed at the end of the month in arrears and if you choose 1-year or 3-year subscription option, you can either prepay upfront or pay in monthly installments.
*   **Billing:** The customer will receive two bills - one for the VMware on AWS SDDC account billed by VMware and another for the connected account billed by AWS.

 **Attachments:** 


[image2020-5-21_11-33-53.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-21_11-33-53.png)
