---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ApiKeyConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ApiKeyConfig
title: ApiKeyConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The API secret.

Fields

`apiKeySecretVersion` `string`

Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version}

`apiKeyString` `string`

The API key string.

Either this or `apiKeySecretVersion` must be set.

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
  &quot;apiKeySecretVersion&quot;: string,
  &quot;apiKeyString&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
