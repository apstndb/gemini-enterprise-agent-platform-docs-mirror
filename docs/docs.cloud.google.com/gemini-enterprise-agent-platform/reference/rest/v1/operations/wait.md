---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/operations/wait
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/operations/wait
title: 'Method: operations.wait'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : operations.wait

Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state. If the operation is already done, the latest state is immediately returned. If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC timeout is used. If the server does not support this method, it returns `google.rpc.Code.UNIMPLEMENTED` . Note that this method is on a best-effort basis. It may return the latest state before the specified timeout (including immediately), meaning even an immediate response is no guarantee that the operation is done.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:wait`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

The name of the operation resource to wait on.

### Query parameters

`timeout` ` string ( Duration  ` format)

The maximum duration to wait before timing out. If left blank, the wait will be at most the time permitted by the underlying HTTP/RPC protocol. If RPC context deadline is also specified, the shorter one will be used.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
