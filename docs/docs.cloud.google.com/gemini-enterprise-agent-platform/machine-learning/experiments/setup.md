---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/setup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/setup
title: Set up for Vertex AI Experiments
description: Set up your project for Gemini Enterprise Agent Platform Experiments.
data_source: docs.cloud.google.com
---

Vertex AI Experiments is supported by the Agent Platform SDK for Python and Google Cloud console. Vertex AI Experiments requires and depends on [Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) .

## Set up

1.  Create a Service account. See [Create a service account with required permissions](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-training#create_a_service_account_with_required_permissions) .
2.  Install the [Agent Platform SDK for Python.](https://docs.cloud.google.com/vertex-ai/docs/start/install-sdk)
3.  Check for existence of the `default` Metadata Store in your project. (required)
      - To see if your project has the `default` Metadata Store, go to the `Metadata` page in the Google Cloud console.
      - If the `default` Metadata Store doesn't exist, it's created when
          - you run the first PipelineJob ,
          - or, create your first experiment in the Agent Platform SDK for Python.  
            Optional: To configure with CMEK, see [Configure your project's metadata store.](https://docs.cloud.google.com/vertex-ai/docs/ml-metadata/configure)

## Supported Locations

The [Feature availability](https://docs.cloud.google.com/vertex-ai/docs/general/locations#americas_1) table lists the available locations for Vertex AI Experiments. When using Agent Platform Pipelines or Vertex AI TensorBoard, they must be in the same location as your Agent Platform experiment.

## What's next

  - [Create an experiment](https://docs.cloud.google.com/vertex-ai/docs/experiments/create-experiment)

## Relevant notebook tutorials

1.  [Compare trained and evaluated models](https://docs.cloud.google.com/vertex-ai/docs/experiments/user-journey/uj-compare-models)
2.  [Model training with prebuilt data pre-processing code](https://docs.cloud.google.com/vertex-ai/docs/experiments/user-journey/uj-model-training)
3.  [Compare pipeline runs](https://docs.cloud.google.com/vertex-ai/docs/experiments/user-journey/uj-compare-pipeline-runs)
4.  [Autologging](https://docs.cloud.google.com/vertex-ai/docs/experiments/user-journey/uj-autologging)
