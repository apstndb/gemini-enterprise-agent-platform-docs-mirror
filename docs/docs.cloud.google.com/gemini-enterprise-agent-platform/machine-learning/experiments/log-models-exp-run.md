---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-models-exp-run
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-models-exp-run
title: Log models to an experiment run
description: Describes logging the model to Vertex AI Experiments.
data_source: docs.cloud.google.com
---

In order for a model to be tracked, shared, and analyzed, the Agent Platform SDK for Python provides an API that serializes a machine learning model into an [`ExperimentModel`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel) class and logs the model to Vertex AI Experiments.

After selecting the best model to use, you can register that model from Vertex AI Experiments to Gemini Enterprise Agent Platform Model Registry.

Supported frameworks are scikit-learn, XGBoost, and TensorFlow.

### Save and log ML model

### Save models

The Vertex AI SDK provides the [`save_model`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_save_model) method to serialize an ML model, upload the model to Cloud Storage, and represent the model as a Vertex ML Metadata artifact.

### Python

    from typing import Optional, Union
    
    from google.cloud import aiplatform
    
    
    def save_model_sample(
        project: str,
        location: str,
        model: Union[
            "sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"  # noqa: F821
        ],
        artifact_id: Optional[str] = None,
        uri: Optional[str] = None,
        input_example: Optional[
            Union[list, dict, "pd.DataFrame", "np.ndarray"]  # noqa: F821
        ] = None,
        display_name: Optional[str] = None,
        staging_bucket: Optional[str] = None,
    ) -> None:
        aiplatform.init(project=project, location=location)
    
        aiplatform.save_model(
            model=model,
            artifact_id=artifact_id,
            uri=uri,
            input_example=input_example,
            display_name=display_name,
            staging_bucket=staging_bucket,
        )

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)
  - `model` : (Required). A machine learning model. `(Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"])`
  - `artifact_id` : Optional. The resource ID of the artifact. This ID must be globally unique in a metadataStore. It might be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character can't be a number or a hyphen.
  - `uri` : Optional. A gcs directory in which to save the model file. If a uri isn't provided, `gs://default-bucket/timestamp-uuid-frameworkName-model` is used. If a default staging bucket isn't set, it must be passed in the `staging_bucket` parameter.
  - `input_example` : Optional. Each model takes input data and then produces a prediction. Each model accepts one particular format of input (for example, a number, a string, 2d array) and is stored as a yaml file in the gcs uri. Accepts list, dict, pd.DataFrame, and np.ndarray The value inside a list must be a scalar or list. The value inside a dict must be a scalar, list, or np.ndarray. `(Union[list, dict, pd.DataFrame, np.ndarray])` .
  - `display_name` : The display name of the artifact.
  - `staging_bucket` : Optional. The staging bucket used to save the model. If not provided, the staging bucket set in `aiplatform.init` is used. A staging bucket or uri is required for saving a model.

### Log models

The Vertex AI SDK provides a [`log_model`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_model) method, which orchestrates [`save_model`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_save_model) and an additional step to log the Vertex ML Metadata artifact to the current experiment run. The `log_model` method to manage and analyze multiple ML models in Vertex AI Experiments.

### Python

    from typing import Optional, Union
    
    from google.cloud import aiplatform
    
    
    def log_model_sample(
        experiment_name: str,
        run_name: str,
        project: str,
        location: str,
        model: Union[
            "sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"  # noqa: F821
        ],
        artifact_id: Optional[str] = None,
        uri: Optional[str] = None,
        input_example: Optional[
            Union[list, dict, "pd.DataFrame", "np.ndarray"]  # noqa: F821
        ] = None,  # noqa: F821
        display_name: Optional[str] = None,
    ) -> None:
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)
    
        aiplatform.log_model(
            model=model,
            artifact_id=artifact_id,
            uri=uri,
            input_example=input_example,
            display_name=display_name,
        )

  - `experiment_name` : Provide the name of your experiment. You can find your list of experiments in the Google Cloud console by selecting "Experiments" in the section nav.
  - `run_name` : Specify a run name.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `model` : Required. A machine learning model. `(Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"])`
  - `uri` : Optional. A gcs directory in which to save the model file. If a uri is not provided, `gs://default-bucket/timestamp-uuid-frameworkName-model` is used. If a default staging bucket is not set, a new bucket is created.
  - `input_example` : Optional. Each model takes input data and then produces a prediction. Each model accepts one particular format of input (for example, a number, a string, 2d array) and is stored as a yaml file in the gcs uri. Accepts list, dict, pd.DataFrame, and np.ndarray The value inside a list must be a scalar or list. The value inside a dict must be a scalar, list, or np.ndarray. `(Union[list, dict, pd.DataFrame, np.ndarray])` .
  - `display_name` : Optional. The display name of the artifact.

### Track `ExperimentModel`

### Get experiment model

To use [`get_experiment_model`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_get_experiment_model) to return a saved model, pass it the saved model's artifact ID.

### Python

    from google.cloud import aiplatform
    
    
    def get_experiment_model_sample(
        project: str,
        location: str,
        artifact_id: str,
    ) -> "ExperimentModel":  # noqa: F821
        aiplatform.init(project=project, location=location)
        experiment_model = aiplatform.get_experiment_model(artifact_id=artifact_id)
    
        return experiment_model

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `artifact_id` : Required: The resource ID of the existing model.

### Get experiment models

The [`get_experiment_models`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun#google_cloud_aiplatform_ExperimentRun_get_experiment_models) method gets a list of all the `ExperimentModel` 's that are logged to a particular experiment run.

### Python

    from typing import List, Union
    
    from google.cloud import aiplatform
    
    
    def get_experiment_run_models_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
    ) -> List["ExperimentModel"]:  # noqa: F821
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name, experiment=experiment, project=project, location=location
        )
    
        return experiment_run.get_experiment_models()

  - `run_name` : Specify a run name.
  - `experiment` : Provide the name of your experiment. You can find your list of experiments in the Google Cloud console by selecting "Experiments" in the section nav.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Get model information

The `get_model_info` method returns the model's metadata of a given `ExperimentModel` instance, for example, model class, framework type.

### Python

    from typing import Any, Dict
    
    from google.cloud import aiplatform
    
    
    def get_model_info_sample(
        artifact_id: str,
        project: str,
        location: str,
    ) -> Dict[str, Any]:
        experiment_model = aiplatform.get_experiment_model(
            artifact_id=artifact_id, project=project, location=location
        )
    
        return experiment_model.get_model_info()

  - `artifact_id` : Required The resource ID of the existing `ExperimentModel` .
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Load `ExperimentModel`

### Load model

The `load_experiment_model` method helps you deserialize an `ExperimentModel` instance back to the original ML model.

### Python

    from typing import Union
    
    from google.cloud import aiplatform
    
    
    def load_experiment_model_sample(
        artifact_id: str,
        project: str,
        location: str,
    ) -> Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"]:  # noqa: F821:
        experiment_model = aiplatform.get_experiment_model(
            artifact_id=artifact_id, project=project, location=location
        )
    
        return experiment_model.load_model()

  - `artifact_id` : (Required). The resource ID of the existing `ExperimentModel` . Example: `artifact_id="my-sklearn-model"`
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Register `ExperimentModel`

### Register saved model

The `register_experiment_model` API enables registering the model that was deemed the best, in Gemini Enterprise Agent Platform Model Registry with a minimum amount of configuration. The API automatically chooses a [prebuilt prediction container](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) based on the model's framework and version.

### Python

    from google.cloud import aiplatform
    
    
    def register_experiment_model_sample(
        artifact_id: str,
        project: str,
        location: str,
        display_name: str,
    ) -> aiplatform.models.Model:
        experiment_model = aiplatform.get_experiment_model(
            artifact_id=artifact_id, project=project, location=location
        )
    
        return experiment_model.register_model(display_name=display_name)

  - `artifact_id` : (Required). The resource ID of the existing `ExperimentModel` .
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `display_name` : Optional. The user-defined name of the registered model.

## View experiment runs list in the Google Cloud console

1.  In the Google Cloud console, go to the **Experiments** page.  
      
    A list of experiments appears.
2.  Select the experiment that you want to check.  
    A list of runs appears.

![Vertex AI experiment list page](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/experiment-runs-list.png)

## What's next

  - [Compare and analyze runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs)

### Relevant notebook sample

  - [Compare models trained and evaluated locally](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models)

### Blog post

  - [Machine Learning Experiments in Gaming and Why it Matters](https://cloud.google.com/blog/topics/developers-practitioners/machine-learning-experiments-gaming-and-why-it-matters)
