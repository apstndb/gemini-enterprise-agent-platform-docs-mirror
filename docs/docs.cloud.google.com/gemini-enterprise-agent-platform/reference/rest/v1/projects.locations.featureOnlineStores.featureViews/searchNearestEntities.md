---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/searchNearestEntities
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/searchNearestEntities
title: 'Method: featureViews.searchNearestEntities'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.searchNearestEntities

Search the nearest entities under a FeatureView. Search only works for indexable feature view; if a feature view isn't indexable, returns Invalid argument response.

### Endpoint

post `https: / /{service-endpoint} /v1 /{featureView}:searchNearestEntities`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView` `string`

Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Request body

The request body contains data with the following structure:

Fields

`query` ` object ( NearestNeighborQuery  ` )

Required. The query.

`returnFullEntity` `boolean`

Optional. If set to true, the full entities (including all vector values and metadata) of the nearest neighbors are returned; otherwise only entity id of the nearest neighbors will be returned. Note that returning full entities will significantly increase the latency and cost of the query.

### Response body

Response message for `  FeatureOnlineStoreService.SearchNearestEntities  `

If successful, the response body contains data with the following structure:

Fields

`nearestNeighbors` ` object ( NearestNeighbors  ` )

The nearest neighbors of the query entity.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;nearestNeighbors&quot;: {object (NearestNeighbors)}}</code></pre></td>
</tr>
</tbody>
</table>

## NearestNeighborQuery

A query to find a number of similar entities.

Fields

`neighborCount` `integer`

Optional. The number of similar entities to be retrieved from feature view for each query.

`stringFilters[]` ` object ( StringFilter  ` )

Optional. The list of string filters.

`numericFilters[]` ` object ( NumericFilter  ` )

Optional. The list of numeric filters.

`perCrowdingAttributeNeighborCount` `integer`

Optional. Crowding is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than sper\_crowding\_attribute\_neighbor\_count of the k neighbors returned have the same value of crowdingAttribute. It's used for improving result diversity.

`parameters` ` object ( Parameters  ` )

Optional. Parameters that can be set to tune query on the fly.

`instance` `Union type`

`instance` can be only one of the following:

`entityId` `string`

Optional. The entity id whose similar entities should be searched for. If embedding is set, search will use embedding instead of entityId.

`embedding` ` object ( Embedding  ` )

Optional. The embedding vector that be used for similar search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;neighborCount&quot;: integer,&quot;stringFilters&quot;: [{object (StringFilter)}],&quot;numericFilters&quot;: [{object (NumericFilter)}],&quot;perCrowdingAttributeNeighborCount&quot;: integer,&quot;parameters&quot;: {object (Parameters)},// instance&quot;entityId&quot;: string,&quot;embedding&quot;: {object (Embedding)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Embedding

The embedding vector.

Fields

`value[]` `number`

Optional. Individual value in the embedding.

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
  &quot;value&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## StringFilter

String filter is used to search a subset of the entities by using boolean rules on string columns. For example: if a query specifies string filter with 'name = color, allowTokens = {red, blue}, denyTokens = {purple}',' then that query will match entities that are red or blue, but if those points are also purple, then they will be excluded even if they are red/blue. Only string filter is supported for now, numeric filter will be supported in the near future.

Fields

`name` `string`

Required. column names in BigQuery that used as filters.

`allowTokens[]` `string`

Optional. The allowed tokens.

`denyTokens[]` `string`

Optional. The denied tokens.

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
  &quot;name&quot;: string,
  &quot;allowTokens&quot;: [
    string
  ],
  &quot;denyTokens&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## NumericFilter

Numeric filter is used to search a subset of the entities by using boolean rules on numeric columns. For example: Database Point 0: {name: "a" valueInt: 42} {name: "b" valueFloat: 1.0} Database Point 1: {name: "a" valueInt: 10} {name: "b" valueFloat: 2.0} Database Point 2: {name: "a" valueInt: -1} {name: "b" valueFloat: 3.0} Query: {name: "a" valueInt: 12 operator: LESS} // Matches Point 1, 2 {name: "b" valueFloat: 2.0 operator: EQUAL} // Matches Point 1

Fields

`name` `string`

Required. column name in BigQuery that used as filters.

`Value` `Union type`

The type of Value must be consistent for all datapoints with a given name. This is verified at runtime. `Value` can be only one of the following:

`valueInt` `string ( int64 format)`

int value type.

`valueFloat` `number`

float value type.

`valueDouble` `number`

double value type.

`op` ` enum ( Operator  ` )

Optional. This MUST be specified for queries and must NOT be specified for database points.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,// Value&quot;valueInt&quot;: string,&quot;valueFloat&quot;: number,&quot;valueDouble&quot;: number// Union type&quot;op&quot;: enum (Operator)}</code></pre></td>
</tr>
</tbody>
</table>

## Operator

Datapoints for which Operator is true relative to the query's value field will be allowlisted.

Enums

`OPERATOR_UNSPECIFIED`

Unspecified operator.

`LESS`

Entities are eligible if their value is \< the query's.

`LESS_EQUAL`

Entities are eligible if their value is \<= the query's.

`EQUAL`

Entities are eligible if their value is == the query's.

`GREATER_EQUAL`

Entities are eligible if their value is \>= the query's.

`GREATER`

Entities are eligible if their value is \> the query's.

`NOT_EQUAL`

Entities are eligible if their value is \!= the query's.

## Parameters

Parameters that can be overrided in each query to tune query latency and recall.

Fields

`approximateNeighborCandidates` `integer`

Optional. The number of neighbors to find via approximate search before exact reordering is performed; if set, this value must be \> neighborCount.

`leafNodesSearchFraction` `number`

Optional. The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0.

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
  &quot;approximateNeighborCandidates&quot;: integer,
  &quot;leafNodesSearchFraction&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## NearestNeighbors

Nearest neighbors for one query.

Fields

`neighbors[]` ` object ( Neighbor  ` )

All its neighbors.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;neighbors&quot;: [{object (Neighbor)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Neighbor

A neighbor of the query vector.

Fields

`entityId` `string`

The id of the similar entity.

`distance` `number`

The distance between the neighbor and the query vector.

`entityKeyValues` ` object ( FetchFeatureValuesResponse  ` )

The attributes of the neighbor, e.g. filters, crowding and metadata Note that full entities are returned only when "returnFullEntity" is set to true. Otherwise, only the "entityId" and "distance" fields are populated.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;entityId&quot;: string,&quot;distance&quot;: number,&quot;entityKeyValues&quot;: {object (FetchFeatureValuesResponse)}}</code></pre></td>
</tr>
</tbody>
</table>
