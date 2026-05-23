---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/upsertDatapoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/upsertDatapoints
title: 'Method: indexes.upsertDatapoints'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexes.upsertDatapoints

Add/update Datapoints into an Index.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{index}:upsertDatapoints`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`index` `string`

Required. The name of the Index resource to be updated. Format: `projects/{project}/locations/{location}/indexes/{index}`

### Request body

The request body contains data with the following structure:

Fields

`datapoints[]` ` object ( IndexDatapoint  ` )

A list of datapoints to be created/updated.

`updateMask` ` string ( FieldMask  ` format)

Optional. Update mask is used to specify the fields to be overwritten in the datapoints by the update. The fields specified in the updateMask are relative to each IndexDatapoint inside datapoints, not the full request.

Updatable fields:

  - Use `all_restricts` to update both restricts and numericRestricts.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Response body

If successful, the response body is empty.

## IndexDatapoint

A datapoint of Index.

Fields

`datapointId` `string`

Required. Unique identifier of the datapoint.

`featureVector[]` `number`

Required. feature embedding vector for dense index. An array of numbers with the length of \[NearestNeighborSearchConfig.dimensions\].

`sparseEmbedding` ` object ( SparseEmbedding  ` )

Optional. feature embedding vector for sparse index.

`restricts[]` ` object ( Restriction  ` )

Optional. List of Restrict of the datapoint, used to perform "restricted searches" where boolean rule are used to filter the subset of the database eligible for matching. This uses categorical tokens. See: <https://cloud.google.com/vertex-ai/docs/matching-engine/filtering>

`numericRestricts[]` ` object ( NumericRestriction  ` )

Optional. List of Restrict of the datapoint, used to perform "restricted searches" where boolean rule are used to filter the subset of the database eligible for matching. This uses numeric comparisons.

`crowdingTag` ` object ( CrowdingTag  ` )

Optional. CrowdingTag of the datapoint, the number of neighbors to return in each crowding can be configured during query.

`embeddingMetadata` ` object ( Struct  ` format)

Optional. The key-value map of additional metadata for the datapoint.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;datapointId&quot;: string,&quot;featureVector&quot;: [number],&quot;sparseEmbedding&quot;: {object (SparseEmbedding)},&quot;restricts&quot;: [{object (Restriction)}],&quot;numericRestricts&quot;: [{object (NumericRestriction)}],&quot;crowdingTag&quot;: {object (CrowdingTag)},&quot;embeddingMetadata&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

## SparseEmbedding

feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.

Fields

`values[]` `number`

Required. The list of embedding values of the sparse vector.

`dimensions[]` `string ( int64 format)`

Required. The list of indexes for the embedding values of the sparse vector.

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
  &quot;values&quot;: [
    number
  ],
  &quot;dimensions&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## Restriction

Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).

Fields

`namespace` `string`

The namespace of this restriction. e.g.: color.

`allowList[]` `string`

The attributes to allow in this namespace. e.g.: 'red'

`denyList[]` `string`

The attributes to deny in this namespace. e.g.: 'blue'

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
  &quot;namespace&quot;: string,
  &quot;allowList&quot;: [
    string
  ],
  &quot;denyList&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## NumericRestriction

This field allows restricts to be based on numeric comparisons rather than categorical tokens.

Fields

`namespace` `string`

The namespace of this restriction. e.g.: cost.

`op` ` enum ( Operator  ` )

This MUST be specified for queries and must NOT be specified for datapoints.

`Value` `Union type`

The type of Value must be consistent for all datapoints with a given namespace name. This is verified at runtime. `Value` can be only one of the following:

`valueInt` `string ( int64 format)`

Represents 64 bit integer.

`valueFloat` `number`

Represents 32 bit float.

`valueDouble` `number`

Represents 64 bit float.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;namespace&quot;: string,&quot;op&quot;: enum (Operator),// Value&quot;valueInt&quot;: string,&quot;valueFloat&quot;: number,&quot;valueDouble&quot;: number// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Operator

Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's value field will be allowlisted.

Enums

`OPERATOR_UNSPECIFIED`

Default value of the enum.

`LESS`

Datapoints are eligible iff their value is \< the query's.

`LESS_EQUAL`

Datapoints are eligible iff their value is \<= the query's.

`EQUAL`

Datapoints are eligible iff their value is == the query's.

`GREATER_EQUAL`

Datapoints are eligible iff their value is \>= the query's.

`GREATER`

Datapoints are eligible iff their value is \> the query's.

`NOT_EQUAL`

Datapoints are eligible iff their value is \!= the query's.

## CrowdingTag

Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowdingAttribute.

Fields

`crowdingAttribute` `string`

The attribute value used for crowding. The maximum number of neighbors to return per crowding attribute value (perCrowdingAttributeNumNeighbors) is configured per-query. This field is ignored if perCrowdingAttributeNumNeighbors is larger than the total number of neighbors to return for a given query.

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
  &quot;crowdingAttribute&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
