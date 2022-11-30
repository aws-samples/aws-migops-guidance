  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes steps which can be taken to create a forensics AMI.

**Procedure**
-------------

1.  Choose a base Amazon Machine Image (AMI) (such as Linux or Windows) that can be used as a forensic workstation;
2.  Launch an Amazon EC2 instance from that base AMI;
3.  Harden the operating system, remove unnecessary software packages, and configure relevant auditing and logging mechanisms;
4.  Install your preferred suite of open source or private toolkits, as well as any vendor software and packages you need;
5.  Stop the Amazon EC2 instance and create a new AMI from the stopped instance;
6.  Create a weekly or monthly process to update and rebuild the AMI with the latest software patches.

 **Attachments:** 

