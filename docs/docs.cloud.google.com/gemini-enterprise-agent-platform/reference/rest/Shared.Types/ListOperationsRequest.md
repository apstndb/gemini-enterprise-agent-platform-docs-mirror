---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsRequest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsRequest
title: ListOperationsRequest
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The request message for `  Operations.ListOperations  ` .

Fields

`name` `string`

The name of the operation's parent resource.

`filter` `string`

The standard list filter.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token.

`returnPartialSuccess` `boolean`

When set to `true` , operations that are reachable are returned as normal, and those that are unreachable are returned in the `  ListOperationsResponse.unreachable  ` field.

This can only be `true` when reading across collections. For example, when `parent` is set to `"projects/example/locations/-"` .

This field is not supported by default and will result in an `UNIMPLEMENTED` error if set unless explicitly documented otherwise in service or product specific documentation.

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
  &quot;name&quot;: string,
  &quot;filter&quot;: string,
  &quot;pageSize&quot;: integer,
  &quot;pageToken&quot;: string,
  &quot;returnPartialSuccess&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
