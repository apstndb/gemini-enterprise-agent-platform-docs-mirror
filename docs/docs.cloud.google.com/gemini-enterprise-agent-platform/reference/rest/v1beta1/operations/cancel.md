---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/operations/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/operations/cancel
title: 'Method: operations.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : operations.cancel

Starts asynchronous cancellation on a long-running operation. The server makes a best effort to cancel the operation, but success is not guaranteed. If the server doesn't support this method, it returns `google.rpc.Code.UNIMPLEMENTED` . Clients can use `  Operations.GetOperation  ` or other methods to check whether the cancellation succeeded or whether the operation completed despite cancellation. On successful cancellation, the operation is not deleted; instead, it becomes an operation with an `  Operation.error  ` value with a `  google.rpc.Status.code  ` of `1` , corresponding to `code.CANCELLED` .

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

The name of the operation resource to be cancelled.

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
