---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/searchDataItems
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/searchDataItems
title: 'Method: datasets.searchDataItems'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.searchDataItems

Searches DataItems in a Dataset.

### Endpoint

get `https: / /{service-endpoint} /v1 /{dataset}:searchDataItems`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`dataset` `string`

Required. The resource name of the Dataset from which to search DataItems. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Query parameters

` savedQuery (deprecated)  ` `string`

The resource name of a SavedQuery(annotation set in UI). Format: `projects/{project}/locations/{location}/datasets/{dataset}/savedQueries/{savedQuery}` All of the search will be done in the context of this SavedQuery.

`dataLabelingJob` `string`

The resource name of a DataLabelingJob. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{dataLabelingJob}` If this field is set, all of the search will be done in the context of this DataLabelingJob.

`dataItemFilter` `string`

An expression for filtering the DataItem that will be returned.

  - `data_item_id` - for = or \!=.
  - `labeled` - for = or \!=.
  - `has_annotation(ANNOTATION_SPEC_ID)` - true only for DataItem that have at least one annotation with annotationSpecId = `ANNOTATION_SPEC_ID` in the context of SavedQuery or DataLabelingJob.

For example:

  - `dataItem=1`
  - `has_annotation(5)`

` annotationsFilter (deprecated)  ` `string`

An expression for filtering the Annotations that will be returned per DataItem. \* `annotationSpecId` - for = or \!=.

`annotationFilters[]` `string`

An expression that specifies what Annotations will be returned per DataItem. Annotations satisfied either of the conditions will be returned. \* `annotationSpecId` - for = or \!=. Must specify `savedQueryId=` - saved query id that annotations should belong to.

`fieldMask` ` string ( FieldMask  ` format)

Mask specifying which fields of `  DataItemView  ` to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`annotationsLimit` `integer`

If set, only up to this many of Annotations will be returned per DataItemView. The maximum value is 1000. If not set, the maximum value will be used.

`pageSize` `integer`

Requested page size. Server may return fewer results than requested. Default and maximum page size is 100.

` orderBy (deprecated)  ` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending.

`pageToken` `string`

A token identifying a page of results for the server to return Typically obtained via `  SearchDataItemsResponse.next_page_token  ` of the previous `  DatasetService.SearchDataItems  ` call.

`order` `Union type`

`order` can be only one of the following:

`orderByDataItem` `string`

A comma-separated list of data item fields to order by, sorted in ascending order. Use "desc" after a field name for descending.

`orderByAnnotation` ` object ( OrderByAnnotation  ` )

Expression that allows ranking results based on annotation's property.

### Request body

The request body must be empty.

### Response body

Response message for `  DatasetService.SearchDataItems  ` .

If successful, the response body contains data with the following structure:

Fields

`dataItemViews[]` ` object ( DataItemView  ` )

The DataItemViews read.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to `  SearchDataItemsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataItemViews&quot;: [{object (DataItemView)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## OrderByAnnotation

Expression that allows ranking results based on annotation's property.

Fields

`savedQuery` `string`

Required. Saved query of the Annotation. Only Annotations belong to this saved query will be considered for ordering.

`orderBy` `string`

A comma-separated list of annotation fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Must also specify savedQuery.

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
  &quot;savedQuery&quot;: string,
  &quot;orderBy&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## DataItemView

A container for a single DataItem and Annotations on it.

Fields

`dataItem` ` object ( DataItem  ` )

The DataItem.

`annotations[]` ` object ( Annotation  ` )

The Annotations on the DataItem. If too many Annotations should be returned for the DataItem, this field will be truncated per annotationsLimit in request. If it was, then the hasTruncatedAnnotations will be set to true.

`hasTruncatedAnnotations` `boolean`

True if and only if the Annotations field has been truncated. It happens if more Annotations for this DataItem met the request's annotationFilter than are allowed to be returned by annotationsLimit. Note that if Annotations field is not being returned due to field mask, then this field will not be set to true no matter how many Annotations are there.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataItem&quot;: {object (DataItem)},&quot;annotations&quot;: [{object (Annotation)}],&quot;hasTruncatedAnnotations&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>
