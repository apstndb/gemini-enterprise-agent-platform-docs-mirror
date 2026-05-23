---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/resource-naming
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/resource-naming
title: Resource names
description: Review rules and guidance for naming models and endpoints in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

You must specify a name for every Gemini Enterprise Agent Platform model and endpoint that you create. The rules for naming are consistent for both types of resource. Each name:

  - Must only contain letters, numbers, dashes and underscores.
  - Is case-sensitive.
  - Must start with a letter.
  - Must be no more than 128 characters long.

You should create names that you can distinguish in lists of resources or identify by the dataset they use, for example:

  - `  USE_CASE -a-v1-model `
  - `  USE_CASE -a-v1-endpoint `
  - `  USE_CASE -a-v1-pipeline `
  - `  OWNER_NAME - USE_CASE -a-v1-model `
