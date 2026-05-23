---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MeasurementSelectionType
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MeasurementSelectionType
title: MeasurementSelectionType
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose LAST\_MEASUREMENT. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose BEST\_MEASUREMENT. B) Are your measurements significantly noisy and/or irreproducible? If so, BEST\_MEASUREMENT will tend to be over-optimistic, and it may be better to choose LAST\_MEASUREMENT. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen.

Enums

`MEASUREMENT_SELECTION_TYPE_UNSPECIFIED`

Will be treated as LAST\_MEASUREMENT.

`LAST_MEASUREMENT`

Use the last measurement reported.

`BEST_MEASUREMENT`

Use the best measurement reported.
