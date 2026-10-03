---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig
title: GeminiRequestReadConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration for how to read Gemini requests from a multimodal dataset.

Fields

`read_config` `Union type`

The read config for the dataset. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`templateConfig` `object ( `[`GeminiTemplateConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig#GeminiTemplateConfig)` )`

Gemini request template with placeholders.

`assembledRequestColumnName` `string`

Optional. column name in the dataset table that contains already fully assembled Gemini requests.

End of mutually exclusive fields.

**JSON representation**

```
{

  // read_config
  "templateConfig": {
    object (GeminiTemplateConfig)
  },
  "assembledRequestColumnName": string
  // Union type
}
```

## GeminiTemplateConfig

Template configuration to create Gemini examples from a multimodal dataset.

Fields

`geminiExample` `object ( `[`GeminiExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample)` )`

Required. The template that will be used for assembling the request to use for downstream applications.

`fieldMapping` `map (key: string, value: string)`

Required. Map of template parameters to the columns in the dataset table.

**JSON representation**

```
{
  "geminiExample": {
    object (GeminiExample)
  },
  "fieldMapping": {
    string: string,
    ...
  }
}
```
