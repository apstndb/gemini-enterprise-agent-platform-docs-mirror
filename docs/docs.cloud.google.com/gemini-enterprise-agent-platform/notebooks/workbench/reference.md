---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference
title: Notebooks API usage overview
description: Learn about Gemini Enterprise Agent Platform Workbench options for working with the Notebooks API
data_source: docs.cloud.google.com
---

This guide provides an overview of using the Notebooks API and its reference documentation.

## REST, gRPC, and client libraries

You can access the API via REST, gRPC, or one of the provided client libraries (built on gRPC).

### Client libraries

Google provides [client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/libraries) for many popular languages to access this API. If your desired programming language is supported by the client libraries, you should use this option.

| Pros                                                                                                                                                                                                                                               | Cons                                         |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| Maintained by Google. Built-in [authentication](https://docs.cloud.google.com/docs/authentication) . Built-in retries. Idiomatic for each language. Efficient [protocol buffer](https://developers.google.com/protocol-buffers) HTTP request body. | Not available for all programming languages. |

### REST

This API supports [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) . See the [REST reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest) for this API. Also see [How to call Google APIs: REST edition](https://googleapis.github.io/HowToREST) .

| Pros                                                                                      | Cons                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Simple JSON interface. Well supported by many Google and third-party tools and libraries. | You must build your own client. You must [implement authentication](https://developers.google.com/identity/protocols/OAuth2) . You must implement retries. Less efficient JSON HTTP request body. REST streaming is not supported by this API. |

### gRPC

This API supports [gRPC](https://grpc.io/) . See the [RPC reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc) for this API, which provides a generic description of the types, methods, and fields generated for a gRPC library. Also see [How to call Google APIs: RPC edition](https://googleapis.github.io/HowToRPC.html) .

| Pros                                                                                                                                                                    | Cons                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Supports [many programming languages](https://grpc.io/docs/reference/) . Efficient [protocol buffer](https://developers.google.com/protocol-buffers) HTTP request body. | You must generate your own client from Google-supplied protocol buffers. You must [implement authentication](https://grpc.io/docs/guides/auth.html) . You must implement retries. |

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
