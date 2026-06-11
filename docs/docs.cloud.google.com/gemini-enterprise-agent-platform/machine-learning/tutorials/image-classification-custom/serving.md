---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/serving
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/serving
title: 'Hello custom training: Serve predictions from a custom image classification model'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page walks through serving predictions from your image classification model and viewing these predictions in a web app.

This tutorial has several pages:

1.  [Setting up your project and environment.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom)

2.  [Training a custom image classification model.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/training)

3.  Serving predictions from a custom image classification model.

4.  [Cleaning up your project.](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/cleanup)

Each page assumes that you have already performed the instructions from the previous pages of the tutorial.

The rest of this document assumes that you are using the same Cloud Shell environment that you created when following the [first page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom) . If your original Cloud Shell session is no longer open, you can return to the environment by doing the following:

1.  In the Google Cloud console, activate Cloud Shell.

2.  In the Cloud Shell session, run the following command:
    
        cd hello-custom-sample

## Create an endpoint

To get online predictions from the ML model that you trained when following the previous page of this tutorial, create an Vertex AI *endpoint* . Endpoints serve online predictions from one or more models.

1.  In the Google Cloud console, in the Vertex AI section, go to the **Models** page.

2.  Find the row of the model that you trained in the [previous step of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/training) , `hello_custom` , and click the model's name to open the model detail page.

3.  On the **Deploy & test** tab, click **Deploy to endpoint** to open the **Deploy to endpoint** pane.

4.  On the **Define your endpoint** step, add some basic information for your endpoint:
    
    1.  Select **Create new endpoint** .
    
    2.  In the **Endpoint name** field, enter `hello_custom` .
    
    3.  In the **Model settings** section, ensure that you see the name of your model, which is also called `hello_custom` . Specify the following model settings:
        
        1.  In the **Traffic split** field, enter `100` . Vertex AI supports splitting traffic for an endpoint to multiple models, but this tutorial doesn't use that feature.
        
        2.  In the **Minimum number of compute nodes** field, enter `1` .
        
        3.  In the **Machine type** drop-down list, select **n1-standard-2** from the **Standard** section.
        
        4.  Click **Done** .
    
    4.  In the **Logging** section, ensure that both types of prediction logging are enabled.
    
    Click **Continue** .

5.  On the **Endpoint details** step, confirm that your endpoint will be deployed to `us-central1 (Iowa)` .
    
    Do not select the **Use a customer-managed encryption key (CMEK)** checkbox. This tutorial does not use [CMEK](https://docs.cloud.google.com/vertex-ai/machine-learning/general/cmek) .

6.  Click **Deploy** to create the endpoint and deploy your model to the endpoint.

After a few minutes, check\_circle appears next to the new endpoint in the **Endpoints** table. At the same time, you also receive an email indicating that you have successfully created the endpoint and deployed your model to the endpoint.

## Deploy a Cloud Run function

You can get predictions from the Vertex AI endpoint that you just created by sending requests to the Vertex AI API's REST interface. However, only principals with the [`aiplatform.endpoints.predict` permission](https://docs.cloud.google.com/vertex-ai/machine-learning/general/access-control) can send online prediction requests. You cannot make the endpoint public for anybody to send requests to, for example via a web app.

In this section, deploy code to [Cloud Run functions](https://docs.cloud.google.com/functions/docs) to handle unauthenticated requests. The sample code that you downloaded when you read the [first page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom) contains code for this Cloud Run function in the `function/` directory. Optionally, run the following command to explore the Cloud Run function code:

    less function/main.py

Deploying the function serves the following purposes:

  - You *can* configure a Cloud Run function to receive unauthenticated requests. Additionally, functions run using [a service account with the Editor role by default](https://docs.cloud.google.com/functions/docs/securing/function-identity) , which includes the `aiplatform.endpoints.predict` permission necessary to get predictions from your Vertex AI endpoint.

  - This function also performs useful preprocessing on requests. The Vertex AI endpoint expects prediction requests in the format of the trained TensorFlow Keras graph's first layer: a tensor of normalized floats with fixed dimensions. The function takes the URL of an image as input and preprocesses the image into this format before requesting a prediction from the Vertex AI endpoint.

To deploy the Cloud Run function, do the following:

1.  In the Google Cloud console, in the Vertex AI section, go to the **Endpoints** page.

2.  Find the row of the endpoint that you created in the previous section, named `hello_custom` . In this row, click **Sample request** to open the **Sample request** pane.

3.  In the **Sample request** pane, find the line of shell code that matches the following pattern:
    
        ENDPOINT_ID="ENDPOINT_ID"
    
    ENDPOINT\_ID is a number that identifies this particular endpoint.
    
    Copy this line of code, and run it in your Cloud Shell session to set the `ENDPOINT_ID` variable.

4.  Run the following command in your Cloud Shell session to deploy the Cloud Run function:
    
        gcloud functions deploy classify_flower \
          --region=us-central1 \
          --source=function \
          --runtime=python37 \
          --memory=2048MB \
          --trigger-http \
          --allow-unauthenticated \
          --set-env-vars=ENDPOINT_ID=${ENDPOINT_ID}

## Deploy a web app to send prediction requests

Finally, host a static web app on Cloud Storage to get predictions from your trained ML model. The web app sends requests to your Cloud Run function, which preprocesses them and gets predictions from the Vertex AI endpoint.

The `webapp` directory of the sample code that you downloaded contains a sample web app. In your Cloud Shell session, run the following commands to prepare and deploy the web app:

1.  Set a couple of shell variables for commands in following steps to use:
    
        PROJECT_ID=PROJECT_ID
        BUCKET_NAME=BUCKET_NAME
    
    Replace the following:
    
      - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - BUCKET\_NAME : The name of the Cloud Storage bucket that you created when following the [first page of this tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom) .

2.  Edit the app to provide it with the trigger URL of your Cloud Run function:
    
        echo "export const CLOUD_FUNCTION_URL = 'https://us-central1-${PROJECT_ID}.cloudfunctions.net/classify_flower';" \
          > webapp/function-url.js

3.  Upload the `webapp` directory to your Cloud Storage bucket:
    
        gcloud storage cp webapp gs://${BUCKET_NAME}/ --recursive

4.  Make the web app files that you just uploaded [publicly readable](https://docs.cloud.google.com/storage/docs/access-control/making-data-public) :
    
        gcloud storage objects update gs://${BUCKET_NAME}/webapp/** --add-acl-grant=entity=allUsers,role=READER
    
    > **Note:** Shells (like bash, zsh) sometimes attempt to expand wildcards in ways that can be surprising. For more details, see [URI wildcards](https://docs.cloud.google.com/storage/docs/wildcards#surprising-behavior) .

5.  You can now navigate to the following URL to open web app and get predictions:
    
        https://storage.googleapis.com/BUCKET_NAME/webapp/index.html
    
    Open the web app and click an image of a flower to see your ML model's classification of the flower type. The web app presents the prediction as a list of flower types and the probability that the image contains each type of flower.
    
    > **Note:** This web app gets predictions for images that were also included in the training dataset for the model. Therefore the model might appear more accurate than it actually is due to [overfitting](https://developers.google.com/machine-learning/glossary#overfitting) .

![In the following screenshot, the web app has already gotten one prediction and is in the process of sending another prediction request.](https://docs.cloud.google.com/static/vertex-ai/docs/tutorials/image-classification-custom/webapp-screenshot.png)

## What's next

Follow the [last page of the tutorial](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/cleanup) to clean up resources that you have created.
