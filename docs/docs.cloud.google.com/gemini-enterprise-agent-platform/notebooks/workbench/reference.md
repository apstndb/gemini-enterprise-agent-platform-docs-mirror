---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference
title: Notebooks API usage overview
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This guide provides an overview of using the Notebooks API and its reference documentation.

## REST, gRPC, and client libraries

You can access the API via REST, gRPC, or one of the provided client libraries (built on gRPC).

### Client libraries

Google provides [client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/workbench/reference/libraries) for many popular languages to access this API. If your desired programming language is supported by the client libraries, you should use this option.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Pros</th>
<th>Cons</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Maintained by Google.<br />
Built-in <a href="https://docs.cloud.google.com/docs/authentication">authentication</a> .<br />
Built-in retries.<br />
Idiomatic for each language.<br />
Efficient <a href="https://developers.google.com/protocol-buffers" class="external">protocol buffer</a> HTTP request body.</td>
<td>Not available for all programming languages.</td>
</tr>
</tbody>
</table>

### REST

This API supports [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) . See the [REST reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/workbench/reference/rest) for this API. Also see [How to call Google APIs: REST edition](https://googleapis.github.io/HowToREST) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Pros</th>
<th>Cons</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Simple JSON interface.<br />
Well supported by many Google and third-party tools and libraries.</td>
<td>You must build your own client.<br />
You must <a href="https://developers.google.com/identity/protocols/OAuth2" class="external">implement authentication</a> .<br />
You must implement retries.<br />
Less efficient JSON HTTP request body.<br />
REST streaming is not supported by this API.</td>
</tr>
</tbody>
</table>

### gRPC

This API supports [gRPC](https://grpc.io/) . See the [RPC reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/workbench/reference/rpc) for this API, which provides a generic description of the types, methods, and fields generated for a gRPC library. Also see [How to call Google APIs: RPC edition](https://googleapis.github.io/HowToRPC.html) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Pros</th>
<th>Cons</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Supports <a href="https://grpc.io/docs/reference/" class="external">many programming languages</a> .<br />
Efficient <a href="https://developers.google.com/protocol-buffers" class="external">protocol buffer</a> HTTP request body.</td>
<td>You must generate your own client from Google-supplied protocol buffers.<br />
You must <a href="https://grpc.io/docs/guides/auth.html" class="external">implement authentication</a> .<br />
You must implement retries.</td>
</tr>
</tbody>
</table>

## Type, method, and field names

Depending on whether you are using client libraries, REST, or gRPC, the type, method, and field names for the API vary somewhat:

  - REST is arranged by resource hierarchies and their methods.
  - Client libraries and gRPC are arranged by services and their methods.
  - REST field names use camel case, though the API service will accept either camel case or snake case.
  - gRPC field names use snake case.
  - Client library field names use either title case, camel case or snake case, depending on which name is idiomatic for the language.

## Protocol buffers

Whether you are using client libraries, REST, or gRPC, the underlying service is defined using [protocol buffers](https://developers.google.com/protocol-buffers) . In particular, the service uses [proto3](https://developers.google.com/protocol-buffers/docs/proto3) .

When calling the API, some request or response fields can require a basic understanding of [protocol buffer well-known types](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf) .

In addition, when calling the REST API, the [default value](https://developers.google.com/protocol-buffers/docs/proto3#default) behavior for protocol buffers may result in missing fields in a JSON response. These fields are simply set to the default value, so they are not included in the response.

## API versions

The following API versions are available:

  - **v2** ( [generally available](https://cloud.google.com/products#product-launch-stages) ) is for managing Gemini Enterprise Agent Platform Workbench instances.
