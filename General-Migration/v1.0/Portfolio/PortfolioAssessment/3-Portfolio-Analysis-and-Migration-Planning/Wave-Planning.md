  

**Document Lifecycle Status**

|    |    |    |    |
| --- | --- | --- | --- |

  

[[_TOC_]]

Guidelines
----------

If the Discovery Tool of choice does not include Wave Planning features, you can use the ProServe Migration Portfolio Assessment ([MPA](http://mpa-proserve.amazonaws.com/ "http://mpa-proserve.amazonaws.com/")) tool (available to AWS Employees and Partners) to construct the plan. Ensure all assets and communications data from the discovery tool of choice have been exported and then imported into MPA. This information is key to analyze dependencies during the Wave Planning process.

Besides the tool of choice, start with socializing the following definitions:

*   **Soft Dependency:** is a relationship between two or more assets such as servers, containers, applications, etc. that is not dependent on the location of the interacting components. For example, two systems that operate in the same local network (or same infrastructure) can be split apart by moving one of those systems to the cloud whilst the other remains on-premises. The communication can continue, with no impact to functional/non-functional requirements, over WAN links such as Direct Connect.
    
*   **Hard Dependency:** is a relationship between two or more assets such as servers, containers, applications, etc. that is dependent on location. For example, two systems that operate in the same local network and that are heavily dependent on low latency for communication (e.g., application server and database server). Moving only one of these systems to the cloud would cause functionality/performance problems that cannot be resolved. Likewise, non-technical reasons such as resource availability (e.g., team performing the migration) or operational constraints might create a hard dependency between assets. For example, moving two applications that are dependant to each other in different waves would cause a double outage experience that is not practical or acceptable.
    
*   **Dependency Groups:** these are composed of assets that must be migrated at the same time due to dependencies that cannot be resolved (i.e., hard dependencies). Groups will be combined into waves. A dependency group can be as small as containing one application component and one server, or as large as containing several applications and dozens of servers.
    
*   **Migration Waves:** consist of one or more dependency groups and span a period of time that could range from days to weeks or months. Waves are aligned to a criteria in order to define its duration and the groups they will contain. For example, waves can be aligned to business outcomes. Ideally, the completion of a wave should reflect a measurable achievement. In some cases, other criteria can be used to create waves. For example, crating waves by environment, or by migration strategy.
    

Creating a Wave Plan
--------------------

Start with analyzing dates to create an initial high-level structure of empty waves. **Consider the following**:

*   What is the total migration program length? What are the deadlines? Fixed Data Center exit dates? Co-location contract end dates? Refresh cycles? Application release cycles? Plot these items into a a plan.
    
*   Are there any dates where migrations should be avoided? (e.g., end of year, holidays, business events, release cycles)
*   What is the maximum size of a wave in terms of the number of dependency groups it can contain? Note: wave size is typically dictated by risk appetite (e.g., how much parallel change can be tolerated), and resource availability (e.g., how much parallel change can be performed with the available resources and budget). However, do not be limited by resource requirements/availability during early planning, waves that contain more than one dependency group can be decomposed into smaller waves later on, if needed.
    
*   What is the default wave length? Note: smaller waves are preferable (e.g., 6 weeks). Wave length will be a function of the time required to complete the migration of one or more dependency groups, including the time to assess/design the AWS target architecture, create migration runbooks and cutover planning, setup migration tooling, time to replicate data, operational readiness, time to perform the cut-over, test and go live/roll-back, and post-migration operational handover and wave closure.
    
*   Are there specific Compliance/Regulatory requirements that need to be factored in? (e.g., workload validation pre- and post-migration)
    

  

### High-level plan sample

  

[PlanSample](/.attachments/DK-Portfolio/PlanSample.drawio)
[PlanSample](/.attachments/DK-Portfolio/PlanSample.drawio)

Note the overlap between waves in the diagram above. This is in order to accelerate the migration process. The key to overlapped waves is to define and consider that happens within a wave. Typically, deployment activities, platform validation, and data synchronization will occur during the first half of a wave. The second half will focus on cut-over preparation, the actual migration, testing, and operational handover. This means that different teams are involved in the process and that some efficiencies can be gained.  For example, as soon as the team involved in platform preparation has completed their work they can start working on the requirements of the next wave whilst the migration team takes over.

Also, note that not all waves have the same length. This will occur later in the wave planning process when the size of a given wave must be extended in order to meet dependency or operational requirements. In general, it is preferable that most waves have a similar length and structure in order to facilitate a factory-like approach to migrations.

  

Structure of a wave (sample). Note that phases within the wave have been specified to group activities into specific wave phases. This will help to plan resources and to schedule the waves activities.

[WaveConstruct](/.attachments/DK-Portfolio/WaveConstruct.drawio)
[WaveConstruct](/.attachments/DK-Portfolio/WaveConstruct.drawio)

### Analyzing Dependencies and assigning groups of applications to waves

Consider the wave structure and how the platform and migration teams are organized when constructing the initial plan. Once the initial high-level plan has been defined, use the **Artifact - Application Prioritization Criteria** (at this stage it expected this artifact has been baselined to prioritize applications based on business drivers or other factors) to select a chunk of applications from the top of the ranking. Next, analyze dependencies and start to compose the **Dependency Groups** for those applications. When using tooling, these groups might be automatically populated based on communication patterns and communication criticality, if this is the case, proceed to review and validate these groups. In general, a chunk of prioritized applications does not equate to a Dependency Group and it will only serve as a planning guide. Analyze application dependencies in order to classify these as Soft or Hard. Hard dependencies will drag more applications into the groups, including applications that are currently at the bottom of the the prioritization list. Establish the Dependency Groups for the chunk of applications that have been prioritized. In some cases, this will require to remove a prioritized application from a wave. Then, align those groups to one or more waves depending on business outcomes and the established wave capacity.

When using the [MPA tool (available to AWS Employees and Partners)](http://mpa-proserve.amazonaws.com/) to create wave plans  or Discovery Tooling that has wave planning functionality, these Dependency Groups will be automatically populated based on communication data and patterns. However, the fact that two or more servers/applications communicate does not mean they need to be migrated together (refer to the Soft and Hard dependency definitions above). Some of these communications might be between applications that can operate in different locations via WAN links. Likewise, shared infrastructure services, such as DNS or Active Directory (considered Soft dependencies) can create false dependency groups. Depending the tool capabilities, it might not discriminate between Soft and Hard dependencies automatically, hence, this is something that could require manual assessment. Verify auto-generated dependency groups and remove soft dependencies.

Most Discovery Tools and MPA have a group visualization feature that permits to analyze the dependencies in graphical mode. If necessary, select the auto-generated groups and remove applications where its dependency can be considered Soft. In MPA, this will automatically place the removed application into a new group. MPA contains a default group named 'Shared Infrastructure', applications marked as shared infrastructure will be automatically placed in this group and dependencies will be automatically ignored. Consider using this feature when working with this type of asset. However, this will place any system marked as shared into this unique group, this means that the whole group will be migrated at some point. In some cases this is not practical, especially when these shared services will be moved or extended at different points in time. If this is your case, then break dependencies to the shared services in order to place the shared service into a new application group.

When analyzing dependencies, consider these questions:

*   Can these dependencies be ignored?
*   Can these applications be removed from the group?
    
*   Is there any shared service?
    
*   Is there a missed dependency that forces incorporating more applications into a group?
    

Once the Dependency Groups for a given Wave have been established, review resource requirements to migrate the wave. Consider adjusting the wave size (i.e., dependency groups it contains) based on resource requirements. This could lead to smaller or bigger waves. Iterate the wave plan as needed until all waves have been defined. Work with the Migration workstream to define the level of effort and skill required to migrate each wave, consider resource availability and parallel work in order to define wave duration.

**Important Note:** wave planning within the Portfolio Analysis Party is aimed at creating the initial wave skeleton and at defining dependency groups for Wave 1 where possible. Wave planning is a time consuming activity and will require iteration over subsequent weeks in order to obtain a baselined version.

Migration Scope
---------------

The portfolio of applications and associated infrastructure will change during the lifecycle of migration programs. This is expected and should be managed. Scope changes will affect Dependency Groups and Waves. It is key to establish a scope control mechanism in order to handle change and minimize impact. It is expected that the scope of a wave or dependency group will require changes, especially closer to the migration date when a previously unknown dependency is identified or a new server is included in the inventory. Sometimes this can happen during the migration itself. Long-running migration programs coexist with normal business evolution and change. Applications keep evolving as they wait to migrated. Servers are added/removed, new infrastructure is deployed on-premises, etc. A wave plan must be prepared to handle these changes.

A scope change control mechanisms requires the definition of a single source of truth for the scope. This could be a tool to manage the scope, a csv file or spreadsheet, or a database, as defined by the program. The key is to identify changes, analyze impact, and communicate change to the relevant stakeholders to take action. The wave plan will be iterated as a result.

Wave Plan
---------

Export the Wave Plan from the Discovery Tool of choice or provide a link to the tool. If using MPA, export the Wave plan and include it in this page.

 **Attachments:** 


[PlanSample.drawio](/.attachments/DK-Portfolio/PlanSample.drawio)

[PlanSample.drawio.png](/.attachments/DK-Portfolio/PlanSample.drawio.png)

[WaveConstruct.drawio](/.attachments/DK-Portfolio/WaveConstruct.drawio)

[WaveConstruct.drawio.png](/.attachments/DK-Portfolio/WaveConstruct.drawio.png)
