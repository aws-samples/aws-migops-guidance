  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines common account credentials compromise scenarios and mitigation recommendations.

**Procedure**
-------------

#### Detection and Analysis

If \[Customer\] suspects or receives notification of an AWS account credentials compromise, \[Customer\] should validate and determine the scope of exposure. Below are some of the actions that can be taken:

1.  Identify the credentials’ owner: identifying the owner of the credentials helps understand the risk of exposure as well as confirm if the credentials were actually compromised. This can be done using IAM console or AWS CLI which can be helpful when searching through a large number of users as well as when mapping access keys to an IAM user.
2.  Assess privileges associated with the compromised credentials as well as current use of credentials: before deactivating credentials, AWS recommends to understanding how the credentials are used and by what applications/users. This will help replace the credentials quickly without interruption to production. \[Customer\] can use the following tools:
    1.  IAM Access Advisor to understand the access provided by the credentials;
    2.  Descriptive naming policy to identify the owner/application;
    3.  CloudTrail logs;
    4.  Additional documentation that can be used by \[Customer\] to track this information.
3.  Assess possible exposure from the compromised credentials: it is important to make sure that the credentials were not used in any unauthorized way, and that no further exposure in the environment has occurred. \[Customer\] can use the following tools:
    1.  CloudTrail logs to review API logs for the compromised credentials to get an idea of what services and resources were accessed with the credentials;
    2.  AWS Config to check history of resource changes.

#### Containment, Eradication and Recovery

During the analysis stage, \[Customer\] should have identified the owner of the compromised credentials and their usage patterns to ensure that appropriate actions are taken to replace the credentials without interruption to production. If it was concluded that the credentials were used in any unauthorized way, \[Customer\] may decide to revoke privileged access, revoke outstanding sessions or invalidate credentials to eliminate further exposure in the environment.

If \[Customer\] decides to invalidate the credentials, the following steps can be executed in an order and timeframe appropriate to the selected balance between downtime and risk of further unauthorized access:

1.  Create a new set of credentials and configure all affected applications to use them: this can involve changing EC2 Role or replacing Access Keys.
2.  Deactivate credentials and monitor impact: AWS recommends deactivating/disabling the credentials first instead of deleting them to minimize a risk of a production workflow impact. \[Customer\] can monitor CloudWatch for any increased errors associated with services or applications that were using the compromised credentials.
3.  Delete compromised credentials: once it is confirmed that no applications are using the compromised credentials, they can be deleted from the account.

#### Post-Incident Activity

Depending on the method that was used to detect and notify \[Customer\] security team about account credentials compromise and the nature of the compromise, \[Customer\] may need to perform the following:

1.  Investigate how the credentials were compromised: It is necessary to investigate how the credentials were compromised to help put in controls and educate the users so that this doesn’t occur in the future.
    1.  Review user login activities (Location, IP address, etc.) to identify any abnormal behavior that might help with the investigation;
    2.  Review logs from security services such as GuardDuty that monitors for anomalies in user login activities;
    3.  Review user’s machine for malware.
2.  Identify and implement preventive measures that could have prevented the initial compromise:
    1.  Strong password policies;
    2.  Regular access key rotation;
    3.  IAM policies that restrict login activities to certain IP ranges;
    4.  Multi-factor authentication.
3.  Identify possible automations and services that could help speed up the remediation process:
    1.  AWS CLI commands/scripts to map access key/secret access keys to IAM users;
    2.  Create pre-existing queries in the monitoring solutions (Splunk, Elasticsearch/Kibana, etc.) to search through CloudTrail and VPC flow logs;
    3.  Utilize services such as GuardDuty, Macie, CloudWatch Alarm for timely notifications.
    4.  Re-examine the incident response process and look for ways to improve efficiencies and minimize disruption.

 **Attachments:** 

