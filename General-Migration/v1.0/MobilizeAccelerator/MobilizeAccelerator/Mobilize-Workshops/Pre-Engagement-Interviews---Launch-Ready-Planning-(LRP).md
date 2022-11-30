Every Mobilize engagement should commence with Pre-Engagement/Launch Ready Planning (LRP) sessions per workstream prior to Customer Kickoff.  A one hour session for each workstream is recommended, to bring together the key stakeholders of each workstream to discuss the defined statement of work (SOW) activity and deliverables;  engagement objectives, customer goals and focus areas.  This will enable each workstream to gather additional customer information to then tailor their specific workstream roadmap and backlog prior to Customer Kickoff/Project Launch. 

The LRP session should align the team, remove any points of uncertainty and allow the team to then focus on stakeholder goals and outcomes. LRP sessions can also be used for more than readiness for Customer Kickoff/Project Launch. Larger engagements may choose to hold LRP sessions every 60-90 days to reconfirm stakeholder goals, outcomes and to refresh roadmaps and the supporting backlog. 

Depending on the size and complexity of the Mobilize Engagement, LRPs can take place as one combined LRP, however separate events are often preferred based on customer resource availability.  The sample interview questions below should be used as a guide only.  Interview questions should be reviewed and tailored by each workstream lead based upon the defined scope of work (SOW) activity and deliverables, and the background materials shared by the AWS Account Team.

Planning, Governance, and Agile Delivery
========================================

### Recommended Participants

Program Manager, Project Leads, Scrum Masters

### Sample Interview Questions

**Customer Onboarding Checklist**

Landing Zone
============

### Recommended Participants

Network Leads, Security Leads, Enterprise Architects

### Sample Interview Questions

1.  How will the LZ be used and scaled – vision for what the LZ will provide?
2.  Do you have an existing Landing Zone (LZ) strategy to build upon?
3.  How are teams structured in your org for apps/platform/security?
4.  What is the SDLC process? How is code promoted?
5.  What’s your process for creating new AWS accounts?
6.  Will you be building in just 1 AWS region, and if so, which one? (us-east-1?)
7.  Network Connectivity:
    1.  How will you connect to the new environment (DX/VPN) to an existing on-prem network?
    2.  Are there any requirements that require ingress or egress traffic to traverse a packet inspection firewall?
    3.  Are there any additional WAN connections required?
    4.  Are you inspecting network traffic? What are your requirements from a regulatory and compliance perspective?
8.  Active Directory and DNS:
    1.  Where are your domain controllers and will you be extending them to AWS?
    2.  What are you using for DNS on-prem?
9.  AWS Console and CLI Access
    1.  Do you have an existing Identity Provider solution for Federation in place what you’d want to use, and if so, which one?
10.  What do you see as potential roadblocks?

Security
========

### Recommended Participants

CISO, Information Security Leads, Security Engineers, Security Analyst, Compliance/Audit Leads

### Sample Interview Questions

1.  What Security approvals and timelines are required to support agent-based software installation across the datacentre to support the migration? (for example, Cloud Endure is an agent-based installation)
    
2.  What compliance must you adhere to?  (examples NIST 800-53)
    
3.  What type of data will be stored?  PHI, PII, PCI, etc..
    
4.  What are your requirements for data in transit and at rest? 
    
5.  What will you use for encryption? (will KMS work or will you require CloudHSM, etc..)
    
6.  Do you have restrictions regarding network traffic (ie banned countries, threat lists, etc…)?
    
7.  Do you require a Palo Alto or currently use one now?
    
8.  Do you have restrictions on network Ingress/Egress traffic? (must all traffic pass through a company managed firewall?)
    
9.  What are your logging requirements?  How long must they be kept?
    
10.  Any additional controls required for customer?
    

Operations
==========

### Recommended Participants

Operations Leads, Service Delivery Leads, Infrastructure Support Leads

### Sample Interview Questions

General Operations

1.  Is your operations model centralized or dynamic across teams?
2.  Are you leveraging any automation technologies for operational efficiency
3.  Is there centralized or application level SLA/SLOs in place?
4.  Are there any third part vendors involved in your operations process?
5.  Who are your key stakeholders across your standard operational domains

Operational Domains

1.  How does your teams perform patching of resources?
2.  What does your current tagging strategy look like?
3.  What does your provisioning processes look like (I.E. automation, catalogs, etc.)?
4.  Are resource details and configurations centralized somewhere? (i.e. CMDB)
5.  How do you view and track events in your environment ( i.e. Logging and monitoring tooling)
6.  What is the process flow for Incident Management today?
7.  What is the current Change Management process?
8.  Which tools are you using for service management?
9.  What are the backup and continuity management requirements? (i.e. RPO/ RTO)
10.  Do you have any specific licensing needs?
11.  What is your organizational cost strategy (i.e. application level, budgeting)
12.  Any operational governance or compliance requirements that we need to be aware of?

Portfolio
=========

### Recommended Participants

Application & Database Leads, Development Leads, Operations Leads

### Sample Interview Questions

1.  Have you undergone a portfolio discovery/analysis exercise recently.  Can results of this be shared?  
    
    1.  Does this output include detailed server info (CPU/RAM/Disk utilization/IOPS) as well as server dependencies?
        
    2.  Does this output include server – application – environment mapping?
        
    3.  Does this output include database server – database schema – database – database cluster – application mapping?
        
2.  If portfolio discovery/analysis has not been undertaken recently, is this to be undertaken as part of the engagement?
    1.  Has a tool or mechanism for discovery been discussed and agreed?
    2.  Who would undertake the deployment of required agents and/or sensors in order to conduct the discovery?
    3.  Would discovery require the support of a third party vendor to deploy and gather (i.e. DC vendor)?
3.  Are detailed application architecture diagrams readily available across the entire portfolio?
4.  Is there a preference around migration patterns (lift-and-shift vs. clean install) for the applications in scope?
    1.  Concerns around installing migration agents on on-premise servers?
    2.  Concerns around resourcing to install applications onto empty instances in the cloud?
5.  Are there security/compliance requirements in the AWS cloud that differ from the standard in your on-premise workloads?
    1.  Hardened/’golden’ machine images
    2.  Operating systems/versions
6.  Could you confirm the desired licensing approach (BYOL vs. Windows/Linux on AWS licenses) for this migration?
7.  Is there an established set of applications that are typically selected for pilots?
8.  Are there any anticipated changes to application deployment processes/tools expected as part of this migration?
9.  Are application build/deployment processes standard across the portfolio, or do they vary by application, application team, business unit, etc?
10.  Do applications largely run out of attached block storage (SAN) or is shared file storage/clustered databases common?

 **Attachments:** 

