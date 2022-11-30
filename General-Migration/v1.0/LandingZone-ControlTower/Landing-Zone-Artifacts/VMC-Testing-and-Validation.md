  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

### Summary

No configuration is complete without a comprehensive test. Once SDDC is deployed and HCX is configured to migrate virtual machines, ensure that you verify functionality using the below framework during a pilot migration of workloads.

### Basic Functional Testing

-  Validate connectivity between on-prem and VMC vCenter environments -  Validate that the on-prem HCX environment connectivity -  Validate that cloud workloads are visible to the on-prem HCX plugin

### Solution Design Testing

-  Demonstrate the ability to migrate and protect workloads between VMware Cloud on AWS and Client’s on premises data center environment -  Create L2 Stretch network with HCX -  Test recovering one workload on stretched network, verify connectivity -  Migrate defined workloads with HCX and test the functionality and data

### Performance Testing

-  Work with team to measure data throughput during data migrations to validate transfer speed assumption (based on network used, and adjusted to fit proposed future network connectivity) -  Work with team to measure data transfers to estimate approximate de-dupe rates and network optimization benefit

 **Attachments:** 

