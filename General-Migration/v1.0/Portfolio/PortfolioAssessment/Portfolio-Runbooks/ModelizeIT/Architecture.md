ModelizeIT is an Agentless discovery tool that runs scripts on the on target clients and collect information on inventory, utilization, and dependency for a fixed period of time (default: 7 days). The output files are thereafter loaded into the RejuvenApptor Webserver, where aggregated data for all servers discovered can be analyzed. ModelizeIT supports various models of script execution, upload and analysis of data. The details of the various configurations and other documentation can be found [here](https://www.modelizeit.com/documentation/toc.html). This document describes automated execution of scripts and upload of data to SaaS based RejuvenApptor app.  
  
The main components of Modelize IT are:

1.  Gatherer Server: Engine to run the automation for execution of scripts, collection of output and upload of output results to Parser.
    
2.  Parser: This is an application modeler, intermediate processing engine that processes raw OUT files from each server and converts them into per-server application reports in CSV format.
    
3.  RejuvenApptor: Web application allowing analysis of all collected data. Allows further manipulation of data dependency to create a migration wave plan.
    

  

[ArchModelizeIT](/.attachments/DK-Portfolio/ArchModelizeIT.drawio)
[ArchModelizeIT](/.attachments/DK-Portfolio/ArchModelizeIT.drawio)

Many On-Premises Gatherer servers can be installed. This enables each Gatherer server to collect data across the organization separated by different locations and networking zones. Users may not have access to the on-premise Gatherer Server over the internet and will have to access the Gatherer Server through VPN or take help from customer in accessing it.

\*Not all servers within a customer landscape may be accessible through the On-Premise Gatherer server. In such case the data collection scripts should be run on the Target servers manually and the output files recovered and stored on a particular location in Gatherer server for them to be uploaded to the RejuvenApptor (Analysis) Server (or directly uploaded to the analysis server).

 ![](/.attachments/DK-Portfolio/modelizeit_efs_with_ports_new_icons_AWSbox-ab.jpg)

**Modelize IT deployment architecture**

 **Attachments:** 


[ArchModelizeIT.drawio](/.attachments/DK-Portfolio/ArchModelizeIT.drawio)

[ArchModelizeIT.drawio.png](/.attachments/DK-Portfolio/ArchModelizeIT.drawio.png)

[Modeliez%20IT%20architecture.drawio.png](/.attachments/DK-Portfolio/Modeliez%20IT%20architecture.drawio.png)

[image-20200919-095331.png](/.attachments/DK-Portfolio/image-20200919-095331.png)

[image-20200922-190350.png](/.attachments/DK-Portfolio/image-20200922-190350.png)

[modelizeit_efs_with_ports_new_icons_AWSbox-ab.jpg](/.attachments/DK-Portfolio/modelizeit_efs_with_ports_new_icons_AWSbox-ab.jpg)

[~ArchModelizeIT.drawio.tmp](/.attachments/DK-Portfolio/~ArchModelizeIT.drawio.tmp)
