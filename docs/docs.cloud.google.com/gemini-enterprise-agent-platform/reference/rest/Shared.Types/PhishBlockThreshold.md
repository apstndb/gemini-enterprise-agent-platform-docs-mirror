---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PhishBlockThreshold
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PhishBlockThreshold
title: PhishBlockThreshold
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

These are available confidence level user can set to block malicious urls with chosen confidence and above. For understanding different confidence of webrisk, please refer to <https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel>

Enums

`PHISH_BLOCK_THRESHOLD_UNSPECIFIED`

Defaults to unspecified.

`BLOCK_LOW_AND_ABOVE`

Blocks Low and above confidence URL that is risky.

`BLOCK_MEDIUM_AND_ABOVE`

Blocks Medium and above confidence URL that is risky.

`BLOCK_HIGH_AND_ABOVE`

Blocks High and above confidence URL that is risky.

`BLOCK_HIGHER_AND_ABOVE`

Blocks Higher and above confidence URL that is risky.

`BLOCK_VERY_HIGH_AND_ABOVE`

Blocks Very high and above confidence URL that is risky.

`BLOCK_ONLY_EXTREMELY_HIGH`

Blocks Extremely high confidence URL that is risky.
