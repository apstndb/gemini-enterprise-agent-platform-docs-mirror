---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PrivateServiceConnectConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PrivateServiceConnectConfig
title: PrivateServiceConnectConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents configuration for private service connect.

Fields

`enablePrivateServiceConnect` `boolean`

Required. If true, expose the IndexEndpoint via private service connect.

`projectAllowlist[]` `string`

A list of Projects from which the forwarding rule will target the service attachment.

`pscAutomationConfigs[]` `object ( `[`PSCAutomationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PSCAutomationConfig)` )`

Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only.

`serviceAttachment` `string`

Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect.

**JSON representation**

```
{
  "enablePrivateServiceConnect": boolean,
  "projectAllowlist": [
    string
  ],
  "pscAutomationConfigs": [
    {
      object (PSCAutomationConfig)
    }
  ],
  "serviceAttachment": string
}
```
