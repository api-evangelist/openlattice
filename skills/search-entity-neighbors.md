---
name: search-entity-neighbors
description: Run graph neighbor searches over OpenLattice EntitySets to find related entities and their connecting associations.
api: OpenLattice API
method: generated
source: openapi/openlattice-openapi.yaml
operations:
- getEntitySetId
- executeEntityNeighborSearch
- executeFilteredEntityNeighborSearch
- executeFilteredEntityNeighborIdSearch
---

# Search OpenLattice entity neighbors

OpenLattice stores data as a graph of entities connected by associations. Use this skill to traverse from a set of entities to their neighbors.

## Auth
`Authorization: Bearer <JWT>`. Base URL: `https://api.openlattice.com`.

## Steps
1. Resolve the target EntitySet UUID with `getEntitySetId` (`GET /datastore/edm/ids/entity/set/{entitySetName}`) if you only have a name.
2. For a broad traversal, call `executeEntityNeighborSearch` (`POST /datastore/search/{entitySetId}/neighbors`) with the entity ids to expand.
3. To constrain by association/neighbor types, call `executeFilteredEntityNeighborSearch` (`POST /datastore/search/{entitySetId}/neighbors/advanced`) passing a `neighborSearchFilter`.
4. When you only need neighbor ids (not full entities), use `executeFilteredEntityNeighborIdSearch` (`POST /datastore/search/{entitySetId}/neighbors/advanced/ids`).

## Notes
- Filters use the `neighborSearchFilter` schema (source/destination entity set ids + association types).
- Pagination, where present, is token-based via `pagingToken`.
