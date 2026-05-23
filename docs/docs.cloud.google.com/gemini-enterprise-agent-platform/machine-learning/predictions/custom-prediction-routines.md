---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-prediction-routines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-prediction-routines
title: Custom inference routines
description: Learn about custom inference routines, which let you build custom containers with preprocessing and postprocessing code without managing HTTP server setup or container creation from scratch.
data_source: docs.cloud.google.com
---

Custom inference routines let you build [custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) with preprocessing and postprocessing code, without dealing with the details of setting up an HTTP server or building a container from scratch. You can use preprocessing to normalize and transform the inputs or make calls to external services to get additional data, and use postprocessing to format the model inference or run business logic.

The following diagram depicts the user workflow both with and without custom inference routines.

![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/predictions/images/cpr.svg)

The main differences are:

  - You don't need to write a model server or a Dockerfile. The model server, which is the HTTP server that hosts the model, is provided for you.

  - You can deploy and debug the model locally, speeding up the iteration cycle during development.

## Build and deploy a custom container

This section describes how to use CPR to build a custom container with preprocessing and postprocessing logic and deploy to both a local and online endpoint.

### Setup

You must have [Agent Platform SDK for Python](https://github.com/googleapis/python-aiplatform) and [Docker](https://www.docker.com/) installed in your environment.

### Write custom `Predictor` inference interface

Implement the [`Predictor`](https://github.com/googleapis/python-aiplatform/blob/main/google/cloud/aiplatform/prediction/predictor.py) interface.

For example, see [Sklearn's `Predictor` implementation](https://github.com/googleapis/python-aiplatform/blob/main/google/cloud/aiplatform/prediction/sklearn/predictor.py) .

### Write custom `Handler` (optional)

Custom handlers have access to the raw request object, and thus, are useful in rare cases where you need to customize web server related logic, such as supporting additional request and response headers or deserializing non-JSON formatted inference requests.

Here is a [sample notebook](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/prediction/custom_prediction_routines/SDK_Custom_Predict_and_Handler_SDK_Integration.ipynb) that implements both Predictor and Handler.

Although it isn't required, for better code organization and reusability, we recommend that you implement the web server logic in the Handler and the ML logic in the Predictor as shown in the default handler.

### Build custom container

Put your custom code and an additional `requirements.txt` file, if you need to install any packages in your images, in a directory.

Use Agent Platform SDK for Python to build custom containers as follows:

    from google.cloud.aiplatform.prediction import LocalModel
    
    # {import your predictor and handler}
    
    local_model = LocalModel.build_cpr_model(
        {PATH_TO_THE_SOURCE_DIR},
        f"{REGION}-docker.pkg.dev/{PROJECT_ID}/{REPOSITORY}/{IMAGE}",
        predictor={PREDICTOR_CLASS},
        handler={HANDLER_CLASS},
        requirements_path={PATH_TO_REQUIREMENTS_TXT},
    )

You can inspect the container specification to get useful information such as image URI and environment variables.

    local_model.get_serving_container_spec()

### Run the container locally (optional)

This step is required only if you want to run and test the container locally which is useful for faster iteration. In the following example, you deploy to a local endpoint and send an inference request (format for [request body](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#request-body) ).

    with local_model.deploy_to_local_endpoint(
        artifact_uri={GCS_PATH_TO_MODEL_ARTIFACTS},
        credential_path={PATH_TO_CREDENTIALS},
    ) as local_endpoint:
        health_check_response = local_endpoint.run_health_check()
        predict_response = local_endpoint.predict(
            request_file={PATH_TO_INPUT_FILE},
            headers={ANY_NEEDED_HEADERS},
        )

Print out the health check and inference response.

    print(health_check_response, health_check_response.content)
    print(predict_response, predict_response.content)

Print out all the container logs.

    local_endpoint.print_container_logs(show_all=True)

### Upload to Gemini Enterprise Agent Platform Model Registry

Your model will need to access your model artifacts (the files from training), so make sure you've uploaded them to Google Cloud Storage.

Push the image to the [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs) .

    local_model.push_image()

Then, upload to Model Registry.

    from google.cloud import aiplatform
    
    model = aiplatform.Model.upload(
        local_model=local_model,
        display_name={MODEL_DISPLAY_NAME},
        artifact_uri={GCS_PATH_TO_MODEL_ARTIFACTS},
    )

Once your model is uploaded to Model Registry, it may be used to [get batch inferences](https://docs.cloud.google.com/vertex-ai/docs/predictions/batch-predictions) or deployed to a Agent Platform endpoint to get online inferences.

### Deploy to Agent Platform endpoint

    endpoint = model.deploy(machine_type="n1-standard-4")

Once your model is deployed, you can [get online inferences](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-predictions#get_online_predictions) .

## Notebook Samples

The samples showcase the different ways you can deploy a model with custom preprocessing and postprocessing using Vertex AI Inference.

  - [Custom Predictor with custom pre/post-processing for Sklearn, build your own container with Agent Platform SDK for Python.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/prediction/custom_prediction_routines/SDK_Custom_Preprocess.ipynb)
      - Implement only loading of serialized preprocessor, preprocess, and postprocess methods in the Predictor. Inherit default model loading and predict behavior from Agent Platform-distributed `SklearnPredictor` .
  - [Custom Predictor, build your own container with Agent Platform SDK for Python.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/prediction/custom_prediction_routines/SDK_Custom_Predict_SDK_Integration.ipynb)
      - Custom implementation of the entire Predictor.
  - [Custom Predictor and Handler, build your own container with Agent Platform SDK for Python.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/prediction/custom_prediction_routines/SDK_Custom_Predict_and_Handler_SDK_Integration.ipynb)
      - Custom implementation of Predictor and Handler.
      - Customizing the Handler allows the model server to handle csv inputs.
  - [Custom Predictor, build your own container with Agent Platform SDK for Python and PyTorch.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/prediction/custom_prediction_routines/SDK_Pytorch_Custom_Predict.ipynb)
      - Custom implementation of the Predictor.
  - [Existing image, test inference locally and deploy models with Agent Platform SDK for Python.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/prediction/custom_prediction_routines/SDK_Triton_PyTorch_Local_Prediction.ipynb)
      - Use NVIDIA Triton inference server for PyTorch models.
