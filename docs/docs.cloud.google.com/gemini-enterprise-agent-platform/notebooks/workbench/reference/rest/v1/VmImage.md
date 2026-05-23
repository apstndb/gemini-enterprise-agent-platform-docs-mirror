---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/VmImage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/VmImage
title: VmImage
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Definition of a custom Compute Engine virtual machine image for starting a notebook instance with the environment installed directly on the VM.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;project&quot;: string,// Union field image can be only one of the following:&quot;imageName&quot;: string,&quot;imageFamily&quot;: string// End of list of possible types for union field image.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`project`

`string`

Required. The name of the Google Cloud project that this VM image belongs to. Format: `{projectId}`

Union field `image` . The reference to an external Compute Engine VM image. `image` can be only one of the following:

`imageName`

`string`

Use VM image name to find the image.

`imageFamily`

`string`

Use this VM image family to find the image; the newest image in this family will be used.
