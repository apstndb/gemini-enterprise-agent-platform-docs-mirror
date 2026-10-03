---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric
title: Rubric
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

message representing a single testable criterion for evaluation. One input prompt could have multiple rubrics.

Fields

`rubricId` `string`

Unique identifier for the rubric. This id is used to refer to this rubric, e.g., in RubricVerdict.

`content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric#Content)` )`

Required. The actual testable criteria for the rubric.

`type` `string`

Optional. A type designator for the rubric, which can inform how it's evaluated or interpreted by systems or users. It's recommended to use consistent, well-defined, upper snake_case strings. Examples: "SUMMARIZATION_QUALITY", "SAFETY_HARMFUL_CONTENT", "INSTRUCTION_ADHERENCE".

`importance` `enum ( `[`Importance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric#Importance)` )`

Optional. The relative importance of this rubric.

**JSON representation**

```
{
  "rubricId": string,
  "content": {
    object (Content)
  },
  "type": string,
  "importance": enum (Importance)
}
```

## Content

Content of the rubric, defining the testable criteria.

Fields

`content_type` `Union type`

The specific type of content that defines the rubric. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`property` `object ( `[`Property`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric#Property)` )`

Evaluation criteria based on a specific property.

End of mutually exclusive fields.

**JSON representation**

```
{

  // content_type
  "property": {
    object (Property)
  }
  // Union type
}
```

## Property

Defines criteria based on a specific property.

Fields

`description` `string`

description of the property being evaluated. Example: "The model's response is grammatically correct."

**JSON representation**

```
{
  "description": string
}
```

## Importance

Importance level of the rubric.

| Enums                    |                              |
|--------------------------|------------------------------|
| `IMPORTANCE_UNSPECIFIED` | Importance is not specified. |
| `HIGH`                   | High importance.             |
| `MEDIUM`                 | Medium importance.           |
| `LOW`                    | Low importance.              |
