# Migration journeys<a name="migration-journeys"></a>

A migration journey is an Amazon resource that you create and use to plan, organize, and track the migration of your solutions to AWS\. A journey consists of phases that represent the main stages of a migration\. Each phase consists of modules, which in turn consist of discrete tasks\.

## Creating a journey<a name="journey-creation"></a>

AWS MigOps provides templates that you can use to create your migration journey\. These templates represent common migration scenarios and follow best practices\. When you can create a journey from a template, you get a journey with predefined phases, modules, tasks, and subtasks\.

If you have a migration scenario that doesn't match any of the templates, you can create a custom journey\. In this case, you get an empty journey to which you add the phases, modules, tasks, and subtasks that you need for your migration\.

Whether you use a template or create a custom journey, you can edit the structure and details of the journey at any time\.

**To create a migration journey from a template**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. Choose **Create migration journey**\.

1. In the **Journey creation method** tile, keep the default option\.

1. In the **Journey details** tile, enter a name for the journey\.

   The description and target date files are optional\. If you leave them blank, you can specify them after you create the journey\.

   Choose the migration space in which you want to put the journey\. Alternatively, you can enter a name for a new migration space, and MigOps will create the migration space at the same time it creates the journey\. 

1. Choose the template that you want to use for the journey\.

1. Choose **Create migration journey**\.

**To create a custom migration journey**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. Choose **Create migration journey**\.

1. In the **Journey creation method** tile, choose **Create custom journey**\.

1. In the **Journey details** tile, enter a name for the journey\.

   The description and target date files are optional\. If you leave them blank, you can specify them after you create the journey\.

   Choose the migration space in which you want to put the journey\. Alternatively, you can enter a name for a new migration space, and MigOps will create the migration space at the same time it creates the journey\. 

1. In the **Create phases** tile, you can specify the phases that you want your journey to have\. However, you are not required to specify any phases while creating the journey\. You can add and remove phases after you create the journey\.

   To specify a phase, enter a name and an optional description for it\.

   To add a second phase, choose **Add phase**\.

1. Choose **Create migration journey**\.

## Journey status<a name="journey-status"></a>

A migration journey can have any of the status values that appear in the following table\. For information about how to change the status of a journey, see [Updating a journey](#journey-updates)\.


****  

| Status | Meaning | 
| --- | --- | 
| Not started | This is the initial status of a migration journey after you create the journey\. | 
| In progress | This status means that journey members have started working on the journey\. | 
| Completed | This status marks the journey as complete\. | 
| Creation failed | This status indicates that there was an error that prevented the successful creation of the journey\. If you see this status, delete the journey\. | 

## Updating a journey<a name="journey-updates"></a>

The following procedure shows you how to update the status, description, and target date of a migration journey\.

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey that you want to update\.

1. Choose **Actions**, then choose **Edit journey details**\.

1. Specify new values for the fields that you want to change, and then choose **Update**\.

For information about how to update the phases of a journey, see [Phases](phases.md)\.

For information about how to update the tasks of a journey, see [Tasks and subtasks](tasks.md)\.

## Transferring a journey<a name="journey-transfers"></a>

After you create a migration journey, you can send a request to transfer the journey to another individual\. If that individual accepts the transfer, they can move the journey to another migration space where they have the `MigrationSpaceAdmin` role\. That individual then becomes a `JourneyAdmin` for that journey\. For information about roles, see [Roles and permissions](permissions.md)\.

**To transfer a journey**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey that you want to transfer\.

1. Choose **Actions**, then choose **Transfer journey ownership**\.

1. Enter the email address of the person to whom you want to transfer the journey, and then choose **Transfer**\.

1. Notify the individual to whom you sent the transfer request that they will receive an email from the following address: `no-reply@es.prod.us-east-2.service.migops.migration-services.aws.dev`

   The body of the email will have a **Respond** button that they can use to accept or reject the transfer\.

   In addition to the invitation email, the individual can also go to **Pending actions** to see the transfer request that you sent them and to accept it or reject it\. For more information, see [Pending actions](pending-actions.md)\.
**Important**  
For the transfer to take effect, the individual to whom you sent the transfer request must accept that request\. To accept the request, they can choose **Respond** in the transfer email, or they can go directly to **Pending actions** in the AWS MigOps console\. For more information, see [Pending actions](pending-actions.md)\. 