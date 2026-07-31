---
name: manage-organization-permissions
description: Create and administer OpenLattice organizations, their members and roles, and the ACL permissions over their EntitySets.
api: OpenLattice API
method: generated
source: openapi/openlattice-openapi.yaml
operations:
- getOrganizations
- createOrganizationIfNotExists
- getOrganization
- getOrganizationEntitySets
- updateAcl
- getAcl
---

# Manage OpenLattice organizations and permissions

OpenLattice governs access with organizations, roles, principals, and ACLs (access control lists of ACEs) over securable objects.

## Auth
`Authorization: Bearer <JWT>`. Base URL: `https://api.openlattice.com`.

## Steps
1. List organizations you can see with `getOrganizations` (`GET /datastore/organizations/`).
2. Create one (idempotent-by-name on the server side) with `createOrganizationIfNotExists` (`POST /datastore/organizations/`).
3. Inspect an organization with `getOrganization` (`GET /datastore/organizations/{organizationId}`) and its EntitySets with `getOrganizationEntitySets`.
4. Read the current ACL on a securable object with `getAcl` (`POST /datastore/authorizations/`-family / `getAcl`).
5. Grant or revoke permissions by writing an `acl` (list of `ace` entries binding a `principal` to `permission`s) with `updateAcl`.

## Notes
- Principals and roles are the subjects of ACEs; permissions are enumerated (READ/WRITE/OWNER/...).
- Confirm the caller is authorized first via the authorizations endpoints before mutating an ACL.
