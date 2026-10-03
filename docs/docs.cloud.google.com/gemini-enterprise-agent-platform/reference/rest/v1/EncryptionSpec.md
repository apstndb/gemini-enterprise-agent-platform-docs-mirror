---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec
title: EncryptionSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a customer-managed encryption key specification that can be applied to a Agent Platform resource.

Fields

`kmsKeyName` `string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

**JSON representation**

```
{
  "kmsKeyName": string
}
```
