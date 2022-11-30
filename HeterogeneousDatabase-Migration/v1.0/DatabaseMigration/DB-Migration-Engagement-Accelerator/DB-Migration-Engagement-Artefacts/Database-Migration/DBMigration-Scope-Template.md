This is the baseline scope document template that will be prepared by the AWS DB Consultant post discovery, analysis and estimation of effort. This is presented to the customer team to do a walk through of the scope and get an agreement with respect to in/out of scope items.

 ![](/.attachments/DK-DatabaseMigration/att_1_for_1978105915.png)

<<Database Name>>
=================

MIGRATION SCOPE
===============

DOCUMENT
========

|   Author Name   |   Description   |   Date   |
| --- | --- | --- |
|   |   |   |

  

[<<Source Database Details >> 2](#_Toc71721441)

[Scope 2](#_Toc71721442)

[In Scope 2](#_Toc71721443)

[SCT Converted code Location 2](#_Toc71721444)

[Scope - Database Objects Summary 2](#_Toc71721445)

[Out of Scope 3](#_Toc71721446)

[List of Objects in/out of scope - 3](#_Toc71721447)

[List of Objects which need change in definition 3](#_Toc71721448)

[Assumptions 3](#_Toc71721449)

[Risks 3](#_Toc71721450)

[Links to Tracker 4](#_Toc71721451)

  

<<Source Database Details >>
----------------------------

|   Database Name   |   |
| --- | --- |
|   Tech Stack   |   |
|   Git   |   |
|   Source DB details   |   |
|   App Owner   |   |
|   DB Owner   |   |
|   Deep Dive Link   |   |

Scope
-----

<<DB Name>> database migration contains xx databases to be migrated.

### In Scope

1.  Migrate all the existing objects to work in PostgreSQL (Creation of PostgreSQL schema(s) and objects)
    
2.  Data Load using DMS from Source SQL Server to PostgreSQL
    
3.  Sample Data Validation using DMS such as counts, null specific value, special characters, Case sensitive data.
    
4.  Unit testing of all migrated objects, conversion of Unit Test Suite (in case existing)
    
5.  Addressing performance issues that are a by-product of migration, limited to very specific changes made for code conversion.
    
6.  Handover documentation
    
7.  Application Support on Dev testing and Staging setup.
    

Total databases

SSIS/SSRS

### SCT Converted code Location

|   **#**   |   **Database Name**   |   **Location**   |
| --- | --- | --- |
|   |   |   |
|   |   |   |

### Scope - Database Objects Summary

|   #   |   Object   |   Count   |
| --- | --- | --- |
|   1   |   INLINE\_FUNCTION   |   1   |
|   2   |   TABLE\_TYPE   |   2   |
|   3   |   SCALAR\_FUNCTION   |   5   |
|   4   |   PROCEDURE   |   11   |
|   5   |   VIEW   |   53   |
|   6   |   TRIGGER   |   14   |
|   7   |   INDEX   |   63   |
|   8   |   CONSTRAINT   |   774   |
|   9   |   TABLE   |   569/611   |
|   10   |   SCHEMA   |   |
|   11   |   SQL\_syntax\_elements\_number   |   |
|   12   |   Storage\_objects\_count   |   |
|   13   |   Code\_objects\_count   |   |

Out of Scope
------------

<<Call out all out of scope items such as Objects not converted or >>

### List of Objects out of scope -

|   #   |   Object Type   |   Object Name   |   Out of Scope (yes/no)   |
| --- | --- | --- | --- |
|   1   |   schema   |   |   |
|   2   |   schema   |   |   |
|   3   |   schema   |   |   |
|   4   |   Agent Job   |   |   |
|   5   |   Procedure   |   |   |
|   6   |   schema   |   |   |

### List of Objects which need change in definition

|   #   |   Object type   |   Database   |   Object Under   |   Object Name   |   Change recommendation   |
| --- | --- | --- | --- | --- | --- |
|   1   |   Column name   |   |   |   |   |
|   2   |   Column name   |   |   |   |   |

Assumptions
-----------

<< List all assumptions here>>

Risks
-----

<<List all risks here>>

Links to Tracker
----------------

*   SCT Report
    
*   Estimation

 **Attachments:** 


[DBMigration_Scope_Template.docx](/.attachments/DK-DatabaseMigration/DBMigration_Scope_Template.docx)

[att_1_for_1978105915.png](/.attachments/DK-DatabaseMigration/att_1_for_1978105915.png)
