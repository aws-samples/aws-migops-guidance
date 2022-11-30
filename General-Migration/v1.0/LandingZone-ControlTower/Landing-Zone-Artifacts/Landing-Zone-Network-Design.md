  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

  

* * *

Purpose
=======

This page captures the design details for Customer's Network Connectivity between resources in AWS and Customer data center sites. It adheres to AWS Well-Architected Reliability best practices of ensuring a highly available connectivity between AWS and on-premises environments through the use of multiple AWS Direct Connect circuits, multiple VPN tunnels, and AWS Marketplace appliances as applicable.

AWS Regions
===========

Customer will use the following regions, #R\_Region(s), as their primary regions for workloads. Details on region selection can be found on the **Landing Zone AWS Region Design** page.

VPC Design 
===========

Customer's VPC Design for the number of Availability zones, subnets, CIDR Block ranges can be found on the **Landing Zone VPC and Subnet Design** page.

AWS Direct Connect Details
==========================

  

|    |    |    |    |
| --- | --- | --- | --- |

  

Customer will provision a #R\_NumberOf AWS Direct Connect connections from each of the Customer colocations, #R\_Site\_names. For each colocation, different AWS Direct Connect facilities will be used to provide the bandwidth and redundancy required to support hybrid operations during the shutdown of colocations and then for long-term connectivity to AWS regions from the remaining Customer facilities. Since #R\_Regions will be the primary regions, both colocations will have Direct Connect Connections directly into #R\_Regions.

[direct_connect](/.attachments/DK-LandingZone-ControlTower/direct_connect.drawio)
[direct_connect](/.attachments/DK-LandingZone-ControlTower/direct_connect.drawio)

AWS DX Locations
----------------

Source: [https://aws.amazon.com/directconnect/features/#AWS\_Direct\_Connect\_Locations](https://aws.amazon.com/directconnect/features/#AWS_Direct_Connect_Locations)

AWS Direct Connect Pricing
--------------------------

Source: [https://aws.amazon.com/directconnect/pricing/](https://aws.amazon.com/directconnect/pricing/)

| Type | Size | Cost | Notes |
| --- | --- | --- | --- |
| Port Cost | 10G |     |     |
| Port Cost | 1G |     |     |
| Data Transfer in | GB |     |     |
| Data Transfer out | GB |     |     |
| Cross Region Transfer between us-east-1 and us-east-2 | GB |     |     |
| Cross Region Transfer between other US regions | GB |     |     |

  

Hybrid Connectivity Patterns
============================

There are a number of machine and human interactions that are broken down into a set of patterns. These patterns are detailed below.

1 - On-Prem System and AWS VPC System Communications
----------------------------------------------------

  

|    |    |    |    |
| --- | --- | --- | --- |

  

Customer Colocations will use VPN tunnels over Direct Connect Public VIFs to connect directly to each AWS VPC. Each Customer GW create two tunnels through it's DX Public VIF to the VGW in each region. The VGW will route individual flows out a single tunnel with the shortest path to the destination. As noted in the AWS Direct Connect Pricing table above, Data Transfer out charges are ~450% less over Direct Connect vs over a Non DX Internet connection.

### Supported Use Cases

*   *   On-Prem System to AWS VPC System
    *   AWS VPC System to On-Prem System

[OnPremise2VPC](/.attachments/DK-LandingZone-ControlTower/OnPremise2VPC.drawio)
[OnPremise2VPC](/.attachments/DK-LandingZone-ControlTower/OnPremise2VPC.drawio)

2 - On-Prem Systems and Users to AWS Public Service Endpoints
-------------------------------------------------------------

  

|    |    |    |    |
| --- | --- | --- | --- |

  

Most AWS Services are only exposed via Public API Endpoints. To access these services, On-Prem systems and users will be routed through an AWS Direct Connect Connection Public VIF. As noted in the AWS Direct Connect Pricing table above, Data Transfer out charges are ~450% less over Direct Connect vs over a Non DX Internet connection.

### Supported Use Cases

*   On-Prem System to AWS Services with Public API Endpoints
*   On-Prem Users to AWS Services with Public API Endpoints

3 - AWS Services via VPC Endpoints
----------------------------------

  

|    |    |    |    |
| --- | --- | --- | --- |

  

### AWS Services with VPC Endpoints

VPC Endpoints will be used to provide access to all AWS Services that are supported. By utilizing Transit Gateway, a centralized AWS private link endpoints can be built. Complexity can be lessened by deploying complexity to a single account.

A reference to this design and its limitations can be seen here in this [blog](https://aws.amazon.com/blogs/networking-and-content-delivery/integrating-aws-transit-gateway-with-aws-privatelink-and-amazon-route-53-resolver/). 

There can be scenarios where Endpoints such as S3 should be deployed by a per VPC basis due to the cost of data traffic traversing through a transit gateway attachment . For more information on VPC endpoint policies, use this [link](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-access.html). 

### AWS Endpoints

**Interface Endpoints (Powered by AWS PrivateLink)**

An [interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) is an elastic network interface with a private IP address that serves as an entry point for traffic destined to a supported service. These services include some AWS services, services hosted by other AWS customers and Partners in their own VPCs (referred to as _endpoint services_), and supported AWS Marketplace Partner services. The owner of the service is the _service provider_, and you, as the principal creating the interface endpoint, are the _service consumer_.

**VPC Endpoint Services **(Powered by AWS PrivateLink)****

An [Endpoint services](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-service.html) allows you to create your own application in your VPC and configure it as an AWS PrivateLink-powered service (referred to as an _endpoint service_). Other AWS principals can create a connection from their VPC to your endpoint service using an [interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html). You are the _service provider_, and the AWS principals that create connections to your service are _service consumers_. 

**Gateway Endpoints**

A [gateway endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html) is a gateway that is a target for a specified route in your route table, used for traffic destined to a supported AWS service. The following AWS services are supported:

*   Amazon S3
    
*   DynamoDB
    

Source: [https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html)

### Supported Use Cases

*   Interface Endpoints ( AWS PrivateLink ) 
    *   AWS Systems Manager
    *   AWS Storage Gateway
*   Gateway Endpoints 
    *   Amazon S3

For additional list of use cases, here is a link. [https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html).

**VPC to VPC and VPC to On-Premises with VPC Endpoints**

  

[R53VPCEOnprem](/.attachments/DK-LandingZone-ControlTower/R53VPCEOnprem.drawio)
[Untitled Diagram](/.attachments/DK-LandingZone-ControlTower/Untitled Diagram.drawio)

**VPC Endpoints for AWS Services**

[PrivateVpcEndpoints](/.attachments/DK-LandingZone-ControlTower/PrivateVpcEndpoints.drawio)
[PrivateVpcEndpoints](/.attachments/DK-LandingZone-ControlTower/PrivateVpcEndpoints.drawio)

4 - AWS VPC Systems to Public Internet Sites and Service Endpoints
------------------------------------------------------------------

  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

Some Customer Systems will need to access sites and Public API Endpoints for various reasons. AWS partners provide additional tools to control egress traffic. These tools provide network security capabilities that are often required by customers looking to perform additional levels of packet inspection for network intrusion detection and prevention (IDP), implement data loss prevention services (DLP), or perform application-level traffic filtering. These solutions can be grouped in to the following categories: host-based solutions, forward proxy servers, and in-line gateways.

### Supported Use Cases

*   AWS VPC Systems to Public Internet Sites and Service Endpoints

  

[vpcEgressTraffic](/.attachments/DK-LandingZone-ControlTower/vpcEgressTraffic.drawio)
[vpcEgressTraffic](/.attachments/DK-LandingZone-ControlTower/vpcEgressTraffic.drawio)

5 - In-Region VPC System to VPC System Communications
-----------------------------------------------------

  

|    |    |    |    |
| --- | --- | --- | --- |

  

  

This section will be updated to remove VPC Peering once  AWS Transit Gateway support for the Security Group rule reference feature is released.

All "trusted" account intra AWS region communications will be built via VPC Peering. This will ensure that there are no EC2-level routing hops in the flow and Security Group nesting\* can be used to streamline access control between the layers of each application and between servers and shared services.

All "untrusted" account intra AWS region communications will be built via Transit Gateway except for VMC via HCX configuration which will be completed by VPN site to site connection. 

In Day 1, 0.0.0.0/0 traffic from within each VPC is routed through the account's IGW. Resources within the private subnet will go through NAT gateway and follow the route table for the Public "DMZ" subnets.

In Day 1, NACL will set to default for the VPCs.

An image of VPC to VPC communication design is located with this link: 

[InterVPC](/.attachments/DK-LandingZone-ControlTower/InterVPC.drawio)
[InterVPC](/.attachments/DK-LandingZone-ControlTower/InterVPC.drawio)

6 - Cross-Region VPC System to VPC System Communications
--------------------------------------------------------

  

|    |    |    |    |
| --- | --- | --- | --- |

  

For the operational readiness state, a single region (us-east-1) has been selected. Cross-Region VPC system to VPC system will be designed if/when a decision to use multiple regions is made.

Transit Gateway Inter-Region Peering is an option to peer VPC from one region to another.

[TGW-RegionPeering](/.attachments/DK-LandingZone-ControlTower/TGW-RegionPeering.drawio)
[TGW-RegionPeering](/.attachments/DK-LandingZone-ControlTower/TGW-RegionPeering.drawio)

  

* * *

Well-Architected Best Practices for Considering Networking Solutions
====================================================================

**Understand how networking impacts 
performance**: Analyze and understand how network-related decisions impact workload 
performance. For example, network latency often impacts the user experience, and using the wrong protocols can starve network capacity through excessive overhead.

**Understand available product options**: Understand the service-level features that are available to optimize network-related performance; for example, EC2 instance network capability, [enhanced networking](https://wa.aws.amazon.com/wat.concept.enhanced-networking.en.html "Enhanced networking uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types."), [Amazon EBS-optimized instances](https://wa.aws.amazon.com/wat.concept.amazon-ebs-optimized-instance.en.html), [Amazon S3 Transfer Acceleration](https://wa.aws.amazon.com/wat.concept.amazon-s3-transfer-acceleration.en.html "Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront's globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path."), and [dynamic content delivery](https://wa.aws.amazon.com/wat.concept.dynamic-content-delivery.en.html "Delivery of application generated content that includes elements that are personalized to each viewer") with [Amazon CloudFront](https://wa.aws.amazon.com/wat.concept.amazoncf.en.html "An AWS content delivery service that helps you improve the performance, reliability, and availability of your websites and applications.").

**Evaluate available networking features**: Evaluate networking features in AWS that increase performance. Measure the impact of these features through testing, metrics, and analysis. For example, take advantage of network-level features that are available (including Amazon Route 53 [latency-based routing](https://wa.aws.amazon.com/wat.concept.latency-based-routing.en.html "Improves performance by routing your customers to the AWS endpoint (e.g. EC2 instances, Elastic IPs or ELBs) that provides the fastest experience based on actual performance measurements of the different AWS regions where your application is running."), Amazon [VPC endpoints](https://wa.aws.amazon.com/wat.concept.vpc-endpoint.en.html "A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network."), or [AWS Direct Connect](https://wa.aws.amazon.com/wat.concept.awsdirectconnect.en.html "A web service that simplifies establishing a dedicated network connection from your premises to AWS. Using AWS Direct Connect, you can establish private connectivity between AWS and your data center, office, or colocation environment.")) to reduce [latency](https://wa.aws.amazon.com/wat.concept.latency.en.html "A measurement of the amount of time between an action and the result, often between a request and a response."), network distance, or jitter.

**Use minimal 
network ACLs**: Design your network to minimize the number of ACLs while still meeting requirements. Having too many ACLs can negatively impact network performance, reducing system performance or efficiency.

**Leverage encryption offloading and load-balancing**: Use load balancing for offloading encryption termination (TLS) to improve performance and to manage and route traffic effectively. Distribute traffic across multiple resources or services to allow your workload to take advantage of the elasticity that AWS provides.

**Choose network protocols to improve 
performance**: When choosing protocols for communication between systems and networks, make decisions based on how those protocols will impact workload 
performance.

**Choose location based on network requirements**: Use the location options available (for example, AWS Region, Availability Zone, placement groups, and edge locations) to reduce network latency or improve throughput.

**Optimize network configuration based on metrics**: Use data that is collected and analyzed to make informed decisions about optimizing your network configuration. Measure the impact of those changes and use the impact measurements to make future decisions.

 **Attachments:** 


[1-NetworkConnectivty.xml](/.attachments/DK-LandingZone-ControlTower/1-NetworkConnectivty.xml)

[InterVPC.drawio](/.attachments/DK-LandingZone-ControlTower/InterVPC.drawio)

[InterVPC.drawio.png](/.attachments/DK-LandingZone-ControlTower/InterVPC.drawio.png)

[OnPremise2VPC.drawio](/.attachments/DK-LandingZone-ControlTower/OnPremise2VPC.drawio)

[OnPremise2VPC.drawio.png](/.attachments/DK-LandingZone-ControlTower/OnPremise2VPC.drawio.png)

[Onprem2VPC.drawio](/.attachments/DK-LandingZone-ControlTower/Onprem2VPC.drawio)

[Onprem2VPC.drawio.png](/.attachments/DK-LandingZone-ControlTower/Onprem2VPC.drawio.png)

[PrivateVpcEndpoints.drawio](/.attachments/DK-LandingZone-ControlTower/PrivateVpcEndpoints.drawio)

[PrivateVpcEndpoints.drawio-992e8dfc925992b3523e7f26d94b3e865ec0a519.png](/.attachments/DK-LandingZone-ControlTower/PrivateVpcEndpoints.drawio-992e8dfc925992b3523e7f26d94b3e865ec0a519.png)

[PrivateVpcEndpoints.drawio.png](/.attachments/DK-LandingZone-ControlTower/PrivateVpcEndpoints.drawio.png)

[TGW-RegionPeering.drawio](/.attachments/DK-LandingZone-ControlTower/TGW-RegionPeering.drawio)

[TGW-RegionPeering.drawio.png](/.attachments/DK-LandingZone-ControlTower/TGW-RegionPeering.drawio.png)

[TransitGatewayVPCEndpoints.drawio](/.attachments/DK-LandingZone-ControlTower/TransitGatewayVPCEndpoints.drawio)

[TransitGatewayVPCEndpoints.drawio.png](/.attachments/DK-LandingZone-ControlTower/TransitGatewayVPCEndpoints.drawio.png)

[Untitled%20Diagram.drawio](/.attachments/DK-LandingZone-ControlTower/Untitled%20Diagram.drawio)

[Untitled%20Diagram.drawio.png](/.attachments/DK-LandingZone-ControlTower/Untitled%20Diagram.drawio.png)

[direct_connect.drawio](/.attachments/DK-LandingZone-ControlTower/direct_connect.drawio)

[direct_connect.drawio.png](/.attachments/DK-LandingZone-ControlTower/direct_connect.drawio.png)

[vpcEgressTraffic.drawio](/.attachments/DK-LandingZone-ControlTower/vpcEgressTraffic.drawio)

[vpcEgressTraffic.drawio.png](/.attachments/DK-LandingZone-ControlTower/vpcEgressTraffic.drawio.png)

[~drawio~5db8728fa766000da47cc72d~PrivateVpcEndpoints.drawio.tmp](/.attachments/DK-LandingZone-ControlTower/~drawio~5db8728fa766000da47cc72d~PrivateVpcEndpoints.drawio.tmp)
