---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-mlops
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-mlops
title: MLOps on Gemini Enterprise Agent Platform
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=1ykDWsnL2LE)

This section describes Gemini Enterprise Agent Platform services that help you implement *Machine learning operations (MLOps)* with your machine learning (ML) workflow.

After your models are deployed, they must keep up with changing data from the environment to perform optimally and stay relevant. MLOps is a set of practices that improves the stability and reliability of your ML systems.

Gemini Enterprise Agent Platform MLOps tools help you collaborate across AI teams and improve your models through predictive model monitoring, alerting, diagnosis, and actionable explanations. All the tools are modular, so you can integrate them into your existing systems as needed.

For more information about MLOps, see [Continuous delivery and automation pipelines in machine learning](https://docs.cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning) and the [Practitioners Guide to MLOps](https://services.google.com/fh/files/misc/practitioners_guide_to_mlops_whitepaper.pdf) .

![diagram of MLOps capabilities](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/start/images/mlops.png)

  - **Orchestrate workflows** : Manually training and serving your models can be time-consuming and error-prone, especially if you need to repeat the processes many times.
    
      - [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) helps you automate, monitor, and govern your ML workflows.

  - **Manage and scale training jobs** : Efficiently managing compute resources for training is a core MLOps challenge, especially when scaling from experimentation to production. Vertex AI Training addresses this by providing flexible, fully managed services with compute options to fit the entire ML lifecycle.
    
      - For experimentation and variable workloads, [custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-mlops) involves the default serverless platform that provisions resources on-demand, offering maximum flexibility.
    
      - For large-scale, predictable workloads, [Gemini Enterprise Agent Platform training clusters](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/overview) on reserved clusters provides a persistent, dedicated environment that ensures resource availability, delivers stable performance, and helps optimize costs for high-utilization teams.

  - **Track the metadata used in your ML system** : In data science, it's important to track the parameters, artifacts, and metrics used in your ML workflow, especially when you repeat the workflow multiple times.
    
      - [Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) lets you record the metadata, parameters, and artifacts that are used in your ML system. You can then query that metadata to help analyze, debug, and audit the performance of your ML system or the artifacts that it produces.

  - **Identify the best model for a use case** : When you try new training algorithms, you need to know which trained model performs the best.
    
      - [Vertex AI Experiments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments) lets you track and analyze different model architectures, hyper-parameters, and training environments to identify the best model for your use case.
    
      - [Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction) helps you track, visualize, and compare ML experiments to measure how well your models perform.

  - **Manage model versions** : Adding models to a central repository helps you keep track of model versions.
    
      - [Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) provides an overview of your models so you can better organize, track, and train new versions. From Model Registry, you can evaluate models, deploy models to an endpoint, create batch inferences, and view details about specific models and model versions.

  - **Manage features** : When you re-use ML features across multiple teams, you need a quick and efficient way to share and serve the features.
    
      - [Vertex AI Feature Store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/overview) provides a centralized repository for organizing, storing, and serving ML features. Using a central featurestore enables an organization to re-use ML features at scale and increase the velocity of developing and deploying new ML applications.

  - **Monitor model quality** : A model deployed in production performs best on inference input data that is similar to the training data. When the input data deviates from the data used to train the model, the model's performance can deteriorate, even if the model itself hasn't changed.
    
      - [Gemini Enterprise Agent Platform Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) monitors models for training-serving skew and inference drift and sends you alerts when the incoming inference data skews too far from the training baseline. You can use the alerts and feature distributions to evaluate whether you need to retrain your model.

  - **Scale AI and Python applications** : [Ray](https://docs.ray.io/en/latest/ray-overview/index.html) is an open-source framework for scaling AI and Python applications. Ray provides the infrastructure to perform distributed computing and parallel processing for your machine learning (ML) workflow.
    
      - [Ray on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray) is designed so you can use the same open source Ray code to write programs and develop applications on Gemini Enterprise Agent Platform with minimal changes. You can then use Gemini Enterprise Agent Platform's integrations with other Google Cloud services such as [Vertex AI Inference](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) and [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) as part of your machine learning (ML) workflow.

## What's next

  - [Gemini Enterprise Agent Platform interfaces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-interfaces)
