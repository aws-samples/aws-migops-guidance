  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

[[_TOC_]]

* * *

Description
===========

This page covers strategies for expanding the customer Internal and External DNS capability to support hybrid DNS use cases.

Approach
========

There are multiple approaches to addressing hybrid DNS use cases. The recommended solution is to use the Amazon Route 53 Resolver (outbound) to forward DNS resolution requests of Customer's domains to their DNS servers. R53 resolver will provide a highly available low cost solution. When you create a VPC using Amazon VPC, you automatically get DNS resolution within the VPC from Route 53 Resolver. By default, Resolver answers DNS queries for VPC domain names such as domain names for EC2 instances or ELB load balancers. Resolver performs recursive lookups against public name servers for all other domain names.

DNSSec (Optional Section If Required)
-------------------------------------

DNSSec resolutions with Route 53 is not supported at this time. Any AWS resources that needs to be defined in the customer's DNSSec domains, will be created within the Customer's DNS servers. 

Forward DNS queries from resolvers on your network to Route 53 Resolver (Remove if required to use DNSSec)
----------------------------------------------------------------------------------------------------------

DNS resolvers on your network can forward DNS queries to Resolver in a specified VPC. This allows your DNS resolvers to easily resolve domain names for AWS resources such as EC2 instances or records in a Route 53 private hosted zone. For more information, see How DNS Resolvers on Your Network Forward DNS Queries to Route 53 Resolver.

Conditionally forward queries from a VPC to resolvers on your network
---------------------------------------------------------------------

You can configure Resolver to forward queries that it receives from EC2 instances in your VPCs to DNS resolvers on your network. To forward selected queries, you create Resolver rules that specify the domain names for the DNS queries that you want to forward (such as [acme.org](http://www.acme.org)), and the IP addresses of the DNS resolvers on your network that you want to forward the queries to. If a query matches multiple rules ([acme.org](http://www.acme.org), [test.acme.org](http://www.test.acme.org)), Resolver chooses the rule with the most specific match ([test.acme.org](http://www.test.acme.org/)) and forwards the query to the IP addresses that you specified in that rule. For more information, see How Route 53 Resolver Forwards DNS Queries from Your VPCs to Your Network under [references section](https://myitportal.atlassian.net/wiki/spaces/DKLZCT/pages/304054293/Landing+Zone+DNS+Design#LandingZoneDNSDesign-References).

Route 53 Resolver Endpoints
===========================

Do not implement Inbound endpoints if DNS Sec is required. 

| Component | AWS Account | VPC | Subnet | AZ | IP | Tags |
| --- | --- | --- | --- | --- | --- | --- |
| Inbound endpoint 1 | Transit Network | Transit Network VPC | subnet-xxxxx | us-east-1a | x.x.x.x |   Name: InboundEndpoint1  Application: LandingZone   |
| Inbound endpoint 2 | Transit Network | Transit Network VPC | subnet-yyyyy | us-east-1b | x.x.x.x |   Name: InboundEndpoint1  Application: LandingZone   |
| Outbound endpoint 1 | Transit Network | Transit Network VPC | subnet-xxxxx | us-east-1a | x.x.x.x |   Name: OutboundEndpoint1  Application: LandingZone   |
| Outbound endpoint 2 | Transit Network | Transit Network VPC | subnet-yyyyy | us-east-1b | x.x.x.x |   Name: OutboundEndpoint2  Application: LandingZone   |

Route 53 Resolver Rules
=======================

| Name | Endpoint | Type | Owner | Tags |
| --- | --- | --- | --- | --- |
| Internet Resolver | Route 53 Service | Recursive | Route 53 Resolver Service |   Name: InternetResolverRule  Application: LandingZone   |
| acme.org | Outbound | Forward | Transit Network Account |   Name: acme.org  Application: LandingZone   |
| acme-seconddomain.org | Outbound | Forward | Transit Network Account |   Name: acme-seconddomain.org  Application: LandingZone   |
| x.x.in-addr.arpa | Outbound | Forward | Transit Network Account |     |
| 10.in-addr.arpa | Outbound | Forward | Transit Network Account |     |

DNS Domains
===========

This is a list of authoritative domains used by the organization.

| Subdomain |   Internal, External  or Split-Brain   | Application or Host | Other details |
| --- | --- | --- | --- |
| acme.org | External | Application | Authoritative - DNSSEC? |
| myportal.acme.org | External | Application | Authoritative - DNSSEC? |
| mysite1.acme.org | Split-Brain | Application | Authoritative\* |
| mysite2.acme.org | Split-Brain | Application |     |
| \*.corp.acme.org | Internal | Linux & Windows Hosts | hostname records |
| \*.aws.acme.org | Internal | Linux & Windows Hosts | hostname records |
| x.x.in-addr.arpa | Both | Host | Reverse x.x.x.x |
| 10.in-addr.arpa | Internal | Host | Reverse 10.x.x.x |

Use Case Matrix
===============

They utilize Chef to setup the DNS name of a hostname. In particular ASG, thinking of chef recipe to run needs to have a hostname. This is all Day 1

| ID | Who owns the record | Public or Private | Description |
| --- | --- | --- | --- |
| OP-1 | ACME DNS Servers - CNAME | Public | On-prem host resolving the hostname of a standalone Public AWS EC2 instance |
| OP-2 | R53 - using aws.newdomain.cloud | Private | On-prem host resolving the hostname of a standalone Private AWS EC2 instance. If its private - users wont care, so they will use R53.  |
| OP-3 | ACME DNS Server - CNAME | Public | On-prem host resolving an AWS ELB, ALB, NLB ALIAS. Elastic IPs |
| OP-4 |   ACME DNS Servers - CNAME   | Private  | On-prem host resolving an AWS ELB, ALB, NLB ALIAS.   |
| OP-5 | R53 - using aws.newdomain.cloud | Private | On-prem host resolving an AWS ELB, ALB, NLB ALIAS. |
| OP-6 | S3 static websites will be a CNAME owned by ACME DNS servers |     |   On-prem host resolving an AWS Service API CNAME - Same case as OP4        |
| AWS-1 | R53. resolver forward - rules  | Public | AWS EC2 instance resolving the hostname / CNAME of an on-prem host  ( acme.org, test.acme.org,acme-seconddomain.org )  |
| AWS-2 | R53. resolver forward - rules  | Private | AWS EC2 instance resolving the hostname / CNAME of an on-prem host  ( acme.org, test.acme.org,acme-seconddomain.org )  |
| AWS-3 | R53. resolver forward - rules  | Private  | .Campus - AD DNS. multiple zones (Bind), there are other items besides AD  |
| AWS-4 | R53-private hosted zones | private |  AWS EC2 instance resolving the hostname of another AWS EC2 instance in the same VPC |
| AWS-5 | R53-public hosted zone  | public |  AWS EC2 instance resolving the hostname of another AWS EC2 instance in the same VPC  |
| AWS-6 | R53-public hosted zone | public |  AWS EC2 instance resolving the hostname of another AWS EC2 instance in a different VPC |
| AWS-7 | R53-private hosted zone | private  |  AWS EC2 instance resolving the hostname of another AWS EC2 instance in a different VPC |

  

References
==========

| Title/Description | URL | Description |
| --- | --- | --- |
|   Advanced Architectures with AWS Transit Gateway   |   Youtube:   Slideshare: [https://www.slideshare.net/AmazonWebServices/advanced-architectures-with-aws-transit-gateway](https://www.slideshare.net/AmazonWebServices/advanced-architectures-with-aws-transit-gateway)   |   In this session, we discuss the need for AWS Transit Gateway, dive into common use cases, and discuss reference architectures. The session will prepare you with the fundamentals to understand AWS Transit Gateway operations and create advanced architectures. Learn how AWS Transit Gateway interacts with other services, like Amazon Route 53 Resolver and AWS PrivateLink, to provide enterprise scale service in large operating environments.     |
|   AWS re:Invent 2018: Introduction to Amazon Route 53 Resolver for Hybrid Cloud (NET215)   |   Youtube:  Slideshare: [https://www.slideshare.net/AmazonWebServices/introduction-to-amazon-route-53-resolver-for-hybrid-cloud-net215-aws-reinvent-2018](https://www.slideshare.net/AmazonWebServices/introduction-to-amazon-route-53-resolver-for-hybrid-cloud-net215-aws-reinvent-2018)     |     |
|   Amazon Route 53 Resolver for Hybrid Clouds   | [https://aws.amazon.com/blogs/aws/new-amazon-route-53-resolver-for-hybrid-clouds/](https://aws.amazon.com/blogs/aws/new-amazon-route-53-resolver-for-hybrid-clouds/) |     |
|   Resolving DNS Queries Between VPCs and Your Network   | [https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html) |     |

Route 53 Resolver Benefits
--------------------------

### Reduced Complexity and Cost

 ![](/.attachments/DK-LandingZone-ControlTower/R53-ReducedComplexity.png)

### Highly Available

 ![](/.attachments/DK-LandingZone-ControlTower/R53-HighlyAvailable.png)

### Centrally Managed Cross Account Rules Sharing

 ![](/.attachments/DK-LandingZone-ControlTower/R53-CrossAccountRuleSharing.png)

 **Attachments:** 


[R53-CrossAccountRuleSharing.png](/.attachments/DK-LandingZone-ControlTower/R53-CrossAccountRuleSharing.png)

[R53-HighlyAvailable.png](/.attachments/DK-LandingZone-ControlTower/R53-HighlyAvailable.png)

[R53-ReducedComplexity.png](/.attachments/DK-LandingZone-ControlTower/R53-ReducedComplexity.png)
