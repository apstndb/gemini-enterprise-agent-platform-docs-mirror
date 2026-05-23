---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnterpriseWebSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnterpriseWebSearch
title: EnterpriseWebSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Tool to search public web data, powered by Agent Platform Search and Sec4 compliance.

Fields

`excludeDomains[]` `string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.

`blockingConfidence` ` enum ( PhishBlockThreshold  ` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)}</code></pre></td>
</tr>
</tbody>
</table>
