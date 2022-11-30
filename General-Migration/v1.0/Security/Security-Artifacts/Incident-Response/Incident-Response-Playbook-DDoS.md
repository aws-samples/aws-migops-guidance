  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines common DDoS attack scenarios and mitigation recommendations.

**Procedure**
-------------

#### Detection and Analysis

To validate a DoS incident and determine its scope, \[Customer\] should review the performance and availability of applications/resources affected. This will help to determine if the resources have the proper configuration to handle the attack. \[Customer\] can take the following actions:

1.  Review Load Balancer and Auto-scaling configurations and metrics.
2.  Review CloudWatch metrics for increased utilization on resources such as EC2.
3.  Review application level logs for increased error rates.

The \[Customer\] security team will have to balance between lowering business impact and reducing the exposure to genuine malicious activities. If any of the escalation actions are identified or responder concludes that this is a live incident, \[Customer\] should proceed to the incident full investigation and containment activities.

#### Containment, Eradication and Recovery

With an AWS account \[Customer\] automatically benefits from AWS Shield Standard protection which provides protection against common and most frequently occurring infrastructure (Layer 3 and 4) attacks. The majority of Layer 3 and 4 attacks such as SYN Floods and UDP reflection attacks are blocked automatically by services such as ELB/ALB, CloudFront, Route53 that have anomaly and known attacks signature detection engines. However, it is \[Customer\]’s responsibility to implement a [DDoS resilient architecture](https://aws.amazon.com/answers/networking/aws-ddos-attack-mitigation/) that would allow \[Customer\] to take advantages of the DDoS mitigation capabilities that AWS provides. Moreover, since Layer 7 attacks mitigation requires an intimate knowledge of applications, extra steps have to be taken by \[Customer\] to prevent and mitigate such attacks. AWS provides tools such as WAF and Shield Advanced to address them. AWS Shield Advanced provides additional detection and mitigation against large and sophisticated DDoS attacks.

If based on the incident analysis, \[Customer\] determines that one or more of their EC2 instances are under a DoS attack, the following steps can be taken to mitigate:

1.  Block attacker traffic as identified from the logs (VPC FlowLogs, ELB/ALB, CloudFront, Instance logs). AWS recommends keeping note of all the blocked IPs as they might be just spoofed and represent legitimate traffic in the future. \[Customer\] can use the following methods to block an attack:
    1.  NACL can be used to block an attacker IP addresses (blocks traffic on a subnet level);
    2.  CloudFront geolocation filtering can be used to block all unexpected countries or countries an attack is originating from;
    3.  CloudFront can be used to block unexpected HTTP Methods;
    4.  EC2 Instance Linux iptables can be used to block an attacker IP addresses;
    5.  AWS WAF can be used to block an attacker IP address/country, malicious HTTP headers, or URI strings;
    6.  AWS WAF Rate Based limiting rules can be used to block DDoS attacks if they originate from constantly changing IPs and if they use legitimate HTTP methods and strings;
2.  If above actions did not mitigate the attack and if the attack vector is constantly changing, scale up or out to sustain the attack and avoid service interruption.
3.  If required, contact AWS Premium Support for assistance in investigation and mitigation.
4.  If subscribed to AWS Shield Advanced, AWS Premium Support may involve AWS DRT (DDoS Response team) to mitigate the attack. To facilitate fast resolution, proactively allow DRT access to your environment.

In the event of a massive DoS/DDoS activity detected by AWS DRT (DDoS Response Team), DRT team may limit traffic and API activity for the involved instances/accounts to eliminate negative impact on AWS infrastructure and other customers. In this case, DRT team will engage AWS Premium Support to notify \[Customer\] and to advise on further actions.

#### Post-Incident Activity

Depending on the results of the initial incident analysis and the root cause, \[Customer\] may need to perform the following:

1.  Determine if this is indeed a DoS attack or an anomalous increase in traffic; the following metrics can be reviewed to determine the volume of traffic and how it compares to historical trends:
    1.  CloudFront metrics;
    2.  Amazon WAF metrics;
    3.  AWS Shield Advanced (If available);
    4.  Load Balancer metrics;
    5.  EC2 network utilization metrics.
2.  Identify and implement any additional preventive measures that could have prevented the initial compromise:
    1.  Architect by using services such as CloudFront, Route53, ELB/ALB/NLB, Auto-scaling;
    2.  Subscribe to AWS Shield Advance.
3.  Identify possible automations and services that could help speed up the remediation process:
    1.  Create alarms and notifications based on metrics from different services (CloudFront, Route 53, ELB/ALB/NLB, WAF);
    2.  Automatically trigger support tickets to AWS DRT teams;
    3.  Utilize services such as GuardDuty, Macie, CloudWatch Alarm for timely notifications;
    4.  Re-examine the incident response process and look for ways to improve efficiencies and minimize disruption.

 **Attachments:** 

