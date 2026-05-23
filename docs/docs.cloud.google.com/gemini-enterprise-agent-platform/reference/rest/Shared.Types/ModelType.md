---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ModelType
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ModelType
title: ModelType
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Enums

`MODEL_TYPE_UNSPECIFIED`

Should not be set.

`CLOUD`

A Model best tailored to be used within Google Cloud, and which cannot be exported. Default.

`CLOUD_1`

A model type best tailored to be used within Google Cloud, which cannot be exported externally. Compared to the CLOUD model above, it is expected to have higher prediction accuracy.

`MOBILE_TF_LOW_LATENCY_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

`MOBILE_TF_VERSATILE_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device with afterwards.

`MOBILE_TF_HIGH_ACCURACY_1`

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow or Core ML model and used on a mobile or edge device afterwards. Expected to have a higher latency, but should also have a higher prediction quality than other mobile models.
