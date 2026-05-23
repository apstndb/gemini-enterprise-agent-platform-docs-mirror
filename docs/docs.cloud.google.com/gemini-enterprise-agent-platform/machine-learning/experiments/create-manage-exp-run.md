---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-manage-exp-run
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-manage-exp-run
title: Create and manage experiment runs
description: Use the Agent Platform SDK for Python to create and manage your experiment runs. Use the {{dynamic_data.site_values.cloud_name_short}} console to delete experiment runs
data_source: docs.cloud.google.com
---

Use the Agent Platform SDK for Python to create and manage your experiment runs. You can use the Google Cloud console to delete experiment runs.

### Agent Platform SDK for Python

The following samples use the methods [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) , [`start_run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) , and [`end_run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_end_run) from the `aiplatform` [Package functions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#functions) , and [`delete`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun#google_cloud_aiplatform_ExperimentRun_delete) from the [`ExperimentClass`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun) .

### Create and start run

### Python

    from typing import Optional, Union
    
    from google.cloud import aiplatform
    
    
    def create_experiment_run_sample(
        experiment_name: str,
        run_name: str,
        experiment_run_tensorboard: Optional[Union[str, aiplatform.Tensorboard]],
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, tensorboard=experiment_run_tensorboard)

  - `experiment_name` : Provide the name of your experiment. You can find your list of experiments in the Google Cloud console by selecting "Experiments" in the section nav.
  - `run_name` : Specify a run name to associate with your current session. See [`start_run`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) in the Agent Platform SDK reference documentation.
  - `experiment_run_tensorboard` : Optional. A backing TensorBoard resource to enable and store time series metrics logged to this experiment run using [`log_time_series_metrics`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log_time_series_metrics) .
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations)

### End run

### Python

    from google.cloud import aiplatform
    
    
    def end_experiment_run_sample(
        experiment_name: str,
        run_name: str,
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)
    
        aiplatform.end_run()

  - `experiment_name` : Provide the name of your experiment. You can find your list of experiments in the Google Cloud console by selecting "Experiments" in the section nav.
  - `run_name` : Specify a run name.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations)

### Resume run

### Python

    from google.cloud import aiplatform
    
    
    def resume_experiment_run_sample(
        experiment_name: str,
        run_name: str,
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)

  - `experiment_name` : Provide the name of your experiment. You can find your list of experiments in the Google Cloud console by selecting "Experiments" in the section nav.
  - `run_name` : Specify name of run that you want to resume.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations)

### Delete run

### Python

    from typing import Union
    
    from google.cloud import aiplatform
    
    
    def delete_experiment_run_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
        delete_backing_tensorboard_run: bool = False,
    ):
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name, experiment=experiment, project=project, location=location
        )
    
        experiment_run.delete(delete_backing_tensorboard_run=delete_backing_tensorboard_run)

  - `experiment` : The name or instance of this experiment. You can find your list of experiments in the Google Cloud console by selecting "Experiments" in the section nav.
  - `run_name` : Specify name of run that you want to delete.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations)
  - `delete_backing_tensorboard_run` : Whether to delete the backing Vertex AI TensorBoard run that stores time series metrics for this run.

### Manage status

### Python

    from typing import Union
    
    from google.cloud import aiplatform
    
    
    def update_experiment_run_state_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
        state: aiplatform.gapic.Execution.State,
    ) -> None:
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name,
            experiment=experiment,
            project=project,
            location=location,
        )
    
        experiment_run.update_state(state)

  - `run_name` : run name associated with your experiment
  - `experiment_name` : name of your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these Project IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations)
  - `state` : Possible values for `state` , which shows up as "status" in the Google Cloud console, are:
      - `aiplatform.gapic.Execution.State.CACHED`
      - `aiplatform.gapic.Execution.State.CANCELLED`
      - `aiplatform.gapic.Execution.State.COMPLETE`
      - `aiplatform.gapic.Execution.State.FAILED`
      - `aiplatform.gapic.Execution.State.NEW`
      - `aiplatform.gapic.Execution.State.RUNNING`

### Google Cloud console

Follow these steps to delete an experiment run .

1.  In the Google Cloud console, go to the **Experiments** page.  
2.  In the experiment details page, click the name of the experiment that is associated with the experiment run you want to delete. The **Experiment runs** page appears with the list of all the experiment runs for that experiment.
3.  Select the checkbox associated with the run that you want to delete. The **Delete** button appears.
4.  Click **Delete**
      - Alternatively, you can go to the more\_vert options menu that's in the same row as the experiment run and select **delete** .

## View list of experiment runs and run details

The Google Cloud console provides a visualization of the data associated with these runs.

  - [View experiment run data](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs#view-experiment-run-data)
  - [Compare experiment runs](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs#compare-experiment-runs)

## What's next

  - [Add pipeline run to an experiment or experiment run](https://docs.cloud.google.com/vertex-ai/docs/experiments/add-pipelinerun-experiment)
