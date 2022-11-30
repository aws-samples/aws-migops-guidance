  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

Disposition Tree
================

The following tree is a base model intended to be updated/validated with the with the relevant stakeholders according to the organization's unique journey and circumstances. It can be edited with [draw.io](https://app.diagrams.net/). 

**Important Note:** consider an approach where a group of applications, based on similar business criticality, architecture, and technology stacks are passed through the tree in order to obtain a recommended strategy. This will save time when working with large portfolios.

[7Rs-DecisionTree-baseModel](/.attachments/DK-Portfolio/7Rs-DecisionTree-baseModel.drawio)
[7Rs-DecisionTree-baseModel](/.attachments/DK-Portfolio/7Rs-DecisionTree-baseModel.drawio)

  

7Rs
===

 ![](/.attachments/DK-Portfolio/7RsFlowChart.png)

Migration Strategies
====================

|   **Migration** **Strategy**   | Description |   **Sample use cases**   |
| --- | --- | --- |
|   **Retire**   |   Decommission the application without migrating or modernizing   |   *   Application and host decommission at source *   No migration to target *   Existing Decommission Program Scope *   Disaster Recovery Component or Passive instances being recreated in Cloud   |
|   **Retain**   | Do nothing and keep running the application in the current location |   *   Client will keep host / application in their source environment *   Unknown application, high risk migration *   Hard dependency to another application being retained *   Unresolved Physical Dependencies   |
| Relocate | Rapid migration of servers and applications to VMware cloud on AWS |   *   Lift-Shift infrastructure onto AWS at the Hypervisor level *   No change in operating model/operations *   Very fast migration   |
|   **Rehost**   |   Rapid migration of servers and applications without architectural, technology or functionality changes        |   *   Like for Like application migration of supported workloads to target cloud *   Minimal effort to make the application work on the target cloud infrastructure (minimal application layout change)   |
|   **Repurchase**   | Purchase, configure or customize a COTS (Commercial Of The Shelf) or SaaS (Software as a Service) product |   *   Application will be replaced, potentially to new cloud-native application or SaaS platform. Data migration may be needed.   |
|   **Replatform**   | Enhanced modernization or upgrade of the application/service underlaying components such as OS and Databases |   *   Up-Version of the OS and/or Database onto the target cloud *   Data migration to cloud storage service *   Application reinstallation on the target *   DB migration onto RDS (same product)   |
|   **Refactor** **/**  **Rearchitect**   | Modernization of the application by applying changes to the code base in order to support a modernization pattern and/or changing its architecture (e.g., containerization, serverless) |   *   OS and/or Database porting *   Middleware and application change to cloud service offering *   Data conversion; Database transition to MySQL, Aurora, etc. *   Application architecture changes may also require Up-Version or Porting *   Custom / complex application changes   |

  

7R's Workshop - Deck
====================

 [AWS%207R%20Workshop.pptx](/.attachments/DK-Portfolio/AWS%207R%20Workshop.pptx)

 **Attachments:** 


[7Rs-DecisionTree-baseModel.drawio](/.attachments/DK-Portfolio/7Rs-DecisionTree-baseModel.drawio)

[7Rs-DecisionTree-baseModel.drawio.png](/.attachments/DK-Portfolio/7Rs-DecisionTree-baseModel.drawio.png)

[7RsFlowChart.png](/.attachments/DK-Portfolio/7RsFlowChart.png)

[AWS%207R%20Workshop.pptx](/.attachments/DK-Portfolio/AWS%207R%20Workshop.pptx)
