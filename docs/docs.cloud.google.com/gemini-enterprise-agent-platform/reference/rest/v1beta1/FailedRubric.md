---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FailedRubric
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FailedRubric
title: FailedRubric
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a specific failed rubric and the associated analysis.

Fields

`rubricId` `string`

The unique id of the rubric (if available from the metric source). Clients use this id to query the corresponding rubric verdict.

`classificationRationale` `string`

The rationale provided by the Loss Analysis Classifier for why this failure maps to this specific Loss Cluster. e.g., "The agent claimed an action without a tool call, matching 'Hallucination of Action'."

**JSON representation**

```
{
  "rubricId": string,
  "classificationRationale": string
}
```
