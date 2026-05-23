---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction
title: Introduction to Vertex AI TensorBoard
description: Vertex AI TensorBoard lets you track, visualize, and compare ML experiments and share them with your team
data_source: docs.cloud.google.com
---

Vertex AI TensorBoard is an enterprise-ready managed version of [Open Source TensorBoard](https://www.tensorflow.org/tensorboard/get_started) (TB), which is a Google Open Source project for machine learning experiment visualization.

With Vertex AI TensorBoard, you can track, visualize, and compare ML experiments and share them with your team.

![TensorBoard view appears](https://docs.cloud.google.com/static/vertex-ai/docs/experiments/images/tb-view-appears.png)

Vertex AI TensorBoard provides various detailed visualizations, that includes:

  - tracking and visualizing metrics such as loss and accuracy over time,
  - visualizing model computational graphs (ops and layers),
  - viewing histograms of weights, biases, or other tensors as they change over time,
  - projecting embeddings to a lower dimensional space,
  - and displaying image, text, and audio samples.

In addition to the powerful visualizations from TensorBoard, Vertex AI TensorBoard provides:

  - a persistent, shareable link to your experiment's, Vertex AI TensorBoard experiment,
  - tight integrations with Gemini Enterprise Agent Platform services for model training,
  - enterprise-grade security, privacy, and compliance.

Integration with Gemini Enterprise Agent Platform Experiments lets you:

  - use a searchable and compare list of all experiments in a project,
  - view time series metrics in the Google Cloud console,
  - compare scalars across experiments and experiment runs,
  - have direct access to Vertex AI TensorBoard.

## Vertex AI TensorBoard and the Google Cloud console

The Google Cloud console is used to:

  - create or delete Vertex AI TensorBoard instances,
  - create [Vertex AI Experiments](https://docs.cloud.google.com/vertex-ai/docs/experiments/create-experiment#google-cloud-console) ,
  - view Vertex AI TensorBoard instance storage size → associated costs,
  - view associated [Vertex AI Experiments, Custom Jobs, and Pipeline Runs](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs) ,
  - visualize some [time series metrics](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-view#visualize_metrics_console) .

## What's next

  - [Setup Vertex AI TensorBoard](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-setup)
  - Check out the [TensorBoard API documentation](https://www.tensorflow.org/tensorboard/get_started) .
