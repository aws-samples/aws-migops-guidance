# Phases<a name="phases"></a>

A migration journey consists of phases\. For example, a journey might have phases named Assess, Mobilize, Migrate, and Operate\. When you create a journey from a template, you get a journey with the phases that the template defines\. When you create a custom journey, you get an empty journey with no phases, and you can start adding the phases that make sense for your migration scenario\.

This topic describes the actions that you can perform on a phase\. Your role determines which of these actions you can perform\. For information about roles and permissions, see [Roles and permissions](permissions.md)\.

**To view the phases of a migration journey**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey whose phases you want to view\.

1. Choose the **Phases** tab\.



**To add a phase to a migration journey**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey where you want to add a phase\.

1. Choose the **Phases** tab\.

1. Choose **Add phase**\.

1. Enter a title and an optional description, then choose **Add phase**\.



**To view the modules in a phase**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey that contains the phase whose modules you want to view\.

1. Choose the **Phases** tab\.

1. Find the tile that represents the phase whose modules you want to view\.

1. Choose the number under **Number of modules**\.



**To move a phase out of scope**

You can move a phase out of scope\. This action removes its modules from the journey but doesn't delete the phase\. You can move the phase back in scope again at any time and that action puts its modules back in the journey\. There's no limit on the number of times that you can move a phase out of scope or back in scope\.

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey that contains the phase\.

1. Choose the **Phases** tab\.

1. In the tile that represents the phase that you want to move out of scope, choose **Actions**, then choose **Move phase out of scope**\.



**To move a phase back in scope**

When you move a phase back in scope, this action puts its modules back in the journey\. There's no limit on the number of times that you can move a phase out of scope or back in scope again\.

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey that contains the phase\.

1. Choose the **Phases** tab\.

1. In the tile that represents the phase that you want to move back in scope, choose **Actions**, then choose **Move phase into scope**\.



**To delete a phase**

When you delete a phase, you permanently remove it from the journey\. To delete a phase, you must first delete all of its tasks\. Only a member with the `JourneyAdmin` role can delete a phase\. A `JourneyContributor` can't delete a phase\. For more information about roles and permissions, see [Roles and permissions](permissions.md)\.

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the left navigation pane, choose **Migration journeys**\.

1. In the list of migration journeys, choose the name of the journey from which you want to delete a phase\.

1. Choose the **Phases** tab\.

1. Find the tile that represents the phase that you want to delete, then choose **Actions** button in that tile\. Choose **Delete phase**\.