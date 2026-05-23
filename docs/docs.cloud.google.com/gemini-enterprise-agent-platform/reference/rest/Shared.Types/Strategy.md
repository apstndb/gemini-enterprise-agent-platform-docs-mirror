---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Strategy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Strategy
title: Strategy
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

Enums

`STRATEGY_UNSPECIFIED`

Strategy will default to STANDARD.

`ON_DEMAND`

Deprecated. Regular on-demand provisioning strategy.

> This item is deprecated\!

`LOW_COST`

Deprecated. Low cost by making potential use of spot resources.

> This item is deprecated\!

`STANDARD`

Standard provisioning strategy uses regular on-demand resources.

`SPOT`

Spot provisioning strategy uses spot resources.

`FLEX_START`

Flex Start strategy uses DWS to queue for resources.
