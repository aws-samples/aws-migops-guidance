### Summary

The installation of the vRNI is fairly straightforward and involves provisioning and configuring appliances in the vCenter environment that allow analyzing the network information via traffic flows that are collected. Please review [VMware documentation](https://docs.vmware.com/en/VMware-vRealize-Network-Insight/5.2/com.vmware.vrni.install.doc/GUID-7363C8A6-7849-480C-A0AC-368C2B5CF341.html) for the most updated information.

### Workflow

[Untitled Diagram](/.attachments/DK-Portfolio/Untitled Diagram.drawio)
[Untitled Diagram](/.attachments/DK-Portfolio/Untitled Diagram.drawio)

### Detailed Overview

|   **Action**   |   **Description**   |
| --- | --- |
|   Download Network Insight Collectors   |   You can set up vRealize Network Insight collectors by importing OVA to your vCenter server.   |
|   Install sFlow Collector and add datasource   |   You can add a physical flow collector and configure the switches to push sFlow. The collector VM that is used for sFlow is a dedicated collector. It cannot be used for any other data source.  1.  In the Settings page, click Accounts and Data Sources.      2.  Click Add Source.      3.  Under Flows, click Physical Flow Collector sFlow. sFlows are accepted only on the physical collector.      4.  Enter Nickname and Notes as required.      5.  Click Submit.       Configure the switches to push the flows to the Physical Flow Collector.  *   Define the destination (Collector IP address that you added in vRealize Network Insight).      *   Set the port for the flow collector.      *   Assign poll interval.        |
|   Install NetFlow Collector and add datasource   |   You can add a physical flow collector and configure the switches to push NetFlow. The collector VM that is used for NetFlow is a dedicated collector. It cannot be used for any other data source.  1.  In the Settings page, click Accounts and Data Sources.      2.  Click Add Source.      3.  Under Flows, click Physical Flow Collector NetFlow.      4.  Enter Nickname and Notes as required.      5.  Click Submit.       Configure the switches to push the flows to the Physical Flow Collector.  *   Define the destination (Collector IP address that you added in vRealize Network Insight).      *   Set the port for the flow collector.      *   Assign poll interval.        |
|   Activate License   |   After installing the vRealize Network Insight Platform OVA, open https://<vRealize Network Insight Platform IP address>.  1.  Enter the license key received in the welcome email.      2.  For UI admin (`admin@local`) user name, set the password.      3.  Click Activate.      4.  Add the vRealize Network Insight Collector after activating the license.        |
|   Generate Shared Secret   |   You can generate and import the vRealize Network Insight collector virtual appliance. Generate a shared secret and import the vRealize Network Insight collector virtual appliance.  1.  Log into the vRealize Network Insight UI.      2.  Expand Infrastructure and Support and click Overview and Updates.      3.  Scroll down and click Add Proxy VM. The Add a new Network Insight Data Collector virtual appliance dialog appears.      4.  Click Copy to copy the shared secret from the dialog and click Done. You will require this during the deployment of vRealize Network Insight Collector OVA.        |
|   Add vCenter servers as datasource   |   1.  Click Add vCenter.      2.  Click Add new source and customize the options.      3.  Click Validate.      4.  Select Enable Netflow (IPFIX) on this vCenter to enable IPFIX.      5.  Click Submit to add the vCenter Server system. The vCenter Server systems appear on the homepage.        |
|   Analyze Traffic and Generate reports   |   You can use vRealize Network Insight to analyze flows in your datacenter. At least two hours of data collection must occur before starting the flow analysis.  1.  Specify the scope of the analysis. For example, if you are interested in flows of all virtual machines in a Cluster, select Cluster from the drop-down menu. You can alternately select all virtual machines connected to a VLAN or VXLAN.      2.  Select the entity name for which you want to analyze the flows.      3.  Select the duration and click Analyze.        |

 **Attachments:** 


[Untitled%20Diagram.drawio](/.attachments/DK-Portfolio/Untitled%20Diagram.drawio)

[Untitled%20Diagram.drawio.png](/.attachments/DK-Portfolio/Untitled%20Diagram.drawio.png)
