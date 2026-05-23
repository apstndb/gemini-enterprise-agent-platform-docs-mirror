---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookEucConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookEucConfig
title: NotebookEucConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The euc configuration of NotebookRuntimeTemplate.

Fields

`eucDisabled` `boolean`

Input only. Whether EUC is disabled in this NotebookRuntimeTemplate. In proto3, the default value of a boolean is false. In this way, by default EUC will be enabled for NotebookRuntimeTemplate.

`bypassActasCheck` `boolean`

Output only. Whether ActAs check is bypassed for service account attached to the VM. If false, we need ActAs check for the default Compute Engine service account. When a Runtime is created, a VM is allocated using Default Compute Engine service Account. Any user requesting to use this Runtime requires service Account user (ActAs) permission over this SA. If true, Runtime owner is using EUC and does not require the above permission as VM no longer use default Compute Engine SA, but a P4SA.

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
  &quot;eucDisabled&quot;: boolean,
  &quot;bypassActasCheck&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
