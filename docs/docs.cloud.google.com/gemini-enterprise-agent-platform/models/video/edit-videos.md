---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/edit-videos
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/edit-videos
title: Edit videos
description: You can use Gemini Omni Flash to edit videos that you provide. Use either the {{dynamic_data.site_values.cloud_name_short}} console or the Agent Platform API to send a request.
data_source: docs.cloud.google.com
---

You can use Gemini Omni Flash to edit videos by using the Google Cloud console or the Agent Platform API.

The following models support editing videos:

#### Click to expand supported models

  - [`gemini-omni-flash-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-flash-preview) preview
  - [`gemini-omni-1.1-flash-preview`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash) preview

For information about writing effective text prompts for video generation, see the [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide) .

## Before you begin

1.  Set up authentication for your environment.
    
    Select the tab for how you plan to use the samples on this page:
    
    ### Console
    
    When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.
    
    ### REST
    
    To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.
    
    For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Edit videos using Gemini Omni Flash

To edit videos using Gemini Omni Flash, do the following:

### REST

Video generation can take over a minute to complete. To generate a video to download immediately after completion, use a synchronous request. To generate a video that you can download later, send an asynchronous request by setting the `background` parameter to `true` . Asynchronous requests are retained for up to 14 days.

For more information about using the Gemini Omni Flash API, seek [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .

### Synchronous request

Before using any of the request data, make the following replacements:

  - `  PROJECT_ID  ` : A string representing your Google Cloud project ID.

  - `  MODEL_ID  ` : A string representing the model ID to use. The following are accepted values:
    
      - `"gemini-omni-flash-preview"`
      - `"gemini-omni-1.1-flash-preview"`

  - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.

  - `  CLOUD_STORAGE_VIDEO_URI  ` : A string representing the Cloud Storage bucket that contains the input video. For example: `"gs://video-bucket/input/"` .

  - `  VIDEO_MIME  ` : A string representing a video MIME type. The following are accepted values:
    
      - `video/3gpp`
      - `video/mp4`
      - `video/mpeg`
      - `video/quicktime`
      - `video/webm`
      - `video/x-flv`
      - `video/x-ms-wmv`

  - `  OUTPUT_RESOLUTION  ` :
    
    Optional: A string representing the video output resolution. If not provided, the output defaults to 720p.
    
    `gemini-omni-1.1-flash-preview` supports the following values:
    
      - `"360p"`
      - `"720p"`
      - `"1080p"`
      - `"4k"`
    
    `gemini-omni-flash-preview` only supports `"720p"` .

  - `  CLOUD_STORAGE_OUTPUT_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .

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
          "type": "video",
          "uri": "CLOUD_STORAGE_VIDEO_URI",
          "mime_type": "VIDEO_MIME"
        }
      ],
      "response_format": [
        {
          "type": "video",
          "delivery": "uri",
          "output": "OUTPUT_RESOLUTION",
          "gcs_uri": "CLOUD_STORAGE_OUTPUT_URI"
        }
      ],
      "generation_config": {
        "video_config": {
          "task": "edit"
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
      - `"gemini-omni-flash-preview"`

  - `  TEXT_PROMPT  ` : The text prompt used to guide video generation.

  - `  CLOUD_STORAGE_VIDEO_URI  ` : A string representing the Cloud Storage bucket that contains the input video. For example: `"gs://video-bucket/input/"` .

  - `  VIDEO_MIME  ` : A string representing a video MIME type. The following are accepted values:
    
      - `video/3gpp`
      - `video/mp4`
      - `video/mpeg`
      - `video/quicktime`
      - `video/webm`
      - `video/x-flv`
      - `video/x-ms-wmv`

  - `  OUTPUT_RESOLUTION  ` :
    
    Optional: A string representing the video output resolution. If not provided, the output defaults to 720p.
    
    `gemini-omni-1.1-flash-preview` supports the following values:
    
      - `"360p"`
      - `"720p"`
      - `"1080p"`
      - `"4k"`
    
    `gemini-omni-flash-preview` only supports `"720p"` .

  - `  CLOUD_STORAGE_OUTPUT_URI  ` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .

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
          "type": "video",
          "uri": "CLOUD_STORAGE_VIDEO_URI",
          "mime_type": "VIDEO_MIME"
        }
      ],
      "response_format": [
        {
          "type": "video",
          "delivery": "uri",
          "resolution": "OUTPUT_RESOLUTION",
          "gcs_uri": "CLOUD_STORAGE_OUTPUT_URI"
        }
      ],
      "generation_config": {
        "video_config": {
          "task": "edit"
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

## What's next

  - [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide)

  - [Best practices for generating videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice)

  - [Generate videos from text prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)

  - [Generate videos from an image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)

  - [Generate videos using first and last video frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)

  - [Generate videos from references](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references)

  - [Understand responsible AI and usage guidelines for Veo on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines)
