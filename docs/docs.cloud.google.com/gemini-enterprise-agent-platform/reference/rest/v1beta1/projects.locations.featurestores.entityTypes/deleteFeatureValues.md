---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/deleteFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes/deleteFeatureValues
title: 'Method: entityTypes.deleteFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.deleteFeatureValues

Delete feature values from Featurestore.

The progress of the deletion is tracked by the returned operation. The deleted feature values are guaranteed to be invisible to subsequent read operations after the operation is marked as successfully done.

If a delete feature values operation fails, the feature values returned from reads and exports may be inconsistent. If consistency is required, the caller must retry the same delete request again and wait till the new operation returned is marked as successfully done.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{entityType}:deleteFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType` `string`

Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`

### Request body

The request body contains data with the following structure:

Fields

`DeleteOption` `Union type`

Defines options to select feature values to be deleted. `DeleteOption` can be only one of the following:

`selectEntity` ` object ( SelectEntity  ` )

Select feature values to be deleted by specifying entities.

`selectTimeRangeAndFeature` ` object ( SelectTimeRangeAndFeature  ` )

Select feature values to be deleted by specifying time range and features.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## SelectEntity

message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

Fields

`entityIdSelector` ` object ( EntityIdSelector  ` )

Required. Selectors choosing feature values of which entity id to be deleted from the EntityType.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;entityIdSelector&quot;: {object (EntityIdSelector)}}</code></pre></td>
</tr>
</tbody>
</table>

## EntityIdSelector

Selector for entityId. Getting ids from the given source.

Fields

`entityIdField` `string`

Source column that holds entity IDs. If not provided, entity IDs are extracted from the column named entity\_id.

`EntityIdsSource` `Union type`

Details about the source data, including the location of the storage and the format. `EntityIdsSource` can be only one of the following:

`csvSource` ` object ( CsvSource  ` )

Source of Csv

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;entityIdField&quot;: string,// EntityIdsSource&quot;csvSource&quot;: {object (CsvSource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## SelectTimeRangeAndFeature

message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.

Fields

`timeRange` ` object ( Interval  ` )

Required. Select feature generated within a half-inclusive time range. The time range is lower inclusive and upper exclusive.

`featureSelector` ` object ( FeatureSelector  ` )

Required. Selectors choosing which feature values to be deleted from the EntityType.

`skipOnlineStorageDelete` `boolean`

If set, data will not be deleted from online storage. When time range is older than the data in online storage, setting this to be true will make the deletion have no impact on online serving.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timeRange&quot;: {object (Interval)},&quot;featureSelector&quot;: {object (FeatureSelector)},&quot;skipOnlineStorageDelete&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>
