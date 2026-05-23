---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CheckTrialEarlyStoppingStateMetatdata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CheckTrialEarlyStoppingStateMetatdata
title: CheckTrialEarlyStoppingStateMetatdata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

Fields

`genericMetadata` ` object ( GenericOperationMetadata  ` )

Operation metadata for suggesting Trials.

`study` `string`

The name of the Study that the Trial belongs to.

`trial` `string`

The Trial name.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;genericMetadata&quot;: {object (GenericOperationMetadata)},&quot;study&quot;: string,&quot;trial&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
