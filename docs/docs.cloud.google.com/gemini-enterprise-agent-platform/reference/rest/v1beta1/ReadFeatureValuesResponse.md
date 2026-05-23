---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReadFeatureValuesResponse
title: ReadFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  FeaturestoreOnlineServingService.ReadFeatureValues  ` .

Fields

`header` ` object ( Header  ` )

Response header.

`entityView` ` object ( EntityView  ` )

Entity view with feature values. This may be the entity in the Featurestore if values for all Features were requested, or a projection of the entity in the Featurestore if values for only some Features were requested.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;header&quot;: {object (Header)},&quot;entityView&quot;: {object (EntityView)}}</code></pre></td>
</tr>
</tbody>
</table>

## Header

Response header with metadata for the requested `  ReadFeatureValuesRequest.entity_type  ` and Features.

Fields

`entityType` `string`

The resource name of the EntityType from the `ReadFeatureValuesRequest` . value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .

`featureDescriptors[]` ` object ( FeatureDescriptor  ` )

List of feature metadata corresponding to each piece of `  ReadFeatureValuesResponse.EntityView.data  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;entityType&quot;: string,&quot;featureDescriptors&quot;: [{object (FeatureDescriptor)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureDescriptor

metadata for requested Features.

Fields

`id` `string`

feature id.

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
  &quot;id&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## EntityView

Entity view with feature values.

Fields

`entityId` `string`

id of the requested entity.

`data[]` ` object ( Data  ` )

Each piece of data holds the k requested values for one requested feature. If no values for the requested feature exist, the corresponding cell will be empty. This has the same size and is in the same order as the features from the header `  ReadFeatureValuesResponse.header  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;entityId&quot;: string,&quot;data&quot;: [{object (Data)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Data

Container to hold value(s), successive in time, for one feature from the request.

Fields

`data` `Union type`

`data` can be only one of the following:

`value` ` object ( FeatureValue  ` )

feature value if a single value is requested.

`values` ` object ( FeatureValueList  ` )

feature values list if values, successive in time, are requested. If the requested number of values is greater than the number of existing feature values, nonexistent values are omitted instead of being returned as empty.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// data&quot;value&quot;: {object (FeatureValue)},&quot;values&quot;: {object (FeatureValueList)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureValueList

Container for list of values.

Fields

`values[]` ` object ( FeatureValue  ` )

A list of feature values. All of them should be the same data type.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [{object (FeatureValue)}]}</code></pre></td>
</tr>
</tbody>
</table>
