This is the DB Migration Questionnaire, that the AWS DB Consultants can use during discovery of the database to be migrated. This can be customised on the type of migration that the team is conducting.

|   |   **AWS Database Migration Questionnaire**   |  |
| --- | --- | --- |
|   |   Directions: Please compete the questions below for the Database to be migrated.    |  |
|   #   |   Category   |   Question   |
|   1   |   General Information   |   Timestamp   |
|   2   |   Email Address   |
|   3   |   Database Name   |
|   4   |   Dependent Application Names   |
|   5   |   Number of App's   |
|   6   |   |   |
|   7   |   Database Information   |   Is the database architecture documented? Provide if Architecture diagram is available?   |
|   8   |   How many concurrent users/clients use the Database? Approximately how many users?   |
|   9   |   What operating system does the application/workload run on? including Host server details (Including edition) ?   |
|   10   |   Is the database approaching a major version upgrade or end of life?   |
|   11   |   Is the development of database code is being freezed before starting the database migration?   |
|   12   |   What environments exist for the Databases? Describe the number/type of environments(DEV/TEST/STAGE/PROD) that exist to support this workload?   |
|   13   |   Are there any data classification requirements?   |
|   14   |   Are required ports and external access requirements documented?   |
|   15   |   Do you have regularly scheduled blackout/maintenance periods? If yes, what are they?   |
|   16   |    Is this database using any set of images/files / xml /JSON etc? Where and how are they managed? Are there any plans to move these to S3 or a suitable storage in AWS?   |
|   17   |   Do you have any cross database connections(upstream or downstream), Linked server or Any ETL's   |
|   18   |   |   |
|   19   |   Application and Integration   |   What kind of applications are making use of the database.   |
|   20   |   What is the primary application which make use of this database   |
|   21   |   what are other applications(BI,ETL,NIghtly batch job etc) connect to database.   |
|   22   |   What is connection pool setting (Minimum and maximum no. of connections)   |
|   23   |   Application making connection to database using JDBC or ODBC connection   |
|   24   |   What connection string being used by application   |
|   25   |   How other applications are connecting to database   |
|   26   |   Does the application uses Windows AD Authentication or SQL Authentication    |
|   27   |   Are applications using SSL connection to connect to database   |
|   28   |   |   |
|   29   |   Compliance and Data Sovereignty   |   Does the database have compliance requirements?   |
|   30   |   Are there any compliance frameworks that the database/workload operates under? (PCI/HIPPA?)   |
|   31   |   Are there specific encryption requirements? Is data encrypted at rest or in-transit?   |
|   32   |   |   |
|   33   |   Migration Specific   |   How many schemas are participating in migration   |
|   34   |   What is the total size of the database   |
|   35   |   Are you using any custom datatype   |
|   36   |   What is the total temporary tablespace size   |
|   37   |   What is the total size of transaction log space   |
|   38   |   collect the object status for each schema and object type   |
|   39   |   Do have any table with data type LOB/CLOB   |
|   40   |   What is the size of the largest LOB column   |
|   41   |   Is there any table which does not have  primary key or Unique-key/index   |
|   42   |   Get the list of all the tablespaces   |
|   43   |   What is the maximum no. of columns in tables   |
|   44   |   Are you  partitioning  the tables and what is the type of partition.   |
|   45   |   Are you using non-sql function definition written in C,java,Python etc.   |
|   46   |   Do have any table with data type var binary   |
|   47   |   |   |
|   48   |   SQL Server Features   |   Does your application uses Database mail to send out emails    |
|   49   |   Does your application uses xp\_cmdshell in code to execute OS commands (file copy , delete , execute ps script etc)   |
|   50   |   Does your database have any SQL agent jobs   |
|   51   |   Does your database have any SSIS packages in MSDB or filesystem   |
|   52   |   Does your application have any SSRS reports    |
|   53   |   Does your database have any FullText Indexes   |
|   54   |   Does your database have any cubes or does it utilises SSAS    |
|   55   |   Does your database use non default collation other than 'SQL\_Latin1\_General\_CP1\_CI\_AS'   |
|   56   |   Does your application utilises SQL server service broker for queuing   |
|   57   |   Is this database a publisher or a subscriber to any other database (replicating data to\\from any other database)   |
|   58   |   |   |
|   59   |   Monitoring   |   How do you monitor the instances ?    |
|   60   |   What third party tools are used to monitor the health of instances.   |
|   61   |   What metrics you collect and do you have a customised dashboard.   |
|   62   |   |   |
|   63   |   Production / cutover   |   Is downtime permitted for the database/migration to take place? What is the Acceptable Downtime   |
|   64   |   Does a ticket need to be submitted for firewall rules?   |
|   65   |   Does a ticket need to be submitted for cutover? Who needs to be notified for cutover of a database?   |
|   66   |   Who provides the final smoke and UAT tests sign off and is there a ticket for this?   |
|   67   |   Who is responsible for post cutover scripts, any tools installations?   |
|   68   |   |   |
|   69   |   Performance   |   Are you using default auto maintenance ?   |
|   70   |   Have you implemented any automation to gather stats other than jobs, any profiling setup   |
|   71   |   How much is the IOPS database is making during peak hours and special day/seasonal peaks   |
|   72   |   Collect few reports-- from non peak hours   |
|   73   |   Collect few reports-- from peak hours   |
|   74   |   Collect few reports for the special day/season  peak hours   |
|   75   |   Collect information about top wait events for the database   |
|   76   |   Collect information about log files switch frequency   |
|   77   |   How much archive/transaction(rollback) are getting generated per hour/day   |
|   78   |   |   |
|   79   |   Open Problems and incident   |   Any open error getting reported in log files   |
|   80   |   Any Recent outage/issues due to errors or due to performance problem   |
|   81   |   |   |
|   82   |   Testing and success criteria   |   How migration testing would be carried out(eg Unit testing,Data Validation,Object Validation)   |
|   83   |   How Performance/Stress testing will be carry out and what kind of support is needed   |
|   84   |   what are the tools which are going to be used for stress/performance testing   |
|   85   |   What would be our criteria to conclude migration is successful   |
|   86   |   Understanding of acceptable performance and functionality   |
|   |   |   |

 **Attachments:** 


[Database%20Migration%20Questionnaire-DK.xlsx](/.attachments/DK-DatabaseMigration/Database%20Migration%20Questionnaire-DK.xlsx)
