  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document describes steps to be taken to complete KMS Customer-managed keys lifecycle while ensuring that encrypted data does not become not recoverable.

**Procedure**
-------------

1.  Assess key past usage:
    1.  examine key permissions to determine scope of the potential usage;
    2.  examine CloudTrail logs for the actual usage.
2.  Disable key and actively monitor the usage:
    1.  look for application errors;
    2.  examine CloudTrail logs for failed API calls.
3.  Schedule key for deletion and actively monitor the usage:
    1.  set a waiting period appropriate for the key (7 to 30 days);
    2.  set a CloudWatch Alarm to catch failed API calls against the key;
    3.  if no key usage attempts were observed, no further action is required; otherwise, cancel key deletion before the waiting period ends.

 **Attachments:** 

