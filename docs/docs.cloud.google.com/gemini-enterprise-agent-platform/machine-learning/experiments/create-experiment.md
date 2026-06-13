---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-experiment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-experiment
title: Create or delete an experiment
description: You can use either the Agent Platform SDK for Python or {{dynamic_data.site_values.cloud_name_short}} console to either create or delete an experiment.
data_source: docs.cloud.google.com
---

You can use either the Agent Platform SDK for Python or the Google Cloud console to create or delete an experiment. The SDK is a library of Python code that you can use to programmatically create and manage experiments. The console is a web-based user interface that you can use to create and manage experiments visually.

> When creating an experiment using the Google Cloud console for the first time, be sure that there's a `default` Metadata Store. To check, go to your project's **Metadata** page in the Google Cloud console. See [Configure your project's metadata store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/configure)

## Create experiment with a TensorBoard instance

### Agent Platform SDK for Python

Create an experiment and, optionally, associate a Vertex AI TensorBoard instance using the Agent Platform SDK for Python. Add a description for the experiment to document its purpose. See [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) in the Agent Platform SDK reference documentation.  

### Python

    from typing import Optional, Union
    
    from google.cloud import aiplatform
    
    
    def create_experiment_sample(
        experiment_name: str,
        experiment_description: str,
        experiment_tensorboard: Optional[Union[str, aiplatform.Tensorboard]],
        project: str,
        location: str,
    ):
        aiplatform.init(
            experiment=experiment_name,
            experiment_description=experiment_description,
            experiment_tensorboard=experiment_tensorboard,
            project=project,
            location=location,
        )

  - `experiment_name` : Provide a name for your experiment.
  - `experiment_description` : Provide a description for your experiment.
  - `experiment_tensorboard` : Optional. The Vertex TensorBoard instance to use as a backing TensorBoard for the provided experiment. If no `experiment_tensorboard` is provided, a default TB instance is created and used by this experiment. Note: If CMEK (encryption keys) need to be associated with the TensorBoard instance, then `experiment_tensorboard` is no longer optional.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.  
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) Be sure to use a region that supports TensorBoard if creating a TensorBoard instance.

### Google Cloud console

Use these instructions to create an experiment.

1.  In the Google Cloud console, go to the **Experiments** page.  
2.  Be sure you're in the project you want to create the experiment in.  
    ![Agent Platform select project](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/project-select.png)
3.  Click **add\_box Create** to open the **Experiment** pane. The **Create experiment** pane appears.
4.  In the **Experiment name** field, provide a name to uniquely identify your experiment.
5.  Optional. In the **TensorBoard instance** field, select an instance from the drop-down or provide a name for your new TensorBoard instance.
6.  Click **Create** to create your experiment.

## Create an experiment without a default TensorBoard instance

### Agent Platform SDK for Python

Create an experiment. Add a description for the experiment to document its purpose. See [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) in the Agent Platform SDK reference documentation.  

### Python

    from google.cloud import aiplatform
    
    
    def create_experiment_without_default_tensorboard_sample(
        experiment_name: str,
        experiment_description: str,
        project: str,
        location: str,
    ):
        aiplatform.init(
            experiment=experiment_name,
            experiment_description=experiment_description,
            experiment_tensorboard=False,
            project=project,
            location=location,
        )

  - `experiment_name` : Provide a name for your experiment.
  - `experiment_description` : Provide a description for your experiment.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.  
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) Be sure to use a region that supports TensorBoard if creating a TensorBoard instance.

## Delete experiment

Deleting an experiment deletes that experiment and all experiment runs associated with the experiment. The Vertex AI TensorBoard experiment associated with the experiment is not deleted. To delete a TensorBoard experiment, see [Delete outdated Vertex AI TensorBoard experiment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-delete-outdated-tb-experiments) .

Also, any pipeline runs, artifacts, and executions associated with the deleted experiment are not removed. These can be found in the Google Cloud console. For artifacts and executions, a $10/GB monthly charge is handled by the Vertex ML Metadata service.

### Agent Platform SDK for Python

The following sample uses the [`delete`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun#google_cloud_aiplatform_ExperimentRun_delete) method from the [`ExperimentClass`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun) .

### Python

    from google.cloud import aiplatform
    
    
    def delete_experiment_sample(
        experiment_name: str,
        project: str,
        location: str,
        delete_backing_tensorboard_runs: bool = False,
    ):
        experiment = aiplatform.Experiment(
            experiment_name=experiment_name, project=project, location=location
        )
    
        experiment.delete(delete_backing_tensorboard_runs=delete_backing_tensorboard_runs)

  - `experiment_name` : Provide a name for your experiment.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations)
  - `delete_backing_tensorboard_runs` : If True will also delete the Vertex AI TensorBoard runs associated with the experiment runs under this experiment that we used to store time series metrics.

### Console

Use the following instructions to delete an experiment.

1.  In the Google Cloud console, go to the **Experiments** page.  
2.  Select the checkbox associated with the experiment you want to delete. The **Delete** option appears.
3.  Click **Delete** .
      - Alternatively, you can go to the more\_vert options menu that is in the same row as the experiment and select **delete** .

## View list of experiments in Google Cloud console

1.  In the Google Cloud console, in the Gemini Enterprise Agent Platform section, go to the **Experiments** page.

2.  Check to be sure you are in the correct project.

3.  A list of experiments for your project appears in the **Experiment tracking** view.  
    If you associated a Vertex AI TensorBoard instance with your experiment it shows up in the list as " *your-experiment* Backing TensorBoard Experiment".

![Agent Platform List of experiments](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/experiments-list-console.png)

## What's next

  - [Create and manage experiment runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-manage-exp-run)
  - [Delete outdated Vertex AI TensorBoard experiment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-delete-outdated-tb-experiments)

### Relevant notebook sample

  - [Model training with prebuilt data pre-processing code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-model-training)
