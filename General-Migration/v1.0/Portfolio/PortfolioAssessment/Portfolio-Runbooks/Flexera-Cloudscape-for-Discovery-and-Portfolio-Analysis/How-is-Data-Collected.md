  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

This page includes links that require a login to the RISC Portal. Please notify the Portfolio Work Stream Lead and/or EM for this engagement to request access.

How We Collect
--------------

The following page outlines the process the RISC Networks RN150 virtual appliance follows once a customer has deployed the appliance and begun the first scan.

The RN150 collects data in three distinct stages: Discovery, Inventory, and Performance. The details of each of these stages are below. For information on what data is collected at each stage please see ["What We Collect"](https://documentation.riscnetworks.com/overview/what-we-collect)

 ![](/.attachments/DK-Portfolio/Cloudscape_DataIngest.png)

  

Discovery Stage
---------------

The virtual appliance performs network discovery using standard network mapping software. The virtual appliance will only scan the subnets that are provided into the RN150 virtual appliance by the Customer and/or Partner. This stage of the Analytics engagement is designed to introduce minimal amounts of traffic onto the network and is therefore rate limited. A class B subnet typically takes about 2.5 hours to scan.

During this stage the appliance will perform an ICMP sweep on the input subnets and then will perform a select port scan on those IPs that respond to ping. If a device is found to have an open port corresponding to one of our credential types we will then attempt to access the device given the provided credentials. The RN150 will cycle through relevant credentials until it makes a successful match or fails entirely. All devices that respond to ping and are successfully accessed via the credentials are considering "Interesting Devices." This ends the discovery stage.

Inventory Stage
---------------

During this stage the appliance revisits those "Interesting Devices" determined during the Discovery Stage using the matched credentials to gather workload specific data. All workload specific data is then compressed, encrypted, and uploaded via a secure SSL connection to the RISC Networks’ SCE. At the end of the inventory phase a populated asset report and licensing page will be available in the RISC Networks portal. The user can then select devices within the licensing page that will move on to the Performance Stage. This ends the Inventory Stage.

Performance Phase
-----------------

**Process:**

Once devices have been licensed within the portal performance collection occurs via any matched credential type. Performance statistics are accessed at an interval of no greater than 1 sampling every 5 minute interval. During this stage the RN150 virtual appliance sends regular uploads to the RISC Networks’ SCE for processing and access within the portal. The upload frequency and size is determined algorithmically to limit impact on the host network. The performance stage continues as long as the partner/customer has an active subscription and has devices licensed.

For information on what data is collected at each stage please see ["What We Collect"](https://documentation.riscnetworks.com/overview/what-we-collect)

Collection Specifics
--------------------

  
More detailed technical descriptions of some of our collection methods can be found on the following links:

*   [SSH Collection Module](https://documentation.riscnetworks.com/overview/how-we-collect/ssh-collection-module)
    
*   [Database Module - Preview](https://documentation.riscnetworks.com/overview/how-we-collect/database-module)
    
*   [Windows Collection Module](https://documentation.riscnetworks.com/overview/how-we-collect/windows-collection-module)
    
*   [Load Balancers](https://documentation.riscnetworks.com/overview/how-we-collect/load-balancers)
    
*   [Performance Counter Disambiguation](https://documentation.riscnetworks.com/overview/how-we-collect/performance-counter-disambiguation)

 **Attachments:** 


[Cloudscape_DataIngest.png](/.attachments/DK-Portfolio/Cloudscape_DataIngest.png)
