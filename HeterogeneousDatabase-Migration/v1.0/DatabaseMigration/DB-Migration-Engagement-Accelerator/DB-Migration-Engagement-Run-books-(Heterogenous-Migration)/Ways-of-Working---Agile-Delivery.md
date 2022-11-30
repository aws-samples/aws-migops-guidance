* * *

Objective
---------

Based on Agile principles, incorporating the AWS Engagement Delivery Framework (EDF) as a Delivery mechanism. This run book can be leveraged by Engagement Manager while onboarding team for new Work Stream or re-iterating through the Ways of Working on adhoc basis during long engagements.

Audience
--------

*   AWS Team
    
    *   Engagement Manager
        
    *   Sr. Database Consultant
        
    *   Database Consultant
        
*   Partner Team
    
    *   Database/DevOps Consultant
        
*   Customer Team
    
    *   Outcome Owner (Product Owner)
        

Approach
--------

Key reason to undertake an Agile delivery approach is to reduce risk.

Scrum relies on cross-functional teams to deliver products and services in _**short cycles**_, enabling:

*   **Fast feedback**
    
*   **Continuous improvement**
    
*   **Rapid adaptation to change**
    
*   **Accelerated delivery**
    

Developing in short iterative cycles, ensures resources, time and budget are spent on highest value and most important items first.

Providing regular communication channels through Sprint Reviews (demonstrations), allows for opportunities for early correction, to ensure the end outcome adds value to Qantas and meets business expectations.

Agile Framework
---------------

The framework consists of 3 Team Roles, 3 key Artefacts and 4 key Events. 

|   **Artefacts**   |   **Roles**   |   **Events**   |
| --- | --- | --- |
|   *   Product Backlog      *   Sprint Backlog and      *   Developed (delivered) increment        |   1.  Outcome (Product) Owner      2.  Scrum Master      3.  Delivery Team        |   1.  Sprint Planning      2.  Daily Scrum      3.  Sprint Review       4.  Sprint Retro      5.  Backlog Grooming        |

 ![](/.attachments/DK-DatabaseMigration/image-20211007-053528.png)

**Scrum Teams - Pods**
----------------------

A typical **Scrum team (Pod)** consists of 5 to 8 **people** and generally includes the typical functional roles required to complete the project.

**Scrum Team Events**
---------------------

**Ceremonies scheduling suggestion:**  

**Note:** That as some teams will have off-shore resources in India, you may want to have your Sprint Planning in Day 10 after the Retro or move your Retro to Day 1 afternoon. 

|    **Day -2**   |    **Day -1**   |   **Day 1**   |   **Day 2**   |   **Day 3**   |   **Day 4**   |   **Day 5**   |   **Day 6**   |   **Day 7**   |   **Day 8**   |   **Day 9**   |   **Day 10**   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|   Backlog Grooming   |   Backlog Grooming   |   New Sprint   |         |         |         |         |         |         |         |         |   Sprint Review (demo for current sprint)  (1 hour)   |
|         |         |   Sprint Planning  (2-3 hours for a 2 week sprint)   |         |         |         |         |         |         |         |         |   Retrospective for current sprint  (30-45min)   |
|   Stand up   |   Stand up   |         |   Stand up   |   Stand up   |   Stand up   |   Stand up   |   Stand up   |   Stand up   |   Stand up   |   Stand up   |   Stand up   |

**Backlog Grooming**
--------------------

Goal**:** The aim is to be two to three sprints ahead in terms of prepared Epics and User Stories. An additional meeting/workshop is needed with the respective individuals to groom (refine) the user stories to get them ready to enter Sprint Plan.

### Epics and User Stories

Epics is a large User Story and contains smaller User Stories. Epics and User Stories should have the same description format.

#### User Story Format

Start with the description in the following format:

*   As a (**who** wants to accomplish something)
    
*   I want to (**what** they want to accomplish)
    
*   So that (**why** they want to accomplish that thing)
    

**Epic example**: "**As a** user, **I want to** back up my entire hard drive **so that** I don't lose my work."

**Story example:** "**As a** user, **I want to** indicate folders not to backup **so that** my backup drive isn't filled up with things I don't need saved."

The 'Acceptance Criteria' within a User Story should state what the outputs are or what conditions should be met for this story to be considered complete. In other words, it is like writing a high level acceptance test. The format of 'If, Then, When' can be used if desired.

#### Epic Title Format

The suggested Title format for Epics in Project, is as follows:

*   AXXX-AppName Discovery
    
*   AXXX-AppName Transformation
    
*   AXXX-AppName Implementation
    
*   AXXX-AppName Decommission
    

For streams where this does not apply, please consider having an Epic for grouping of key activities/work, for example:

*   Discovery
    
*   PoC
    
*   Integration
    
*   Transformation
    
*   Implementation
    
*   Decommission
    
*   etc...
    

### Definition of Ready and Done

The below criteria should be met for a User Story to be ready to go into Sprint Planning.

|   **Definition of Ready**   |
| --- |
|   *   Value of Story is indicated        |
|   *   Acceptance criteria is described        |
|   *   User stories dependencies are identified/met        |
|   *   Business stakeholders are briefed if applicable        |
|   *   Solution Design is endorsed        |
|   *   Performance criteria identified (NFR)        |
|   *   User story is sized (S,M,L)        |
|   *   Person who will work on user story is identified        |
|   *   Team know how to demo user story        |

For a User Story to be considered as completed, it should meet the following Definition of Done (DoD) criteria. 

|   **Definition of Done**   |
| --- |
|   *   Unit tests passed        |
|   *   Code reviewed        |
|   *   Acceptance criteria met        |
|   *   Functional tests passed        |
|   *   Non functional requirements met        |
|   *   Outcome owner accepts user story or Epic as Done        |

**User Story Estimation**
-------------------------

**T-Shirt** sizing and **Fibonacci.**   
Note: Fibonacci scale consists of a **sequence** of **numbers** used for estimating the relative size of user stories in points. The [**Fibonacci**](https://en.wikipedia.org/wiki/Fibonacci_scale_(agile)#Procedure) **sequence** consists of **numbers** that are the summation of the two preceding **numbers**, starting with \[0, 1, 2, 3, 5, 8, 13, etc\].

|   **T-shirt Size**   |   **Points Equivalence**   |
| --- | --- |
|   XS   |   1 (This is likely a task and not a story. See if it can be a sub-task of a story)   |
|   S   |   3   |
|   M   |   5   |
|   L   |   8   |
|   XL   |   13 and above  (Need to split the story)   |

**Estimation Assumptions**

Point estimations are a sizing only and do not align to a specific amount of time, however the assumptions we have used to guide the team are as below:

*   the team will use T-shirt sizing of XS (1 point), S(3 points), M (5 points), L (8 points), XL (13 points).
    
*   User Stories in a Sprint can only be between 3 and 8 points.
    
*   If below 3 points then it's not a story but a sub-task of a story. If it's over 8 points then it is too big and needs further clarification and refinement (i.e. backlog grooming). 
    

**Daily-stand ups**
-------------------

Daily scrum : 15 minutes

To be run at a time that ensures all Dojo team members can attend.

  
**Sprint Review/Demo**

The Streams will each have a Sprint Review at the end of their sprints. It is suggested to have a single review session per stream, irrespective of the number of teams in the stream. Reviews should be approximately 1 hour. Below is a suggested Agenda format for the session:

|   **DUR.**   |   **ACTIVITY**   |   **DESCRIPTION**   |   **WHO**   |
| --- | --- | --- | --- |
|   5 min   |   Goal of the Sprint   |   •Introduction into Sprint Goal  •Review of Backlog Roadmap   |   Outcome Owner   |
|   15 min   |   Sprint Status   |   •Plan vs reality  •Sprint statistics  •Statics of bug fixes   |   Scrum Master   |
|   30 min   |   Demonstration   |   •Demonstration of key completed stories   |   Team   |
|    5 min   |   What’s next?   |   •User stories in focus for the next Sprint   |   Scrum Master   |

**Sprint Retrospective**
------------------------

Will be held at the end of each sprint for approximately 30-45 min.

Focus on Continuous improvements on what was done right and what can be done better.

**Code Review Process**
-----------------------

It is the responsibility of the Lead Database Consultant in each Scrum team to ensure Peer reviews are taking place.

Architecture Endorsement Process - Governance Forum
---------------------------------------------------

Weekly forum held weekly on Tuesdays with key decision makers, including Customer Security. The key objective of this forum is to endorse Database Migration Plans for the Customer Cloud Platform.

Please use the Architecture Decision template to present at the Governance Forum

Architecture decisions will be documented in Confluence: **Architecture Decisions Logs**

References
----------

 [Ways%20of%20Working%20-%20Work%20Stream%20Alignment%20Pack.pptx](/.attachments/DK-DatabaseMigration/Ways%20of%20Working%20-%20Work%20Stream%20Alignment%20Pack.pptx)

 **Attachments:** 


[Ways%20of%20Working%20-%20Work%20Stream%20Alignment%20Pack.pptx](/.attachments/DK-DatabaseMigration/Ways%20of%20Working%20-%20Work%20Stream%20Alignment%20Pack.pptx)

[image-20211007-053528.png](/.attachments/DK-DatabaseMigration/image-20211007-053528.png)
