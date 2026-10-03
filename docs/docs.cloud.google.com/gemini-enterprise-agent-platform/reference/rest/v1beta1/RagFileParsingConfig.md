---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileParsingConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileParsingConfig
title: RagFileParsingConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specifies the parsing config for RagFiles.

Fields

`useAdvancedPdfParsing `**`(deprecated)`** `boolean`

> This item is deprecated!

Whether to use advanced PDF parsing.

`parser` `Union type`

The parser to use for RagFiles. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`advancedParser` `object ( `[`AdvancedParser`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileParsingConfig#AdvancedParser)` )`

The Advanced Parser to use for RagFiles.

`layoutParser` `object ( `[`LayoutParser`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileParsingConfig#LayoutParser)` )`

The Layout Parser to use for RagFiles.

`llmParser` `object ( `[`LlmParser`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora#LlmParser)` )`

The LLM Parser to use for RagFiles.

End of mutually exclusive fields.

**JSON representation**

```
{
  "useAdvancedPdfParsing": boolean,

  // parser
  "advancedParser": {
    object (AdvancedParser)
  },
  "layoutParser": {
    object (LayoutParser)
  },
  "llmParser": {
    object (LlmParser)
  }
  // Union type
}
```

## AdvancedParser

Specifies the advanced parsing for RagFiles.

Fields

`useAdvancedPdfParsing` `boolean`

Whether to use advanced PDF parsing.

**JSON representation**

```
{
  "useAdvancedPdfParsing": boolean
}
```

## LayoutParser

Document AI Layout Parser config.

Fields

`processorName` `string`

The full resource name of a Document AI processor or processor version. The processor must have type `LAYOUT_PARSER_PROCESSOR` . If specified, the `additionalConfig.parse_as_scanned_pdf` field must be false. Format: \* `projects/{projectId}/locations/{location}/processors/{processorId}` \* `projects/{projectId}/locations/{location}/processors/{processorId}/processorVersions/{processor_version_id}`

`maxParsingRequestsPerMin` `integer`

The maximum number of requests the job is allowed to make to the Document AI processor per minute. Consult <https://cloud.google.com/document-ai/quotas> and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM would be used.

`globalMaxParsingRequestsPerMin` `integer`

The maximum number of requests the job is allowed to make to the Document AI processor per minute in this project. Consult <https://cloud.google.com/document-ai/quotas> and the Quota page for your project to set an appropriate value here. If this value is not specified, maxParsingRequestsPerMin will be used by indexing pipeline as the global limit.

**JSON representation**

```
{
  "processorName": string,
  "maxParsingRequestsPerMin": integer,
  "globalMaxParsingRequestsPerMin": integer
}
```
