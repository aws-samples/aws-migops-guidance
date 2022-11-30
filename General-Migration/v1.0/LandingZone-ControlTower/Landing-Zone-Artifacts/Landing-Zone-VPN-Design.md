  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Purpose
=======

This page captures the details for the customer's landing zone VPN design. 

Operational Readiness State
===========================

Two VPN Connections from separate Customer Gateway Routers for each AWS VPC. 

 ![](/.attachments/DK-LandingZone-ControlTower/AWSManagedVPN.png)

Jira Decision Ticket: 

VPN Design Details
==================

Initial access between customer data center and AWS is to be established by attaching an Amazon Virtual Private Gateway (VGW) to each VPC, creating a custom route table within each VPC, updating the security group rules, and creating AWS-managed VPN connections.

*   Each VPC will utilize two static, point-to-point IPSEC tunnels back to the on-premise environment.
*   Based on Amazon VGW capabilities, IKEv1 and Pre-Shared-Key (PSK) authentication will be used for the tunnels that transit to the customer on-premise environment.
*   Amazon supports PSK lengths between 8 and 64 characters, with a 32 character default setting.  Prefer to use the maximum length, 64 characters.
*   The PSK for the Amazon VGW is limited to alphanumeric characters, periods (.), and underscores (\_).  Given the reduced complexity available, the maximum length PSK is to be used.
*   The AWS-managed VPN connections are limited to IPv4.  IPv6 traffic will not pass thru the AWS-managed VPN tunnels.

VPN Configuration Parameter Table
=================================

Pre-shared keys are stored in Secrets Manager in Master Billing. Secret name: VpnTunnelPreSharedKeys

Individual router configuration settings can be downloaded in the VPC Console.

  

| LZ Account Name | Status | Purpose | BGP ASN | Onprem Gateway IP Address |   Tunnel 1  Public & Private IPs   |   Tunnel 2  Public & Private IPs   |
| --- | --- | --- | --- | --- | --- | --- |
| SandboxVpnA | Up | New Primary VPN for Sandbox VPC | 65000 | x.x.x.x |   *   x.x.x.x *   x.x.x.x       *   AWS x.x.x.x     *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
|   SandboxVpnB   | Up | Secondary VPN for Sandbox VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| SharedServicesVpnA | AWS VPN Provisioned | New Primary VPN for Shared Services VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| SharedServicesVpnB | AWS VPN Provisioned | Secondary VPN for Shared Services VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| DevVpnA | AWS VPN Provisioned | New Primary VPN for Dev VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| DevVpnB | AWS VPN Provisioned | Secondary VPN for Dev VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| SecurityVpnA | Need CIDR for Security VPC | New Primary VPN for Security VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| SecurityVpnB | Need CIDR for Security VPC | Secondary VPN for Security VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| MasterBillingVpnA | AWS VPN Provisioned | New Primary VPN for Master Billing VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
|   MasterBillingVpnB   | AWS VPN Provisioned | Secondary VPN for Master Billing VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| ProdVpnA | AWS VPN Provisioned | New Primary VPN for Prod VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| ProdVpnB | AWS VPN Provisioned | Secondary VPN for Prod VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| TestVpnA | AWS VPN Provisioned | New Primary VPN for Test VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |
| TestVpnB | AWS VPN Provisioned | Secondary VPN for Test VPC | 65000 | x.x.x.x |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |   *   *   x.x.x.x     *   x.x.x.x           *   AWS x.x.x.x         *   CGW x.x.x.x   |

References:
===========

[https://docs.aws.amazon.com/vpc/latest/userguide/VPC\_VPN.html](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html)

[https://docs.aws.amazon.com/vpc/latest/adminguide/cisco-asa-vti-bgp.html](https://docs.aws.amazon.com/vpc/latest/adminguide/cisco-asa-vti-bgp.html)

 **Attachments:** 


[AWSManagedVPN.png](/.attachments/DK-LandingZone-ControlTower/AWSManagedVPN.png)
