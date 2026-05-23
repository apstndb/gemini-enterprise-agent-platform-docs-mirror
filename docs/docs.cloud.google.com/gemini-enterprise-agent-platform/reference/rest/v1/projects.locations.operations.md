---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.operations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.operations
title: 'REST Resource: projects.locations.operations'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Operation

This resource represents a long-running operation that is the result of a network API call.

Fields

`name` `string`

The server-assigned name, which is only unique within the same service that originally returns it. If you use the default HTTP mapping, the `name` should be a resource name ending with `operations/{uniqueId}` .

`metadata` `object`

service-specific metadata associated with the operation. It typically contains progress information and common metadata such as create time. Some services might not provide such metadata. Any method that returns a long-running operation should document the metadata type, if any.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

`done` `boolean`

If the value is `false` , it means the operation is still in progress. If `true` , the operation is completed, and either `error` or `response` is available.

`result` `Union type`

The operation result, which can be either an `error` or a valid `response` . If `done` == `false` , neither `error` nor `response` is set. If `done` == `true` , exactly one of `error` or `response` can be set. Some services might not provide the result. `result` can be only one of the following:

`error` ` object ( Status  ` )

The error result of the operation in case of failure or cancellation.

`response` `object`

The normal, successful response of the operation. If the original method returns no data on success, such as `Delete` , the response is `google.protobuf.Empty` . If the original method is standard `Get` / `Create` / `Update` , the response should be the resource. For other methods, the response should have the type `XxxResponse` , where `Xxx` is the original method name. For example, if the original method name is `TakeSnapshot()` , the inferred response type is `TakeSnapshotResponse` .

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;metadata&quot;: {&quot;@type&quot;: string,field1: ...,...},&quot;done&quot;: boolean,// result&quot;error&quot;: {object (Status)},&quot;response&quot;: {&quot;@type&quot;: string,field1: ...,...}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            cancel           `

Starts asynchronous cancellation on a long-running operation.

### `            delete           `

Deletes a long-running operation.

### `            get           `

Gets the latest state of a long-running operation.

### `            list           `

Lists operations that match the specified filter in the request.

### `            wait           `

Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.
