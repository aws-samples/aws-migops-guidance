  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

This page includes links that require a login to the RISC Portal. Please notify the Portfolio Work Stream Lead and/or EM for this engagement to request access.

RISC Networks’ offers an optional deployment architecture that allows all customer specific data to be kept onsite or in a location of the customer’s choosing. For example, [all data collected](https://documentation.riscnetworks.com/overview/what-we-collect) by the RN150 Virtual Appliance will remain within the FlexDeploy pod at the customer site or within an environment that the customer chooses to use for data warehousing. The FlexDeploy architecture from RISC Networks consists of a separate Virtual Appliance, deployed as an OVF that houses both a data warehouse, as well as RISC Networks’ analytics engine. All customer data is processed within the pod and can be accessed by browsing to the local FlexDeploy pod IP address (e.g. [https://192.168.1.100](https://192.168.1.100)).

### What are the requirements for FlexDeploy?

A Flex Deploy pod is instantiated by deploying an OVF file into the customer’s VMware infrastructure. RISC Networks FlexDeploy is only supported on VMWare ESXi 5.0 or higher. FlexDeploy pod resource requirements are as follows:

*   4 CPU Cores (vcpus)
    
*   32 GB of Memory
    
*   1 TB of Hard Drive
    
*   1 Network Interface (100Mbps or 1Gbps)
    

In addition, the FlexDeploy pod server must have outbound Internet access for port 443 to the following:

*   **[orchestration.riscnetworks.com](http://orchestration.riscnetworks.com)** ( 34.192.184.110, 34.192.195.90 )
    
*   **[initial.riscnetworks.com](http://initial.riscnetworks.com)** ( 34.192.43.78, 34.192.198.28 )
    
*   **[app1.riscnetworks.com](http://app1.riscnetworks.com)** ( 34.192.198.73 )
    

### Why does the FlexDeploy pod need Internet Access?

All customer specific data is securely kept on the local FlexDeploy pod (FDP). Only orchestration, authentication, and licensing information is transmitted to the RISC Networks Secure Cloud Environment (SCE). All communication from the FDP to the RISC Networks SCE is handled via SSL Encrypted HTTPS web service calls. No inbound connectivity is required. The FDP uses the secure web service calls to perform the following functions:

*   Log users into the appliance and verify their entitlement
    
*   Download security updates and runtime code
    
*   Validate entitlement for device counts and licensing
    
*   Communicate the health of the FDP to the RISC SCE for issue notification
    
*   Facilitate [advanced debugging and troubleshooting](https://documentation.riscnetworks.com/overview/architecture%252C-data-handling%252C-and-security/advanced-debugging) (requires customer enablement)
    

### FlexDeploy Technical Architecture

The FlexDeploy pod (FDP) consists of a collapsed storage, analysis, and presentation layer. In RISC Networks cloud based delivery model, these are separate operational units. When run onsite, they are combined into a single entity. All communication between the on-premise RN150 and the on-premise FDP is conducted via HTTPS. Periodically, the RN150 will upload data to the FDP for processing. The upload frequency and size is determined algorithmically to limit impact on the host network. The uploaded data is stored in the FDP until the data processing service is notified and begins to process the data. Processing of the data occurs on the FDP through a number of analytics engines. Once processed, the data is made available in the FlexDeploy database, which is accessible through the FDP web interface. At no time does any customer specific environment data leave the FlexDeploy pod.

### Customer Responsibilities for FlexDeploy

Because RISC Networks does not have access to the FlexDeploy pod (FDP), we are unable to verify and validate that the underlying VMware infrastructure is properly configured. The customer is responsible for ensuring that the VMware host has adequate CPU/Memory/Disk resources and that the FDP is properly backed up and available for access. Customers who do not wish to handle this responsibility should consider using RISC Networks’ secure cloud based delivery.  
In addition, while RISC Networks has implemented technical controls to restrict the leakage of data from the FDP out of the customer environment, RISC Networks can not control access to the FDP itself. The restriction of access to the pod itself is the responsibility of the customer. The destruction of the FDP is also the responsibility of the customer should they choose to stop using the RISC Networks platform. RISC Networks is not responsible for the following data leakage events/challenges :

*   Restricting physical or logical access to the FlexDeploy pod
    
*   Data Exported from the system via the web interface of the FlexDeploy pod
    
*   Failure to properly destroy the FlexDeploy pod VM at the conclusion of use of the RISC Networks platform

 **Attachments:** 

