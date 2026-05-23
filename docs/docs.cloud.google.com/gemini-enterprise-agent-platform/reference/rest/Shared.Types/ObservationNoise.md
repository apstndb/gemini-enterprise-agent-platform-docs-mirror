---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ObservationNoise
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ObservationNoise
title: ObservationNoise
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.

Enums

`OBSERVATION_NOISE_UNSPECIFIED`

The default noise level chosen by Agent Platform.

`LOW`

Agent Platform assumes that the objective function is (nearly) perfectly reproducible, and will never repeat the same Trial parameters.

`HIGH`

Agent Platform will estimate the amount of noise in metric evaluations, it may repeat the same Trial parameters more than once.
