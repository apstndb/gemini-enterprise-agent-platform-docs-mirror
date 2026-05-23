---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs
title: Compare and analyze runs
description: You can use the Agent Platform SDK for Python to view Vertex AI Experiments runs data and compare the runs. The {{dynamic_data.site_values.cloud_name_short}} console provides a visualization of the data associated with these runs.
data_source: docs.cloud.google.com
---

You can use the Agent Platform SDK for Python to view Vertex AI Experiments runs data and compare the runs.

  - [Get runs data](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs#api-analyze-runs)
  - [Compare runs](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs#api-compare-runs)

The Google Cloud console provides a visualization of the data associated with these runs.

  - [View experiment run data](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs#view-experiment-run-data)
  - [Compare experiment runs](https://docs.cloud.google.com/vertex-ai/docs/experiments/compare-analyze-runs#compare-experiment-runs)

## Get experiment runs data

These samples involve getting run metrics, run parameters, runtime series metrics, artifacts, and classification metrics for a particular experiment run.

### Summary metrics

### Python

    from typing import Dict, Union
    
    from google.cloud import aiplatform
    
    
    def get_experiment_run_metrics_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
    ) -> Dict[str, Union[float, int]]:
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name, experiment=experiment, project=project, location=location
        )
    
        return experiment_run.get_metrics()

  - `run_name` : Specify the appropriate run name for this session.
  - `experiment` : The name or instance of this experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

### Parameters

### Python

    from typing import Dict, Union
    
    from google.cloud import aiplatform
    
    
    def get_experiment_run_params_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
    ) -> Dict[str, Union[float, int, str]]:
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name, experiment=experiment, project=project, location=location
        )
    
        return experiment_run.get_params()

  - `run_name` : Specify the appropriate run name for this session.
  - `experiment` : The name or instance of this experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

### Time series metrics

### Python

    from typing import Union
    
    from google.cloud import aiplatform
    
    
    def get_experiment_run_time_series_metric_data_frame_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
    ) -> "pd.DataFrame":  # noqa: F821
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name, experiment=experiment, project=project, location=location
        )
    
        return experiment_run.get_time_series_data_frame()

  - `run_name` : Specify the appropriate run name for this session.
  - `experiment` : The name or instance of this experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

### Artifacts

### Python

    from typing import List, Union
    
    from google.cloud import aiplatform
    from google.cloud.aiplatform.metadata import artifact
    
    
    def get_experiment_run_artifacts_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
    ) -> List[artifact.Artifact]:
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name,
            experiment=experiment,
            project=project,
            location=location,
        )
    
        return experiment_run.get_artifacts()

  - `run_name` : Specify the appropriate run name for this session.
  - `experiment` : The name or instance of this experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

### Classification metrics

### Python

    from typing import Dict, List, Union
    
    from google.cloud import aiplatform
    
    
    def get_experiment_run_classification_metrics_sample(
        run_name: str,
        experiment: Union[str, aiplatform.Experiment],
        project: str,
        location: str,
    ) -> List[Dict[str, Union[str, List]]]:
        experiment_run = aiplatform.ExperimentRun(
            run_name=run_name, experiment=experiment, project=project, location=location
        )
    
        return experiment_run.get_classification_metrics()

  - `run_name` : Specify the appropriate run name for this session.
  - `experiment` : The name or instance of this experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

## Compare runs

Using the Agent Platform SDK for Python, you can retrieve the data associated with your experiment. The data for the experiment runs is returned in a DataFrame.

### Compare runs

The data for the experiment runs is returned in a DataFrame.

### Python

    from google.cloud import aiplatform
    
    
    def get_experiments_data_frame_sample(
        experiment: str,
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment, project=project, location=location)
    
        experiments_df = aiplatform.get_experiment_df()
    
        return experiments_df

  - `experiment_name` : Provide a name for the experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

## Google Cloud console

Use the Google Cloud console to view details of your experiment runs and compare the experiment runs to each other.

### View experiment run data

1.  In the Google Cloud console, go to the **Experiments** page.  
    .  
    A list of experiments associated with a project appears.
2.  Select the experiment containing the run that you want to check.  
    A list of runs, timeseries data charts, and a metrics and parameters data table appear. Notice, in this case, three runs are selected, but only two lines appear in the timeseries data charts. There is no third line because the third experiment run does not have any timeseries data to display.  
    ![Vertex AI list of runs, timeseries data, and metrics & parameters table](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/runs-timeseries-charts-metrics-params.png)  
3.  Click the name of the run to navigate to its details page.  
    ![Vertex AI experiment run navigation](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-specific-run-details.png)  
    The navigation bar and timeseries data charts appear.  
    ![Vertex AI navigation bar with timeseries data charts](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-single-run-details.png)
4.  To view metrics, parameters, artifacts, and details for your selected run, click the respective buttons in the navigation bar.
      - Metrics  
        ![Vertex AI experiment run metrics](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-single-metrics.png)
      - Parameters  
        ![Vertex AI experiment run parameters](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-single-parameters.png)
      - Artifacts  
        ![Vertex AI experiment run artifacts](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-single-artifacts.png)  
        To view artifact lineage, click the **Open artifact in Metadata Store** link. The lineage graph associated with the run appears.  
        ![Vertex AI artifact lineage graph](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/artifact-lineage-graph.png)
      - Details  
        ![Vertex AI experiment run details](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-single-details.png)

To share the data with others, use the URLs associated with the views. For example, share the list of experiment runs associated with an experiment:

![Vertex AI share list of runs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/share-list-of-runs.png)

### Compare experiment runs

You can select runs to compare both within an experiment and across experiments.

1.  In the Google Cloud console, go to the **Experiments** page.  
    .  
    A list of experiments appears.
2.  Select the experiment containing the runs that you want to compare. A list of runs appears. ![Vertex AI list of runs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/list-of-runs.png)
3.  Select the experiment runs that you want to compare. Click **Compare** .  
    ![Vertex AI select runs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/select-runs.png)  
    By default, charts appear comparing timeseries metrics of the selected experiment runs. ![Vertex AI run charts](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/run-charts.png)
4.  To add additional runs from any experiment in your project, click **Add run** . ![Vertex AI add runs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/add-runs.png)

To share the data with others, use the URLs associated with the views. For example, share the comparison view of timeseries metrics data:

![Vertex AI share data](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-share-data.png)

See [Create and manage experiment runs](https://docs.cloud.google.com/vertex-ai/docs/experiments/create-manage-exp-run) for how to update the status of a run.

## What's next

  - [Track executions and artifacts](https://docs.cloud.google.com/vertex-ai/docs/experiments/track-executions-artifacts)
