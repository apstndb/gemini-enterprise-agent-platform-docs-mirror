---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data
title: Manually log data to an experiment run
description: To manually log data to an experiment run, you can use the Agent Platform SDK for Python. Supported metrics and parameters include summary metrics, time series metrics, parameters, and classification metrics.
data_source: docs.cloud.google.com
---

For logging purposes, use the Agent Platform SDK for Python.

Supported metrics and parameters:

  - summary metrics
  - time series metrics
  - parameters
  - classification metrics

### Agent Platform SDK for Python

Note: When the optional `resume` parameter is specified as `TRUE` , the previously started run resumes. When not specified, `resume` defaults to `FALSE` and a new run is created.

The following sample uses the [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) method, from the [aiplatform functions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#functions) .

### Summary metrics

Summary metrics are single value scalar metrics stored next to time series metrics and represent a final summary of an experiment run .

One example use case is early stopping where a patience configuration allows continued training but the candidate model is restored from an earlier step and the metrics calculated for the model at that step would be represented as a summary metric because the latest time series metric is not representative of the restored model. The [`log_metrics`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_metrics) API for summary metrics is used for this purpose.

### Python

    from typing import Dict
    
    from google.cloud import aiplatform
    
    
    def log_metrics_sample(
        experiment_name: str,
        run_name: str,
        metrics: Dict[str, float],
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name)
    
        aiplatform.log_metrics(metrics)

  - `experiment_name` : Provide a name for your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `run_name` : Specify a run name (see [`start_run`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) ).
  - `metric` : Metrics key-value pairs. For example: `{'learning_rate': 0.1}`
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)

### Time series metrics

To log time series metrics, Vertex AI Experiments requires a backing Vertex AI TensorBoard instance.

#### Assign backing Vertex AI TensorBoard resource for Time Series Metric Logging.

All metrics logged through [`log_time_series_metrics`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_time_series_metrics) are stored as time series metrics . Vertex AI TensorBoard is the backing time series metric store.

The `experiment_tensorboard` can be set at both the experiment and experiment run levels. Setting the `experiment_tensorboard` at the run level overrides the setting at the experiment level. Once the `experiment_tensorboard` is set in a run, the run's `experiment_tensorboard` can't be changed.

  - Set `experiment_tensorboard` at experiment level:
    
    ``` 
      aiplatform.init(experiment='my-experiment',
                   experiment_tensorboard='projects/.../tensorboard/my-tb-resource')
    ```

  - Set `experiment_tensorboard` at run level: Note: Overrides setting at experiment level.
    
    ``` 
      aiplatform.start_run(run_name='my-other-run',
                        tensorboard='projects/.../.../other-resource')
    aiplatform.log_time_series_metrics(...)
    ```

### Python

    from typing import Dict, Optional
    
    from google.cloud import aiplatform
    from google.protobuf import timestamp_pb2
    
    
    def log_time_series_metrics_sample(
        experiment_name: str,
        run_name: str,
        metrics: Dict[str, float],
        step: Optional[int],
        wall_time: Optional[timestamp_pb2.Timestamp],
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)
    
        aiplatform.log_time_series_metrics(metrics=metrics, step=step, wall_time=wall_time)

  - `experiment_name` : Provide the name of your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `run_name` : Specify a run name (see [`start_run`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) ).
  - `metrics` : Dictionary of where keys are metric names and values are metric values.
  - `step` : Optional. Step index of this data point within the run.
  - `wall_time` : Optional. Wall clock timestamp when this data point is generated by the end user. If not provided, `wall_time` is generated based on the value from time.time()
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)

#### Step and walltime

The `log_time_series_metrics` API optionally accepts `step` and `walltime` .

  - `step` : Optional. Step index of this data point within the run. If not provided, an increment over the latest step among all time series metrics already logged is used. If the step exists for any of the provided metric keys, the step is overwritten.
  - `wall_time` : Optional. The seconds after epoch of the logged metric. If this is not provided the default is to Python's `time.time` .

For example:

    aiplatform.log_time_series_metrics({"mse": 2500.00, "rmse": 50.00})

##### Log to a specific step

    aiplatform.log_time_series_metrics({"mse": 2500.00, "rmse": 50.00}, step=8)

##### Include `wall_time`

    aiplatform.log_time_series_metrics({"mse": 2500.00, "rmse": 50.00}, step=10)

### Parameters

Parameters are keyed input values that configure a run, regulate the behavior of the run, and affect the results of the run. Examples include learning rate, dropout rate, and number of training steps. Log parameters using the [log\_params](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_params) method.

### Python

    from typing import Dict, Union
    
    from google.cloud import aiplatform
    
    
    def log_params_sample(
        experiment_name: str,
        run_name: str,
        params: Dict[str, Union[float, int, str]],
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)
    
        aiplatform.log_params(params)

    aiplatform.log_params({"learning_rate": 0.01, "n_estimators": 10})

  - `experiment_name` : Provide a name for your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `run_name` : Specify a run name (see [`start_run`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) ).
  - `params` : Parameter key-value pairs For example: `{'accuracy': 0.9}` (see [`log_params`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_params) ). [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)

### Classification metrics

In addition to summary metrics and time series metrics, confusion matrices and ROC curves are commonly used metrics. They can be logged to Vertex AI Experiments using the [`log_classification_metrics`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_classification_metrics) API.

### Python

    from typing import List, Optional
    
    from google.cloud import aiplatform
    
    
    def log_classification_metrics_sample(
        experiment_name: str,
        run_name: str,
        project: str,
        location: str,
        labels: Optional[List[str]] = None,
        matrix: Optional[List[List[int]]] = None,
        fpr: Optional[List[float]] = None,
        tpr: Optional[List[float]] = None,
        threshold: Optional[List[float]] = None,
        display_name: Optional[str] = None,
    ) -> None:
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)
    
        aiplatform.log_classification_metrics(
            labels=labels,
            matrix=matrix,
            fpr=fpr,
            tpr=tpr,
            threshold=threshold,
            display_name=display_name,
        )

  - `experiment_name` : Provide a name for your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `run_name` : Specify a run name (see [`start_run`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) ).
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `labels` : List of label names for the confusion matrix. Must be set if 'matrix' is set.
  - `matrix` : Values for the confusion matrix. Must be set if 'labels' is set.
  - `fpr` : List of false positive rates for the ROC curve. Must be set if 'tpr' or 'thresholds' is set.
  - `tpr` : List of true positive rates for the ROC curve. Must be set if 'fpr' or 'thresholds' is set.
  - `threshold` : List of thresholds for the ROC curve. Must be set if 'fpr' or 'tpr' is set.
  - `display_name` : The user-defined name for the classification metric artifact.

## View experiment runs list in the Google Cloud console

1.  In the Google Cloud console, go to the **Experiments** page.  
      
    A list of experiments appears.
2.  Select the experiment that you want to check.  
    A list of runs appears.

![Vertex AI experiment list page](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/experiment-runs-list.png)  
For more details, see [Compare and analyze runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs#console-compare-analyze-runs) .

## What's next

  - [Compare and analyze runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs)

### Notebook tutorial

  - [Compare models trained and evaluated locally](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)

### Blog post

  - [Machine Learning Experiments in Gaming and Why it Matters](https://cloud.google.com/blog/topics/developers-practitioners/machine-learning-experiments-gaming-and-why-it-matters)
