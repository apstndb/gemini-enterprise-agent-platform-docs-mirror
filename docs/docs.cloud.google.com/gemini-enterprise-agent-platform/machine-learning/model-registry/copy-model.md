---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/copy-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/copy-model
title: Copy a model in Gemini Enterprise Agent Platform Model Registry
description: Learn how Gemini Enterprise Agent Platform Model Registry lets you copy a well-performing model to another project or location to avoid re-training and ensure consistency.
data_source: docs.cloud.google.com
---

Training your AutoML, large models, and custom models in Agent Platform to the level you want requires time and experimentation. If you have a well-performing model that you'd like to use in another project or location, training a new model isn't the best option. Model training is non-deterministic in nature therefore it's unlikely you'd end up with an identical model from identical data. Additionally, training a model in each region or project isn't a foolproof way to maintain cross-region model behavior consistency. With Gemini Enterprise Agent Platform Model Registry copy model, you can copy a model from the Gemini Enterprise Agent Platform Model Registry into a separate location in the same project or to a different project.

> **Note:** Copy model doesn't support copying AutoML Natural Language and BigQuery ML models.

When performing a model copy, if you don't specify the model version you want to copy over, the default model version is copied. To learn more about model default or the model alias, see [How to use model aliases](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-alias) .

## Limitations

When you copy a model, not all model information is copied over. The copied model won't retain the following:

  - Version aliases.
  - The custom model ID. You can specify a new ID once the model is copied.
  - Any existing model evaluation.
  - Encryption specs. You're required to specify the encryption key when copying the model for your target region.
  - Deployments and batch inferences.

For cross-project copy, you can't copy custom models that have a third-party container image.

## Copy models between projects

### Prerequisites

To copy a model across projects, the source model owner needs to first grant the model export permission to the destination project:

### Default

1.  Select your source project from the Google Cloud console.
2.  Navigate to the IAM & Admin page.
3.  On the IAM permissions page, click **Grant access** and a pop up window appears to let you add a new principal to the source project.
4.  Get the per-product, per-project service account (P4SA) `service-{project_number}@gcp-sa-aiplatform.iam.gserviceaccount.com` of the destination project.
5.  Add the P4SA of the destination project as a new principal to the source project and assign the Gemini Enterprise Agent Platform Service Agent role to it.
6.  After clicking **Save** , the destination project P4SA will have permissions to export models from the source project.

> **Note:** Granting the model export permission to the destination project P4SA means that anyone with model upload access on the other project can trigger the model export process.

### Using custom service account

1.  Create a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#setup) or use your existing one. This service account must belong to the destination project where the model is copied to and you need to have the `iam.serviceAccounts.actAs` permission on this service account.
2.  Select your source project from the Google Cloud console.
3.  Navigate to the IAM & Admin page.
4.  On the IAM permissions page, click **Grant access** and a pop up window appears to let you add a new principal to the source project.
5.  Add the custom service account as a new principal to the source project and assign the `Gemini Enterprise Agent Platform User` role to it or any custom role with the `aiplatform.models.export` permission.
6.  After clicking **Save** , the custom service account will have permissions to export models from the source project.
7.  Get the per-product, per-project service account (P4SA) `service-{project_number}@gcp-sa-aiplatform.iam.gserviceaccount.com` of the destination project.
8.  Grant the P4SA of the destination project with the `Service Account Token Creator` role on the custom service account.

Copy models between projects:

### REST

> **Note:** Add the `customServiceAccount` field in the request JSON body if you are using a custom service account.

Before using any of the request data, make the following replacements:

  - `  DESTINATION_LOCATION  ` : The region where you want to copy the model to. For example, `us-central1`
  - `  DESTINATION_PROJECT_ID  ` : The project ID or project number where you want to copy the model to.
  - `  SOURCE_PROJECT_ID  ` : Your project ID or project number.
  - `  SOURCE_LOCATION  ` : The Agent Platform region from which you are copying a model.
  - `  SOURCE_MODEL_ID  ` : The source of the model ID to copy.
  - `  VERSION_ID  ` : (Optional) ID of the model version to copy (if not provided the default version is copied)

HTTP method and URL:

    POST https://DESTINATION_LOCATION-aiplatform.googleapis.com/v1/projects/DESTINATION_PROJECT_ID/locations/DESTINATION_LOCATION/models:copy

Request JSON body:

``` 
   {
    "sourceModel": "projects/SOURCE_PROJECT_ID/locations/SOURCE_LOCATION/models/SOURCE_MODEL_ID"
    }
```

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://DESTINATION_LOCATION-aiplatform.googleapis.com/v1/projects/DESTINATION_PROJECT_ID/locations/DESTINATION_LOCATION/models:copy"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://DESTINATION_LOCATION-aiplatform.googleapis.com/v1/projects/DESTINATION_PROJECT_ID/locations/DESTINATION_LOCATION/models:copy" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

``` 
  {
    "name": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID/operations/OPERATION_ID",
    "metadata": {
      "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CopyModelOperationMetadata",
      "genericMetadata": {
        "createTime": "2022-07-01T00:10:55.621355Z",
        "updateTime": "2022-07-01T00:10:55.621355Z"
      }
    }
  }
```

### Console

  

Use the following instructions to copy a models to a different project.

1.  In the Google Cloud console, go to the **Gemini Enterprise Agent Platform Model Registry** page.
2.  From the Model Registry, select the **More actions** menu more\_vert for the model you want to copy.  
3.  Click **Copy model** .
4.  Choose either **To another project** or **To another region** .

**Copy model to a different project**

1.  Choose **To another project** .
2.  Choose the model version you want to copy.
3.  Choose the destination project you want to copy to.
4.  Choose the destination region, for example, `us-central1` .
5.  **Advanced options** : Optional to choose the encryption method, using a Google-owned and Google-managed encryption key or a Cloud KMS key.

## Copy models between locations

### REST

Before using any of the request data, make the following replacements:

  - `  DESTINATION_LOCATION  ` : The region where you are using Vertex AI. For example, `us-central1`
  - `  SOURCE_LOCATION  ` : The Vertex AI region from which you will copy the model.
  - `  PROJECT_ID  ` : Your project ID or project number.
  - `  MODEL_ID  ` :ID of the model to copy.
  - `  VERSION_ID  ` : (Optional) ID of the model version to copy (if not provided the default version is copied)

HTTP method and URL:

    POST https://DESTINATION_LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/models:copy

Request JSON body:

    {"sourceModel": "projects/PROJECT_ID/locations/SOURCE_LOCATION/models/MODEL_ID[@VERSION_ID]"
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://DESTINATION_LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/models:copy"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://DESTINATION_LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/models:copy" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

``` 
  {
    "name": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID/operations/OPERATION_ID",
    "metadata": {
      "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CopyModelOperationMetadata",
      "genericMetadata": {
        "createTime": "2022-07-01T00:10:55.621355Z",
        "updateTime": "2022-07-01T00:10:55.621355Z"
      }
    }
  }
```

### Console

  
With a cross-region copy, you can copy a model over as a new model within the target region, or as a new version of an existing model in that region.

Use the following instructions to copy models.

1.  In the Google Cloud console, go to the **Gemini Enterprise Agent Platform Model Registry** page.
2.  From the Model Registry, select the **More actions** menu more\_vert for the model you want to copy.  
3.  Click **Copy model**
4.  Choose either **To another project** or **To another region** .

**Copy model to a different region**

1.  Choose **To another region** .
2.  Choose the model version you want to copy.
3.  Select either **Copy as new model** or **Copy as new version** .
4.  Choose the destination region.
5.  Add the destination model name or model ID. If you copy over a model for the first time, it's assigned the default alias in the new region.
