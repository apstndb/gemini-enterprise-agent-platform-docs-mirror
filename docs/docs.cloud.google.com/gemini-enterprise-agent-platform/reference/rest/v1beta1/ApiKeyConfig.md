---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ApiKeyConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ApiKeyConfig
title: ApiKeyConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The API secret.

Fields

`apiKeySecretVersion` `string`

Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version}

`apiKeyString` `string`

The API key string.

Either this or `apiKeySecretVersion` must be set.

**JSON representation**

```
{
  "apiKeySecretVersion": string,
  "apiKeyString": string
}
```
