---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Algorithm
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Algorithm
title: Algorithm
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The available search algorithms for the Study.

Enums

`ALGORITHM_UNSPECIFIED`

The default algorithm used by Agent Platform for [hyperparameter tuning](https://cloud.google.com/vertex-ai/docs/training/hyperparameter-tuning-overview) and [Agent Platform Vizier](https://cloud.google.com/vertex-ai/docs/vizier) .

`GRID_SEARCH`

Simple grid search within the feasible space. To use grid search, all parameters must be `INTEGER` , `CATEGORICAL` , or `DISCRETE` .

`RANDOM_SEARCH`

Simple random search within the feasible space.
