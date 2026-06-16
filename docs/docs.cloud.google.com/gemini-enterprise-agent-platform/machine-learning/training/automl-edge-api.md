---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api
title: Train an AutoML Edge model using the Agent Platform API
description: Learn how to create an AutoML Edge training pipeline and get model information.
data_source: docs.cloud.google.com
---

You create an AutoML model directly in the [Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console) , or by creating a training pipeline programmatically, using the API or one of the [Agent Platform client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) .

This model is created using a prepared dataset provided by you using the [console](https://docs.cloud.google.com/vertex-ai/docs/training/automl-edge-console) or the Agent Platform API. The Agent Platform API uses the items from the dataset to train the model, test it, and evaluate model performance. Review the evaluations results, adjust the training dataset as needed, and create a new training pipeline using the improved dataset.

Model training can take several hours to complete. The Agent Platform API lets you get the status of the training job.

## Create an AutoML Edge training pipeline

When you have a dataset with a representative set of training items, you are ready to create an AutoML Edge training pipeline.

Select the tab below for your objective:

### Classification

At training time you can choose the type of AutoML Edge model you want, depending on your specific use case:

  - low latency ( `MOBILE_TF_LOW_LATENCY_1` )
  - general purpose usage ( `MOBILE_TF_VERSATILE_1` )
  - higher prediction quality ( `MOBILE_TF_HIGH_ACCURACY_1` )

Select the tab below for your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where dataset is located and Model is created. For example, `us-central1` .
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TRAININGPIPELINE\_DISPLAYNAME : Required. A display name for the trainingPipeline.
  - DATASET\_ID : The ID number for the dataset to use for training.
  - fractionSplit : Optional. One of several possible ML use [split options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#inputdataconfig) for your data. For `fractionSplit` , values must sum to 1. For example:
      - `{"trainingFraction": "0.7","validationFraction": "0.15","testFraction": "0.15"}`
  - MODEL\_DISPLAYNAME <sup>\*</sup> : A display name for the model uploaded (created) by the TrainingPipeline.
  - MODEL\_DESCRIPTION <sup>\*</sup> : A description for the model.
  - modelToUpload.labels <sup>\*</sup> : Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - EDGE\_MODELTYPE <sup>†</sup> : The type of Edge model to train. The options are:
      - `MOBILE_TF_LOW_LATENCY_1`
      - `MOBILE_TF_VERSATILE_1`
      - `MOBILE_TF_HIGH_ACCURACY_1`
  - NODE\_HOUR\_BUDGET <sup>†</sup> : The actual training cost will be equal or less than this value. For Edge models the budget must be: 1,000 - 100,000 milli node hours (inclusive).
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

|    |                                                                                                    |
| -- | -------------------------------------------------------------------------------------------------- |
| \* | Schema file's description you specify in `trainingTaskDefinition` describes the use of this field. |
| †  | Schema file you specify in `trainingTaskDefinition` declares and describes this field.             |

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": "DECIMAL",
          "validationFraction": "DECIMAL",
          "testFraction": "DECIMAL"
        }
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "description": "MODEL_DESCRIPTION",
        "labels": {
          "KEY": "VALUE"
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_classification_1.0.0.yaml",
      "trainingTaskInputs": {
        "multiLabel": "true",
        "modelType": ["EDGE_MODELTYPE"],
        "budgetMilliNodeHours": NODE_HOUR_BUDGET
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": 0.7,
          "validationFraction": 0.15,
          "testFraction": 0.15
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_classification_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": "EDGE_MODELTYPE",
        "budgetMilliNodeHours": "NODE_HOUR_BUDGET"
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "labels": {
          "KEY1": "VALUE1",
          "KEY2": "VALUE2"
        }
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-07-14T17:16:55.098953Z",
      "updateTime": "2020-07-14T17:16:55.098953Z"
    }

You can [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api#get-pipeline) of the trainingPipeline job using the TRAININGPIPELINE\_ID .

### Classification

At training time you can choose the type of AutoML Edge model you want, depending on your specific use case:

  - low latency ( `MOBILE_TF_LOW_LATENCY_1` )
  - general purpose usage ( `MOBILE_TF_VERSATILE_1` )
  - higher prediction quality ( `MOBILE_TF_HIGH_ACCURACY_1` )

Select the tab below for your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where dataset is located and Model is created. For example, `us-central1` .
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TRAININGPIPELINE\_DISPLAYNAME : Required. A display name for the trainingPipeline.
  - DATASET\_ID : The ID number for the dataset to use for training.
  - fractionSplit : Optional. One of several possible ML use [split options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#inputdataconfig) for your data. For `fractionSplit` , values must sum to 1. For example:
      - `{"trainingFraction": "0.7","validationFraction": "0.15","testFraction": "0.15"}`
  - MODEL\_DISPLAYNAME <sup>\*</sup> : A display name for the model uploaded (created) by the TrainingPipeline.
  - MODEL\_DESCRIPTION <sup>\*</sup> : A description for the model.
  - modelToUpload.labels <sup>\*</sup> : Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - EDGE\_MODELTYPE <sup>†</sup> : The type of Edge model to train. The options are:
      - `MOBILE_TF_LOW_LATENCY_1`
      - `MOBILE_TF_VERSATILE_1`
      - `MOBILE_TF_HIGH_ACCURACY_1`
  - NODE\_HOUR\_BUDGET <sup>†</sup> : The actual training cost will be equal or less than this value. For Edge models the budget must be: 1,000 - 100,000 milli node hours (inclusive).
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

|    |                                                                                                    |
| -- | -------------------------------------------------------------------------------------------------- |
| \* | Schema file's description you specify in `trainingTaskDefinition` describes the use of this field. |
| †  | Schema file you specify in `trainingTaskDefinition` declares and describes this field.             |

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": "DECIMAL",
          "validationFraction": "DECIMAL",
          "testFraction": "DECIMAL"
        }
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "description": "MODEL_DESCRIPTION",
        "labels": {
          "KEY": "VALUE"
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_classification_1.0.0.yaml",
      "trainingTaskInputs": {
        "multiLabel": "true",
        "modelType": ["EDGE_MODELTYPE"],
        "budgetMilliNodeHours": NODE_HOUR_BUDGET
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": 0.7,
          "validationFraction": 0.15,
          "testFraction": 0.15
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_classification_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": "EDGE_MODELTYPE",
        "budgetMilliNodeHours": "NODE_HOUR_BUDGET"
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "labels": {
          "KEY1": "VALUE1",
          "KEY2": "VALUE2"
        }
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-07-14T17:16:55.098953Z",
      "updateTime": "2020-07-14T17:16:55.098953Z"
    }

You can [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api#get-pipeline) of the trainingPipeline job using the TRAININGPIPELINE\_ID .

### Object detection

At training time you can choose the type of AutoML Edge model you want, depending on your specific use case:

  - low latency ( `MOBILE_TF_LOW_LATENCY_1` )
  - general purpose usage ( `MOBILE_TF_VERSATILE_1` )
  - higher prediction quality ( `MOBILE_TF_HIGH_ACCURACY_1` )

Select the tab below for your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where dataset is located and Model is created. For example, `us-central1` .
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TRAININGPIPELINE\_DISPLAYNAME : Required. A display name for the trainingPipeline.
  - DATASET\_ID : The ID number for the dataset to use for training.
  - `fractionSplit` : Optional. One of several possible ML use [split options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#inputdataconfig) for your data. For `fractionSplit` , values must sum to 1. For example:
      - `{"trainingFraction": "0.7","validationFraction": "0.15","testFraction": "0.15"}`
  - MODEL\_DISPLAYNAME <sup>\*</sup> : A display name for the model uploaded (created) by the TrainingPipeline.
  - MODEL\_DESCRIPTION <sup>\*</sup> : A description for the model.
  - modelToUpload.labels <sup>\*</sup> : Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - EDGE\_MODELTYPE <sup>†</sup> : The type of Edge model to train. The options are:
      - `MOBILE_TF_LOW_LATENCY_1`
      - `MOBILE_TF_VERSATILE_1`
      - `MOBILE_TF_HIGH_ACCURACY_1`
  - NODE\_HOUR\_BUDGET <sup>†</sup> : The actual training cost will be equal or less than this value. For Cloud models the budget must be: 20,000 - 900,000 milli node hours (inclusive). The default value is 216,000 which represents one day in wall time, assuming 9 nodes are used.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

|    |                                                                                                    |
| -- | -------------------------------------------------------------------------------------------------- |
| \* | Schema file's description you specify in `trainingTaskDefinition` describes the use of this field. |
| †  | Schema file you specify in `trainingTaskDefinition` declares and describes this field.             |

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": "DECIMAL",
          "validationFraction": "DECIMAL",
          "testFraction": "DECIMAL"
        }
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "description": "MODEL_DESCRIPTION",
        "labels": {
          "KEY": "VALUE"
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_object_detection_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": ["EDGE_MODELTYPE"],
        "budgetMilliNodeHours": NODE_HOUR_BUDGET
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": 0.7,
          "validationFraction": 0.15,
          "testFraction": 0.15
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_object_detection_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": "EDGE_MODELTYPE",
        "budgetMilliNodeHours": "NODE_HOUR_BUDGET"
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "labels": {
          "KEY1": "VALUE1",
          "KEY2": "VALUE2"
        }
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-07-14T17:16:55.098953Z",
      "updateTime": "2020-07-14T17:16:55.098953Z"
    }

You can [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api#get-pipeline) of the trainingPipeline job using the TRAININGPIPELINE\_ID .

## Get trainingPipeline status

Use the following code to programmatically get the status of trainingPipeline creation.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where TrainingPipeline is located.
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TRAININGPIPELINE\_ID : The ID of the specific TrainingPipeline.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID" | Select-Object -Expand Content

The `"state"` field shows the current status of the operation. A completed trainingPipeline shows

You should see output similar to the following for a completed **create trainingPipeline operation** :

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "PIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": 0.7,
          "validationFraction": 0.15,
          "testFraction": 0.15
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_classification_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": "MOBILE_TF_VERSATILE_1",
        "budgetMilliNodeHours": "1000"
      },
      "modelToUpload": {
        "name": "projects/PROJECT_NUMBER/locations/LOCATION/models/4030440191519883264",
        "displayName": "image_classification_edge_model1",
        "labels": {
          "env": "prod",
          "tier": "backend"
        }
      },
      "state": "PIPELINE_STATE_SUCCEEDED",
      "createTime": "2020-07-14T17:16:55.098953Z",
      "startTime": "2020-07-14T17:16:55.360691Z",
      "endTime": "2020-07-14T18:46:08.169170Z",
      "updateTime": "2020-07-14T18:46:08.169170Z"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.DeployedModelRef;
    import com.google.cloud.aiplatform.v1.EnvVar;
    import com.google.cloud.aiplatform.v1.FilterSplit;
    import com.google.cloud.aiplatform.v1.FractionSplit;
    import com.google.cloud.aiplatform.v1.InputDataConfig;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.PipelineServiceClient;
    import com.google.cloud.aiplatform.v1.PipelineServiceSettings;
    import com.google.cloud.aiplatform.v1.Port;
    import com.google.cloud.aiplatform.v1.PredefinedSplit;
    import com.google.cloud.aiplatform.v1.PredictSchemata;
    import com.google.cloud.aiplatform.v1.TimestampSplit;
    import com.google.cloud.aiplatform.v1.TrainingPipeline;
    import com.google.cloud.aiplatform.v1.TrainingPipelineName;
    import com.google.rpc.Status;
    import java.io.IOException;
    
    public class GetTrainingPipelineSample {
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String trainingPipelineId = "YOUR_TRAINING_PIPELINE_ID";
        getTrainingPipeline(project, trainingPipelineId);
      }
    
      static void getTrainingPipeline(String project, String trainingPipelineId) throws IOException {
        PipelineServiceSettings pipelineServiceSettings =
            PipelineServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PipelineServiceClient pipelineServiceClient =
            PipelineServiceClient.create(pipelineServiceSettings)) {
          String location = "us-central1";
          TrainingPipelineName trainingPipelineName =
              TrainingPipelineName.of(project, location, trainingPipelineId);
    
          TrainingPipeline trainingPipelineResponse =
              pipelineServiceClient.getTrainingPipeline(trainingPipelineName);
    
          System.out.println("Get Training Pipeline Response");
          System.out.format("\tName: %s\n", trainingPipelineResponse.getName());
          System.out.format("\tDisplay Name: %s\n", trainingPipelineResponse.getDisplayName());
          System.out.format(
              "\tTraining Task Definition: %s\n", trainingPipelineResponse.getTrainingTaskDefinition());
          System.out.format(
              "\tTraining Task Inputs: %s\n", trainingPipelineResponse.getTrainingTaskInputs());
          System.out.format(
              "\tTraining Task Metadata: %s\n", trainingPipelineResponse.getTrainingTaskMetadata());
          System.out.format("\tState: %s\n", trainingPipelineResponse.getState());
          System.out.format("\tCreate Time: %s\n", trainingPipelineResponse.getCreateTime());
          System.out.format("\tStart Time: %s\n", trainingPipelineResponse.getStartTime());
          System.out.format("\tEnd Time: %s\n", trainingPipelineResponse.getEndTime());
          System.out.format("\tUpdate Time: %s\n", trainingPipelineResponse.getUpdateTime());
          System.out.format("\tLabels: %s\n", trainingPipelineResponse.getLabelsMap());
          InputDataConfig inputDataConfig = trainingPipelineResponse.getInputDataConfig();
    
          System.out.println("\tInput Data Config");
          System.out.format("\t\tDataset Id: %s\n", inputDataConfig.getDatasetId());
          System.out.format("\t\tAnnotations Filter: %s\n", inputDataConfig.getAnnotationsFilter());
          FractionSplit fractionSplit = inputDataConfig.getFractionSplit();
    
          System.out.println("\t\tFraction Split");
          System.out.format("\t\t\tTraining Fraction: %s\n", fractionSplit.getTrainingFraction());
          System.out.format("\t\t\tValidation Fraction: %s\n", fractionSplit.getValidationFraction());
          System.out.format("\t\t\tTest Fraction: %s\n", fractionSplit.getTestFraction());
          FilterSplit filterSplit = inputDataConfig.getFilterSplit();
    
          System.out.println("\t\tFilter Split");
          System.out.format("\t\t\tTraining Filter: %s\n", filterSplit.getTrainingFilter());
          System.out.format("\t\t\tValidation Filter: %s\n", filterSplit.getValidationFilter());
          System.out.format("\t\t\tTest Filter: %s\n", filterSplit.getTestFilter());
          PredefinedSplit predefinedSplit = inputDataConfig.getPredefinedSplit();
    
          System.out.println("\t\tPredefined Split");
          System.out.format("\t\t\tKey: %s\n", predefinedSplit.getKey());
          TimestampSplit timestampSplit = inputDataConfig.getTimestampSplit();
    
          System.out.println("\t\tTimestamp Split");
          System.out.format("\t\t\tTraining Fraction: %s\n", timestampSplit.getTrainingFraction());
          System.out.format("\t\t\tTest Fraction: %s\n", timestampSplit.getTestFraction());
          System.out.format("\t\t\tValidation Fraction: %s\n", timestampSplit.getValidationFraction());
          System.out.format("\t\t\tKey: %s\n", timestampSplit.getKey());
          Model modelResponse = trainingPipelineResponse.getModelToUpload();
    
          System.out.println("\t\tModel to upload");
          System.out.format("\t\tName: %s\n", modelResponse.getName());
          System.out.format("\t\tDisplay Name: %s\n", modelResponse.getDisplayName());
          System.out.format("\t\tDescription: %s\n", modelResponse.getDescription());
          System.out.format("\t\tMetadata Schema Uri: %s\n", modelResponse.getMetadataSchemaUri());
          System.out.format("\t\tMeta Data: %s\n", modelResponse.getMetadata());
          System.out.format("\t\tTraining Pipeline: %s\n", modelResponse.getTrainingPipeline());
          System.out.format("\t\tArtifact Uri: %s\n", modelResponse.getArtifactUri());
          System.out.format(
              "\t\tSupported Deployment Resources Types: %s\n",
              modelResponse.getSupportedDeploymentResourcesTypesList().toString());
          System.out.format(
              "\t\tSupported Input Storage Formats: %s\n",
              modelResponse.getSupportedInputStorageFormatsList().toString());
          System.out.format(
              "\t\tSupported Output Storage Formats: %s\n",
              modelResponse.getSupportedOutputStorageFormatsList().toString());
          System.out.format("\t\tCreate Time: %s\n", modelResponse.getCreateTime());
          System.out.format("\t\tUpdate Time: %s\n", modelResponse.getUpdateTime());
          System.out.format("\t\tLabels: %s\n", modelResponse.getLabelsMap());
          PredictSchemata predictSchemata = modelResponse.getPredictSchemata();
    
          System.out.println("\tPredict Schemata");
          System.out.format("\t\tInstance Schema Uri: %s\n", predictSchemata.getInstanceSchemaUri());
          System.out.format(
              "\t\tParameters Schema Uri: %s\n", predictSchemata.getParametersSchemaUri());
          System.out.format(
              "\t\tPrediction Schema Uri: %s\n", predictSchemata.getPredictionSchemaUri());
    
          for (Model.ExportFormat supportedExportFormat :
              modelResponse.getSupportedExportFormatsList()) {
            System.out.println("\tSupported Export Format");
            System.out.format("\t\tId: %s\n", supportedExportFormat.getId());
          }
          ModelContainerSpec containerSpec = modelResponse.getContainerSpec();
    
          System.out.println("\tContainer Spec");
          System.out.format("\t\tImage Uri: %s\n", containerSpec.getImageUri());
          System.out.format("\t\tCommand: %s\n", containerSpec.getCommandList());
          System.out.format("\t\tArgs: %s\n", containerSpec.getArgsList());
          System.out.format("\t\tPredict Route: %s\n", containerSpec.getPredictRoute());
          System.out.format("\t\tHealth Route: %s\n", containerSpec.getHealthRoute());
    
          for (EnvVar envVar : containerSpec.getEnvList()) {
            System.out.println("\t\tEnv");
            System.out.format("\t\t\tName: %s\n", envVar.getName());
            System.out.format("\t\t\tValue: %s\n", envVar.getValue());
          }
    
          for (Port port : containerSpec.getPortsList()) {
            System.out.println("\t\tPort");
            System.out.format("\t\t\tContainer Port: %s\n", port.getContainerPort());
          }
    
          for (DeployedModelRef deployedModelRef : modelResponse.getDeployedModelsList()) {
            System.out.println("\tDeployed Model");
            System.out.format("\t\tEndpoint: %s\n", deployedModelRef.getEndpoint());
            System.out.format("\t\tDeployed Model Id: %s\n", deployedModelRef.getDeployedModelId());
          }
    
          Status status = trainingPipelineResponse.getError();
          System.out.println("\tError");
          System.out.format("\t\tCode: %s\n", status.getCode());
          System.out.format("\t\tMessage: %s\n", status.getMessage());
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def get_training_pipeline_sample(
        project: str,
        training_pipeline_id: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.PipelineServiceClient(client_options=client_options)
        name = client.training_pipeline_path(
            project=project, location=location, training_pipeline=training_pipeline_id
        )
        response = client.get_training_pipeline(name=name)
        print("response:", response)

## Get model information

After the trainingPipeline creation completes you can use the model's display name to get more detailed model information.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where Model is located. For example, `us-central1`
  - PROJECT : .
  - MODEL\_DISPLAYNAME : The display name of your model that you specified when creating a trainingPipeline job.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models?filter=display_name=MODEL_DISPLAYNAME

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models?filter=display_name=MODEL_DISPLAYNAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models?filter=display_name=MODEL_DISPLAYNAME" | Select-Object -Expand Content

You should see output similar to the following for a trained AutoML Edge model. The following sample output is for an image AutoML Edge model:

#### Response

    {
      "models": [
        {
          "name": "projects/PROJECT/locations/LOCATION/models/MODEL_ID",
          "displayName": "MODEL_DISPLAYNAME",
          "predictSchemata": {
            "instanceSchemaUri": "https://storage.googleapis.com/google-cloud-aiplatform/schema/predict/instance/image_classification_1.0.0.yaml",
            "parametersSchemaUri": "https://storage.googleapis.com/google-cloud-aiplatform/schema/predict/params/image_classification_1.0.0.yaml",
            "predictionSchemaUri": "https://storage.googleapis.com/google-cloud-aiplatform/schema/predict/prediction/classification_1.0.0.yaml"
          },
          "metadataSchemaUri": "https://storage.googleapis.com/google-cloud-aiplatform/schema/model/metadata/automl_image_classification_1.0.0.yaml",
          "metadata": {
            "modelType": "MOBILE_TF_VERSATILE_1",
            "trainingDataItemsCount": "2174",
            "validationDataItemsCount": "467",
            "trainingAnnotationsCount": "2174",
            "validationAnnotationsCount": "467",
            "eligibleAsBaseModel": true
          },
          "trainingPipeline": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID",
          "supportedDeploymentResourcesTypes": [
            "AUTOMATIC_RESOURCES"
          ],
          "supportedInputStorageFormats": [
            "jsonl"
          ],
          "supportedOutputStorageFormats": [
            "jsonl"
          ],
          "createTime": "2020-07-14T17:16:55.098953Z",
          "updateTime": "2020-07-14T18:46:08.169225Z",
          "etag": "AMEw9yNjhttIyiGUgec8vGNeidfX8mGcFT1owDOq1iDT6mmQ7HLHwoomie30pLCTtJ4=",
          "labels": {
            "env": "prod",
            "tier": "backend"
          },
          "supportedExportFormats": [
            {
              "id": "tflite"
            },
            {
              "id": "edgetpu-tflite"
            },
            {
              "id": "tf-saved-model"
            },
            {
              "id": "core-ml"
            },
            {
              "id": "tf-js"
            }
          ]
        }
      ]
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.DeployedModelRef;
    import com.google.cloud.aiplatform.v1.EnvVar;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.Model.ExportFormat;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.ModelName;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import com.google.cloud.aiplatform.v1.Port;
    import com.google.cloud.aiplatform.v1.PredictSchemata;
    import java.io.IOException;
    
    public class GetModelSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        getModelSample(project, modelId);
      }
    
      static void getModelSample(String project, String modelId) throws IOException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          ModelName modelName = ModelName.of(project, location, modelId);
    
          Model modelResponse = modelServiceClient.getModel(modelName);
          System.out.println("Get Model response");
          System.out.format("\tName: %s\n", modelResponse.getName());
          System.out.format("\tDisplay Name: %s\n", modelResponse.getDisplayName());
          System.out.format("\tDescription: %s\n", modelResponse.getDescription());
    
          System.out.format("\tMetadata Schema Uri: %s\n", modelResponse.getMetadataSchemaUri());
          System.out.format("\tMetadata: %s\n", modelResponse.getMetadata());
          System.out.format("\tTraining Pipeline: %s\n", modelResponse.getTrainingPipeline());
          System.out.format("\tArtifact Uri: %s\n", modelResponse.getArtifactUri());
    
          System.out.format(
              "\tSupported Deployment Resources Types: %s\n",
              modelResponse.getSupportedDeploymentResourcesTypesList());
          System.out.format(
              "\tSupported Input Storage Formats: %s\n",
              modelResponse.getSupportedInputStorageFormatsList());
          System.out.format(
              "\tSupported Output Storage Formats: %s\n",
              modelResponse.getSupportedOutputStorageFormatsList());
    
          System.out.format("\tCreate Time: %s\n", modelResponse.getCreateTime());
          System.out.format("\tUpdate Time: %s\n", modelResponse.getUpdateTime());
          System.out.format("\tLabels: %s\n", modelResponse.getLabelsMap());
    
          PredictSchemata predictSchemata = modelResponse.getPredictSchemata();
          System.out.println("\tPredict Schemata");
          System.out.format("\t\tInstance Schema Uri: %s\n", predictSchemata.getInstanceSchemaUri());
          System.out.format(
              "\t\tParameters Schema Uri: %s\n", predictSchemata.getParametersSchemaUri());
          System.out.format(
              "\t\tPrediction Schema Uri: %s\n", predictSchemata.getPredictionSchemaUri());
    
          for (ExportFormat exportFormat : modelResponse.getSupportedExportFormatsList()) {
            System.out.println("\tSupported Export Format");
            System.out.format("\t\tId: %s\n", exportFormat.getId());
          }
    
          ModelContainerSpec containerSpec = modelResponse.getContainerSpec();
          System.out.println("\tContainer Spec");
          System.out.format("\t\tImage Uri: %s\n", containerSpec.getImageUri());
          System.out.format("\t\tCommand: %s\n", containerSpec.getCommandList());
          System.out.format("\t\tArgs: %s\n", containerSpec.getArgsList());
          System.out.format("\t\tPredict Route: %s\n", containerSpec.getPredictRoute());
          System.out.format("\t\tHealth Route: %s\n", containerSpec.getHealthRoute());
    
          for (EnvVar envVar : containerSpec.getEnvList()) {
            System.out.println("\t\tEnv");
            System.out.format("\t\t\tName: %s\n", envVar.getName());
            System.out.format("\t\t\tValue: %s\n", envVar.getValue());
          }
    
          for (Port port : containerSpec.getPortsList()) {
            System.out.println("\t\tPort");
            System.out.format("\t\t\tContainer Port: %s\n", port.getContainerPort());
          }
    
          for (DeployedModelRef deployedModelRef : modelResponse.getDeployedModelsList()) {
            System.out.println("\tDeployed Model");
            System.out.format("\t\tEndpoint: %s\n", deployedModelRef.getEndpoint());
            System.out.format("\t\tDeployed Model Id: %s\n", deployedModelRef.getDeployedModelId());
          }
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const modelId = 'YOUR_MODEL_ID';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Model Service Client library
    const {ModelServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const modelServiceClient = new ModelServiceClient(clientOptions);
    
    async function getModel() {
      // Configure the parent resource
      const name = `projects/${project}/locations/${location}/models/${modelId}`;
      const request = {
        name,
      };
      // Get and print out a list of all the endpoints for this resource
      const [response] = await modelServiceClient.getModel(request);
    
      console.log('Get model response');
      console.log(`\tName : ${response.name}`);
      console.log(`\tDisplayName : ${response.displayName}`);
      console.log(`\tDescription : ${response.description}`);
      console.log(`\tMetadata schema uri : ${response.metadataSchemaUri}`);
      console.log(`\tMetadata : ${JSON.stringify(response.metadata)}`);
      console.log(`\tTraining pipeline : ${response.trainingPipeline}`);
      console.log(`\tArtifact uri : ${response.artifactUri}`);
      console.log(
        `\tSupported deployment resource types : \
          ${response.supportedDeploymentResourceTypes}`
      );
      console.log(
        `\tSupported input storage formats : \
          ${response.supportedInputStorageFormats}`
      );
      console.log(
        `\tSupported output storage formats : \
          ${response.supportedOutputStoragFormats}`
      );
      console.log(`\tCreate time : ${JSON.stringify(response.createTime)}`);
      console.log(`\tUpdate time : ${JSON.stringify(response.updateTime)}`);
      console.log(`\tLabels : ${JSON.stringify(response.labels)}`);
    
      const predictSchemata = response.predictSchemata;
      console.log('\tPredict schemata');
      console.log(`\tInstance schema uri : ${predictSchemata.instanceSchemaUri}`);
      console.log(
        `\tParameters schema uri : ${predictSchemata.prametersSchemaUri}`
      );
      console.log(
        `\tPrediction schema uri : ${predictSchemata.predictionSchemaUri}`
      );
    
      const [supportedExportFormats] = response.supportedExportFormats;
      console.log('\tSupported export formats');
      console.log(`\t${supportedExportFormats}`);
    
      const containerSpec = response.containerSpec;
      console.log('\tContainer Spec');
      if (!containerSpec) {
        console.log(`\t\t${JSON.stringify(containerSpec)}`);
        console.log('\t\tImage uri : {}');
        console.log('\t\tCommand : {}');
        console.log('\t\tArgs : {}');
        console.log('\t\tPredict route : {}');
        console.log('\t\tHealth route : {}');
        console.log('\t\tEnv');
        console.log('\t\t\t{}');
        console.log('\t\tPort');
        console.log('\t\t{}');
      } else {
        console.log(`\t\t${JSON.stringify(containerSpec)}`);
        console.log(`\t\tImage uri : ${containerSpec.imageUri}`);
        console.log(`\t\tCommand : ${containerSpec.command}`);
        console.log(`\t\tArgs : ${containerSpec.args}`);
        console.log(`\t\tPredict route : ${containerSpec.predictRoute}`);
        console.log(`\t\tHealth route : ${containerSpec.healthRoute}`);
        const env = containerSpec.env;
        console.log('\t\tEnv');
        console.log(`\t\t\t${JSON.stringify(env)}`);
        const ports = containerSpec.ports;
        console.log('\t\tPort');
        console.log(`\t\t\t${JSON.stringify(ports)}`);
      }
    
      const [deployedModels] = response.deployedModels;
      console.log('\tDeployed models');
      console.log('\t\t', deployedModels);
    }
    getModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def get_model_sample(project: str, location: str, model_name: str):
    
        aiplatform.init(project=project, location=location)
    
        model = aiplatform.Model(model_name=model_name)
    
        print(model.display_name)
        print(model.resource_name)
        return model

## What's next

  - [Evaluating AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/evaluating-automl-models) .
  - [Exporting AutoML Edge models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-edge-model) .
