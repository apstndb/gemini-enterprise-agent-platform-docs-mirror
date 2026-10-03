---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models
title: Open model deprecations
description: Get deprecation and retirement details for open models offered through Model as a Service (MaaS).
data_source: docs.cloud.google.com
---

This page lists deprecation and retirement details for open models offered through Model as a Service (MaaS).

## Key terms

- **Deprecation** : When a model reaches its **deprecation date** , notice is given that the model is planned for retirement. During the deprecation period, the model endpoint remains functional for existing workloads so that you can plan and implement migrations, but no new features or updates are added and new use of the endpoint may be restricted.
- **Retirement** : When a model reaches its **retirement date** , the model endpoint is permanently deactivated and is no longer accessible or supported. API requests calling a retired model ID will fail.

## Minimum availability for Preview models

Open models offered at the Preview launch stage are available for at least 45 days from their release date. Google might extend availability beyond this period based on usage and demand.

This period is a minimum, not a scheduled deprecation. If a model is deprecated, the deprecation is announced on this page along with the model's retirement date, and the endpoint remains functional throughout the deprecation period so that you can plan and implement a migration.

## Deprecation and retirement details

The following table lists the deprecation and retirement schedules for open models offered through Model as a Service (MaaS), as well as a recommended self-deploy alternative. To learn more about self-deploying a model on Model Garden, see [Overview of self-deployed models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/self-deployed-models) . Alternatively, you can migrate your workloads to alternative managed endpoints before the retirement date.

| Model ID                              | Deprecation date | Retirement date  | Self-deploy alternative |
|---------------------------------------|------------------|------------------|-------------------------|
| `deepseek-ocr-maas`                   | July 21, 2026    | October 21, 2026 |                         |
| `deepseek-r1-0528-maas`               | July 21, 2026    | October 21, 2026 |                         |
| `deepseek-v3.2-maas`                  | July 21, 2026    | October 21, 2026 |                         |
| `deepseek-v3.1-maas`                  | July 21, 2026    | October 21, 2026 |                         |
| `glm-5-maas`                          | July 21, 2026    | October 21, 2026 |                         |
| `glm-4.7-maas`                        | July 21, 2026    | October 21, 2026 |                         |
| `gpt-oss-20b-maas`                    | July 21, 2026    | October 21, 2026 |                         |
| `kimi-k2-thinking-maas`               | July 21, 2026    | October 21, 2026 |                         |
| `llama-3.3-70b-instruct-maas`         | July 21, 2026    | October 21, 2026 |                         |
| `minimax-m2-maas`                     | July 21, 2026    | October 21, 2026 |                         |
| `multilingual-e5-large-instruct-maas` | July 21, 2026    | October 21, 2026 |                         |
| `multilingual-e5-small-maas`          | July 21, 2026    | October 21, 2026 |                         |
| `qwen3-235b-a22b-instruct-2507-maas`  | July 21, 2026    | October 21, 2026 |                         |
| `qwen3-coder-480b-a35b-instruct-maas` | July 21, 2026    | October 21, 2026 |                         |
| `qwen3-next-80b-a3b-instruct-maas`    | July 21, 2026    | October 21, 2026 |                         |
| `qwen3-next-80b-a3b-thinking-maas`    | July 21, 2026    | October 21, 2026 |                         |
