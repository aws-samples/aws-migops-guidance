  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

This section will be updated to include AWS Transit Gateway Security Group nesting features are released.

Purpose
=======

This page captures the design details for the customer's landing zone VPCs and Subnets. This is a reference implementation for the Landing Zone that should be customized during design workshops to meet the specific needs of the customer. Following AWS Well-Architected best practices, you will want to ensure IP subnet allocation accounts for expansion and availability. Individual VPC IP address ranges should be large enough to accommodate an application's requirements, including factoring in future expansion and allocation of IP address to subnets across Availability Zones.

VPCs and Subnets 
=================

|   Account     |   Account ID     |   VPC Name     |   VPC CIDR Range     |   Priv Subnet1 CIDR     |   Priv Subnet2 CIDR     |   Priv Subnet3 CIDR     | Pub Subnet1 CIDR   | Pub Subnet2 CIDR | Pub Subnet3 CIDR |   VLAN     |   Virtual Interface Name     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|   Dev     |   xxxxxxxxxxxx   |   Dev     |   10.36.0.0/16   |   10.36.8.0/21     |   10.36.16.0/21     |   10.36.24.0/21   | 10.36.32.0/23 | 10.36.34.0/23 | 10.36.36.0/23 |   2010     |   Dev     |
|   Test     |   xxxxxxxxxxxx   |   Test     |   10.38.0.0/16   |   10.38.8.0/21   |   10.38.16.0/21     |   10.38.24.0/21   | 10.38.32.0/23 | 10.38.34.0/23 | 10.38.36.0/23 |   2020     |   Test     |
|   Prod     |   xxxxxxxxxxxx   |   Prod     |   10.20.0.0/16   |   10.20.8.0/21     |   10.20.16.0/21     |   10.20.24.0/21   | 10.20.32.0/23 | 10.20.34.0/23 | 10.20.36.0/23 |   2030   |   Prod     |
|   SharedServices     |   xxxxxxxxxxxx   |   SharedServices     |   10.32.0.0/16   |   10.32.8.0/21     |   10.32.16.0/21     |   10.32.24.0/21   |     |     |     |   2040     |   Share     |
|   Sandbox     |   xxxxxxxxxxxx   |   Sandbox     |   10.34.0.0/16   |   10.34.8.0/21     |   10.34.16.0/21     |   10.34.24.0/21   | 10.34.32.0/23 | 10.34.34.0/23 | 10.34.36.0/23 |   2050     | Sandbox |
| Transit | xxxxxxxxxxxx | VPN-B2B | 10.40.0.0/16 |     |     |     | 10.40.8.0/22 | 10.40.16.0/22   | 10.40.24.0/22 | 2060 | VPNB2B |
| Transit | xxxxxxxxxxxx | VPN-Client | 10.41.0.0/16 |     |    |     | 10.41.8.0/22 | 10.41.16.0/22 | 10.41.24.0/22 | 2070 | VPNClt |
| Transit | xxxxxxxxxxxx | Gateway | 10.42.0.0/16 |     |     |     | 10.42.8.0/22 | 10.42.16.0/22 | 10.42.24.0/22 | 2080 | GW |

VPC Resource IDs
================

|   VPC Name     |   VPC ID     | VPC Endpoint Gateway |   Subnet1 ID     |   Subnet2 ID     |   Subnet3 ID     |
| --- | --- | --- | --- | --- | --- |
|   Dev     |   vpc-xxxxxxxx     | vpce-xxxxxxxxx |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |   vpc-xxxxxxxx     |
|   Test     |   vpc-xxxxxxxx    | vpce-xxxxxxxxx |   subnet-xxxxxxxx     |   subnet-xxxxxxxx    |   subnet-xxxxxxxx     |
|   Prod     |   vpc-xxxxxxxx    | vpce-xxxxxxxxx |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |
|   SharedServices     |   vpc-xxxxxxxx     | vpce-xxxxxxxxx |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |
|   Sandbox     |   vpc-xxxxxxxx    | vpce-xxxxxxxxx |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |   subnet-xxxxxxxx     |
| TransitNetwork | vpc-xxxxxxxx | vpce-xxxxxxxxx | subnet-xxxxxxxx   | subnet-xxxxxxxx   | subnet-xxxxxxxx   |

 **Attachments:** 


[VPCSubnetDiagram](/.attachments/DK-LandingZone-ControlTower/VPCSubnetDiagram)

[VPCSubnetDiagram.png](/.attachments/DK-LandingZone-ControlTower/VPCSubnetDiagram.png)
