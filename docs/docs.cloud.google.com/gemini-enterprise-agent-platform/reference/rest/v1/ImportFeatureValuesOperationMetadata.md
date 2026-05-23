---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ImportFeatureValuesOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ImportFeatureValuesOperationMetadata
title: ImportFeatureValuesOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Details of operations that perform import feature values.

Fields

`genericMetadata` ` object ( GenericOperationMetadata  ` )

Operation metadata for Featurestore import feature values.

`importedEntityCount` `string ( int64 format)`

Number of entities that have been imported by the operation.

`importedFeatureValueCount` `string ( int64 format)`

Number of feature values that have been imported by the operation.

`sourceUris[]` `string`

The source URI from where feature values are imported.

`invalidRowCount` `string ( int64 format)`

The number of rows in input source that weren't imported due to either \* Not having any featureValues. \* Having a null entityId. \* Having a null timestamp. \* Not being parsable (applicable for CSV sources).

`timestampOutsideRetentionRowsCount` `string ( int64 format)`

The number rows that weren't ingested due to having timestamps outside the retention boundary.

`blockingOperationIds[]` `string ( int64 format)`

List of ImportFeatureValues operations running under a single EntityType that are blocking this operation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;genericMetadata&quot;: {object (GenericOperationMetadata)},&quot;importedEntityCount&quot;: string,&quot;importedFeatureValueCount&quot;: string,&quot;sourceUris&quot;: [string],&quot;invalidRowCount&quot;: string,&quot;timestampOutsideRetentionRowsCount&quot;: string,&quot;blockingOperationIds&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>
