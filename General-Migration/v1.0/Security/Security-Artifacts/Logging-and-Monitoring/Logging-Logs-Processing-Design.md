  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

**Purpose**
-----------

This document outlines a strategy for AWS logs centralized processing and correlation.

**Implementation**
------------------

_Description of SIEM/Logs Analytics solution and ingestion patterns. _This should include automating alerts on key indicators, in accordance with Well-Architected best practices.__

\[Customer\] will utilize the following AWS native services and features to query collected logs for security operations purposes:

1.  [AWS](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events) [CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events) [Filtering](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events)
2.  [AWS](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events) [CloudWatch Log Groups Filtering](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events)
3.  [AWS](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events) [](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html)[CloudWatch Insights](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-console.html#filtering-cloudtrail-events)
4.  [AWS Athena](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html)

#### Pricing Information

1.  [AWS CloudTrail](https://aws.amazon.com/cloudtrail/pricing/)
2.  [AWS CloudWatch](https://aws.amazon.com/cloudwatch/pricing)
3.  [AWS Athena](https://aws.amazon.com/athena/pricing/)

#### Future State

The following additional services and solutions can be considered for implementation in the future:

1.  [Splunk integration](https://www.splunk.com/blog/2018/02/22/serving-it-up-with-aws-and-splunk-aws-serverless-application-repository-now-available.html)
2.  [AWS ElasticSearch](https://docs.aws.amazon.com/elasticsearch-service/index.html)
3.  [AWS Centralized Logging](https://aws.amazon.com/solutions/centralized-logging/)

 **Attachments:** 

