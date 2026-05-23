---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PrivateServiceConnectConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PrivateServiceConnectConfig
title: PrivateServiceConnectConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents configuration for private service connect.

Fields

`enablePrivateServiceConnect` `boolean`

Required. If true, expose the IndexEndpoint via private service connect.

`projectAllowlist[]` `string`

A list of Projects from which the forwarding rule will target the service attachment.

`pscAutomationConfigs[]` ` object ( PSCAutomationConfig  ` )

Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only.

`serviceAttachment` `string`

Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enablePrivateServiceConnect&quot;: boolean,&quot;projectAllowlist&quot;: [string],&quot;pscAutomationConfigs&quot;: [{object (PSCAutomationConfig)}],&quot;serviceAttachment&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
