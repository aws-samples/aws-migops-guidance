This section describes on how to use the data collected in the discovery phase by Modelize IT and using it to create Migration Waves in ModelizeIT.

### Understanding Discovered data

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2019.17.35.png)

The capacity plan section shows the total number of discovered servers. The section can be exported to csv by changing the url from .html to .csv. Some noteworthy columns are described below.

|   **Column name**   |   **Details**   |
| --- | --- |
|   Details   |   Has value Yes/No which is used to denote if the server data is collected through automation and is complete.   |
|   IP addresses   |   These are all the IP address discovered on the server, can banter   |
|   Strategy   |   This is the migration strategy, it uses the same rules as MPA for Strategy decision   |
|   Applications   |   Application assigned to the server   |
|   Affinities   |   Relationship group between applications (or/and servers)   |
|   Waves   |   Migration Waves   |

### Analysing applications

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2019.28.53.png)

When starting there will be no applications in the “Unknown App” section. The application identification has to be populated by clicking on identify (bottom button on the left navigation.)

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.40.35.png)

Once clicked on the button the “Unknown Apps” will be filled with multiple applications mapped to 1 or more servers/VM under them. The migration expert should look together with the application team to verify that the application grouping is correct and if so then name the “unknown” app.

Unknown Apps

For example an application (APP 5) is identified as DataProc app with Development running in Dev environment in the UK DC. Additional server names (from the discovered list in capacity plan) can also be added to the application group in the contains section.

Adding details to an Unknown App

Any application that should not be migrated can be marked out of scope by adding OOS as the Environment.

Once an application details are filled out, it moves from the “**Unknown**” category to “**Business Apps**” category.

#### Application Connections

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.19.41.png)

Application connection details can be viewed (at application or server level) by clicking on the icon

The list contains all the connections that were established by the servers in the group, usually only the connections with STATUS “Established” are considered important (to be confirmed with the application team). This information can be used to understand the relation between applications and derive the required firewall/security group rules.

#### Application Storage

Application storage can be analyzed by choosing Architecture (with NAS) diagram. This diagram will show network shares and which servers/users access the file systems.

When creating applications it is a good practice to base the group on the combination of

*   application name
    
*   Data centre or Location (if more than one)
    
*   Environment
    

This will help identification of affinity and creation of migration waves.

### Creating Affinity groups

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.46.27.png)

The affinity group is also empty initially and has to be populated by clicking on the identify button.

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.40.35.png)

This button will automatically create affinities based on the relationship between different applications. Usually one affinity has large number of applications while remaining affinities are less complex. Affinity groups will only be created from Business Apps (not Unknown Apps).

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.58.10.png)

The affinity with large complexity (number of applications) will have to be broken down to smaller chunks. This can be done based on the location of the applications, environment (Prod / Non Prod/ Dev) or by eliminating applications within the affinity that can easily be isolated (or do not represent a strong association).

Applications related to Infrastructure such as “Active Directory”, Monitoring systems, Management/ Asset Management applications, Security / Antivirus applications, Citrix, Database administration services etc. Such services are not highly critical to core application functionality and if agreed by customer application/Infa/security teams then can be moved out of the affinity. Usually such services by the virtue of being present in nearly all servers bound multiple applications to one affinity.

Once an affinity group is identified with the desired list of applications then it should be given a meaningful name. Saving it will move it to the “Affinity Groups” section. Changing of application in the affinity group is through the POID of the application. The application can be deleted or new application added to the affinity. Additionally servers can be added to the group by adding the server name.

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2023.19.32.png)

There is no check for duplicity in ModelizeIT so it is possible to have the same application in multiple Affinity groups.

### Creating Waves

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2023.08.07.png)

The waves are also empty initially and have to be populated by clicking on the identify button.

 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.40.35.png)

When clicking this button it will ask for the number of desired waves. The number of waves should be based on the possible and desired capacity of the wave. The application will automatically create Waves. The waves are created with the identified “Affinity Groups” and the best fit for the affinity groups and the desired number of waves. Affinity groups (@Aff\[POID = xx\]), applications(@App\[POID = xx\]) and servers (server hostname) can be added to the waves.

Wave to server mapping for all the servers and waves is available in the capacity plan section and can be downloaded from there.

 **Attachments:** 


[Screenshot%202021-10-04%20at%2019.17.35.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2019.17.35.png)

[Screenshot%202021-10-04%20at%2019.28.53.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2019.28.53.png)

[Screenshot%202021-10-04%20at%2021.37.54.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2021.37.54.png)

[Screenshot%202021-10-04%20at%2021.42.07.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2021.42.07.png)

[Screenshot%202021-10-04%20at%2022.19.41.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.19.41.png)

[Screenshot%202021-10-04%20at%2022.40.35.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.40.35.png)

[Screenshot%202021-10-04%20at%2022.46.27.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.46.27.png)

[Screenshot%202021-10-04%20at%2022.58.10.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2022.58.10.png)

[Screenshot%202021-10-04%20at%2023.08.07.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2023.08.07.png)

[Screenshot%202021-10-04%20at%2023.19.32.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2023.19.32.png)
