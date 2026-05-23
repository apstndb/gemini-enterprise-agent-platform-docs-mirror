---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeleteFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeleteFeatureValuesResponse
title: DeleteFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  FeaturestoreService.DeleteFeatureValues  ` .

Fields

`response` `Union type`

Response based on which delete option is specified in the request `response` can be only one of the following:

`selectEntity` ` object ( SelectEntity  ` )

Response for request specifying the entities to delete

`selectTimeRangeAndFeature` ` object ( SelectTimeRangeAndFeature  ` )

Response for request specifying time range and feature

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// response&quot;selectEntity&quot;: {object (SelectEntity)},&quot;selectTimeRangeAndFeature&quot;: {object (SelectTimeRangeAndFeature)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## SelectEntity

Response message if the request uses the SelectEntity option.

Fields

`offlineStorageDeletedEntityRowCount` `string ( int64 format)`

The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity id and a timestamp. One entity id can have multiple rows in the offline storage.

`onlineStorageDeletedEntityCount` `string ( int64 format)`

The count of deleted entities in the online storage. Each entity id corresponds to one entity.

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
  &quot;offlineStorageDeletedEntityRowCount&quot;: string,
  &quot;onlineStorageDeletedEntityCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SelectTimeRangeAndFeature

Response message if the request uses the SelectTimeRangeAndFeature option.

Fields

`impactedFeatureCount` `string ( int64 format)`

The count of the features or columns impacted. This is the same as the feature count in the request.

`offlineStorageModifiedEntityRowCount` `string ( int64 format)`

The count of modified entity rows in the offline storage. Each row corresponds to the combination of an entity id and a timestamp. One entity id can have multiple rows in the offline storage. Within each row, only the features specified in the request are deleted.

`onlineStorageModifiedEntityCount` `string ( int64 format)`

The count of modified entities in the online storage. Each entity id corresponds to one entity. Within each entity, only the features specified in the request are deleted.

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
  &quot;impactedFeatureCount&quot;: string,
  &quot;offlineStorageModifiedEntityRowCount&quot;: string,
  &quot;onlineStorageModifiedEntityCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
