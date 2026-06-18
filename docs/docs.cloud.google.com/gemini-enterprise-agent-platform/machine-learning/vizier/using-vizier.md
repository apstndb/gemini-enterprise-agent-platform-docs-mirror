---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier/using-vizier
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier/using-vizier
title: Create Agent Platform Vizier studies
description: Learn how to make API requests to Agent Platform Vizier.
data_source: docs.cloud.google.com
---

This page describes how to make API requests to Agent Platform Vizier by using Python. For information about how Agent Platform Vizier works, see [Agent Platform Vizier overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier/overview) .

> To see an example of optimizing multiple objectives as part of a more comprehensive workflow, run the "Optimizing multiple objectives" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vizier/gapic-vizier-multi-objective-optimization.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvizier%2Fgapic-vizier-multi-objective-optimization.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvizier%2Fgapic-vizier-multi-objective-optimization.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vizier/gapic-vizier-multi-objective-optimization.ipynb)

## Before you begin

1.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

2.  [Install the Agent Platform SDK for Python.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries)

## Define constants

To define constants, run the following commands, replacing `  REGION  ` and `  PROJECT_ID  ` with your region and project ID. Create your own study name or use the suggested values.

    import json
    import datetime
    from google.cloud import aiplatform
    
    REGION = "REGION"
    PROJECT_ID = "PROJECT_ID"
    
    # The following placeholder variables are automatically filled in.
    STUDY_DISPLAY_NAME = '{}_study_{}'.format(PROJECT_ID.replace('-', ''), datetime.datetime.now().strftime('%Y%m%d_%H%M%S')) #@param {type: 'string'}
    ENDPOINT = REGION + '-aiplatform.googleapis.com'
    PARENT = 'projects/{}/locations/{}'.format(PROJECT_ID, REGION)

## Construct API requests

The following command-line API requests are written in Python.

### Create a study

A *study* is a series of experiments, or *trials* , that help you optimize your hyperparameters or parameters.

In the following example, the goal is to maximize `y = x^2` with `x` in the range of \[-10. 10\]. This example has only one parameter and uses a calculated function to help demonstrate how to use Agent Platform Vizier.

    param_x = {
        'parameter_id': 'x',
        'double_value_spec': {
            'min_value': -10.0,
            'max_value': 10.0
        }
    }
    
    metric_y = {
        'metric_id': 'y',
        'goal': 'MAXIMIZE'
    }
    
    study = {
        'display_name': STUDY_DISPLAY_NAME,
        'study_spec': {
          'algorithm': 'RANDOM_SEARCH',
          'parameters': [param_x],
          'metrics': [metric_y],
        }
    }

To create the study by using your study configuration, send the following request through `VizierServiceClient` . Use the returned `STUDY_NAME` to query the study.

    vizier_client = aiplatform.gapic.VizierServiceClient(client_options=dict(api_endpoint=ENDPOINT))
    study = vizier_client.create_study(parent=PARENT, study=study)
    STUDY_NAME = study.name

### View your study

After your study is created, you can find the study in the Google Cloud console, in the Gemini Enterprise Agent Platform section, on the **Experiments** page.

### Get a study

To get a study, send the following request.

    vizier_client.get_study({'name': STUDY_NAME})

### List studies

To list studies in a specific project and region, send the following request:

    vizier_client.list_studies({'parent': PARENT})

### Get suggested trials

To get a trial suggestion from Agent Platform Vizier, create a request that contains a `  SUGGEST_COUNT  ` and a `  CLIENT_ID  ` . Pass this information to Agent Platform Vizier by sending the request.

Create the request using the following commands. Change `  SUGGEST_COUNT  ` to the number of suggestions that you want to get from each request.

    suggest_response = vizier_client.suggest_trials({
        'parent': STUDY_NAME,
        'suggestion_count': SUGGEST_COUNT,
        'client_id': CLIENT_ID
        })

`suggest_trials` starts a long-running operation to generate the trial. The response lets you know that Agent Platform Vizier is working on the trial suggestions.

To wait for the returned result, use the `result()` function .

    suggest_response.result().trials

The following format shows an example trial. This trial suggests using value `0.1` for the parameter `x` .

    name: "TRIAL_ID"
    state: ACTIVE
    parameters {
      parameter_id: "x"
      value {
        number_value: 0.1
      }
    }
    start_time {
      seconds: 1618011215
    }

Use the `  TRIAL_ID  ` from the previous response to get the trial:

    vizier_client.get_trial({
            'name': TRIAL_ID
          })

### Evaluate the results

After receiving your trial suggestions, evaluate each trial and record each result as a *measurement* .

For example, if the function you are trying to optimize is `y = x^2` , then you evaluate the function using the trial's suggested value of `x` . Using a suggested value of `0.1` , the function evaluates to `y = 0.1 * 0.1` , which results in `0.01` .

### Add a measurement

After evaluating your trial suggestion to get a measurement, add this measurement to your trial.

Use the following commands to store your measurement and send the request. In this example, replace `  RESULT  ` with the measurement. If the function you are optimizing is `y = x^2` , and the suggested value of `x` is `0.1` , the result is `0.01` .

    vizier_client.add_trial_measurement({
            'trial_name': TRIAL_ID,
            'measurement': {
                'metrics': [{'metric_id': 'y', 'value':RESULT }]
            }
        })

> **Note:** If the evaluation is a multiple-step process and can produce more than one intermediate measurement, you can call the method multiple times by using different `stepCount` and `metrics` values. For example, if you are training a machine learning model, you can report an intermediate measurement for each [epoch](https://developers.google.com/machine-learning/glossary#epoch) .

### Complete a trial

After you've added all measurements for a trial, you must complete the trial by sending a command.

When you complete the trial, you can either send a command to only complete the trial or you can send a command to add a final measurement and complete the trial.

### Without final measurement

To complete a trial without adding a final measurement, send the following request:

    vizier_client.complete_trial({
          'name': TRIAL_ID
      })

### With final measurement

To complete a trial and include a final measurement, use the following commands, replacing `  RESULT  ` with the final measurement.

    vizier_client.complete_trial({
          'name': TRIAL_ID
          'final_measurement': {
            'metrics': [{'metric_id': 'y', 'value': RESULT}]
          }
      })

### List trials

To list trials in a specific study, send the following request:

    vizier_client.list_trials({
        'parent': STUDY_NAME
    })

After you complete all the pending trials, you can call `suggestTrials` for more suggestions, and repeat the trial evaluation process.

### List optimal trials

The following example shows `list_optimal_trials` , which returns the pareto-optimal trials for a multiple-objective study or the optimal trials for a single-objective study:

    vizier_client.list_optimal_trials({
        'parent': STUDY_NAME
    })

## What's next

  - Check the REST reference for [studies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies) .
