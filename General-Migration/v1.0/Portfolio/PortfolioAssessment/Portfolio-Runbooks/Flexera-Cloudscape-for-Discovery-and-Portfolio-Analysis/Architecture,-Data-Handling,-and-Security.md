  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

**RISC Networks Architecture**
------------------------------

Data is collected by the RN150 at the client location and periodically exported, encrypted, and securely transmitted via TLS to the RISC Networks Secure Cloud Environment (SCE) which is the data repository for the engagement. The data is then accessed by browsing to 
[riscnetworks.com](http://riscnetworks.com/) 
and logging in to the assessment portal.

**RN150 Virtual Appliance Security**
------------------------------------

### Advanced Operating System

The virtual appliance runs an advanced proprietary embedded operating system. This system was developed based on the widely adopted 2.6 Linux Kernel. No access to the appliance is allowed with any protocol with the exception of a RISC Networks management session and those connections initiated by the appliance itself. SSH and ICMP are allowed but are used solely for connectivity testing and troubleshooting. Technology built into RISC Networks’ system allows for a stateful operating system on the virtual appliance for the duration of the assessment. For this reason it is recommended that the virtual appliance be deleted at the successful completion of an assessment following the customer’s process for data handling and deletion.

### Encrypted Credentials

Customer security and the proper handling of network credentials are of the utmost importance to RISC Networks as well our partners and customers. To guarantee this security, RISC Networks has implemented the following features with regards to handling credentials:

*   Credentials are encrypted via AES-256 immediately upon being entered through the appliance web interface.
    
*   Credentials remain encrypted on the appliance for the duration of the assessment and will be deleted at the time the appliance image is delete from memory.
    
*   Credentials are NEVER uploaded to RISC Networks’ SCE.
    
*   RISC Networks delivery engineers never know or have access to the credentials used to bootstrap the appliance.
    

### Data Handling and Storage

All data is uploaded from the virtual appliance to the RISC Networks SCE using 256-bit TLSv1.2 encryption (AES-256). Before being uploaded, the raw data is encrypted at rest using AES-256 with a 2048-bit asymmetric public key (RSA-2048). Data uploads will occur on regular intervals in order to limit the upload size and are encrypted at rest in a secure repository that is not directly accessible from the internet.

The encrypted raw data is accessed by the RISC Networks’ platform and is decrypted, stored in transient database instances and accessed for report generation. Final reports are placed into storage and accessible only through the RISC Networks secure web portal for download by customers and partners.

Raw customer assessment data is held in RISC Networks’ SCE for a period of up to 
**35** 
days past the subscription end date. After the subscription expires, the data is deleted and the storage device that data was stored on returns to the pool of data storage available for other RISC Networks’ engagements. When a storage device has reached the end of its useful life, procedures include a decommissioning process that is designed to ensure customer data are not exposed to unauthorized individuals. RISC Networks storage device are decommissioned using the techniques detailed in DoD 5220.22-M (“National Industrial Security Program Operating Manual “) or NIST 800-88 (“Guidelines for Media Sanitization”) to destroy data as part of the decommissioning process. If a hardware device is unable to be decommissioned using these procedures the device will be degaussed or physically destroyed in accordance with industry-standard practices.

#### HealthCheck

For customers utilizing our HealthCheck product, raw customer data is held in RISC Networks SCE for a period of 
**90** 
days after the assessment has ended. After 
**90** 
days, the data is deleted and the storage device that data was stored on returns to the pool of data storage available for other RISC Networks engagements. When a storage device has reached the end of its useful life, procedures include a decommissioning process that is designed to ensure customer data are not exposed to unauthorized individuals. RISC Networks storage device are decommissioned using the techniques detailed in DoD 5220.22-M (“National Industrial Security Program Operating Manual “) or NIST 800-88 (“Guidelines for Media Sanitization”) to destroy data as part of the decommissioning process. If a hardware device is unable to be decommissioned using these procedures the device will be degaussed or physically destroyed in accordance with industry-standard practices

  

**Data confidentiality and compliance**
---------------------------------------

Privacy and security of Customer’s information, including personal data, are a primary concern for RISC Networks. RISC Networks’ data centers adhere to strict regulatory compliance standards such as:

*   PCI DSS Level 1
    
*   SAS 70
    
*   ISO 27001
    

At the end of any engagement, RISC Networks anonymizes data for aggregation reporting.

RISC Networks does not collect personal user data such as:

*   User logins or passwords
    
*   Data Files (office documents, text files, etc)
    
*   Email Files
    
*   Database Files
    
*   Any files containing user information
    
*   Application payload information
    

To the extent that any particular engagement requires the processing of personal data in the EU and their subsequent transfer outside of the EU, RISC Networks, will, as a data processor, upon request, enter into the EU Standard Contractual Clauses for the transfer of personal data to third countries. In addition, RISC Networks is classified as a “Data Processor” under EU privacy laws and shall act only on instructions from its Customer and will have adequate technical and organizational security measures in relation to the processing of any personal data.

 **Attachments:** 

