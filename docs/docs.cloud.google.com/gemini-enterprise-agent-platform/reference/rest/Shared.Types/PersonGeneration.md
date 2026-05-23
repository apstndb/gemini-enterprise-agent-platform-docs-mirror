---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PersonGeneration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PersonGeneration
title: PersonGeneration
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Enum for controlling the generation of people in images.

Enums

`PERSON_GENERATION_UNSPECIFIED`

The default behavior is unspecified. The model will decide whether to generate images of people.

`ALLOW_ALL`

Allows the model to generate images of people, including adults and children.

`ALLOW_ADULT`

Allows the model to generate images of adults, but not children.

`ALLOW_NONE`

Prevents the model from generating images of people.
