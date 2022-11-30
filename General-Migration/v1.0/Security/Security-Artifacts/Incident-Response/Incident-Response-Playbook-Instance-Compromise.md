  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines common instances compromise scenarios and mitigation recommendations.

**Procedure**
-------------

#### Detection and Analysis

If \[Customer\] suspects or receives notification of an instance compromise, \[Customer\] should review the impact on the environment to make sure no other assets or resources have been impacted. \[Customer\] can take the following actions:

1.  Gather additional information about the instance by using EC2 Describe API calls to identify criticality and sensitivity of the assets.
    
     aws ec2 describe-instances --filters "Name=ipaddress,Values=X.X.X.X"\]\]>
    
      
    
2.  Review VPC flow logs for the instance.
3.  Review CloudTrail logs for API calls that originated from the instance.
4.  If the instance has any IAM instance roles attached, review CloudTrail logs for API calls made with that role.
5.  Review AWS Config resource history to understand if any changes were made recently.

#### Containment, Eradication and Recovery

When security events are detected involving an EC2 instance, \[Customer\] will have to decide whether to destroy and replace the instance, or isolate and inspect the instance. If \[Customer\] chooses to isolate the instance for forensic investigation and root cause analysis, then there are some basic steps that will need to be completed.

 ![](/.attachments/DK-Security/image2019-7-19_12-48-8.png)

1.  Communication & responsibility hand-over: Upon determination of a compromised instances and the need for forensic investigation, \[Customer\] security team should communicate to the resource owner (identified by the instance tag) that they need to immediately and completely hand over the instance control to the \[Customer\] security team. Any EC2 instance OS and application access credentials should also be provided to the team to facilitate the investigation. The instance should be tagged and considered unrecoverable for business use.
    
     aws ec2 create-tags -resources i-abcd1234 -tags Key=incident-response,Value=quarantine:REFERENCE-ID\]\]>
    
      
    
2.  Taking compromised instance out of service: \[Customer\] may choose to isolate the instance from further network communication by changing the instance’s security group to a new isolation security group that restricts the network traffic. Prior to this, \[Customer\] should remove the instance from any related Auto Scaling Groups and ELB/ALB Target Groups, and optionally enable termination protection, to prevent the instance from being accidentally terminated.
    
     aws ec2 modify-instance-attribute --instance-id i-abcd1234 --attribute disableApiTermination --value true # Detach from the Auto Scaling Group > aws autoscaling detach-instances --instance-ids i-abcd1234 --auto-scaling-group-name web-asg # Deregister the instance from the Elastic Load Balancer > aws elb deregister-instances-from-load-balancer --instances i-abcd1234 --load-balancer-name web-load-balancer # Switch the EC2 instance's Security Group to a restricted SecurityGroup > aws ec2 modify-instance-attribute --instance-id i-abcd1234 --groups sg-a1b2c3d4\]\]>
    
      
    
3.  Forensics preparation: Once the compromised instance is isolated from the network, \[Customer\] IRT should create a snapshot of all volumes attached to the instance. This should be performed before other activities to preserve the machine state as early as possible. Note that for forensic (and potential legal) investigation purposes the instance should not be stopped while the EBS snapshots are being taken. In some cases, it might be useful to take multiple EBS snapshots to capture the time sequence of disk image changes with the compromised instance. This could occur if software continues to write to disk even when network connectivity is disabled. During this process, the compromised EC2 instance must remain fully isolated.
    
     aws ec2 create-snapshot --volume vol-12xxxx78 --description "ResponderName-Date-REFERENCE-ID"\]\]>
    
      
    
4.  Forensics environment launch: The security team can launch a CloudFormation stack using Forensics template inside the Audit account. This template will deploy a forensics instance and configure appropriate security groups. The Forensics EC2 instance can be launched from a pre-created AMI containing all the tools needed to conduct a forensic investigation. This instance should be designed as single-use. Once an investigation is completed, the Forensics instance will be terminated to avoid contamination.
    
     aws ec2 run-instances --image-id ami-4n6x4n6x --count 1 --instance-type c4.8xlarge --key-name forensicPublicKey --securitygroup-ids sg-1a2b3c4d --subnet-id subnet-6e7f819e # Create a security group rule to allow the new Forensic Workstation to communicate to the contaminated instance. > aws ec2 authorize-security-group-ingress --group-id sg-a1b2c3d4 --protocol tcp --port 0-65535 --source-group sg-1a2b3c4d # Create a forensics environment from a forensics template (if CFT is used) > aws cloudformation create-stack --stack-name forensicsstack --template-body file://forensicstemplate.json --parameters ParameterKey=KeyPairName,ParameterValue=ForensicsKey ParameterKey=SubnetIDs,ParameterValue=ForensicsSubnetID ParameterKey=IsolationSG,ParameterValue=IsolationSGID\]\]>
    
      
    
5.  Online Forensics: \[Customer\] security team can log in to the running compromised instance to see the effect of change to file system, log files and/or memory state. Due to the potential risks involved in making changes to the compromised system, online investigations must only be performed by skilled forensic investigators using the Forensics Instance. Forensic investigators can first log in to the Forensics Workstation, and then connect to the compromised instance. Additional forensic tools may need to be copied from the Forensics Workstation to the compromised instance during the investigation. Although \[Customer\] can authenticate directly to the machine using a standard method—such as Linux secure shell (SSH) or Windows remote desktop (RDP)—manual interaction with the operating system is not a best practice. It is recommended to programmatically use an automation tool to execute tasks on a host. AWS Systems Manager Run Command service can be used to invoke the SSM Agent that executes Linux shell scripts and Windows PowerShell commands. These scripts can load and execute specific tools to capture additional data from the host, such as the Linux Memory Extractor (LiME) kernel module. The memory capture can then be transferred to the forensic workstation in the VPC network, or to an Amazon S3 bucket for durable storage. One method to invoke the SSM Agent is to target the Run Command through Amazon CloudWatch Events when the instance is tagged with a specific tag. For example, if incident-response tag is applied to an affected instance, Amazon CloudWatch Events can trigger two actions: 1) a Lambda function that performs the isolation activities, and 2) a Run Command that executes a shell command to export the Linux memory through the SSM Agent.
    
      
    
6.  Offline Forensics: A safer form of forensic investigation is to perform offline analysis of the compromised instance’s disk image. The captured EBS snapshot can be used to serve that purpose. EBS snapshots can be used to construct a copy of the compromised EBS volume, which can then be mounted to the Forensics Instance for detailed analysis. Below diagram reflects an example incident response for forensics investigation.
    
     aws ec2 create-volume --region us-east-1 --availability-zone us-east-1a --snapshot-id snap-abcd1234 --volume-type io1 --iops 10000 # Attach the volume to the forensic workstation > aws ec2 attach-volume --volume-id vol-1234abcd --instance-id i-0dc02a41b66cf8477 --device /dev/sdf\]\]>
     ![](/.attachments/DK-Security/image2019-7-19_12-51-21.png)
    
      
    
7.  Clean Up: Once the forensic and legal investigations are concluded, the compromised EC2 instance should be shut down. The suspected compromised instance should be considered as unsafe. As such, the Forensics Instance may be contaminated during the investigation process. Therefore, it is a good practice to terminate the Forensics Workstation instances after the investigation is completed. The entire forensics environment should be decommissioned by deleting the corresponding CloudFormation stack.
    
     aws ec2 terminate-instances --instance-ids i-0dc02a41b66cf8474 > aws ec2 terminate-instances --instance-ids i-09db190a411cf51d8 # Terminate forensics environment (if CFT was used) > aws cloudformation delete-stack --stack-name forensicsstack\]\]>
    
      
    
8.  Recovery: As soon as the compromised instance has been removed from the VPC, \[Customer\] can begin restoring the affected service. Instead of attempting to remediate, patch and validate the compromised asset, a good practice is to leverage the cloud’s advantages to launch an instance with last-known good configuration. The complexity and success of this operation depends on the "cloud readiness" of the application. With a "self-healing" application that incorporates elasticity, AWS CloudWatch will detect the missing node, direct Auto Scaling to replace it with a new one, and Elastic Load Balancing will add the new node to the ELB cluster when it is finished coming online, thus providing automated recovery with minimal disruption. In contrast, the system and application may need to be rebuilt by hand and restored from backup. For this step, \[Customer\] security team should contact the business owner and \[Customer\] cloud team to determine the most feasible procedures.

Many of the steps described in this section can be codified and performed programmatically based upon input from a forensic analyst or incident responder.

#### Post-Incident Activity

Depending on the results of the initial incident analysis, \[Customer\] may need to perform the following:

1.  Determine how the instance was infected in the first place: Examine the findings from the forensics phase and mitigate the attack vector or vulnerability that the attacker(s) used to compromise the system. A plan should be developed to mitigate the application and all affected resource types.
2.  Identify and implement any additional preventive measures that could have prevented the initial compromise:
    1.  Instance security groups should be reassessed to appropriately limit access;
    2.  Regular vulnerability scanning solutions have to be put in place.
3.  Identify possible automations and services that could help speed up the remediation process:
    1.  Trigger parts of the incident response workflow (security group isolation, detach IAM roles, take EBS snapshots) with Lambda;
    2.  Create pre-existing queries in the monitoring solutions (Splunk, Elasticsearch/Kibana, etc.) to search through CloudTrail and VPC flow logs;
    3.  Utilize services such as GuardDuty, Macie, CloudWatch Alarm for timely notifications.
    4.  Re-examine the incident response process and look for ways to improve efficiencies and minimize disruption.

 **Attachments:** 

