---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ShieldedVmConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ShieldedVmConfig
title: ShieldedVmConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .

Fields

`enableSecureBoot` `boolean`

Defines whether the instance has [Secure Boot](https://cloud.google.com/compute/shielded-vm/docs/shielded-vm#secure-boot) enabled.

Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails.

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
  &quot;enableSecureBoot&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
