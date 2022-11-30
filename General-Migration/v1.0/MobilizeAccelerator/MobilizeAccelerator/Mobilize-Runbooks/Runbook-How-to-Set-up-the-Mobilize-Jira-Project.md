  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

  

|   Description/Scope       |
| --- |
|   Jira is used to manage the Mobilize engagement backlog. The backlog is refined through agile roadmapping and Accelerator outcomes, then lazy loaded as it's needed. The runbook below describes how to create the Mobilize project to manage this backlog. This is based on best practices from delivering Mobilize.    |
| Pre-conditions |
|   All pre-conditions must be met before starting steps in the migration runbook:  *    Either the AWS Engagement Manager or Customer Jira Admin will implement this runbook to establish the Mobilize Jira Project.    |
| Steps |
|   *   Create a New Project. Select Classic Project (as opposed to Next Gen).    ![](/.attachments/DK-MobilizeAccelerator/ClassicProject.png)  *   Select Scrum Project (as opposed to Kanban).   ![](/.attachments/DK-MobilizeAccelerator/Create%20Project.png)  *   In Project Settings, add a new Issue Type for Risks.    ![](/.attachments/DK-MobilizeAccelerator/ProjectSettings.png)  *   Issue types > Add issue type > Name: "Risk" > Click Add  *   Associate the newly added Issue Type to the "AWS Mobilize" Project.    ![](/.attachments/DK-MobilizeAccelerator/AddRisk.png)  *   In Project Settings > Workflow > Click the Pencil to open for editing. Click Add Status and select "In Review".    ![](/.attachments/DK-MobilizeAccelerator/EditWorkflow.png)  ![](/.attachments/DK-MobilizeAccelerator/AddStatus.png)  *   Add a Transition for this status    ![](/.attachments/DK-MobilizeAccelerator/AddTransition.png)  *   Publish the Workflow    ![](/.attachments/DK-MobilizeAccelerator/Publish.png)  *   In the "AWS Mobilize" Project, click Board Settings.    ![](/.attachments/DK-MobilizeAccelerator/BoardSettings.png)  *   Add a new Column for "In Review"    ![](/.attachments/DK-MobilizeAccelerator/InReview.png)  ![](/.attachments/DK-MobilizeAccelerator/Columns.png)      *   Configure Swimlanes based on Assignee    ![](/.attachments/DK-MobilizeAccelerator/Swimlanes.png)  *   Add a Quick Filter for Risks.    ![](/.attachments/DK-MobilizeAccelerator/Quickfilter-Risks.png)  *   Create a Release for Mobilize.    ![](/.attachments/DK-MobilizeAccelerator/MobilizeRelease.png)  *   Create a Release for Operate & Optimize.    ![](/.attachments/DK-MobilizeAccelerator/OandO-Release.png)  |
|   Post-conditions     |
|   All post-conditions must be met to to successfully finish this runbook:  *   *   All Mobilize participants have access to Jira and permissions to modify, comment, and move issues/tickets through the workflow.      *   The Mobilize backlogs are lazy loaded into the Mobilize Jira project.    |

 **Attachments:** 

