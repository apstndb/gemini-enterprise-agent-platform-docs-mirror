---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews
title: 'REST Resource: projects.locations.featureOnlineStores.featureViews'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeatureView

FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig.

Fields

`name` `string`

Identifier. name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this FeatureView was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this FeatureView was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your FeatureViews.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`syncConfig` ` object ( SyncConfig  ` )

Configures when data is to be synced/updated for this FeatureView. At the end of the sync the latest featureValues for each entityId of this FeatureView are made ready for online serving.

` vectorSearchConfig (deprecated)  ` ` object ( VectorSearchConfig  ` )

> This item is deprecated\!

Optional. Deprecated: please use `  FeatureView.index_config  ` instead.

`indexConfig` ` object ( IndexConfig  ` )

Optional. Configuration for index preparation for vector search. It contains the required configurations to create an index from source data, so that approximate nearest neighbor (a.k.a ANN) algorithms search can be performed during online serving.

`optimizedConfig` ` object ( OptimizedConfig  ` )

Optional. Configuration for FeatureView created under Optimized FeatureOnlineStore.

`serviceAgentType` ` enum ( ServiceAgentType  ` )

Optional. service agent type used during data sync. By default, the Agent Platform service Agent is used. When using an IAM Policy to isolate this FeatureView within a project, a separate service account should be provisioned by setting this field to `SERVICE_AGENT_TYPE_FEATURE_VIEW` . This will generate a separate service account to access the BigQuery source table.

`serviceAccountEmail` `string`

Output only. A service Account unique to this FeatureView. The role bigquery.dataViewer should be granted to this service account to allow Agent Platform feature Store to sync data to the online store.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`bigtableMetadata` ` object ( BigtableMetadata  ` )

Output only. metadata containing information about the Cloud Bigtable.

`source` `Union type`

`source` can be only one of the following:

`bigQuerySource` ` object ( BigQuerySource  ` )

Optional. Configures how data is supposed to be extracted from a BigQuery source to be loaded onto the FeatureOnlineStore.

`featureRegistrySource` ` object ( FeatureRegistrySource  ` )

Optional. Configures the features from a feature Registry source that need to be loaded onto the FeatureOnlineStore.

`vertexRagSource` ` object ( VertexRagSource  ` )

Optional. The Vertex RAG Source that the FeatureView is linked to.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;syncConfig&quot;: {object (SyncConfig)},&quot;vectorSearchConfig&quot;: {object (VectorSearchConfig)},&quot;indexConfig&quot;: {object (IndexConfig)},&quot;optimizedConfig&quot;: {object (OptimizedConfig)},&quot;serviceAgentType&quot;: enum (ServiceAgentType),&quot;serviceAccountEmail&quot;: string,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,&quot;bigtableMetadata&quot;: {object (BigtableMetadata)},// source&quot;bigQuerySource&quot;: {object (BigQuerySource)},&quot;featureRegistrySource&quot;: {object (FeatureRegistrySource)},&quot;vertexRagSource&quot;: {object (VertexRagSource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## BigQuerySource

Fields

`uri` `string`

Required. The BigQuery view URI that will be materialized on each sync trigger based on FeatureView.SyncConfig.

`entityIdColumns[]` `string`

Required. columns to construct entityId / row keys.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;uri&quot;: string,
  &quot;entityIdColumns&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureRegistrySource

A feature Registry source for features that need to be synced to Online Store.

Fields

`featureGroups[]` ` object ( FeatureGroup  ` )

Required. List of features that need to be synced to Online Store.

`projectNumber` `string ( int64 format)`

Optional. The project number of the parent project of the feature Groups.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureGroups&quot;: [{object (FeatureGroup)}],&quot;projectNumber&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureGroup

Features belonging to a single feature group that will be synced to Online Store.

Fields

`featureGroupId` `string`

Required. Identifier of the feature group.

`featureIds[]` `string`

Required. Identifiers of features under the feature group.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;featureGroupId&quot;: string,
  &quot;featureIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## VertexRagSource

A Vertex Rag source for features that need to be synced to Online Store.

Fields

`uri` `string`

Required. The BigQuery view/table URI that will be materialized on each manual sync trigger. The table/view is expected to have the following columns and types at least: - `corpusId` (STRING, NULLABLE/REQUIRED) - `fileId` (STRING, NULLABLE/REQUIRED) - `chunkId` (STRING, NULLABLE/REQUIRED) - `chunk_data_type` (STRING, NULLABLE/REQUIRED) - `chunk_data` (STRING, NULLABLE/REQUIRED) - `embeddings` (FLOAT, REPEATED) - `file_original_uri` (STRING, NULLABLE/REQUIRED)

`ragCorpusId` `string ( int64 format)`

Optional. The RAG corpus id corresponding to this FeatureView.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;uri&quot;: string,
  &quot;ragCorpusId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SyncConfig

Configuration for Sync. Only one option is set.

Fields

`cron` `string`

Cron schedule ( <https://en.wikipedia.org/wiki/Cron> ) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON\_TZ=${IANA\_TIME\_ZONE}" or "TZ=${IANA\_TIME\_ZONE}". The ${IANA\_TIME\_ZONE} may only be a valid string from IANA time zone database. For example, "CRON\_TZ=America/New\_York 1 \* \* \* \*", or "TZ=America/New\_York 1 \* \* \* \*".

`continuous` `boolean`

Optional. If true, syncs the FeatureView in a continuous manner to Online Store.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;cron&quot;: string,
  &quot;continuous&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## VectorSearchConfig

> This item is deprecated\!

Deprecated. Use `  IndexConfig  ` instead.

Fields

`embeddingColumn` `string`

Optional. column of embedding. This column contains the source data to create index for vector search. embeddingColumn must be set when using vector search.

`filterColumns[]` `string`

Optional. columns of features that're used to filter vector search results.

`crowdingColumn` `string`

Optional. column of crowding. This column contains crowding attribute which is a constraint on a neighbor list produced by `  FeatureOnlineStoreService.SearchNearestEntities  ` to diversify search results. If `  NearestNeighborQuery.per_crowding_attribute_neighbor_count  ` is set to K in `SearchNearestEntitiesRequest` , it's guaranteed that no more than K entities of the same crowding attribute are returned in the response.

`distanceMeasureType` ` enum ( DistanceMeasureType  ` )

Optional. The distance measure used in nearest neighbor search.

`algorithm_config` `Union type`

The configuration with regard to the algorithms used for efficient search. `algorithm_config` can be only one of the following:

`treeAhConfig` ` object ( TreeAHConfig  ` )

Optional. Configuration options for the tree-AH algorithm (Shallow tree + Asymmetric Hashing). Please refer to this paper for more details: <https://arxiv.org/abs/1908.10396>

`bruteForceConfig` ` object ( BruteForceConfig  ` )

Optional. Configuration options for using brute force search, which simply implements the standard linear search in the database for each query. It is primarily meant for benchmarking and to generate the ground truth for approximate search.

`embeddingDimension` `integer`

Optional. The number of dimensions of the input embedding.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;embeddingColumn&quot;: string,&quot;filterColumns&quot;: [string],&quot;crowdingColumn&quot;: string,&quot;distanceMeasureType&quot;: enum (DistanceMeasureType),// algorithm_config&quot;treeAhConfig&quot;: {object (TreeAHConfig)},&quot;bruteForceConfig&quot;: {object (BruteForceConfig)}// Union type&quot;embeddingDimension&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## TreeAHConfig

Fields

`leafNodeEmbeddingCount` `string ( int64 format)`

Optional. Number of embeddings on each leaf node. The default value is 1000 if not set.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;leafNodeEmbeddingCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## BruteForceConfig

This type has no fields.

## DistanceMeasureType

Enums

`DISTANCE_MEASURE_TYPE_UNSPECIFIED`

Should not be set.

`SQUARED_L2_DISTANCE`

Euclidean (L\_2) Distance.

`COSINE_DISTANCE`

Cosine Distance. Defined as 1 - cosine similarity.

We strongly suggest using DOT\_PRODUCT\_DISTANCE + UNIT\_L2\_NORM instead of COSINE distance. Our algorithms have been more optimized for DOT\_PRODUCT distance which, when combined with UNIT\_L2\_NORM, is mathematically equivalent to COSINE distance and results in the same ranking.

`DOT_PRODUCT_DISTANCE`

Dot Product Distance. Defined as a negative of the dot product.

## IndexConfig

Configuration for vector indexing.

Fields

`embeddingColumn` `string`

Optional. column of embedding. This column contains the source data to create index for vector search. embeddingColumn must be set when using vector search.

`filterColumns[]` `string`

Optional. columns of features that're used to filter vector search results.

`crowdingColumn` `string`

Optional. column of crowding. This column contains crowding attribute which is a constraint on a neighbor list produced by `  FeatureOnlineStoreService.SearchNearestEntities  ` to diversify search results. If `  NearestNeighborQuery.per_crowding_attribute_neighbor_count  ` is set to K in `SearchNearestEntitiesRequest` , it's guaranteed that no more than K entities of the same crowding attribute are returned in the response.

`distanceMeasureType` ` enum ( DistanceMeasureType  ` )

Optional. The distance measure used in nearest neighbor search.

`algorithm_config` `Union type`

The configuration with regard to the algorithms used for efficient search. `algorithm_config` can be only one of the following:

`treeAhConfig` ` object ( TreeAHConfig  ` )

Optional. Configuration options for the tree-AH algorithm (Shallow tree + Asymmetric Hashing). Please refer to this paper for more details: <https://arxiv.org/abs/1908.10396>

`bruteForceConfig` ` object ( BruteForceConfig  ` )

Optional. Configuration options for using brute force search, which simply implements the standard linear search in the database for each query. It is primarily meant for benchmarking and to generate the ground truth for approximate search.

`embeddingDimension` `integer`

Optional. The number of dimensions of the input embedding.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;embeddingColumn&quot;: string,&quot;filterColumns&quot;: [string],&quot;crowdingColumn&quot;: string,&quot;distanceMeasureType&quot;: enum (DistanceMeasureType),// algorithm_config&quot;treeAhConfig&quot;: {object (TreeAHConfig)},&quot;bruteForceConfig&quot;: {object (BruteForceConfig)}// Union type&quot;embeddingDimension&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## TreeAHConfig

Configuration options for the tree-AH algorithm.

Fields

`leafNodeEmbeddingCount` `string ( int64 format)`

Optional. Number of embeddings on each leaf node. The default value is 1000 if not set.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;leafNodeEmbeddingCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## BruteForceConfig

This type has no fields.

Configuration options for using brute force search.

## DistanceMeasureType

The distance measure used in nearest neighbor search.

Enums

`DISTANCE_MEASURE_TYPE_UNSPECIFIED`

Should not be set.

`SQUARED_L2_DISTANCE`

Euclidean (L\_2) Distance.

`COSINE_DISTANCE`

Cosine Distance. Defined as 1 - cosine similarity.

We strongly suggest using DOT\_PRODUCT\_DISTANCE + UNIT\_L2\_NORM instead of COSINE distance. Our algorithms have been more optimized for DOT\_PRODUCT distance which, when combined with UNIT\_L2\_NORM, is mathematically equivalent to COSINE distance and results in the same ranking.

`DOT_PRODUCT_DISTANCE`

Dot Product Distance. Defined as a negative of the dot product.

## OptimizedConfig

Configuration for FeatureViews created in Optimized FeatureOnlineStore.

Fields

`automaticResources` ` object ( AutomaticResources  ` )

Optional. A description of resources that the FeatureView uses, which to large degree are decided by Agent Platform, and optionally allows only a modest additional configuration. If minReplicaCount is not set, the default value is 2. If maxReplicaCount is not set, the default value is 6. The max allowed replica count is 1000.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;automaticResources&quot;: {object (AutomaticResources)}}</code></pre></td>
</tr>
</tbody>
</table>

## ServiceAgentType

service agent type used during data sync.

Enums

`SERVICE_AGENT_TYPE_UNSPECIFIED`

By default, the project-level Agent Platform service Agent is enabled.

`SERVICE_AGENT_TYPE_PROJECT`

Indicates the project-level Agent Platform service Agent ( <https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents> ) will be used during sync jobs.

`SERVICE_AGENT_TYPE_FEATURE_VIEW`

Enable a FeatureView service account to be created by Agent Platform and output in the field `serviceAccountEmail` . This service account will be used to read from the source BigQuery table during sync.

## BigtableMetadata

metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.

Fields

`readAppProfile` `string`

Output only. The Bigtable App Profile to use for reading from Bigtable.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;readAppProfile&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a new FeatureView in a given FeatureOnlineStore.

### `            delete           `

Deletes a single FeatureView.

### `            directWrite           `

Bidirectional streaming RPC to directly write to feature values in a feature view.

### `            fetchFeatureValues           `

Fetch feature values under a FeatureView.

### `            generateFetchAccessToken           `

RPC to generate an access token for the given feature view.

### `            get           `

Gets details of a single FeatureView.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            list           `

Lists FeatureViews in a given FeatureOnlineStore.

### `            patch           `

Updates the parameters of a single FeatureView.

### `            searchNearestEntities           `

Search the nearest entities under a FeatureView.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            streamingFetchFeatureValues           `

Bidirectional streaming RPC to fetch feature values under a FeatureView.

### `            sync           `

Triggers on-demand sync for the FeatureView.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.
