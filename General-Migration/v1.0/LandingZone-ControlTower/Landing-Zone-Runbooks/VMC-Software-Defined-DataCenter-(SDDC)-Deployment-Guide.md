  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

  

Summary
-------

This run book illustrates how to deploy an SDDC to host your workloads in the cloud. Please find the complete and most up-to-date information in VMware's [documentation](https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws-operations/GUID-BC0EC6C5-9283-4679-91F8-87AADFB9E116.html "https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws-operations/GUID-BC0EC6C5-9283-4679-91F8-87AADFB9E116.html").

SDDC Deployment Procedure
-------------------------

  

1.  Log in to the VMC Console at [https://vmc.vmware.com](https://vmc.vmware.com "https://vmc.vmware.com").
    

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-20_21-41-48.png)

  

2\. Click Create SDDC. Just like that, a SDDC is deployed and available complete with all infrastructure components and configuration – vSphere ESXi hypervisors, vCenter, NSX Manager, NSX Controllers, NSX Edges, and vSAN.

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-48-16.png)

  

3\. Configure SDDC properties 

*   Select the AWS region in which to deploy the SDDC. The following regions are available:
*   Select deployment options. Option Description Single Host Select this option to create Single Host Starter Configuration SDDC. Single Host Starter Configuration SDDCs expire after 30 days. For more information, see [Deploying a Single Host SDDC Starter Configuration](https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws.getting-started/GUID-D976BC01-67D7-447B-9065-19092C6FEE62.html "https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws.getting-started/GUID-D976BC01-67D7-447B-9065-19092C6FEE62.html"). Multi-Host. Select this option to create an SDDC with two or more hosts but three hosts is the default.
*   Enter a name for your SDDC. You can change this name later if you want to.
*   Select the host type. You have two options: i3 and R5. There is a new host type i3EN which has at the time this runbook was pending release.
*   If you selected R5 (EBS) hosts, select the storage capacity per host. The value you select is used for all hosts in the cluster, including any hosts you add to the cluster after creation.
*   If you are creating a multiple host SDDC, specify the initial Number of Hosts you want in the SDDC. You can add or remove hosts later if you need to.

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-9-22.png)

  

4\. Connect to an AWS account

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-56-34.png)

See [AWS VPC Configuration and Availability Requirements](https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws-operations/GUID-BC0EC6C5-9283-4679-91F8-87AADFB9E116.html#GUID-BC0EC6C5-9283-4679-91F8-87AADFB9E116__section_EDA999D3911A4B43966F305E2DA156EC) for important information about requirements for the AWS account and subnets you create in it. Option Description Skip for now If you don't have an AWS account or don't want to connect to one you have now, you can postpone this step for up to 14 days. This option is currently available for Single Host SDDCs only. Use an existing AWS account From the Choose an AWS account drop-down, select an AWS account to use an AWS account that was previously connected to another SDDC. If no accounts are listed in the drop-down, you must Connect to a new AWS account. Connect a new AWS account From the Choose an AWS account drop-down. select Connect to a new AWS account and follow the instructions on the page. The VMC Console shows the progress of the connection.

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-59-55.png)

  

5\. Verify that the SDDC has been created and connected to the AWS customer account with no errors.

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-8-44.png)

  

6\. Click NEXT to configure the Management Subnet in the SDDC. Enter an IP address range for the management subnet as a CIDR block or leave the text box blank to use the default, which is 10.2.0.0/16. You can't change these values after the SDDC has been created, so consider the following when you specify this address range:

*   Choose a range of IP addresses that does not overlap with the AWS subnet you are connecting to. If you plan to connect your SDDC to an on-premises data center, the IP address range of the subnet must be unique within your enterprise network infrastructure. It cannot overlap the IP address range of any of your on-premises networks.
*   If you are deploying a single-host SDDC, the IP address range 192.168.1.0/24 is reserved for the default compute gateway logical network of the SDDC. If you specify a management network address range that overlaps with 192.168.1.0/24, single-host SDDC creation fails. If you are deploying a multi-host SDDC, no compute gateway logical network is created during deployment, so you'll need to create one after the SDDC is deployed.The entire address range 100.64.0.0/10 (reserved for carrier-grade NAT per [RFC 6598](https://tools.ietf.org/html/rfc6598 "https://tools.ietf.org/html/rfc6598")) is reserved by VMware Cloud on AWS for internal use. You cannot access any remote (on-premises) networks in that address range from workloads in the SDDC, and you cannot you use any addresses in that range within the SDDC. In addition, CIDR blocks 10.0.0.0/15 and 172.31.0.0/16 are reserved for internal use. The management network CIDR block cannot overlap either of these ranges.
*   CIDR blocks of size 16, 20, or 23 are supported, and must be in one of the "private address space" blocks defined by [RFC 1918](https://tools.ietf.org/html/rfc1918 "https://tools.ietf.org/html/rfc1918") (10.0.0.0/8, 172.16.0.0/12, or 192.168.0.0/16). The primary factor in choosing a Management CIDR block size is the anticipated scalability requirements of the SDDC. The management CIDR block cannot be changed after the SDDC has been deployed, so a /23 block is appropriate only for SDDCs that will not require much growth in capacity. CIDR block size Number of hosts (Single AZ) Number of hosts (Multi AZ) 23 27 22 20 251 246 16 See [Configuration Maximums for VMware Cloud on AWS](https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws-operations/GUID-10A0804B-04F4-4B8A-9EBA-85169F533223.html "https://docs.vmware.com/en/VMware-Cloud-on-AWS/services/com.vmware.vmc-aws-operations/GUID-10A0804B-04F4-4B8A-9EBA-85169F533223.html").

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-0-58.png)

  

7\. Acknowledge that you understand and take responsibility for the costs you incur when you deploy an SDDC, then click DEPLOY SDDC to create the SDDC. Charges begin when you click DEPLOY SDDC. You cannot pause or cancel the deployment process after it starts. You won't be able to use the SDDC until deployment is complete. Deployment typically takes about two hours.

 ![](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-1-57.png)

 **Attachments:** 


[image2020-5-17_16-48-16.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-48-16.png)

[image2020-5-17_16-56-34.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-56-34.png)

[image2020-5-17_16-58-29.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-58-29.png)

[image2020-5-17_16-59-15.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-59-15.png)

[image2020-5-17_16-59-55.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_16-59-55.png)

[image2020-5-17_17-0-58.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-0-58.png)

[image2020-5-17_17-1-57.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-1-57.png)

[image2020-5-17_17-8-10.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-8-10.png)

[image2020-5-17_17-8-44.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-8-44.png)

[image2020-5-17_17-9-22.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-17_17-9-22.png)

[image2020-5-20_21-41-48.png](/.attachments/DK-LandingZone-ControlTower/image2020-5-20_21-41-48.png)
