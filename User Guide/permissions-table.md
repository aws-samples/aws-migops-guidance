# Permissions<a name="permissions-table"></a>

AWS MigOps defines five roles: `MigrationSpaceAdmin`, `MigrationSpaceContributor`, `JourneyAdmin`, `JourneyContributor`, and `TeamContributor`\. The following sections describe the actions that each of the five roles can perform on migration spaces, migration journeys, and teams\. For information about how to get or assign these roles, see [Roles](roles.md)\.

## Role permissions in migration spaces<a name="migration-space-permissions"></a>

The following table shows the actions that the `MigrationSpaceAdmin` and `MigrationSpaceContributor` roles can perform on a migration space\. The `JourneyAdmin`, `JourneyContributor`, and `TeamContributor` roles don't grant any permissions to perform any of the actions listed in the table on migration spaces\.


| Action | MigrationSpaceAdmin | MigrationSpaceContributor | 
| --- | --- | --- | 
| View migration space | Yes | Yes | 
| Delete migration space | Yes | No | 
| Create migration space membership | Yes | No | 
| View migration space memberships | Yes | Yes | 
| Delete migration space memberships | Yes | No | 

## Role permissions in migration journeys<a name="migration-space-permissions"></a>

The following table shows the actions that the `MigrationSpaceAdmin`, `MigrationSpaceContributor`, `JourneyAdmin`, and `JourneyContributor` roles can perform on a migration journey\. The `TeamContributor` role doesn't grant any permissions to perform any of the actions listed in the table on migration journeys\.


| Action | MigrationSpaceAdmin | MigrationSpaceContributor | JourneyAdmin | JourneyContributor | 
| --- | --- | --- | --- | --- | 
| Create journey | Yes | Yes | No | No | 
| Transfer journey ownership | Yes | No | Yes | No | 
| View journey details | Yes | No | Yes | Yes | 
| View migration space journeys | Yes | No | No | No | 
| Delete journey | Yes | No | Yes | No | 
| Update journey | Yes | No | Yes | Yes | 
| Create journey membership | Yes | No | Yes | No | 
| View journey memberships | Yes | No | Yes | Yes | 
| Delete journey memberships | Yes | No | Yes | No | 
| Create phase | Yes | No | Yes | Yes | 
| Update phase | Yes | No | Yes | Yes | 
| Move phase out of scope | Yes | No | Yes | Yes | 
| Move phase into scope | Yes | No | Yes | Yes | 
| Delete phase | Yes | No | Yes | No | 
| View phases | Yes | No | Yes | Yes | 
| Create module | Yes | No | Yes | Yes | 
| Delete module | Yes | No | Yes | No | 
| View modules | Yes | No | Yes | Yes | 
| View module details | Yes | No | Yes | Yes | 
| Update module | Yes | No | Yes | Yes | 
| Move module out of scope | Yes | No | Yes | Yes | 
| Move module into scope | Yes | No | Yes | Yes | 
| Create task | Yes | No | Yes | Yes | 
| Update task | Yes | No | Yes | Yes | 
| Rerank task | Yes | No | Yes | Yes | 
| Delete task | Yes | No | Yes | No | 
| View tasks | Yes | No | Yes | Yes | 
| View task details | Yes | No | Yes | Yes | 
| Add comment | Yes | No | Yes | Yes | 
| Update comment | Yes | No | Yes | Yes | 
| View comments | Yes | No | Yes | Yes | 
| Delete comment | Yes | No | Yes | No | 
| Upload attachment | Yes | No | Yes | Yes | 
| View attachments | Yes | No | Yes | Yes | 
| Download attachment | Yes | No | Yes | Yes | 
| Delete attachment | Yes | No | Yes | No | 

## Role permissions in teams<a name="team-permissions"></a>

The following table shows the actions that the `MigrationSpaceAdmin`, `MigrationSpaceContributor`, and `TeamContributor` roles can perform on a team\. The `JourneyAdmin` and `JourneyContributor` roles don't grant permissions to perform any of the actions listed in the table on teams\.


| Action | MigrationSpaceAdmin | MigrationSpaceContributor | TeamContributor | 
| --- | --- | --- | --- | 
| Create team | Yes | No | No | 
| View teams | Yes | Yes | No | 
| View team details | Yes | Yes | Yes | 
| Create team membership | Yes | No | No | 
| View team memberships | Yes | Yes | Yes | 
| Delete team membership | Yes | No | No | 