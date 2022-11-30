  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Summary
-------

This checklist contains a list of tasks to be completed once all the virtual machines are migrated into VMware Cloud on AWS.

Checklist
---------

-  Ping sweep the vLANs to ensure that no virtual machine is left behind -  Review all the servers that are in on-premises clusters and compare it with the list of servers for migration to assimilate a list of servers that may not be found in the customer's CMDB -  Un-extend previously stretched vLAN networks -  Delete VM copies left behind on-premises after validating -  Deployment of load balancers -  Update Firewall configuration -  Explore Backup and restore options -  Enable Monitoring and logging for virtual machines and resources spinned up in the connected account -  Configure network post-migration -  Review Disaster Recovery options -  Determine vCenter roles and permissions (especially for SRE and Support teams) -  Determine connected VPC roles and policies

Pre-flight and Post-flight checkoff
-----------------------------------

Use the below table to aggregate information from the application development teams prior to and after migration of workloads to VMware on AWS

*   **Virtual Machine Host Name:** This is the host name for the virtual machine. You can also use IP address to track servers.
*   **Application Name:** This would be the application name that resides in the server.
*   **Application Owner:** Name of the application owner who will test and verify the functionality of the virtual machine
*   **Sync Started:** This would be the data and time when the replication of data started
*   **Pre-Flight Sign Off:** The application team signs off prior to us migrating the virtual machine into VMware on AWS and logs all the known issues
*   **Migrated to VMware on AWS:** This is the exact date and time when the server in the on-premises environment is turned off and the VM in the VMC environment is turned off after performing another delta sync of data
*   **Post-Flight Sign Off:** This is the date when then application team signs off after verifying the server's functionality in the new AWS environment

  

| Virtual Machine Host name | Application Name | Application Owner | Sync Started | Pre-Flight SignOff | Migrated to VMware on AWS | Post Flight Sign-Off |
| --- | --- | --- | --- | --- | --- | --- |
|   CCISALES01   |   SalesApp   |   @John Smith   |   May 11, 2020   |   @John Smith  May 8, 2020   Issue: front end is up App server is down   |   May 15, 2020   |   @John Smith  May 16, 2020  Same issue   |
|     |     |     |     |     |     |     |
|     |     |     |     |     |     |     |

 **Attachments:** 

