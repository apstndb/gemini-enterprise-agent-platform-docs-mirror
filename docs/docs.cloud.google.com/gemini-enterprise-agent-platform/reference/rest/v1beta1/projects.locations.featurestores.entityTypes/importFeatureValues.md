---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/importFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/importFeatureValues
title: 'Method: entityTypes.importFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.importFeatureValues

Imports feature values into the Featurestore from a source storage.

The progress of the import is tracked by the returned operation. The imported features are guaranteed to be visible to subsequent read operations after the operation is marked as successfully done.

If an import operation fails, the feature values returned from reads and exports may be inconsistent. If consistency is required, the caller must retry the same import request again and wait till the new operation returned is marked as successfully done.

There are also scenarios where the caller can cause inconsistency.

  - Source data for import contains multiple distinct feature values for the same entity id and timestamp.
  - Source is modified during an import. This includes adding, updating, or removing source data and/or metadata. Examples of updating metadata include but are not limited to changing storage location, storage class, or retention policy.
  - Online serving cluster is under-provisioned.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{entityType}:importFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType` `string`

Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`

### Request body

The request body contains data with the following structure:

Fields

`entityIdField` `string`

Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity\_id.

`featureSpecs[]` ` object ( FeatureSpec  ` )

Required. Specifications defining which feature values to import from the entity. The request fails if no featureSpecs are provided, and having multiple featureSpecs for one feature is not allowed.

`disableOnlineServing` `boolean`

If set, data will not be imported for online serving. This is typically used for backfilling, where feature generation timestamps are not in the timestamp range needed for online serving.

`workerCount` `integer`

Specifies the number of workers that are used to write data to the Featurestore. Consider the online serving capacity that you require to achieve the desired import throughput without interfering with online serving. The value must be positive, and less than or equal to 100. If not set, defaults to using 1 worker. The low count ensures minimal impact on online serving performance.

`disableIngestionAnalysis` `boolean`

If true, API doesn't start ingestion analysis pipeline.

`source` `Union type`

Details about the source data, including the location of the storage and the format. `source` can be only one of the following:

`avroSource` ` object ( AvroSource  ` )

`bigquerySource` ` object ( BigQuerySource  ` )

`csvSource` ` object ( CsvSource  ` )

`feature_time_source` `Union type`

Source of Feature timestamp for all Feature values of each entity. Timestamps must be millisecond-aligned. `feature_time_source` can be only one of the following:

`featureTimeField` `string`

Source column that holds the feature timestamp for all feature values in each entity.

`featureTime` ` string ( Timestamp  ` format)

Single feature timestamp for all entities being imported. The timestamp must not have higher than millisecond precision.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## AvroSource

The storage details for Avro input content.

Fields

`gcsSource` ` object ( GcsSource  ` )

Required. Google Cloud Storage location.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;gcsSource&quot;: {object (GcsSource)}}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureSpec

Defines the feature value(s) to import.

Fields

`id` `string`

Required. id of the feature to import values of. This feature must exist in the target EntityType, or the request will fail.

`sourceField` `string`

Source column to get the feature values from. If not set, uses the column with the same name as the feature id.

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
  &quot;id&quot;: string,
  &quot;sourceField&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
