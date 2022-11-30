### Objectives

The AWS Schema Conversion Tool (AWS SCT) converts the source database schema and a majority of the database code objects, including views, stored procedures, and functions, to a format compatible with the target database. Any objects that cannot be automatically converted are clearly marked so that they can be manually converted to complete the migration. Based on the SCT Report generated during the Schema Conversion, manual conversions have to made for the objects that have not been automatically converted.

A tracker is maintained to track the conversion progress against which each individual maintains progress and reports updates. This tracker is used to present migration progress made each week to the respective stake holders. This tracker can also be shared with the Customer Teams so that they can use the same to review and share comments in real time.

Typically following are the instances where manual conversions are done - for example in SQL Server to Aurora compatible conversion -

*   Migrating custom data types
    
*   Procedure to function
    
*   Indexes creation to optimise performance
    
*   Optimising queries to match performance with source database
    
*   Sending email from PG Procedures
    

The converted code is typically executed and results are validated against the source database in order to validate correctness of conversion. This is the first step in ensuring that the code has been tested, further more the converted code is optimised to achieve optimal performance. Checks and reviews are conducted to ensure best practices are followed during code conversion.

As there are unique learnings from each Migration assignment it is a good idea to compile all these learnings as artefact(s) that could later be published internally or shared with the customer as a part of enablement.

During this time, the DB Migration team also works with Application teams to ensure that the Database works well with the application connected to the migrated database. This is usually a shared responsibility between the AWS and Customer Teams. AWS team ensures that the database routines and procedures return expected result, while Customer team own the functional testing of the applications. This could vary based on different engagements and scope defined for the project.

### Audience

AWS Migration Team

Customer Team

### Outcomes

*   Code Conversion Standards
    
*   Object Conversion Tracker
    
*   Learnings Manual
    
*   Converted Code
    

### Workflow

 **Attachments:** 


[CodeTransformation](/.attachments/DK-DatabaseMigration/CodeTransformation)

[CodeTransformation.png](/.attachments/DK-DatabaseMigration/CodeTransformation.png)

[Managing%20Large-Scale%20Database%20Migrations%20-%20Governance.pptx](/.attachments/DK-DatabaseMigration/Managing%20Large-Scale%20Database%20Migrations%20-%20Governance.pptx)
