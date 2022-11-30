  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Cluster Breakdown by VM and Mesh
--------------------------------

This table is meant to record meshes with their respective compute profiles.

*   **On-premises cluster:** This is the on-prem cluster from where the virtual machines will be migrated to the VMC environment
*   **Migrating VM count:** This the total number of VMs that will be migrated in this service mesh
*   **Migrating Data:** Total amount of data in TB that will be moved across the service mesh
*   **Mesh Name:** Name of the service mesh created in VMC. An HCX Service Mesh is the effective HCX services configuration for a source and destination site. A Service Mesh can be added to a connected Site Pair that has a valid Compute Profile created on both of the sites.Adding a Service Mesh initiates the deployment of HCX Interconnect virtual appliances on both of the sites. An interconnect Service Mesh is always created at the source site.
*   **Compute Profile Name:** A Compute Profile contains the compute, storage, and network settings that HCX uses to deploy the Interconnect-dedicated virtual appliances when a Service Mesh is added. This column contains the name of the compute profile

  

| **On-prem Cluster** | **Migrating VM Count** | **Migrating TBs** | **Mesh** | **Compute Profile** |
| --- | --- | --- | --- | --- |
|     |     |     |     |     |
|     |     |     |     |     |
|     |     |     |     |     |
|     |     |     |     |     |
|     |     |     |     |     |
|     |     |     |     |     |
|     |     |     |     |     |

Mesh Configuration
------------------

This table is track possible multi-service mesh design configuration. Creating a many to many configuration would likely improve throughput which would be very helpful during a migration.

*   **Mesh Name:** This is the name of the service mesh. The service mesh itself is deployed by selecting a compute profile on both sides of an existing site pair.
*   **Management Cluster:** This is the management cluster which is located on premises.
*   **On-premises HCX Manager IP:** This is the IP address of the on-premises HCX manager.
*   **Interconnect:** This is the name of the HCX IX appliance that was created during creation of service mesh: The HCX-IX service appliance provides replication and vMotion-based migration capabilities over the Internet and private lines to the destination site whereas providing strong encryption, traffic engineering, and virtual machine mobility.
*   **VMC HCX Manager IP:** This is the IP address for the VMC manager
*   **VMs per mesh:** This accounts for all the virtual machines that would be migrated per service mesh

  

| **Mesh Name** | **Management Cluster** | **On-Prem Manager IP** | **Interconnect** | **VMC Manager IP** | **VMs per Mesh** |
| --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     |
|     |     |     |     |     |     |
|     |     |     |     |     |     |
|     |     |     |     |     |     |
|     |     |     |     |     |     |
|     |     |     |     |     |     |

 **Attachments:** 

