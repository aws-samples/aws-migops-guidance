|    |    |    |    |
| --- | --- | --- | --- |

* * *

[[_TOC_]]

* * *

Introduction
============

The Implement DX Public VIF for EC2 and On-premise Access to AWS APIs runbook is part of an AWS Runbook series meant to provide the foundation for a customer’s AWS Operational Knowledge Base. This guide provides the descriptions and methods for implementing an AWS Direct Connect Public Virtual Interface to allow access from on premise to AWS public endpoints. 

Using this Runbook
==================

Each customer environment is unique, so this runbook should be revised to include any existing customer specific processes. The runbooks in this series are also published in Word format but are more valuable when incorporated into a Knowledge Management System that supports linking and indexing.

  

* * *

Direct Connect Public VIF Diagram
=================================

High-Level Steps to Configure a Public VIF
==========================================

Customer Steps
--------------

1.  Select an unused VLAN for the VIF
2.  Provide public IP Addresses for the VIF endpoints (this can be a /31 range)
3.  Identify planned route announcements
4.  Provide public or private Autonomous System Number (ASN)
5.  Specify BGP authentication key
6.  Determine VIF Account assignment

AWS Steps
---------

1.  Configure DX router port with customer-provided IP
2.  Confirm customer owns planned route announcements
3.  Confirm customer owns ASN if in public range
4.  Announces local region routes
    1.  At US DX locations, all US region routes are announced

Example Public VIF Request
--------------------------

 ![](/.attachments/DK-LandingZone-ControlTower/worddavaef9cff0a579e8b505069a530696cd10.png)

 **Attachments:** 


[Public%20and%20Private%20VIF%20Examples](/.attachments/DK-LandingZone-ControlTower/Public%20and%20Private%20VIF%20Examples)

[Public%20and%20Private%20VIF%20Examples.png](/.attachments/DK-LandingZone-ControlTower/Public%20and%20Private%20VIF%20Examples.png)

[worddavaef9cff0a579e8b505069a530696cd10.png](/.attachments/DK-LandingZone-ControlTower/worddavaef9cff0a579e8b505069a530696cd10.png)
