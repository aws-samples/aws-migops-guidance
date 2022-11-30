  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

  

|   Description/Scope       |
| --- |
|   Jira can be used as an IT Governance Decision Catalog to facilitate the IT Decision workflow and serve as a historical record. The runbook below describes how to create a Jira Kanban Board that serves as an IT Governance Decision Catalog. The IT Governance Decision Catalog is intended for all those involved in the project to be able to view all tickets and create draft tickets to propose recommendations and/or request decisions.   |
| Pre-conditions |
|   All pre-conditions must be met before starting steps in the migration runbook:  *   Customer and Engagement Lead have established the approval process and authorizing person for IT Governance Decisions.  *   Decision making and approval process is well understood and reflected in the structure and permissions of the Jira IT Governance Decision Board. (e.g. Decision Maker is the only person with permissions to move a ticket from Under Review to Approved)    |
| Steps |
|   1.  Create a New Project called "IT Governance Decision Catalog". Select Kanban Project (as opposed to SCRUM). 2.  Ensure Workflow aligns to the customer's decision making process. Here is a suggested workflow:  1.  3\. Depending upon the approval/decision-making processes, consider setting permissions so that only the key decision maker(s) can move items from "UNDER REVIEW" to "APPROVED". a. In User Management, create a user group of "governance-decision-catalog-approvers"        b. Add users to this group       c. Open the Workflow for editing. Click on the Transition line between "Under Review" and "Done/Approved".        d. Click "Condition" > Click "Add Condition" > Choose "Only Users in Group "governance-decision-catalog-approvers" e. Navigate to Project Settings > Permissions        f. Change Permissions for "Close Issues" and "Resolve Issues" to: Remove "Any logged in user" and Add the group "governance-decision-catalog-approvers"  2.  4\. Configure the Board by clicking      **...**      and **Board Settings              ![](/.attachments/DK-MobilizeAccelerator/DecisionCatalog-1.png)** 5\. Select **Columns.** Build Columns from Left to Right as follows: TO DO - DRAFT - UNDER REVIEW - APPROVED - UNDER REVISION.              ![](/.attachments/DK-MobilizeAccelerator/DecisionCatalog-2.png)                   6\. Set **Swimlanes** based on the Components.        1.  Create Components that align to the project. Examples are shown below. To create Components, navigate to "View all Projects" and select the  "IT Governance Decision Catalog".      2.  From the left-hand menu, select Project Settings, then click Components.                       ![](/.attachments/DK-MobilizeAccelerator/DecisionCatalog-3.png)                    c. Navigate to Board Settings and configure Swimlanes by Components.                         7\. If you choose, you can import the template decision Backlogs. Follow steps below:    a. AWS Engagement Manager, Navigate to  [AWS Internal Delivery Kit Downloads Site](https://wiki.doleancloud.com/confluence/display/DKD) b. Download the .zip files for the Delivery Kits needed.    c. Open the DK Folder and navigate to DK-Workstream > DecisionBacklog > dk-workstream\_decisions   d. Import the backlog into the Jira project.   The AWS Engagement Manager can do this if they have the proper permissions, if not, provide the backlog to the customer for import.    To import the backlog into Jira, [Run the CSV file import wizard](https://confluence.atlassian.com/adminjiraserver/importing-data-from-csv-938847533.html#ImportingdatafromCSV-howRunningtheCSVfileimportwizard).      |
|   Post-conditions     |
|   All post-conditions must be met to to successfully finish this runbook:  *   *   IT Decisions are being actively identified and documented by all members on the project.     *   The IT Governance Decision Catalog is routinely reviewed (1 time per week is recommended for Mobilize) with the key decision-maker to discuss and approve items in the "Under Review" status.      *   The IT Governance Decision Catalog is regularly shared with Executive Sponsors and the Project Team to ensure visibility and maintain project momentum.   |

 **Attachments:** 

