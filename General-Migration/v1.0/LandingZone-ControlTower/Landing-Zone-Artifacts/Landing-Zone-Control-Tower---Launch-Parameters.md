  

  

|    |    |    |    |
| --- | --- | --- | --- |

Note- The Email address for the Log Archive and Security Account must have the email domain name as the master account( [account\_name@acme.org](mailto:account_name@acme.org) )

  

Control Tower setup and parameters
----------------------------------

| Section | Parameter Name | Parameter Value |
| --- | --- | --- |
| Control Tower Region | Region | us-east-1 |
| Landing Zone Core Account Configuration |
| Log Archive Email Address ( Email address used to create a centralized log archive account) | [aws-logarchive@acme.org](mailto:aws-logarchive@acme.org) |
| Security Account Email Address (Email address used create a centralized security account) | [aws-audit@acme.org](mailto:aws-ss@acme.org) |
|   Security Alert Email Address (Email for all the Security Alerts related to Landing Zone)   | [aws-security@acme.org](mailto:aws-security@acme.org) |

Post Control Tower setup and parameters
---------------------------------------

| Section | Parameter Name | Parameter Value |
| --- | --- | --- |
| Security Notifications | Security Alert Email Address (Email for all the Security Alerts related to Landing Zone) | [soc-notifications-aws@acme.org](mailto:soc-notifications-aws@acme.org) |
| Shared Services VPC & Active Directory Configuration | AD Region (Region for Shared Services VPC & AD to be deployed into e.g. us-west-2) | N/A - not a day 1 |
| Shared Services VPC Options (Create a shared service VPC with subnets in 2 or 3 AZs. The 3 AZ option is recommended for all regions except when the desired AD Region only has 2 AZs) | 2AZ |
| Shared Services VPC CIDR (CIDR block for the Shared Service) | 10.251.64.0/20 |
| VPC Domain DNS Name (Fully qualified domain name (FQDN) of the forest root domain e.g. [example.com)](http://example.com/) | [aws.acme.org](http://aws.acme.org) |
| Domain Net BIOS Name (NetBIOS name of the domain (up to 15 characters) for users of earlier versions of Windows e.g. EXAMPLE) | N/A |
| RDGW Instance Type (Amazon EC2 instance type for the Remote Desktop Gateway instances) | N/A |
| Allowed Remote Desktop External Access CIDR (Allowed CIDR Block for external access to the Remote Desktop Gateways) | N/A |
| Number of RDGW Hosts (Enter the number of Remote Desktop Gateway hosts to create) | N/A |
| AWS SSO Network Configuration | AWS SSO region Endpoint (List of AWS SSO supported endpoint regions.) | us-east-1 is only valid value currently |
| AD Connector VPC CIDR (CIDR block for AD Connector to use for connecting AWS SSO to Active Directory) | Not a day 1 implementation |
| AD Connector VPC Subnet 1 (CIDR block for AD Connector VPC subnet created in AZ1) | Not a day 1 implementation |
| AD Connector VPC Subnet 2 (CIDR block for AD Connector VPC subnet created in AZ2 VPC Flow Logs Retention Policy) | Not a day 1 implementation |

 **Attachments:** 

