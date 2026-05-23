---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportModelOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportModelOperationMetadata
title: ExportModelOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Details of `  ModelService.ExportModel  ` operation.

Fields

`genericMetadata` ` object ( GenericOperationMetadata  ` )

The common part of the operation metadata.

`outputInfo` ` object ( OutputInfo  ` )

Output only. Information further describing the output of this Model export.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;genericMetadata&quot;: {object (GenericOperationMetadata)},&quot;outputInfo&quot;: {object (OutputInfo)}}</code></pre></td>
</tr>
</tbody>
</table>

## OutputInfo

Further describes the output of the ExportModel. Supplements `  ExportModelRequest.OutputConfig  ` .

Fields

`artifactOutputUri` `string`

Output only. If the Model artifact is being exported to Google Cloud Storage this is the full path of the directory created, into which the Model files are being written to.

`imageOutputUri` `string`

Output only. If the Model image is being exported to Google Artifact Registry this is the full path of the image created.

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
  &quot;artifactOutputUri&quot;: string,
  &quot;imageOutputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
