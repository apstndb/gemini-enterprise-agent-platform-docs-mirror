---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/operations/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/operations/list
title: 'Method: operations.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : operations.list

Lists operations that match the specified filter in the request. If the server doesn't support this method, it returns `UNIMPLEMENTED` .

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /operations`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Query parameters

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

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListOperationsResponse  ` .
