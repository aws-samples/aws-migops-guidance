  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

[[_TOC_]]

* * *

Purpose
=======

This page captures the design details for designs for Spoke VPC's and Transit Gateways.

AWS Region Selection
====================

\[Customer\] will use the following regions, \[ selected region \], as their primary regions for workloads. Details on region selection can be found on the **Landing Zone AWS Region Design** page.

VPC Design 
===========

Customer's VPC Design for the number of Availability zones, subnets, CIDR Block ranges can be found on the **Landing Zone VPC and Subnet Design** page.

  

Limits on prefixes

For more information in regards to limits with Transit Gateway and prefixes.

Here is a link, [https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-limits.html](https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-limits.html).

  

Route Table Design
==================

General Spoke VPC Private Subnet Route table

  

|   Route Table   |   Destination   |   Target   |   Notes   |
| --- | --- | --- | --- |
| Spoke VPC - Private  | Spoke VPC CIDR  | Local | Default |
| Spoke VPC - Private | S3 Gateway Endpoint | GW Endpoint | For S3 Bucket endpoint |
| Spoke VPC - Private  | 10.16.0.0/12 | TGW | AWS CIDR Block Range (Summary Route) |
| Spoke VPC - Private |   10.0.0.0/8   | TGW | On-premise summary route  |
| Spoke VPC - Private | 172.16.0.0/15 | TGW  | Another On-premise summary route (VPN) |
| Spoke VPC - Private | 0.0.0.0/0 | NAT GW | Internet |

  

General Spoke VPC Public Subnet Route table

  

|   Route Table   |   Destination   |   Target   |   Notes   |
| --- | --- | --- | --- |
| Spoke VPC - Public  | Spoke VPC CIDR  | Local | Default |
| Spoke VPC - Public | 0.0.0.0 | IGW | Internet Gateway |

  

**Transit Gateway Route Table**

This depends on type of TGW Route table design customer will implement. 

If a VPC has been added to the TGW with an overlapping CIDR with another VPC, the Route table will only show case only one VPC's destination in the route table.

Below is a typical Transit Gateway Route table for a Flat network design full N-S-E-W in terms of connectivity.

  

|   Route Table   |   Destination   |   Target   |   Notes   |
| --- | --- | --- | --- |
| Default | 10.30.0.0/16 | VPC of Development | Propagated and added to default |
| Default | 10.20.0.0/16 | VPC of Production | Propagated and added to default |
| Default | 10.18.0.0/16 | VPC of Shared Services | Propagated and added to default |
| Default | 10.31.0.0/16 | VPC of Sandbox | Propagated and added to default |
|   Default   | 10.22.0.0/16 | VPC of Performance Test | Propagated and added to default |
| Default |   10.0.0.0/8   |   On-Premise-VPN   |   BGP propagation   |
| Default | 192.168.1.0/16 | On-Premise-VPN | BGP propagation |

 **Attachments:** 

