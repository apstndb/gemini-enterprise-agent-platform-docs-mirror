---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/autolog-data
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/autolog-data
title: Autolog data to an experiment run
description: Autologging is a feature in the Vertex AI SDK that automatically logs parameters and metrics from model-training runs to Vertex AI Experiments. Autologging only supports parameter and metric logging.
data_source: docs.cloud.google.com
---

Autologging is a feature in the Vertex AI SDK that automatically logs parameters and metrics from model-training runs to Vertex AI Experiments. This can save time and effort by eliminating the need to manually log this data. Autologging only supports parameter and metric logging.

## Autolog data

There are two options for autologging data to Vertex AI Experiments.

1.  Let the Vertex AI SDK automatically create [ExperimentRun](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun?_gl=1*m6thp1*_ga*NDY0ODI5NjQ5LjE2ODIxMjU5Nzc.*_ga_4LYFWVHBEB*MTY4MjM2MDE5NC40LjEuMTY4MjM2MDcxNy4wLjAuMA..#google_cloud_aiplatform_ExperimentRun) resources for you.  
2.  Specify the ExperimentRun resource that you'd like autologged parameters and metrics to be written to.  

### Auto-created

The Agent Platform SDK for Python handles creating ExperimentRun resources for you. Automatically created ExperimentRun resources will have a run name in the following format: `{ml-framework-name}-{timestamp}-{uid}` , for example: "tensorflow-2023-01-04-16-09-20-86a88".  

The following sample uses the [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) method, from the `aiplatform` [Package functions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#functions) .

### Python

    from typing import Optional, Union
    
    from google.cloud import aiplatform
    
    
    def autologging_with_auto_run_creation_sample(
        experiment_name: str,
        project: str,
        location: str,
        experiment_tensorboard: Optional[Union[str, aiplatform.Tensorboard]] = None,
    ):
        aiplatform.init(
            experiment=experiment_name,
            project=project,
            location=location,
            experiment_tensorboard=experiment_tensorboard,
        )
    
        aiplatform.autolog()
    
        # Your model training code goes here
    
        aiplatform.autolog(disable=True)

  - `experiment_name` : Provide a name for your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `experiment_tensorboard` : (Optional) Provide a name for your Vertex AI TensorBoard instance.
  - `project` : . You can find these Project IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)

### User-specified

Provide your own ExperimentRun names and have metrics and parameters from multiple model-training runs logged to the same ExperimentRun. Any metrics from model to the current run set by calling `aiplatform.start_run("your-run-name")` until `aiplatform.end_run()` is called.  

The following sample uses the [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) method, from the `aiplatform` [Package functions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#functions) .

### Python

    from typing import Optional, Union
    
    from google.cloud import aiplatform
    
    
    def autologging_with_manual_run_creation_sample(
        experiment_name: str,
        run_name: str,
        project: str,
        location: str,
        experiment_tensorboard: Optional[Union[str, aiplatform.Tensorboard]] = None,
    ):
        aiplatform.init(
            experiment=experiment_name,
            project=project,
            location=location,
            experiment_tensorboard=experiment_tensorboard,
        )
    
        aiplatform.autolog()
    
        aiplatform.start_run(run=run_name)
    
        # Your model training code goes here
    
        aiplatform.end_run()
    
        aiplatform.autolog(disable=True)

  - `experiment_name` : Provide the name of your experiment.
  - `run_name` : Provide a name for your experiment run. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these Project IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)
  - `experiment_tensorboard` : (Optional) Provide a name for your Vertex AI TensorBoard instance.

Vertex AI SDK autologging uses MLFlow's autologging in its implementation. Evaluation metrics and parameters from the following frameworks are logged to your ExperimentRun when autologging is enabled.

  - Fastai
  - Gluon
  - Keras
  - LightGBM
  - Pytorch Lightning
  - Scikit-learn
  - Spark
  - Statsmodels
  - XGBoost

## View autologged parameters and metrics

Use the Agent Platform SDK for Python to [compare runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs#compare-runs) and get runs data. The [Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs#console-compare-analyze-runs) provides an easy way to compare these runs.

## Relevant notebook sample

  - [Autolog data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-autologging)

## Blog post

  - [How you can automate ML experiment tracking with Vertex AI Experiments autologging](https://cloud.google.com/blog/products/ai-machine-learning/effortless-tracking-of-your-vertex-ai-model-training)
