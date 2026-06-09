---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model
title: Import models to Gemini Enterprise Agent Platform
description: Learn how to import models into the Gemini Enterprise Agent Platform Model Registry to make them visible in the registry, from where you can then deploy them to an endpoint and run inferences.
data_source: docs.cloud.google.com
---

This guide describes how to import models into the Gemini Enterprise Agent Platform Model Registry. After you import your model, it is visible in the Model Registry. From the Model Registry, you can deploy your imported model to an endpoint and run inferences.

## Required roles

To get the permissions that you need to import models, ask your administrator to grant you the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Prebuilt or custom containers

When you import a model, you associate it with a container for Agent Platform to run inference requests. You can use [prebuilt containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) provided by Agent Platform, or use your own [custom containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) that you build and push to Artifact Registry.

You can use a prebuilt container if your model meets the following requirements:

  - Trained in Python 3.7 or later
  - Trained using TensorFlow, PyTorch, scikit-learn, or XGBoost
  - Exported to meet [framework-specific requirements for one of the prebuilt inference containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts#framework-specific_requirements)

If you are importing a tabular AutoML model that you previously [exported](https://docs.cloud.google.com/vertex-ai/docs/export/export-model-tabular) , you must use a specific custom container provided by Agent Platform.

Otherwise, create a new [custom container](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) , or use an existing custom container that you have in Artifact Registry.

## Upload model artifacts to Cloud Storage

You must store your model artifacts in a Cloud Storage bucket, where the bucket's region matches the locational endpoint you're using.

If your Cloud Storage bucket is in a different Google Cloud project, you need to [grant Agent Platform access](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#different-project) to read your model artifacts.

If you're using a prebuilt container, ensure that your model artifacts have filenames that exactly match the following examples:

  - TensorFlow SavedModel: `saved_model.pb`
  - PyTorch: `model.mar`
  - scikit-learn: `model.joblib`
  - XGBoost: `model.bst` or `model.joblib`

Learn more about [exporting model artifacts for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) .

> **Warning:** To avoid increased latency, ensure the artifacts bucket is located in the same region as the endpoint you are using.

## Import a model using Google Cloud console

To import a model using Google Cloud console:

1.  In the Google Cloud console, go to the Agent Platform **Models** page.

2.  Click **Import** .

3.  Select **Import as new model** to import a new model.

4.  Select **Import as new version** to import a model as a version of an existing model. To learn more about model versioning, see [Model versioning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/versioning) .

5.  **Name and region** : Enter a name for your model. Select the region that matches both your bucket's region, and the Agent Platform locational endpoint you're using. Click **Continue** .

6.  If you expand **Advanced options** , you can optionally decide to add a [customer-managed encryption key](https://docs.cloud.google.com/vertex-ai/docs/general/cmek) .

Depending on the type of container you are using, select the appropriate tab below.

### Prebuilt container

1.  Select **Import model artifacts into a new prebuilt container** .

2.  Select the **Model framework** and **Model framework version** you used to train your model.

3.  If you want to use GPUs for serving inferences, set the **Accelerator type** to **GPUs** .
    
    You select the type of GPU later on, when you [deploy the model to an endpoint](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-console) .

4.  Specify the Cloud Storage path to the directory that contains your model artifacts.
    
    For example, `gs:// BUCKET_NAME /models/` .

5.  Leave the **Predict schemata** blank.

6.  To import your model *without* Vertex Explainable AI settings, click **Import** .
    
    After the import has completed, your model appears on the **Models** page.
    
    Otherwise, continue configuring your model by entering your explainability settings on the **Explainability** tab. Learn more about the [Explainability settings](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations#import-model-example) .

### Custom container

1.  Select **Import an existing custom container** .

2.  Set the container image URI.

3.  If you want to [provide model artifacts in addition to a container image](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#artifacts) , specify the Cloud Storage path to the directory that contains your model artifacts.
    
    For example, `gs:// BUCKET_NAME /models/` .

4.  Specify values for any of the other fields.
    
    Learn more about these [optional fields](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container#create-model) .

5.  To import your model *without* Vertex Explainable AI settings, click **Import** .
    
    After the import has completed, your model appears on the **Models** page.
    
    Otherwise, continue configuring your model by entering your explainability settings on the **Explainability** tab. Learn more about the [Explainability settings](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations#import-model-example) .

### AutoML tabular container

1.  Select **Import an existing custom container** .

2.  In the **Container image** field, enter `  MULTI_REGION -docker.pkg.dev/vertex-ai/automl-tabular/prediction-server-v1:latest ` .
    
    Replace `  MULTI_REGION  ` with `us` , `europe` , or `asia` to select which Docker repository you want to pull the Docker image from. Each repository provides the same Docker image, but choosing the [Artifact Registry multi-region](https://docs.cloud.google.com/artifact-registry/docs/repo-locations#location-mr) closest to the machine where you are running Docker might reduce latency.

3.  In the **Package location** field, specify the Cloud Storage path to the directory that contains your model artifacts.
    
    The path looks similar to the following example:
    
    `gs:// BUCKET_NAME /models- MODEL_ID /tf-saved-model/ TIMESTAMP /`

4.  Leave all other fields blank.

5.  Click **Import** .
    
    After the import has completed, your model appears on the **Models** page. You can use this model just like other AutoML tabular models, except imported AutoML tabular models don't support Vertex Explainable AI.

## Import a model programmatically

The following examples show how to import a model using various tools:

> **Warning:** Don't invoke [UploadModel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/upload) or [DeployModel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) more than once every 2 seconds.

### gcloud

The following example uses the [`gcloud ai models upload` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload) :

    gcloud ai models upload \
      --region=LOCATION \
      --display-name=MODEL_NAME \
      --container-image-uri=IMAGE_URI \
      --artifact-uri=PATH_TO_MODEL_ARTIFACT_DIRECTORY

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - MODEL\_NAME : A display name for the `Model` .
  - IMAGE\_URI : The URI of the container image to use for serving inferences. For example, `us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-1:latest` . Use a [prebuilt container](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) or a [custom container](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) .
  - PATH\_TO\_MODEL\_ARTIFACT\_DIRECTORY : The Cloud Storage URI (beginning with `gs://` ) of a directory in Cloud Storage that contains your [model artifacts](https://docs.cloud.google.com/vertex-ai/machine-learning/training/exporting-model-artifacts) .

The preceding example demonstrates all the flags necessary to import most models. If you are not using a prebuilt container for inference, then you likely need to specify some additional [optional flags](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload#OPTIONAL-FLAGS) so that Agent Platform can use your container image. These flags, which begin with `--container-` , correspond to fields of your `Model` 's [`containerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#modelcontainerspec) .

### REST

Use the following code sample to upload a model using the [`upload` method of the `model` resource](https://docs.cloud.google.com/vertex-ai/docs/reference/rest/v1/projects.locations.models/upload) .

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - MODEL\_NAME : A display name for the `Model` .
  - MODEL\_DESCRIPTION : Optional. A description for the model.
  - IMAGE\_URI : The URI of the container image to use for serving inferences. For example, `us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-1:latest` . Use a [prebuilt container](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) or a [custom container](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) .
  - PATH\_TO\_MODEL\_ARTIFACT\_DIRECTORY : The Cloud Storage URI (beginning with `gs://` ) of a directory in Cloud Storage that contains your [model artifacts](https://docs.cloud.google.com/vertex-ai/machine-learning/training/exporting-model-artifacts) . This variable and the `artifactUri` field are optional if you're using a custom container.
  - `labels` : Optional. Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this training pipeline.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/models:upload

Request JSON body:

    {
      "model": {
        "displayName": "MODEL_NAME",
        "predictSchemata": {},
        "containerSpec": {
          "imageUri": "IMAGE_URI"
        },
        "artifactUri": "PATH_TO_MODEL_ARTIFACT_DIRECTORY",
        "labels": {
          "LABEL_NAME_1": "LABEL_VALUE_1",
          "LABEL_NAME_2": "LABEL_VALUE_2"
        }
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/models:upload"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/models:upload" | Select-Object -Expand Content

#### Response

    {
    "name": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.UploadModelOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-11-10T23:44:21.777760Z",
          "updateTime": "2020-11-10T23:44:21.777760Z"
        }
      }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import com.google.cloud.aiplatform.v1.UploadModelOperationMetadata;
    import com.google.cloud.aiplatform.v1.UploadModelResponse;
    import java.io.IOException;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class UploadModelSample {
      public static void main(String[] args)
          throws InterruptedException, ExecutionException, TimeoutException, IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelDisplayName = "YOUR_MODEL_DISPLAY_NAME";
        String metadataSchemaUri =
            "gs://google-cloud-aiplatform/schema/trainingjob/definition/custom_task_1.0.0.yaml";
        String imageUri = "YOUR_IMAGE_URI";
        String artifactUri = "gs://your-gcs-bucket/artifact_path";
        uploadModel(project, modelDisplayName, metadataSchemaUri, imageUri, artifactUri);
      }
    
      static void uploadModel(
          String project,
          String modelDisplayName,
          String metadataSchemaUri,
          String imageUri,
          String artifactUri)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          LocationName locationName = LocationName.of(project, location);
    
          ModelContainerSpec modelContainerSpec =
              ModelContainerSpec.newBuilder().setImageUri(imageUri).build();
    
          Model model =
              Model.newBuilder()
                  .setDisplayName(modelDisplayName)
                  .setMetadataSchemaUri(metadataSchemaUri)
                  .setArtifactUri(artifactUri)
                  .setContainerSpec(modelContainerSpec)
                  .build();
    
          OperationFuture<UploadModelResponse, UploadModelOperationMetadata> uploadModelResponseFuture =
              modelServiceClient.uploadModelAsync(locationName, model);
          System.out.format(
              "Operation name: %s\n", uploadModelResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          UploadModelResponse uploadModelResponse = uploadModelResponseFuture.get(5, TimeUnit.MINUTES);
    
          System.out.println("Upload Model Response");
          System.out.format("Model: %s\n", uploadModelResponse.getModel());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     */
    
    // const modelDisplayName = 'YOUR_MODEL_DISPLAY_NAME';
    // const metadataSchemaUri = 'YOUR_METADATA_SCHEMA_URI';
    // const imageUri = 'YOUR_IMAGE_URI';
    // const artifactUri = 'YOUR_ARTIFACT_URI';
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
    
    async function uploadModel() {
      // Configure the parent resources
      const parent = `projects/${project}/locations/${location}`;
      // Configure the model resources
      const model = {
        displayName: modelDisplayName,
        metadataSchemaUri: '',
        artifactUri: artifactUri,
        containerSpec: {
          imageUri: imageUri,
          command: [],
          args: [],
          env: [],
          ports: [],
          predictRoute: '',
          healthRoute: '',
        },
      };
      const request = {
        parent,
        model,
      };
    
      console.log('PARENT AND MODEL');
      console.log(parent, model);
      // Upload Model request
      const [response] = await modelServiceClient.uploadModel(request);
      console.log(`Long running operation : ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      const result = response.result;
    
      console.log('Upload model response ');
      console.log(`\tModel : ${result.model}`);
    }
    uploadModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from typing import Dict, Optional, Sequence
    
    from google.cloud import aiplatform
    from google.cloud.aiplatform import explain
    
    
    def upload_model_sample(
        project: str,
        location: str,
        display_name: str,
        serving_container_image_uri: str,
        artifact_uri: Optional[str] = None,
        serving_container_predict_route: Optional[str] = None,
        serving_container_health_route: Optional[str] = None,
        description: Optional[str] = None,
        serving_container_command: Optional[Sequence[str]] = None,
        serving_container_args: Optional[Sequence[str]] = None,
        serving_container_environment_variables: Optional[Dict[str, str]] = None,
        serving_container_ports: Optional[Sequence[int]] = None,
        instance_schema_uri: Optional[str] = None,
        parameters_schema_uri: Optional[str] = None,
        prediction_schema_uri: Optional[str] = None,
        explanation_metadata: Optional[explain.ExplanationMetadata] = None,
        explanation_parameters: Optional[explain.ExplanationParameters] = None,
        sync: bool = True,
    ):
    
        aiplatform.init(project=project, location=location)
    
        model = aiplatform.Model.upload(
            display_name=display_name,
            artifact_uri=artifact_uri,
            serving_container_image_uri=serving_container_image_uri,
            serving_container_predict_route=serving_container_predict_route,
            serving_container_health_route=serving_container_health_route,
            instance_schema_uri=instance_schema_uri,
            parameters_schema_uri=parameters_schema_uri,
            prediction_schema_uri=prediction_schema_uri,
            description=description,
            serving_container_command=serving_container_command,
            serving_container_args=serving_container_args,
            serving_container_environment_variables=serving_container_environment_variables,
            serving_container_ports=serving_container_ports,
            explanation_metadata=explanation_metadata,
            explanation_parameters=explanation_parameters,
            sync=sync,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        return model

To import a model with Vertex Explainable AI settings enabled, refer to the [Vertex Explainable AI model import examples](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations#import-model-example) .

### Get operation status

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Vertex AI provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/vertex-ai/docs/general/long-running-operations) .

## Limitations

  - The maximum model size supported by Model Registry is 1 TB.

## What's next

  - Deploy your model to an endpoint, [programmatically](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) or by [using Google Cloud console](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-console) .
