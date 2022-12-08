# Creating a custom migration journey<a name="custom-migration-tutorial"></a>

In this tutorial, you create a custom journey for the following migration scenario: [Rehost on\-premises workloads in the AWS Cloud: migration checklist](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/rehost-on-premises-workloads-in-the-aws-cloud-migration-checklist.html#rehost-on-premises-workloads-in-the-aws-cloud-migration-checklist-epics)\.

**Create the migration journey**

1. Open the AWS MigOps console at [https://beta.us-west-2.console.migops.migration-services.aws.dev/](https://beta.us-west-2.console.migops.migration-services.aws.dev/)\.

1. Choose **Go to MigOps Dashboard**\.

1. In the navigation pane, choose **Migration journeys**\.

1. Choose **Create journey**\.

1. In the **Journey creation method** tile, choose **Create custom journey**\.

1. In the **Journey details** tile, under **Journey name** enter **custom\-migration\-journey**\.

1. Under **Migration space**, choose **Create migration space**\.

1. In the **Space name** field, enter **tutorial\-two\-space**\.

1. In the **Phases** tile, enter **Planning phase** in the **Phase name** field\.

1. Choose **Add phase**, and then enter **Pre\-discovery** in the **Phase name** field\.

1. Repeat the previous step to add four more phases with the following names: **Discovery**, **Build**, **Test**, and **Cutover**\.

1. Choose **Create migration journey**\.

**Add a module to each of the phases of the journey**

In this procedure, you add a main module to contain the tasks that you will later add to each phase\.

1. In the navigation pane, choose **Migration journeys**\.

1. Choose the name of the journey **custom\-migration\-journey**\.

1. Choose the journey's **Modules** tab\.

1. In the **Modules in the Pre\-discovery phase** tile, choose **Actions**, then choose **Add module**\.

1. In the **Title** field, enter **Pre\-discovery main module**\.

1. For the **Phase** field, use the dropdown list to choose **Pre\-discovery**\.

1. Choose **Add module**\.

1. Repeat the steps in this procedure to add a module to each of the phases of the journey\.

**Add tasks to the modules of the journey**

1. In the journey's **Modules** tab, find the **Modules in the Pre\-discovery phase** tile, and choose **Main module**\.

1. Choose **Create task**\.

1. In the **Title** field, enter **Groom the pre\-discovery backlog\.**\.

1. For the **Module** field, choose **Pre\-discovery main module** from the dropdown list\.

1. For the task description, enter **Conduct the pre\-discovery backlog grooming working session with department leads and application owners\. **

1. Choose **Create task**\.

1. Repeat the steps in this procedure to add to the journey all of the tasks that are listed under [Epics](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/rehost-on-premises-workloads-in-the-aws-cloud-migration-checklist.html#rehost-on-premises-workloads-in-the-aws-cloud-migration-checklist-epics)\.