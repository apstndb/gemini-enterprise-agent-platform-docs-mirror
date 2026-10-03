---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnterpriseWebSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnterpriseWebSearch
title: EnterpriseWebSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Tool to search public web data, powered by Agent Platform Search and Sec4 compliance.

Fields

`excludeDomains[]` `string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.

`blockingConfidence` `enum ( `[`PhishBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PhishBlockThreshold)` )`

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

**JSON representation**

```
{
  "excludeDomains": [
    string
  ],
  "blockingConfidence": enum (PhishBlockThreshold)
}
```
