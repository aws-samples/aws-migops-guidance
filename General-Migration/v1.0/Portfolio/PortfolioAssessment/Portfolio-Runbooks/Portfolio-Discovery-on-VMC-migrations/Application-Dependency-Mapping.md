  

This page illustrates how vRealize Network Insight provides application dependencies mapping via auto discovery and the inbound and outbound dependencies between the applications running on the virtual machine in your environment. Once discovered, these can then be monitored and managed not only at the virtual infrastructure and the OS level, but at the application level as-well providing you with critical business service context when problems arise.  vRNI can be an effective tool for re-locating VMWare-heavy portfolios to VMC but can also be utilized to migrate portfolios with other disposition categories.

Utilizing vRNI for Portfolio Discovery and Analysis
---------------------------------------------------

  

### Creating Application groups automatically by Flow Based Application Discovery

Flow-Based Application Discovery uses Machine Learning algorithms to determine application boundaries by doing connected components & outlier detection, and clustering of the VMs that exhibit related network flow behavior.

 ![](/.attachments/DK-Portfolio/image-20200614-190826.png)

The only requirement to generate a list of discovered applications on VMs is to have network flows coming in for a period of time (i.e., one week to get a good view). You can scope the discovery to single out a specific vSphere Cluster, or vCenter, AWS or Azure account, and more. Once the discovery is running, it’ll continuously look at the incoming network flows and update the discovered applications list. That’s all there is to it!

 ![](/.attachments/DK-Portfolio/image-20200614-190706.png)

### Creating Application groups using naming convention

When your workloads have a consistent naming convention, Network Insight can also pick out the application and tier name from the name of the VM or EC2 instance itself, using a regular expression (or regexp).

 ![](/.attachments/DK-Portfolio/image-20200614-191026.png)

### Creating Application groups through vRNI Console

If you perform a search such as “Flow where application = ‘MyApplication123” group by Source Application”  you will be able to see all of the flows to and from this ‘MyApplication123’ grouped by the source application of the traffic.  You can do the same with Destination Application as well.   Pairing this with “order by sum(bytes)”.  You would be able to see the total amount of traffic to and from your application by source and destination application which should help with deciding which applications to move with one another in the same wave.

1.  In the vRNI Console, navigate to “Applications”
    
2.  Click “Add Application”
    
3.  Input “Application Name”, “Tier”, and populate a list of virtual machines or physical IP addresses
    

### Creating Application groups with PowerShell

1.  Create application-bulk-import.csv
    
    1.  Use data from ServiceNOW export. “Business Service” will be used as “App” name.
        
2.  Generate Token in vRNI console
    
    1.  User Settings > My Account > API Token > Generate Token
        
3.  Install PowerShell 7 and use this [script](https://github.com/PowervRNI/powervrni)
    
    1.  PS C:\\> iex "& { $(irm [https://aka.ms/install-powershell.ps1](https://aka.ms/install-powershell.ps1)) } -UseMSI"
        
    2.  PS C:\\> Install-Module PowervRNI
        
    3.  PS C:\\> Import-Module PowervRNI
        
4.  Connect to vRNI
    
    1.  PS C:\\> Connect-NIServer
        
        1.  \> Input API Token
            
5.  Bypass Digital Signature
    
    1.  PS C:\\> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
        
6.  Run PowerShell with CSV and convert columns to [Comma Separated List](https://convert.town/column-to-comma-separated-list)
    
    1.  PS C:\\> .\\application-bulk-import.ps1 -ApplicationsCSV application-bulk-import.csv
        

*   Convert Column to Comma Separated List: [https://convert.town/column-to-comma-separated-list](https://convert.town/column-to-comma-separated-list)
    

Other Uses
----------

vRealize Network Insight Tool is a resourceful tool with has several use cases:

### Plan Application Security

The security planner (donut) will show all incoming and outgoing connections. The idea is to discover applications using the tags, naming convention, and CMDB sources. Considering these sources are almost always incomplete (it's typically manual work to update the CMDB), vRNI can be used to complete and validate the discovery. If you group by VM or application, and look at the connections, anything that you've missed from the CMDB, tags, or naming convention discovery, will be shown - and you can update the CMDB from it.

 ![](/.attachments/DK-Portfolio/image-20200614-191943.png)

  

### Troubleshoot and Audit virtual environments

Network Insight offers rich traffic analytics, for determining where there are network security and segmentation weaknesses within vSphere infrastructures. Network Insight leverages the rich metadata from NSX and provides real-time metrics and analytics. Including details of virtual machines, network streams, overlay-to-underlay mappings, and firewall rules. All within the context of an application-centric approach. By correlating the cross-domain data, operations teams have full context and visibility of traffic flows while monitoring and troubleshooting issues. Network Insight can deliver detailed reports on port flow, routing information, micro-segmentation setup and nesting. You can also report on all services in a VLAN, the amount of traffic produced  and top consumers on that VLAN. So any information needed for smooth operation of your physical or virtual network, Network Insight can deliver.

 **Attachments:** 


[image-20200613-160554.png](/.attachments/DK-Portfolio/image-20200613-160554.png)

[image-20200613-160939.png](/.attachments/DK-Portfolio/image-20200613-160939.png)

[image-20200614-190636.png](/.attachments/DK-Portfolio/image-20200614-190636.png)

[image-20200614-190706.png](/.attachments/DK-Portfolio/image-20200614-190706.png)

[image-20200614-190826.png](/.attachments/DK-Portfolio/image-20200614-190826.png)

[image-20200614-191026.png](/.attachments/DK-Portfolio/image-20200614-191026.png)

[image-20200614-191943.png](/.attachments/DK-Portfolio/image-20200614-191943.png)
