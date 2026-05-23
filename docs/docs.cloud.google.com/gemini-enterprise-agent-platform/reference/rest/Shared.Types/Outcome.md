---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Outcome
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Outcome
title: Outcome
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Enumeration of possible outcomes of the code execution.

Enums

`OUTCOME_UNSPECIFIED`

Unspecified status. This value should not be used.

`OUTCOME_OK`

code execution completed successfully. `output` contains the stdout, if any.

`OUTCOME_FAILED`

code execution failed. `output` contains the stderr and stdout, if any.

`OUTCOME_DEADLINE_EXCEEDED`

code execution ran for too long, and was cancelled. There may or may not be a partial `output` present.
