---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/veo-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/veo-models
title: Provisioned Throughput for Veo&nbsp;3 models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This section explains how Provisioned Throughput works for the Veo 3 and later models, including quota enforcement behavior and minimum GSU purchase increment.

For Veo 3 models, the [quota enforcement period](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/use-provisioned-throughput#pt-quota-enforcement-period) varies based on the number of GSUs you purchase for the model, and is subject to change. The quota enforcement periods for different GSU sizes are as follows:

  - 1-9 GSUs: 2000 seconds

  - 10-19 GSUs: 400 seconds

  - 20-39 GSUs: 200 seconds

  - 40-66 GSUs: 100 seconds

  - 67 or more GSUs: 60 seconds

Note that this isn't connected to the request latency. The time to process your request isn't the same as the quota enforcement period.

For example, if you have a workload that requires generating a four-second video on the Veo 3 model and you purchase 1 GSU, you can generate that video within a few minutes. However, because the enforcement window for 1 GSU is 2000 seconds, you can't generate a video of the same size until the end of that period. Note that this is subject to Gemini Enterprise Agent Platform clock time and doesn't depend on the time of your request. We recommend using the estimation tool on the Provisioned Throughput page to estimate the number of GSUs required for your workload. For more information about using the estimation tool, see [Purchase a Provisioned Throughput order](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput#place-an-order) . These large enforcement windows ensure that your request is processed within a specific time. If you need to process outputs on Veo 3 more frequently, you must buy enough GSUs and check the corresponding enforcement window.

## What's next

  - [Purchase standard Provisioned Throughput.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput)
