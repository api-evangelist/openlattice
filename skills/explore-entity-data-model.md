---
name: explore-entity-data-model
description: Inspect the OpenLattice Entity Data Model (EDM) — namespaces, schemas, entity types, association types, and property types — and locate the EntitySet you need.
api: OpenLattice API
method: generated
source: openapi/openlattice-openapi.yaml
operations:
- getEntityDataModel
- getEntityDataModelVersion
- getAllEntitySets
- getEntitySetId
- getEntitySet
---

# Explore the OpenLattice Entity Data Model

Use this skill to understand the shape of an OpenLattice deployment before reading or writing data. Everything in OpenLattice is described by the Entity Data Model (EDM).

## Auth
Send `Authorization: Bearer <JWT>` on every request (scheme `http_auth`, JWT bearer). Base URL: `https://api.openlattice.com`.

## Steps
1. Call `getEntityDataModelVersion` (`GET /datastore/edm/version/`) to record the current EDM version you are working against.
2. Call `getEntityDataModel` (`GET /datastore/edm/`) to pull the full model: namespaces, schemas, entity types, association types, and property types.
3. Call `getAllEntitySets` (`GET /datastore/edm/entity/set/`) to list the EntitySets that actually hold data.
4. If you know an EntitySet by name, resolve its UUID with `getEntitySetId` (`GET /datastore/edm/ids/entity/set/{entitySetName}`).
5. Fetch the definition of a specific EntitySet with `getEntitySet` (`GET /datastore/edm/entity/set/{entitySetId}`).

## Notes
- Resources are keyed by UUID (`entitySetId`, `entityTypeId`, `propertyTypeId`).
- Only 200 responses are documented in the spec; treat non-200 as transport/auth errors.
