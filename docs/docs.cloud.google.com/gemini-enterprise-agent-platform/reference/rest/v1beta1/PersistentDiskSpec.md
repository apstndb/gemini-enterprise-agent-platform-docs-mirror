---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PersistentDiskSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PersistentDiskSpec
title: PersistentDiskSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents the spec of \[persistent disk\]\[https://cloud.google.com/compute/docs/disks/persistent-disks\] options.

Fields

`diskType` `string`

type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid state Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk)

`diskSizeGb` `string ( int64 format)`

Size in GB of the disk (default is 100GB).

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
  &quot;diskType&quot;: string,
  &quot;diskSizeGb&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
