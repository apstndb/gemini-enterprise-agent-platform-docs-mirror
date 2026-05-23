---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/queryArtifactLineageSubgraph
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/queryArtifactLineageSubgraph
title: 'Method: artifacts.queryArtifactLineageSubgraph'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.artifacts.queryArtifactLineageSubgraph

Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.

### Endpoint

get `https: / /{service-endpoint} /v1 /{artifact}:queryArtifactLineageSubgraph`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`artifact` `string`

Required. The resource name of the Artifact whose Lineage needs to be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`

The request may error with FAILED\_PRECONDITION if the number of Artifacts, the number of Executions, or the number of events that would be returned for the Context exceeds 1000.

### Query parameters

`maxHops` `integer`

Specifies the size of the lineage graph in terms of number of hops from the specified artifact. Negative value: INVALID\_ARGUMENT error is returned 0: Only input artifact is returned. No value: Transitive closure is performed to return the complete graph.

`filter` `string`

Filter specifying the boolean condition for the Artifacts to satisfy in order to be part of the Lineage Subgraph. The syntax to define filter query is based on <https://google.aip.dev/160> . The supported set of filters include the following:

  - **attribute filtering** : For example: `display_name = "test"` Supported fields include: `name` , `display_name` , `uri` , `state` , `schema_title` , `create_time` , and `update_time` . time fields, such as `create_time` and `update_time` , require values specified in RFC-3339 format. For example: `create_time = "2020-11-19T11:30:00-04:00"`
  - **metadata field** : To filter on metadata fields use traversal operation as follows: `metadata.<fieldName>.<typeValue>` . For example: `metadata.field_1.number_value = 10.0` In case the field name contains special characters (such as colon), one can embed it inside double quote. For example: `metadata."field:1".number_value = 10.0`

Each of the above supported filter types can be combined together using logical operators ( `AND` & `OR` ). Maximum nested expression depth allowed is 5.

For example: `display_name = "test" AND metadata.field1.bool_value = true` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  LineageSubgraph  ` .
