---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageDatasetMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageDatasetMetadata
title: ImageDatasetMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata of Datasets that contain Image DataItems.

Fields

`dataItemSchemaUri` `string`

Points to a YAML file stored on Google Cloud Storage describing payload of the Image DataItems that belong to this Dataset.

`gcsBucket` `string`

Google Cloud Storage Bucket name that contains the blob data of this Dataset.

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
  &quot;dataItemSchemaUri&quot;: string,
  &quot;gcsBucket&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
