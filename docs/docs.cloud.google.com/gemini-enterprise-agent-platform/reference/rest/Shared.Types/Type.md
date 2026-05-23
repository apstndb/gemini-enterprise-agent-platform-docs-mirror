---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Type
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Type
title: Type
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Identifies a type of reservation affinity.

Enums

`TYPE_UNSPECIFIED`

Default value. This should not be used.

`NO_RESERVATION`

Do not consume from any reserved capacity, only use on-demand.

`ANY_RESERVATION`

Consume any reservation available, falling back to on-demand.

`SPECIFIC_RESERVATION`

Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields.
