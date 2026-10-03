---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReviewSnippet
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReviewSnippet
title: ReviewSnippet
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Encapsulates a snippet of a user review that answers a question about the features of a specific place in Google Maps.

Fields

`title` `string`

title of the review.

`url` `string`

A link that corresponds to the user review on Google Maps.

`reviewId` `string`

The id of the review snippet.

**JSON representation**

```
{
  "title": string,
  "url": string,
  "reviewId": string
}
```
