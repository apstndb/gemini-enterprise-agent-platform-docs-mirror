---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Status
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Status
title: Status
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The status of the interaction.

Enums

`UNSPECIFIED`

Default value. This value is unused.

`IN_PROGRESS`

The interaction is in progress.

`REQUIRES_ACTION`

The interaction requires action/input from the user.

`COMPLETED`

The interaction is completed.

`FAILED`

The interaction failed.

`CANCELLED`

The interaction was cancelled.

`INCOMPLETE`

The interaction is completed, but contains incomplete results (e.g. hitting maxTokens).

`BUDGET_EXCEEDED`

The interaction was halted because the token budget was exceeded.

`QUEUED`

The interaction is queued, waiting for processing (e.g. waiting for off-peak capacity).
