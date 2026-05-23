---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HttpBody
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HttpBody
title: HttpBody
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page.

This message can be used both in streaming and non-streaming API methods in the request as well as the response.

It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body.

Example:

    message GetResourceRequest {
      // A unique request id.
      string requestId = 1;
    
      // The raw HTTP body is bound to this field.
      google.api.HttpBody httpBody = 2;
    
    }
    
    service ResourceService {
      rpc GetResource(GetResourceRequest)
        returns (google.api.HttpBody);
      rpc UpdateResource(google.api.HttpBody)
        returns (google.protobuf.Empty);
    
    }

Example with streaming methods:

    service CaldavService {
      rpc GetCalendar(stream google.api.HttpBody)
        returns (stream google.api.HttpBody);
      rpc UpdateCalendar(stream google.api.HttpBody)
        returns (stream google.api.HttpBody);
    
    }

Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged.

Fields

`contentType` `string`

The HTTP Content-type header value specifying the content type of the body.

`data` `string ( bytes format)`

The HTTP request/response body as raw binary.

A base64-encoded string.

`extensions[]` `object`

Application specific response metadata. Must be set in the first response for streaming APIs.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;contentType&quot;: string,
  &quot;data&quot;: string,
  &quot;extensions&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
