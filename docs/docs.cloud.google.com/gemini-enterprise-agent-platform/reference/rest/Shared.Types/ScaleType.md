---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ScaleType
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ScaleType
title: ScaleType
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The type of scaling that should be applied to this parameter.

Enums

`SCALE_TYPE_UNSPECIFIED`

By default, no scaling is applied.

`UNIT_LINEAR_SCALE`

Scales the feasible space to (0, 1) linearly.

`UNIT_LOG_SCALE`

Scales the feasible space logarithmically to (0, 1). The entire feasible space must be strictly positive.

`UNIT_REVERSE_LOG_SCALE`

Scales the feasible space "reverse" logarithmically to (0, 1). The result is that values close to the top of the feasible space are spread out more than points near the bottom. The entire feasible space must be strictly positive.
