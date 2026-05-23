---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ImportFeatureValuesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ImportFeatureValuesResponse
title: ImportFeatureValuesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  FeaturestoreService.ImportFeatureValues  ` .

Fields

`importedEntityCount` `string ( int64 format)`

Number of entities that have been imported by the operation.

`importedFeatureValueCount` `string ( int64 format)`

Number of feature values that have been imported by the operation.

`invalidRowCount` `string ( int64 format)`

The number of rows in input source that weren't imported due to either \* Not having any featureValues. \* Having a null entityId. \* Having a null timestamp. \* Not being parsable (applicable for CSV sources).

`timestampOutsideRetentionRowsCount` `string ( int64 format)`

The number rows that weren't ingested due to having feature timestamps outside the retention boundary.

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
  &quot;importedEntityCount&quot;: string,
  &quot;importedFeatureValueCount&quot;: string,
  &quot;invalidRowCount&quot;: string,
  &quot;timestampOutsideRetentionRowsCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
