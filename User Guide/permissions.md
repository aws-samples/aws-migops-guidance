# Roles and permissions<a name="permissions"></a>

MigOps defines the concept of membership\. Migrastion spaces and migration journeys can have individuals as members\. These are the individuals that can participate in the migration process\. Migration spaces and migration journeys can also have teams as members\. A team consists of individuals\. A team cannot contain other teams\. 

Members can have different roles\. The following table shows the five roles that MigOps defines\. It is possible to simultaneously have roles in different resources\. For example, an individual can simultaneously be a `MigrationSpaceAdmin` in one migration space, a `MigrationSpaceContributor` in another migration space, and a `JourneyAdmin` in several migration journeys in those two migration spaces, a `JourneyContributor` in a journey that's in a migration space of which that individual space isn't a member, and a `TeamContributor` in several teams in multiple migration spaces\. However, an individual or a team cannot simultaneously have more than one role in the same resource\. For example, an individual cannot simultaneously be a `JourneyAdmin` and a `JourneyContributor` within the same migration journey\.


****  

| Resource type | Possible member roles | 
| --- | --- | 
| Migration space | MigrationSpaceAdmin, MigrationSpaceContributor, none | 
| Migration journey | JourneyAdmin, JourneyContributor | 
| Team | TeamContributor | 

The following topics explain how to get these roles or assign them to others, and which actions each of the roles allow you to perform\.

**Topics**
+ [Roles](roles.md)
+ [Permissions](permissions-table.md)