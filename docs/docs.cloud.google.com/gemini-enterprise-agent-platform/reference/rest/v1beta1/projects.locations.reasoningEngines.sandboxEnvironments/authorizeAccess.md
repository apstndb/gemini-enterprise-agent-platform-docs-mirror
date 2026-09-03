---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/authorizeAccess
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/authorizeAccess
title: 'Method: sandboxEnvironments.authorizeAccess'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sandboxEnvironments.authorizeAccess

Checks whether the caller is authorized to access the sandbox environment.

Authorization is performed entirely by the API infrastructure from the `method_policy` below; the handler is a no-op. A successful response means the caller holds `sandboxEnvironments.execute` on the named sandbox. Used by the sandbox data-plane proxy, which forwards the caller's credential and proxies traffic only on success.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:authorizeAccess`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the sandbox environment to authorize access to. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sandboxEnvironments/{sandboxEnvironment}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is empty.
