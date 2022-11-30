  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

  

[[_TOC_]]

  

**Important Note:** capturing application and infrastructure metadata (regardless of the source) is an iterative approach. It can take several weeks to obtain the desired level of detail. The recommendation is to focus on the data that can be obtained now and to keep enriching the data set as more data is available. Do not wait for a full inventory to initiate discussions about tooling, assessment process, prioritization, migration strategy and wave planning.

Template
--------

The following template contains multiple sheets, as follows:

*   **Instructions**: contains information about the workbook and formulas
*   **Infrastructure**: list of IT assets of the following types: Servers, Containers, Appliances, other Devices.
*   **Applications**: list of applications (use unique entries per each SDLC environment/stage and specify the environment type in the relevant field)
*   **Databases**: list of database instances/schemas
*   **Remote Storage**: any storage that is not considered local or attached storage, for example NAS volumes, NFS mounts, Object storage, etc.
*   **Infra2App**: used to create unique records per each infrastructure to application mapping, this sheet is automatically populated based on dependency data from other sheets, see instructions tab.
*   **App2DB**: used to create unique records per each database to application mapping, this sheet is automatically populated based on dependency data from other sheets, see instructions tab.
*   **App2App**: used to create unique records per each application to application mapping.

 **Attachments:** 


[Inventory_Template_v3.xlsm](/.attachments/DK-Portfolio/Inventory_Template_v3.xlsm)
