---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations
title: Supported locations for agents in Agent Platform
description: Review the locations where agents deployed to Gemini Enterprise Agent Platform are available.
data_source: docs.cloud.google.com
---

This page lists the supported locations for Google agents and agent infrastructure features (such as runtime, sessions, and memory banks) in Gemini Enterprise Agent Platform.

To see supported locations for generative AI models on Agent Platform, see [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

Runtime, Sessions, Memory Bank, and Agent Gateway are supported in the following zones, regions, and multi-regions. For more information about regions and zones, see [Geography and regions](https://docs.cloud.google.com/docs/geography-and-regions) .

| Region                                       | Location          | Supported versions                                                              |
| -------------------------------------------- | ----------------- | ------------------------------------------------------------------------------- |
| `us-east1`                                   | South Carolina    | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `us-east4`                                   | Northern Virginia | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `us-west1`                                   | Oregon            | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `us-central1`                                | Iowa              | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-west1`                               | Belgium           | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-west2`                               | London            | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-west3`                               | Frankfurt         | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-west4`                               | Netherlands       | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-west6`                               | Zurich            | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-west8`                               | Milan             | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `europe-southwest1`                          | Madrid            | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `asia-east1`                                 | Taiwan            | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| ` asia-east2         †        `              | Hong Kong         | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `asia-northeast1`                            | Tokyo             | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| ` asia-northeast3         †        `         | Seoul             | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `asia-south1`                                | Mumbai            | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `asia-southeast1`                            | Singapore         | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| ` asia-southeast2         *†        `        | Jakarta           | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| ` australia-southeast2         *        `    | Melbourne         | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `me-west1`                                   | Tel Aviv          | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `northamerica-northeast1`                    | Montréal          | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| ` northamerica-northeast2         *        ` | Toronto           | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |
| `southamerica-east1`                         | São Paulo         | `v1` is supported for GA features. `v1beta1` is supported for Preview features. |

<sup>\*</sup> Memory Bank is not supported in this region. <sup>†</sup> Agent Gateway is not supported in this region.

For [Code Execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/code-execution-overview) (Preview), the following regions are supported.

| Region        | Location | Supported versions              |
| ------------- | -------- | ------------------------------- |
| `us-central1` | Iowa     | `v1beta1` version is supported. |

## Multi-regional and global endpoints

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Memory Bank and Sessions support multi-regional and global endpoints. For global requests, set your location to `global` . For multi-regional requests, set your location to `us` or `eu` .

### Supported agents

Usage of the global endpoint is supported for the following Google agents.

  - [Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/google/deep-research) (Preview)
