  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Introduction
============

This runbook is part of an AWS Runbook series meant to provide the foundation for a customer’s AWS Operational Knowledge Base. This guide provides the descriptions and methods for creating a Direct Connect Private virtual interface in a Landing Zone account VPC from a Direct Connect Connection located in the Landing Zone Shared Services Account. 

Using this Runbook
==================

Each customer environment is unique, so this runbook should be revised to include any existing customer specific processes. The runbooks in this series are also published in Word format but are more valuable when incorporated into a Knowledge Management System that supports linking and indexing.

Purpose
=======

This runbook cover the creation of a Direct Connect Private virtual interface in a Landing Zone account VPC from a Direct Connect Connection located in the Landing Zone Shared Services Account. A minimum of two Direct Connect Connections should be provisioned in the Shared Services account to allow for redundant tunnels between the customer datacenter and the target VPCs. The steps in this runbook will need to be repeated for each additional Direct Connect Connection.   
 ![](/.attachments/DK-LandingZone-ControlTower/worddav4b24ea13095ff404360c57d4701c9210.png)
\----

Collect Required Information
============================

|   **Name**   |   **Value**   |
| --- | --- |
|   Direct Connect Connection IDs   |   Lookup in the Network matrix located on the following page: **Landing Zone Network Design**   (e.g. dxcon-xxxxxxxxy, dxcon-xxxxxxxxx)   |
|   Private Virtual Interface Owner Account ID   |   Lookup in the AWS Account matrix located on the following page: **Landing Zone Account Design**   |
|   VLAN IDs   |   Lookup in the Network matrix located on the following page: **Landing Zone Network Design**   |
|   BGP ASN   |         |
|   Virtual Interface Name   |         |
|   BGP Key   |         |
|   Virtual Private Gateway ID   |         |
|   Customer Router Vendor, Platform, and Software Version   |   e.g. Cisco, Nexxus 7000 Series Switch, NX-OS-5.1+   |

* * *

Steps
=====

Create the Private VIF in the Shared Services Account
-----------------------------------------------------

1.  Log into the Shared Services Account as Admin 
2.  Verify you are in the correct Region - (e.g. US-East-1 Region )
3.  Go to Direct Connect in the console -> Virtual Interfaces 
4.  Create Virtual Interface: 
    1.  Look up the AWS BGP Password 
    2.  Look up the target Account ID, select "Another AWS Account" and enter the Account ID 
    3.  Look up the VLAN 
    4.  Uncheck Auto-generate BGP Key and Use the AWS BGP Password 

 ![](/.attachments/DK-LandingZone-ControlTower/worddav0890b99b44a3058d25c6f33e7b87037c.png)

1.  The following screen should appear:  Pending approval from the target account 

 ![](/.attachments/DK-LandingZone-ControlTower/worddavffb7bc14f665e3632d7513ac7def8ce8.png)

* * *

Create the Virtual Private Gateway on the Target Landing Zone Account
---------------------------------------------------------------------

1.  Log on to the target account  
2.  Go to the VPC console 
3.  Click on VPC from the bottom left menu, Virtual Private Gateways 
4.  Click Create Virtual Private Gateway and give it a name VGW-{Environment}VPC 

* * *

Accept the Virtual Interface in the Target Landing Zone Account
---------------------------------------------------------------

1.  In the same account, switch to Direct Connect 
2.  Check the pending Virtual Interface and click Accept Virtual Interface 

 ![](/.attachments/DK-LandingZone-ControlTower/worddav600aca5ba0194e761e7d3a527f6ccaaf.png)

1.    Verify the correct Gateway is selected.  

 ![](/.attachments/DK-LandingZone-ControlTower/worddav772422ddaba863559d60640fa11eb9e7.png)

* * *

Download the Router Configuration for the Private Virtual Interface
-------------------------------------------------------------------

1.  Log on to the Master account  
2.  Go to the Direct Connect console 
3.  Select the correct Virtual Interface Click Down Router Configuration 

   
  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav5e30422d2cd434b9180c132b5c663265.png)

1.  In Download Router Configuration screen, select Cisco Systems, Nexus 7000 Series. Then Download.

 ![](/.attachments/DK-LandingZone-ControlTower/worddaveef0f566b4a903e154ddc82366f29487.png)

* * *

  

Configure the Private VIF on the Customer Direct Connect Router
---------------------------------------------------------------

1.  Send the Router configuration to the network team and request the configuration applied to the DX router. 
2.  Confirm the BGP status is Up and Virtual Interface State is available. 

 ![](/.attachments/DK-LandingZone-ControlTower/worddavca516d51d17131bf2d33664bf03316ef.png)

* * *

  
  

Enable Route Propagation in the Target VPC Route Tables
-------------------------------------------------------

1.  Log on the Target account 
2.  Go back to VPC -> Virtual Private Gateways. Select the Virtual Private Gateway and attach it to the target VPC. After it is attached, it should show the VPC. 

 
 ![](/.attachments/DK-LandingZone-ControlTower/worddavb9c78812739921116a8705e51c938402.png)
  
  

1.   Enable Route Propagation by navigating to VPC > Route Tables > perform the following steps on each VPC route: 
    1.  Select the Route Propagation Tab 
    2.  Change Propagate from "No" to "Yes" 

  

* * *

Test Routing Between Datacenter and Target VPC Resources
--------------------------------------------------------

1.  Launce a micro ec2 instance in the subnet within the targeted VPC. 
    1.  During the Security Group configuration, create a rule to allow all traffic from all ports on the source CIDR block.
2.  Create a test instance in a datacenter VLAN that has a route to the target VPC.
3.  Initiate connections from the ec2 instance to the datacenter test instance to validate outbound routing through the Private VIF.
4.  Initiate connections from the datacenter test instance to the ec2 instance to validate inbound routing through the Private VIF. 

* * *

Repeat Runbook for all Additional Direct Connect Connections
------------------------------------------------------------

* * *

Appendices
==========

High-Level Steps to Configure a Private VIF
-------------------------------------------

 ![](/.attachments/DK-LandingZone-ControlTower/worddav4de1a4f4dbb2976adaf2393874148377.png)

Source Document
---------------

 [{+}](http://docs.aws.amazon.com/directconnect/latest/UserGuide/getting_started.html#createvirtualinterface)[http://docs.aws.amazon.com/directconnect/latest/UserGuide/getting\_started.html#createvirtualinterface+](http://docs.aws.amazon.com/directconnect/latest/UserGuide/getting_started.html#createvirtualinterface+)

 **Attachments:** 


[worddav0890b99b44a3058d25c6f33e7b87037c.png](/.attachments/DK-LandingZone-ControlTower/worddav0890b99b44a3058d25c6f33e7b87037c.png)

[worddav4b24ea13095ff404360c57d4701c9210.png](/.attachments/DK-LandingZone-ControlTower/worddav4b24ea13095ff404360c57d4701c9210.png)

[worddav4de1a4f4dbb2976adaf2393874148377.png](/.attachments/DK-LandingZone-ControlTower/worddav4de1a4f4dbb2976adaf2393874148377.png)

[worddav5e30422d2cd434b9180c132b5c663265.png](/.attachments/DK-LandingZone-ControlTower/worddav5e30422d2cd434b9180c132b5c663265.png)

[worddav600aca5ba0194e761e7d3a527f6ccaaf.png](/.attachments/DK-LandingZone-ControlTower/worddav600aca5ba0194e761e7d3a527f6ccaaf.png)

[worddav772422ddaba863559d60640fa11eb9e7.png](/.attachments/DK-LandingZone-ControlTower/worddav772422ddaba863559d60640fa11eb9e7.png)

[worddavb9c78812739921116a8705e51c938402.png](/.attachments/DK-LandingZone-ControlTower/worddavb9c78812739921116a8705e51c938402.png)

[worddavca516d51d17131bf2d33664bf03316ef.png](/.attachments/DK-LandingZone-ControlTower/worddavca516d51d17131bf2d33664bf03316ef.png)

[worddaveef0f566b4a903e154ddc82366f29487.png](/.attachments/DK-LandingZone-ControlTower/worddaveef0f566b4a903e154ddc82366f29487.png)

[worddavffb7bc14f665e3632d7513ac7def8ce8.png](/.attachments/DK-LandingZone-ControlTower/worddavffb7bc14f665e3632d7513ac7def8ce8.png)
