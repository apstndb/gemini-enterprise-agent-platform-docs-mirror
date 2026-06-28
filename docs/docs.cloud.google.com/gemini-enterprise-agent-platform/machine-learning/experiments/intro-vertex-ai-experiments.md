---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments
title: Introduction to Gemini Enterprise Agent Platform Experiments
description: Find the best model for your problem by tracking and analyzing different model architectures, hyperparameters, and training environments.
data_source: docs.cloud.google.com
---

> To see an example of getting started with Agent Platform Experiments, run the "Get started with " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb)

Gemini Enterprise Agent Platform Experiments is a tool that helps you track and analyze different model architectures, hyperparameters, and training environments, letting you track the steps, inputs, and outputs of an experiment run. Gemini Enterprise Agent Platform Experiments can also evaluate how your model performed in aggregate, against test datasets, and during the training run. You can then use this information to select the best model for your particular use case.

Experiment runs don't incur additional charges. You're only charged for resources that you use during your experiment as described in [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

| What do you want to do?      | Check out notebook sample                                                                                                                                  |
| :--------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| track metrics and parameters | [Compare models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)               |
| track experiment lineage     | [Model training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-model-training)               |
| track pipeline runs          | [Compare pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-pipeline-runs) |

## Track steps, inputs, and outputs

Agent Platform Experiments lets you track:

  - steps of an experiment run , for example, preprocessing, training,
  - inputs, for example, algorithm, parameters, datasets,
  - outputs of those steps, for example, models, checkpoints, metrics.

You can then figure out what worked and what didn't, and identify further avenues for experimentation.

For user journey examples, check out:

  - [Model training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-model-training)
  - [Compare models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)

## Analyze model performance

Agent Platform Experiments lets you track and evaluate how the model performed in aggregate, against test datasets, and during the training run. This ability helps to understand the performance characteristics of the models -- how well a particular model works overall, where it fails, and where the model excels.

For user journey examples, check out:

  - [Compare pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-pipeline-runs)
  - [Compare models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)

## Compare model performance

Agent Platform Experiments lets you group and compare multiple models across experiment runs . Each model has its own specified parameters, modeling techniques, architectures, and input. This approach helps select the best model.

For user journey examples, check out:

  - [Compare pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-pipeline-runs)
  - [Compare models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)

## Search experiments

The Google Cloud console provides a centralized view of experiments, a cross-sectional view of the experiment runs, and the details for each run. The Agent Platform SDK for Python provides APIs to consume experiments, experiment runs, experiment run parameters, metrics, and artifacts.

Agent Platform Experiments, along with [Gemini Enterprise Agent Platform ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) , provides a way to find the artifacts tracked in an experiment. This lets you quickly view the artifact's lineage and the artifacts consumed and produced by steps in a run.

## Scope of support

Gemini Enterprise Agent Platform Experiments supports development of models using Gemini Enterprise Agent Platform custom training, Gemini Enterprise Agent Platform Workbench notebooks, Notebooks, and all Python ML Frameworks across most ML Frameworks. For some ML frameworks, such as TensorFlow, Gemini Enterprise Agent Platform Experiments provides deep integrations into the framework that makes the user experience automagical. For other ML frameworks, Gemini Enterprise Agent Platform Experiments provides a framework neutral Agent Platform SDK for Python that you can use. (see: [Prebuilt containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) for TensorFlow, scikit-learn, PyTorch, XGBoost).

## Data models and concepts

Gemini Enterprise Agent Platform Experiments is a context in [Agent Platform ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) where an experiment can contain *n* experiment runs in addition to *n* pipeline runs. An experiment run consists of parameters, summary metrics, time series metrics, and [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) , [`Artifact`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact) , and [`Execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution) Gemini Enterprise Agent Platform resources. [Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction) , a managed version of open source TensorBoard, is used for time-series metrics storage. Executions and artifacts of a pipeline run are viewable in the [Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/visualize-pipeline#visualize_pipeline_runs_using) .

## Agent Platform Experiments terms

### Experiment, experiment run, and pipeline run

##### experiment

  - An experiment is a context that can contain a set of n experiment runs in addition to pipeline runs where a user can investigate, as a group, different configurations such as input artifacts or hyperparameters.

See [Create an experiment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-experiment) .

##### experiment run

  - A specific, trackable execution within a Vertex AI Experiment, which logs inputs (like algorithm, parameters, and datasets) and outputs (like models, checkpoints, and metrics) to monitor and compare ML development iterations. For more information, see [Create and manage experiment runs](https://cloud.google.com/vertex-ai/docs/experiments/create-manage-exp-run) .

See [Create and manage experiment runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-manage-exp-run) .

##### pipeline run

  - One or more Vertex PipelineJobs can be associated with an experiment where each PipelineJob is represented as a single run. In this context, the parameters of the run are inferred by the parameters of the PipelineJob. The metrics are inferred from the system.Metric artifacts produced by that PipelineJob. The artifacts of the run are inferred from artifacts produced by that PipelineJob.

One or more Gemini Enterprise Agent Platform [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) resource can be associated with an [`ExperimentRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun) resource. In this context, the parameters, metrics, and artifacts are not inferred.

See [Associate a pipeline with an experiment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/add-pipelinerun-experiment) .

### Parameters and metrics

See [Log parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#parameters) .

##### summary metrics

  - Summary metrics are a single value for each metric key in an experiment run. For example, the test accuracy of an experiment is the accuracy calculated against a test dataset at the end of training that can be captured as a single value summary metric.

See [Log summary metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#summary-metrics) .

##### time series metrics

  - Time series metrics are longitudinal metric values where each value represents a step in the training routine portion of a run. Time series metrics are stored in Vertex AI TensorBoard. Vertex AI Experiments stores a reference to the Vertex TensorBoard resource.

See [Log time series metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#time-series-metrics) .

### Resource types

##### pipeline job

  - A pipeline job or a pipeline run corresponds to the PipelineJob resource in the Vertex AI API. It's an execution instance of your ML pipeline definition, which is defined as a set of ML tasks interconnected by input-output dependencies.

##### artifact

  - An artifact is a discrete entity or piece of data produced and consumed by a machine learning workflow. Examples of artifacts include datasets, models, input files, and training logs.

Agent Platform Experiments lets you use a schema to define the type of artifact. For example, supported schema types include `system.Dataset` , `system.Model` , and `system.Artifact` . For more information, see [System schemas](https://docs.cloud.google.com/vertex-ai/docs/ml-metadata/system-schemas) .

## Notebook tutorial

  - [Get started with Agent Platform Experiments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-get-started-vertex-ai-experiments)

## What's next

  - [Set up to get started with Vertex AI Experiments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/setup)
