---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation
title: Guide video generation using asset and style images
description: You can specify the subject of your Gemini Omni Flash or Veo on Gemini Enterprise Agent Platform generated videos. You use either the {{dynamic_data.site_values.cloud_name_short}} console or the Agent Platform API and specify reference images that the model uses to match the subject that you provided.
data_source: docs.cloud.google.com
---

You can use Gemini Omni Flash or Veo on Gemini Enterprise Agent Platform to guide video generation using reference images.

## Gemini Omni Flash

Gemini Omni Flash lets you use reference images to provide additional input to the model when generating a video. The following Gemini Omni Flash models support reference images:

#### Click to expand supported models

  - [`gemini-omni-flash-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-flash-preview) preview

## Veo

Veo on Gemini Enterprise Agent Platform lets you use reference images to direct your generated video's content and artistic style. You can choose to use one of the following when using reference images with Veo:

  - **Subject image** : You provide up to three images of a single person, character, or product. Veo preserves the subject's appearance in the output video.
    
    The following models support reference asset image to video:
    
    #### Click to expand supported models
    
      - [`veo-2.0-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate#2.0-generate-001)
      - [`veo-2.0-generate-exp`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate#2.0-generate-exp) preview
      - [`veo-2.0-generate-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate#2.0-generate-preview) preview
      - [`veo-3.1-generate-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-generate-preview) preview
      - [`veo-3.1-fast-generate-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-fast-generate-preview) preview
      - [`veo-3.1-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-generate-001)
      - [`veo-3.1-fast-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-fast-generate-001)

  - **Style image** : You provide a single style image. Veo applies the style from your uploaded image in the output video.
    
    The following models support reference style image to video:
    
    #### Click to expand supported models
    
      - [`veo-2.0-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate#2.0-generate-001)
      - [`veo-2.0-generate-exp`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate#2.0-generate-exp) preview
      - [`veo-2.0-generate-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate#2.0-generate-preview) preview

For more information about writing effective text prompts for video generation, see the [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide) .

## Before you begin

1.  Set up authentication for your environment.
    
    Select the tab for how you plan to use the samples on this page:
    
    ### Console
    
    When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.
    
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

## Use Gemini Omni Flash and references to generate videos

### REST

For more information about using the Gemini Omni Flash API, see [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .

Video generation can take over a minute to complete. To generate a video to download immediately after completion, use a synchronous request. To generate a video that can be downloaded later, send an asynchronous request by setting the `background` parameter to `true` . Asynchronous interactions are retained for up to 14 days.

### Synchronous request

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.
  - `  MODEL_ID  ` : A string respresenting the model ID to use. The following are accepted values:
      - `"gemini-omni-flash-preview"`
  - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
  - `  CLOUD_STORAGE_INPUT_URI  ` : A string representing the Cloud Storage bucket that contains the input media. For example: `"gs://video-bucket/input/"` .
  - `  CLOUD_STORAGE_OUTPUT_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .
  - `  ASPECT_RATIO  ` : Optional: A string representing the expected aspect ratio of the output video. If not provided, the aspect ratio is inferred from the prompt. The following are accepted values:
      - `"16:9"`
      - `"9:16"`
  - `  DURATION  ` : A string representing the length of the generated video files. Allowed strings are integers between `3` and `10` , followed by "s" for seconds. For example, `"10s` "

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions

Request JSON body:

    {
      "model": "MODEL_ID",
      "input": [
        {
          "type": "text",
          "text": "TEXT_PROMPT"
        },
        {
          "type": "image",
          "uri": "CLOUD_STORAGE_INPUT_URI",
          "mime_type": "image/png"
        }
      ],
      "response_format": [
        {
          "type": "video",
          "delivery": "uri",
          "gcs_uri": "CLOUD_STORAGE_OUTPUT_URI",
          "aspect_ratio": "ASPECT_RATIO",
          "duration": "DURATION"
        }
      ],
      "generation_config": {
        "video_config": {
          "task": "reference_to_video"
        }
      }
    }

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer TOKEN" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions"

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

    $headers = @{ "Authorization" = "Bearer TOKEN" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content

The response contains an interaction which includes the model thoughts and an output video.

    {
      "id":"INTERACTION_ID",
      "model":"gemini-omni-flash-preview",
      "status":"completed",
      "usage":{
        "total_tokens":479,
        "total_input_tokens":26,
        "input_tokens_by_modality":[
          {
            "modality":"text",
            "tokens":26
          },
          {
            "modality":"image",
            "tokens":124
          }
        ],
        "output_tokens_by_modality": [
          {
            "modality": "video",
            "tokens": 28832
          }
        ],
        "total_output_tokens":28832,
        "total_thought_tokens":453
      },
      "steps":[
        {
          "type":"thought",
          "summary":[
            {
              "type":"text",
              "text":"MODEL THOUGHTS"
            }
          ],
        },
        { 
          "type":"model_output",
          "content":[
            {
              "type":"video",
              "uri":"gs://some/output_path/123.mp4",
              "mime_type":"video/mp4" 
            }
          ]
        }
      ],
      "object":"interaction"
      "role":"model",
      "created":"2026-05-29T02:17:56Z",
      "updated":"2026-05-29T02:17:56Z",
    }

### Asynchronous request

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.
  - `  MODEL_ID  ` : A string respresenting the model ID to use. The following are accepted values:
      - `"gemini-omni-flash-preview"`
  - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
  - `  CLOUD_STORAGE_INPUT_URI  ` : A string representing the Cloud Storage bucket that contains the input media. For example: `"gs://video-bucket/input/"` .
  - `  CLOUD_STORAGE_OUTPUT_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .
  - `  ASPECT_RATIO  ` : Optional: A string representing the expected aspect ratio of the output video. If not provided, the aspect ratio is inferred from the prompt. The following are accepted values:
      - `"16:9"`
      - `"9:16"`
  - `  DURATION  ` : A string representing the length of the generated video files. Allowed strings are integers between `3` and `10` , followed by "s" for seconds. For example, `"10s` "

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions

Request JSON body:

    {
      "model": "MODEL_ID",
      "input": [
        {
          "background": true,
          "type": "text",
          "text": "TEXT_PROMPT"
        },
        {
          "type": "image",
          "uri": "CLOUD_STORAGE_INPUT_URI",
          "mime_type": "image/png"
        }
      ],
      "response_format": [
        {
          "type": "video",
          "delivery": "uri",
          "gcs_uri": "CLOUD_STORAGE_OUTPUT_URI",
          "aspect_ratio": "ASPECT_RATIO",
          "duration": "DURATION"
        }
      ],
      "generation_config": {
        "video_config": {
          "task": "reference_to_video"
        }
      }
    }

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer TOKEN" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions"

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

    $headers = @{ "Authorization" = "Bearer TOKEN" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content

The response contains an interaction ID, which you'll use to get the video you generated.

    {
      "id":"INTERACTION_ID",
      "status":"in_progress",
      "object":"interaction"
    }

Later, use the INTERACTION\_ID to get the generated video:

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.
  - `  INTERACTION_ID  ` : The interaction ID from the asynchronous request.

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID

To send your request, choose one of these options:

#### curl

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer TOKEN" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID"

#### PowerShell

Execute the following command:

    $headers = @{ "Authorization" = "Bearer TOKEN" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID" | Select-Object -Expand Content

The response is in a format similar to the following:

    {
      "id":"INTERACTION_ID",
      "model":"gemini-omni-flash-preview",
      "status":"completed",
      "usage":{
        "total_tokens":479,
        "total_input_tokens":26,
        "input_tokens_by_modality":[
          {
            "modality":"text",
            "tokens":26
          },
          {
            "modality":"image",
            "tokens":124
          }
        ],
        "output_tokens_by_modality": [
          {
            "modality": "video",
            "tokens": 28832
          }
        ],
        "total_output_tokens":28832,
        "total_thought_tokens":453
      },
      "steps":[
        {
          "type": "user_input",
          "content": [
            {
              "type": "text",
              "text": "5 second, 9:16 video. Use the image as the first frame."
            },
            {
              "type": "image",
              "uri": "gs://some/path",
              "mime_type": "image/png"
            }
          ]
        },
        {
          "type":"thought"
          "summary":[
            {
              "type":"text",
              "text":"MODEL THOUGHTS"
            }
          ],
        },
        { 
          "type":"model_output",
          "content":[
            {
              "type":"video",
              "data":"VIDEO DATA",
              "mime_type":"video/mp4" 
            }
          ]
        }
      ],
      "object":"interaction"
      "role":"model",
      "created":"2026-05-29T02:17:56Z",
      "updated":"2026-05-29T02:17:56Z",
    }

## Use Veo and references to generate videos

The following sections describe how to use Veo to generate videos from references.

### Use asset images to generate videos

Do the following:

### Console

1.  In the Google Cloud console, go to the **Agent Platform \> Agent Platform Studio** page.

2.  Click **Generate media** .

3.  Click **Video** .

4.  In the **Task** menu, select **Reference-to-video (Subject)** .

5.  In the **Model** menu, select a model from the available options.
    
    > **Note:** `veo-3.1-generate-preview` only returns 8 second videos when you use subject images.

6.  In the **Subject Images** section, click **Add** .
    
    A file selection dialog is displayed. Choose one to three images on your computer to upload.

7.  Optional: In the **Parameters** section, adjust the following settings:
    
      - **Aspect ratio** : select either **16:9** or **9:16** .
      - **Number of results** : adjust the slider or enter a value between **1** and **4** .
      - **Video length** : select **8** , **6** , or **4** seconds.
      - **Output resolution** : select one of the following:
          - **720p**
          - **1080p**
          - **4k**

8.  Optional: In the **Safety** section, select one of the following **Person generation** settings:
    
      - **Allow (Adults only)** : default value. Generate adult people or faces only. Don't generate youth or children people or faces.
    
      - **Don't allow** : don't generate people or faces.

9.  Optional: In the **Advanced options** section, enter a **Seed** value for randomizing video generation.

10. In the **Prompt** box, enter your text prompt that describes the videos to generate.

11. Click **Run** .

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

    import time
    from google import genai
    from google.genai.types import GenerateVideosConfig, Image, VideoGenerationReferenceImage
    
    client = genai.Client()
    
    # TODO(developer): Update and un-comment below line
    # output_gcs_uri = "gs://your-bucket/your-prefix"
    
    operation = client.models.generate_videos(
        model="veo-3.1-generate-preview",
        prompt="A person walks in carrying a vase full of flowers and places the vase on a kitchen table.",
        config=GenerateVideosConfig(
            reference_images=[
                VideoGenerationReferenceImage(
                    image=Image(
                        gcs_uri="gs://cloud-samples-data/generative-ai/image/vase.png",
                        mime_type="image/png",
                    ),
                    reference_type="asset",
                ),
            ],
            aspect_ratio="9:16",
            output_gcs_uri=output_gcs_uri,
        ),
    )
    
    while not operation.done:
        time.sleep(15)
        operation = client.operations.get(operation)
        print(operation)
    
    if operation.response:
        print(operation.result.generated_videos[0].video.uri)
    
    # Example response:
    # gs://your-bucket/your-prefix

### REST

For more information about the Veo API, see the following:

  - [Method: `endpoints.predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict)
  - [`VideoGenerationModelInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelInstance)
  - [`VideoGenerationModelParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelParams)
  - [`VideoGenerationModelResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelResult)

<!-- end list -->

1.  Use the following commands to send a video generation request. This request begins a long-running operation and stores output to a Cloud Storage bucket you specify.
    
    Before using any of the request data, make the following replacements:
    
      - `  PROJECT_ID  ` : Your Google Cloud project ID.
    
      - `  MODEL_ID  ` : A string representing the model ID to use. The following models are supported:
    
      - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
    
      - `  BASE64_ENCODED_IMAGE  ` : A base64-bytes encoded subject image. You can repeat this field and `mimeType` to specify up to three subject images.
    
      - `  IMAGE_MIME_TYPE  ` : The MIME type of the input image. Only one of the following:
        
          - `image/jpeg`
          - `image/png`
        
        You can repeat this field and `bytesBase64Encoded` to specify up to three subject images.
    
      - `  ASPECT_RATIO  ` : Optional: The aspect ratio of the generated video. Only one of the following:
        
          - `"16:9"`
          - `"9:16"`
        
        The default value is `"16:9"` .
    
      - `  OUTPUT_STORAGE_URI  ` : Optional: The Cloud Storage bucket to store the output videos. If not provided, a Base64-bytes encoded video is returned in the response. For example: `gs://video-bucket/output/` .
    
      - `  RESPONSE_COUNT  ` : The number of video files you want to generate. Accepted integer values: 1-4.
    
      - `  VIDEO_RESOLUTION  ` : Optional: The resolution of the generated video. Only one of the following:
        
          - `"720p"`
          - `"1080p"`
          - `"4k"` (Veo 3.1 Preview models only)
        
        Default value is `"720p"` .
    
      - **Additional optional parameters**
        
        Use the following optional variables depending on your use case. Add some or all of the following parameters in the `"parameters": {}` object.
        
            "parameters": {
              "aspectRatio": "ASPECT_RATIO",
              "negativePrompt": "NEGATIVE_PROMPT",
              "personGeneration": "PERSON_SAFETY_SETTING",
              // "resolution": RESOLUTION, // Veo 3 models only
              "sampleCount": RESPONSE_COUNT,
              "seed": SEED_NUMBER
            }
        
          - `  ASPECT_RATIO  ` : Optional: A string value that describes the aspect ratio of the generated videos. You can use the following values:
            
              - `"16:9"` for landscape
              - `"9:16"` for portrait
            
            The default value is `"16:9"`
        
          - `  NEGATIVE_PROMPT  ` : Optional: A string value that describes content that you want to prevent the model from generating.
        
          - `  PERSON_SAFETY_SETTING  ` : Optional: A string value that controls the safety setting for generating people or face generation. You can use the following values:
            
              - `"allow_adult"` : Only allow generation of adult people and faces.
              - `"disallow"` : Doesn't generate people or faces.
            
            The default value is `"allow_adult"` .
        
          - `  RESOLUTION  ` : Optional: A string value that controls the resolution of the generated video. Supported by **Veo 3 models only.** You can use the following values:
            
              - `"720p"`
              - `"1080p"`
              - `"4k"` (Veo 3.1 Preview models only)
            
            The default value is `"720p"` .
        
          - `  RESPONSE_COUNT  ` : Optional. An integer value that describes the number of videos to generate. The accepted range of values is `1` - `4` .
        
          - `  SEED_NUMBER  ` : Optional. An uint32 value that the model uses to generate deterministic videos. Specifying a seed number with your request without changing other parameters guides the model to produce the same videos. The accepted range of values is `0` - `4294967295` .
    
    HTTP method and URL:
    
        POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:predictLongRunning
    
    Request JSON body:
    
        {
          "instances": [
            {
              "prompt": "TEXT_PROMPT",
              // The following fields can be repeated for up to three total
              // images.
              "referenceImages": [
                {
                  "image": {
                    "bytesBase64Encoded": "BASE64_ENCODED_IMAGE",
                    "mimeType": "IMAGE_MIME_TYPE"
                  },
                  "referenceType": "asset"
                }
              ]
            }
          ],
          "parameters": {
            "aspectRatio":, "ASPECT_RATIO,
            "durationSeconds": 8,
            "storageUri": "OUTPUT_STORAGE_URI",
            "sampleCount": RESPONSE_COUNT,
            "resolution": "VIDEO_RESOLUTION
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
             "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:predictLongRunning"
    
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
            -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:predictLongRunning" | Select-Object -Expand Content
    
    This request returns a full operation name with a unique operation ID. Use this full operation name to poll that status of the video generation request.
    
        {
          "name":
          "projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID/operations/a1b07c8e-7b5a-4aba-bb34-3e1ccb8afcc8"
        }

2.  Optional: Check the status of the video generation long-running operation.
    
    Before using any of the request data, make the following replacements:
    
      - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - MODEL\_ID : The model ID to use.
      - OPERATION\_ID : The unique operation ID returned in the original generate video request.
    
    HTTP method and URL:
    
        POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:fetchPredictOperation
    
    Request JSON body:
    
        {
          "operationName": "projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID/operations/OPERATION_ID"
        }
    
    To send your request, choose one of these options:
    
    #### curl
    
    > **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .
    
    Save the request body in a file named `request.json` , and execute the following command:
    
        curl -X POST \
             -H "Authorization: Bearer $(gcloud auth print-access-token)" \
             -H "Content-Type: application/json; charset=utf-8" \
             -d @request.json \
             "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:fetchPredictOperation"
    
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
            -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:fetchPredictOperation" | Select-Object -Expand Content
    
    This request returns information about the operation, including if the operation is still running or is done.
    
    #### Response
    
        {
          "name": "projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID/operations/OPERATION_ID",
          "done": true,
          "response": {
            "raiMediaFilteredCount": 0,
            "@type": "type.googleapis.com/cloud.ai.large_models.vision.GenerateVideoResponse",
            "videos": [
              {
                "gcsUri":"gs://BUCKET_NAME/TIMESTAMPED_FOLDER/sample_0.mp4",
                "mimeType": "video/mp4"
              }
            ]
          }
        }

### Use style images to generate videos

Do the following:

### Console

1.  In the Google Cloud console, go to the **Agent Platform \> Agent Platform Studio** page.

2.  Click **Generate media** .

3.  Click **Video** .

4.  In the **Task** menu, select **Reference-to-video (Style)** .

5.  In the **Model** menu, select a model from the available options.

6.  In the **Style image** section, click **Add** .
    
    A file selection dialog is displayed. Choose an image on your computer to upload.

7.  Optional: In the **Parameters** section, adjust the following settings:
    
      - **Aspect ratio** : select either **16:9** or **9:16** .
      - **Number of results** : adjust the slider or enter a value between **1** and **4** .
      - **Video length** : select **8** , **7** , **6** , or **5** seconds.

8.  Optional: In the **Safety** section, select one of the following **Person generation** settings:
    
      - **Allow (Adults only)** : default value. Generate adult people or faces only. Don't generate youth or children people or faces.
    
      - **Don't allow** : don't generate people or faces.

9.  Optional: In the **Advanced options** section, enter a **Seed** value for randomizing video generation.

10. In the **Prompt** box, enter your text prompt that describes the videos to generate.

11. Click **Run** .

### REST

For more information about the Veo API, see the [Veo on Gemini Enterprise Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) .

1.  Use the following commands to send a video generation request. This request begins a long-running operation and stores output to a Cloud Storage bucket you specify.
    
    Before using any of the request data, make the following replacements:
    
      - `  PROJECT_ID  ` : Your Google Cloud project ID.
    
      - `  MODEL_ID  ` : A string representing the model ID to use. The following models are supported:
        
        > **Important:** Veo 3.1 models don't support `referenceImages.style` . Use `veo-2.0-generate-exp` when using style images.
    
      - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
    
      - `  BASE64_ENCODED_IMAGE  ` : A base64-bytes encoded style image.
    
      - `  IMAGE_MIME_TYPE  ` : The MIME type of the input image. Only one of the following:
        
          - `image/jpeg`
          - `image/png`
    
      - `  OUTPUT_STORAGE_URI  ` : Optional: The Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `gs://video-bucket/output/` .
    
      - `  RESPONSE_COUNT  ` : The number of video files you want to generate. Accepted integer values: 1-4.
    
      - **Additional optional parameters**
        
        Use the following optional variables depending on your use case. Add some or all of the following parameters in the `"parameters": {}` object.
        
            "parameters": {
              "aspectRatio": "ASPECT_RATIO",
              "negativePrompt": "NEGATIVE_PROMPT",
              "personGeneration": "PERSON_SAFETY_SETTING",
              // "resolution": RESOLUTION, // Veo 3 models only
              "sampleCount": RESPONSE_COUNT,
              "seed": SEED_NUMBER
            }
        
          - `  ASPECT_RATIO  ` : Optional: A string value that describes the aspect ratio of the generated videos. You can use the following values:
            
              - `"16:9"` for landscape
              - `"9:16"` for portrait
            
            The default value is `"16:9"`
        
          - `  NEGATIVE_PROMPT  ` : Optional: A string value that describes content that you want to prevent the model from generating.
        
          - `  PERSON_SAFETY_SETTING  ` : Optional: A string value that controls the safety setting for generating people or face generation. You can use the following values:
            
              - `"allow_adult"` : Only allow generation of adult people and faces.
              - `"disallow"` : Doesn't generate people or faces.
            
            The default value is `"allow_adult"` .
        
          - `  RESOLUTION  ` : Optional: A string value that controls the resolution of the generated video. Supported by **Veo 3 models only.** You can use the following values:
            
              - `"720p"`
              - `"1080p"`
              - `"4k"` (Veo 3.1 Preview models only)
            
            The default value is `"720p"` .
        
          - `  RESPONSE_COUNT  ` : Optional. An integer value that describes the number of videos to generate. The accepted range of values is `1` - `4` .
        
          - `  SEED_NUMBER  ` : Optional. An uint32 value that the model uses to generate deterministic videos. Specifying a seed number with your request without changing other parameters guides the model to produce the same videos. The accepted range of values is `0` - `4294967295` .
    
    HTTP method and URL:
    
        POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:predictLongRunning
    
    Request JSON body:
    
        {
          "instances": [
            {
              "prompt": "TEXT_PROMPT",
              "referenceImages": [
                {
                  "image": {
                    "bytesBase64Encoded": "BASE64_ENCODED_IMAGE",
                    "mimeType": "IMAGE_MIME_TYPE"
                  },
                  "referenceType": "style"
                }
              ]
            }
          ],
          "parameters": {
            "durationSeconds": 8,
            "storageUri": "OUTPUT_STORAGE_URI",
            "sampleCount": RESPONSE_COUNT
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
             "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:predictLongRunning"
    
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
            -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:predictLongRunning" | Select-Object -Expand Content
    
    This request returns a full operation name with a unique operation ID. Use this full operation name to poll that status of the video generation request.
    
        {
          "name":
          "projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID/operations/a1b07c8e-7b5a-4aba-bb34-3e1ccb8afcc8"
        }

2.  Optional: Check the status of the video generation long-running operation.
    
    Before using any of the request data, make the following replacements:
    
      - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - MODEL\_ID : The model ID to use.
      - OPERATION\_ID : The unique operation ID returned in the original generate video request.
    
    HTTP method and URL:
    
        POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:fetchPredictOperation
    
    Request JSON body:
    
        {
          "operationName": "projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID/operations/OPERATION_ID"
        }
    
    To send your request, choose one of these options:
    
    #### curl
    
    > **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .
    
    Save the request body in a file named `request.json` , and execute the following command:
    
        curl -X POST \
             -H "Authorization: Bearer $(gcloud auth print-access-token)" \
             -H "Content-Type: application/json; charset=utf-8" \
             -d @request.json \
             "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:fetchPredictOperation"
    
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
            -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID:fetchPredictOperation" | Select-Object -Expand Content
    
    This request returns information about the operation, including if the operation is still running or is done.
    
    #### Response
    
        {
          "name": "projects/PROJECT_ID/locations/us-central1/publishers/google/models/MODEL_ID/operations/OPERATION_ID",
          "done": true,
          "response": {
            "raiMediaFilteredCount": 0,
            "@type": "type.googleapis.com/cloud.ai.large_models.vision.GenerateVideoResponse",
            "videos": [
              {
                "gcsUri":"gs://BUCKET_NAME/TIMESTAMPED_FOLDER/sample_0.mp4",
                "mimeType": "video/mp4"
              }
            ]
          }
        }

## What's next

  - [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide)
  - [Generate videos from text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)
  - [Understand responsible AI and usage guidelines for Veo on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines)
