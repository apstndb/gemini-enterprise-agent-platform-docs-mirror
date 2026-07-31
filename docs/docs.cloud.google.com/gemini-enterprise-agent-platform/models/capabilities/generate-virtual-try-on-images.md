---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/generate-virtual-try-on-images
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/generate-virtual-try-on-images
title: Generate Virtual Try-On Images
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Virtual Try-On lets you generate images of people to virtually try-on clothing products. You provide an image of a person and an image of a clothing product, and then Virtual Try-On generates an image of the person wearing that product.

The following models support generating virtual try-on images:

#### Click to expand supported models

  - [`virtual-try-on-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/vto/virtual-try-on-001)

## Before you begin

1.  Set up authentication for your environment.
    
    Select the tab for how you plan to use the samples on this page:
    
    ### Python
    
    To use the Python samples on this page in a local development environment, install and initialize the gcloud CLI, and then set up Application Default Credentials with your user credentials.
    
    1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.
    
    2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .
    
    3.  If you're using a local shell, then create local authentication credentials for your user account:
        
            gcloud auth application-default login
        
        You don't need to do this if you're using Cloud Shell.
        
        If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .
    
    For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) in the Google Cloud authentication documentation.
    
    ### REST
    
    To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.
    
    For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Generate images

### Python

#### Install

    pip install --upgrade google-genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_ENTERPRISE=True

    from google import genai
    from google.genai.types import RecontextImageSource, ProductImage
    
    client = genai.Client()
    
    # TODO(developer): Update and un-comment below line
    # output_file = "output-image.png"
    
    image = client.models.recontext_image(
        model="virtual-try-on-001",
        source=RecontextImageSource(
            person_image=Image.from_file(location="test_resources/man.png"),
            product_images=[
                ProductImage(product_image=Image.from_file(location="test_resources/sweater.jpg"))
            ],
        ),
    )
    
    image.generated_images[0].image.save(output_file)
    
    print(f"Created output image using {len(image.generated_images[0].image.image_bytes)} bytes")
    # Example response:
    # Created output image using 1234567 bytes

### REST

For more information about the Virtual Try-On API, see the following:

  - [Method: `endpoints.predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict)
  - [`VirtualTryOnModelInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelInstance)
  - [`VirtualTryOnModelParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelParams)
  - [`VirtualTryOnModelResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelResult)

Before using any of the request data, make the following replacements:

  - REGION : The region that your project is located in. For more information about supported regions, see [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent/platform/resources/locations) .
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
  - BASE64\_PERSON\_IMAGE : The Base64-encoded image of the person image.
  - BASE64\_PRODUCT\_IMAGE : The Base64-encoded image of the product image.
  - IMAGE\_COUNT : The number of images to generate. The accepted range of values is `1` to `4` .
  - GCS\_OUTPUT\_PATH : The Cloud Storage path to store the virtual try-on output to.

HTTP method and URL:

    POST https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/publishers/google/models/virtual-try-on-001:predict

Request JSON body:

    {
      "instances": [
        {
          "personImage": {
            "image": {
              "bytesBase64Encoded": "BASE64_PERSON_IMAGE"
            }
          },
          "productImages": [
            {
              "image": {
                "bytesBase64Encoded": "BASE64_PRODUCT_IMAGE"
              }
            }
          ]
        }
      ],
      "parameters": {
        "sampleCount": IMAGE_COUNT,
        "storageUri": "GCS_OUTPUT_PATH"
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
         "https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/publishers/google/models/virtual-try-on-001:predict"

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
        -Uri "https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/publishers/google/models/virtual-try-on-001:predict" | Select-Object -Expand Content

The request returns image objects. In this example, two image objects are returned, with two prediction objects as base64-encoded images.

    {
      "predictions": [
        {
          "mimeType": "image/png",
          "bytesBase64Encoded": "BASE64_IMG_BYTES"
        },
        {
          "bytesBase64Encoded": "BASE64_IMG_BYTES",
          "mimeType": "image/png"
        }
      ]
    }
