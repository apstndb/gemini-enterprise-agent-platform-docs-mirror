---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos
title: Extend videos
description: You can use Gemini Omni Flash or Veo on Gemini Enterprise Agent Platform to extend videos that you provide. Use either the {{dynamic_data.site_values.cloud_name_short}} console or the Agent Platform API to send a request.
data_source: docs.cloud.google.com
---

You can use Gemini Omni Flash or Veo on Gemini Enterprise Agent Platform to extend videos. The input video is limited between 1 and 30 seconds in length. Videos can be extended up to 40 seconds for Gemini Omni Flash or 37 seconds for Veo on Gemini Enterprise Agent Platform. You can extend videos using either the Google Cloud console or the Agent Platform API.

The following models support extending videos:

**Gemini Omni Flash**

#### Click to expand supported models

  - [`gemini-omni-1.1-flash-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash) preview

**Veo**

#### Click to expand supported models

  - [`veo-3.1-lite-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-lite-generate-001-preview) preview
  - [`veo-3.1-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-generate-001)
  - [`veo-3.1-fast-generate-001`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#3.1-fast-generate-001)

For information about writing effective text prompts for video generation, see the [Video prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide) .

## Before you begin

1.  Set up authentication for your environment.
    
    Select the tab for how you plan to use the samples on this page:
    
    ### Console
    
    When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.
    
    ### REST
    
    To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.
    
    For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Veo limitations

When using Veo to extend videos, input videos are subject to the following limitations:

  - The input file must be MP4.
  - The length must be 1 to 30 seconds.
  - The frame rate must be 24 frames per second.
  - The resolution must be one of: 720p, 1080p, or 4k.
  - The aspect ratio for input videos can be either 9:16 or 16:9.

When using Veo to extend videos, output videos are subject to the following limitations

  - The output file is MP4.
  - The extended length is 7 seconds.
  - The frame rate is 24 frames per second.
  - The resolution can be 720p, 1080p, or 4k.
  - The aspect ratio for output videos can be either 9:16 or 16:9.

## Extend videos using Gemini Omni Flash

To extend videos using Gemini Omni Flash, do the following:

### REST

Video generation can take over a minute to complete. To generate a video to download immediately after completion, use a synchronous request. To generate a video that you can download later, send an asynchronous request by setting the `background` parameter to `true` . Asynchronous requests are retained for up to 14 days.

For more information about using the Gemini Omni Flash API, seek [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .

### Synchronous request

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.
  - `  MODEL_ID  ` : A string representing the model ID to use. The following are accepted values:
      - `"gemini-omni-1.1-flash-preview"`
  - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
  - `  CLOUD_STORAGE_INPUT_URI  ` : A string representing the Cloud Storage bucket that contains the input media. For example: `"gs://video-bucket/input/"` .
  - `  CLOUD_STORAGE_OUTPUT_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .
  - `  ASPECT_RATIO  ` : Optional: A string representing the expected aspect ratio of the output video. If not provided, the aspect ratio is inferred from the prompt. The following are accepted values:
      - `"16:9"`
      - `"9:16"`
  - `  DURATION  ` : A string representing the length of the generated video files. Allowed strings are integers between `3` and `10` , followed by "s" for seconds. For example, `"10s"` .

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
          "task": "extend"
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
      "object":"interaction",
      "role":"model",
      "created":"2026-05-29T02:17:56Z",
      "updated":"2026-05-29T02:17:56Z",
    }

### Asynchronous request

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.
  - `  MODEL_ID  ` : A string representing the model ID to use. The following are accepted values:
      - `"gemini-omni-1.1-flash-preview"`
  - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
  - `  CLOUD_STORAGE_INPUT_URI  ` : A string representing the Cloud Storage bucket that contains the input media. For example: `"gs://video-bucket/input/"` .
  - `  CLOUD_STORAGE_OUTPUT_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .
  - `  ASPECT_RATIO  ` : Optional: A string representing the expected aspect ratio of the output video. If not provided, the aspect ratio is inferred from the prompt. The following are accepted values:
      - `"16:9"`
      - `"9:16"`
  - `  DURATION  ` : A string representing the length of the generated video files. Allowed strings are integers between `3` and `10` , followed by "s" for seconds. For example, `"10s"` .

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
          "task": "extend"
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

    GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID

To send your request, choose one of these options:

#### curl

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer TOKEN" \
         "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID"

#### PowerShell

Execute the following command:

    $headers = @{ "Authorization" = "Bearer TOKEN" }
    
    Invoke-WebRequest `
        -Method GET `
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

## Extend videos using Veo

The following examples show how you can extend a Veo video:

### Console

1.  In the Google Cloud console, go to the **Agent Platform \> Media Studio** page.

2.  Click **Video** .

3.  In the **Task** menu, select **Video extension** .

4.  From the **Model** menu, select a model from the displayed options.

5.  In the **Input video** section, click **Add** .

6.  In the **Prompt** box, enter a text prompt that describes the videos to generate.

7.  Optional: Adjust the following **Parameters** :
    
      - **Number of results** : adjust the slider or enter a value between **1** and **4** .
    
      - **Video length** : select a video length from the menu.

<!-- end list -->

  - **Output directory** : click **Browse** to create or select a [Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/buckets) to store the generated files.

<!-- end list -->

1.  Click **Run** .

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
    from google.genai.types import GenerateVideosConfig, Video
    
    client = genai.Client()
    
    # TODO(developer): Update and un-comment below line
    # output_gcs_uri = "gs://your-bucket/your-prefix"
    
    operation = client.models.generate_videos(
        model="veo-3.1-generate-preview",
        prompt="a butterfly flies in and lands on the flower",
        video=Video(
            uri="gs://cloud-samples-data/generative-ai/video/flower.mp4",
            mime_type="video/mp4",
        ),
        config=GenerateVideosConfig(
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

1.  Use the following command to send a video generation request. This request begins a long-running operation and stores output to a Cloud Storage bucket you specify.
    
    Before using any of the request data, make the following replacements:
    
      - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.
    
      - `  MODEL_ID  ` : A string that represents the model ID to use. Use one of the following when specifying a first or last video frame:
        
          - **Veo 3: `veo-3.1-generate-001`**
          - **Veo 3: `veo-3.1-fast-generate-001`**
    
      - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.
    
      - `  PATH_TO_VIDEO  ` : A string that represents the Cloud Storage path to the Veo video that you're extending. For example: `"gs://video-bucket/input/veo-video.mp4"` .
    
      - `  OUTPUT_STORAGE_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .
    
      - `  RESPONSE_COUNT  ` : The number of video files to generate. The accepted range of values is `1` - `4` .
    
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
               "video": {
                 "gcsUri": "PATH_TO_VIDEO",
                 "mimeType": "video/mp4"
               }
            }
          ],
          "parameters": {
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

  - [Best practices for generating videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice)

  - [Generate videos from text prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)

  - [Generate videos from an image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)

  - [Generate videos using first and last video frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)

  - [Generate videos from references](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references)

  - [Edit videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/edit-videos)

  - [Understand responsible AI and usage guidelines for Veo on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines)
