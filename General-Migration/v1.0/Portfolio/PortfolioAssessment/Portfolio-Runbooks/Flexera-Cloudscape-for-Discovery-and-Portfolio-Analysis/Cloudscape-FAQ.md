  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

  
Q: How will the tool parse through the F5 information to get at the application dependencies?
------------------------------------------------------------------------------------------------

Cloudscape collects F5 VIP information via the SSH collector. This enables the mapping of runtime dependencies that include F5 VIP(s). Without discovering the VIPs we would see that node 1 talks to some IP (which is a VIP) and node 2 talks to some IP (which is a VIP), but you can't tell they're talking to each other via the load balancer. Application parsing  
**Reference:**  
(Add a link to the Security and Architecture page within the customer’s Confluence instance)  
**Source:**  
[https://partners.riscnetworks.com/pdf/deployment\_fundamentals/PD-LoadBalancers-300318-0948.pdf](https://partners.riscnetworks.com/pdf/deployment_fundamentals/PD-LoadBalancers-300318-0948.pdf)  
  

Q: We need architecture diagrams for how the tool is deployed across our environment. How is this tool deployed differently than AWS?
-------------------------------------------------------------------------------------------------------------------------------------

The customer deploys the RN150 virtual appliance within their data center. As the RN150 collects data, it periodically encrypts and exports that data securely via TLS to RISC networks secure cloud environment (AWS). The following pages provides more details on the deployment model, what the RN150 collects, how it collects it, and deployment requirements for it.  
**Reference:**  
(Add a link to the Security and Architecture page within the customer’s Confluence instance)  
**Source: (requires registration and login to the RISC portal)**  
[https://portal.riscnetworks.com/app/documentation/?path=/overview/](https://portal.riscnetworks.com/app/documentation/?path=/overview/)  
  

Q: SaaS and Non-SaaS option – Which option will AWS recommend for our environment? What will be the criteria for the recommendation?
------------------------------------------------------------------------------------------------------------------------------------

AWS recommend the standard Cloudscape deployment vs the Flex Deploy, unless the customer has specific compliance requirements that prevent them from using the standard deployment. The Flex Deploy requires additional setup time and upfront cost. Also, the Flex Deploy does not support connecting with API's and the ServiceNow Bi-Directional API is not available. Flex Deploy is only recommended for extreme regulation and government/GDPR compliance.  
**Reference:**  
(Add a link to the Flex Deploy page within the customer’s Confluence instance)  
**Source: (requires registration and login to the RISC portal)**  
[https://portal.riscnetworks.com/app/documentation/?path=/overview/alternate-and-additional-deployment-methods/flexdeploy/](https://portal.riscnetworks.com/app/documentation/?path=/overview/alternate-and-additional-deployment-methods/flexdeploy/)  
  

Q: Copy of the latest SOC 2 Type 2 Report
-----------------------------------------

The Cloudscape Portal is a SaaS solution built on AWS. Information and links to the AWS SOC reports can be found here:[https://aws.amazon.com/compliance/soc-faqs/](https://aws.amazon.com/compliance/soc-faqs/)  
  

Q: Clear architecture and data flow diagrams that include the specific ports and protocols necessary for SaaS (cloud) implementation
------------------------------------------------------------------------------------------------------------------------------------

Details on all data flows are included in the following section on deployment requirements.  
**Reference:**  
(Add a link to the Deployment Requirements page within the customer’s Confluence instance)  
**Source: (requires registration and login to the RISC portal)**  
[https://portal.riscnetworks.com/app/documentation/?path=/overview/deployment-requirements/](https://portal.riscnetworks.com/app/documentation/?path=/overview/deployment-requirements/)  
  

Q: Confirm that this solution does not touch application data
-------------------------------------------------------------

Please refer to the How we Collect Data, our Compliance documentation, and WMI/SSH documentation for all queries we use to take in data. No application payload information is collected, only meta-data.  
**Reference:**  
(Add a links to the pages within the customer’s Confluence instance)  
**Source: (requires registration and login to the RISC portal)**  
[https://portal.riscnetworks.com/app/documentation/?path=/overview/how-we-collect/](https://portal.riscnetworks.com/app/documentation/?path=/overview/how-we-collect/)

 **Attachments:** 

