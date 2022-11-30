### Objectives

AWS DMS is a common tool used to load data from source database to target database, most of the heterogenous migrations such as Oracle or SQL Server to Amazon Aurora is supported. The team ensures that the replication instance is setup and endpoints for both source and target are available before running the DMS. A test is conducted to ensure connectivity between these endpoints and the replication instance.

A migration task for full load or full load with cdc is created to load the data. Full load task is started and statistics are captured for the table data being loaded which is later useful to determine production downtime required. Once the data load is completed data is verified between the source and the target databases and any anomalies are identified. Any anomaly identified is separately handled and scripts to handle the same are created and checked in.

Thorough testing is conducted to ensure there has been no data loss. Row counts are compared, data comparison tools are used to validate data correctness as well.

Please note that there might be multiple DMS Tasks created if the data volume in a particular table or table(s) is high in order to ensure better performance.

### Audience

AWS Team

*   DB Consultant(s)
    
*   DevOps (Optional)
    

### Outcomes

*   Target Database with loaded data
    
*   DMS Tasks
    
*   Custom SQL Scripts to handle issues
    

### Workflow

 **Attachments:** 


[DataLoad](/.attachments/DK-DatabaseMigration/DataLoad)

[DataLoad.png](/.attachments/DK-DatabaseMigration/DataLoad.png)
