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

    [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

    If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

    For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Edit videos using Gemini Omni Flash

To edit videos using Gemini Omni Flash, do the following:

### REST

Video generation can take over a minute to complete. You can choose from several interaction modes depending on your workflow:

- **Synchronous: stateless** : Generate a video in a single request without persisting the interaction state on the server.
- **Synchronous: stateful** : Set `store` to `true` to persist the interaction state, which lets you retrieve the result later or reference the interaction ID for multi-turn video editing.
- **Synchronous: stateful streaming** : Set both `store` and `stream` to `true` to receive model thoughts incrementally as they are generated, followed by the output video.
- **Asynchronous** : Set `background` to `true` to run video generation in the background and retrieve the result later using the interaction ID.

Stored and asynchronous interactions are retained for up to 14 days.

For more information about using the Gemini Omni Flash API, see [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .

### Synchronous: stateless

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.

- `MODEL_ID` : A string representing the model ID to use. The following are accepted values:
  - `"gemini-omni-flash-preview"`
  - `"gemini-omni-1.1-flash-preview"`

- `TEXT_PROMPT` : The text prompt used to guide video generation.

- `CLOUD_STORAGE_VIDEO_URI` : A string representing the Cloud Storage bucket that contains the input video. For example: `"gs://video-bucket/input/"` .

- `VIDEO_MIME` : A string representing a video MIME type. The following are accepted values:
  - `video/3gpp`
  - `video/mp4`
  - `video/mpeg`
  - `video/quicktime`
  - `video/webm`
  - `video/x-flv`
  - `video/x-ms-wmv`

- `OUTPUT_RESOLUTION` :

  Optional: A string representing the video output resolution. If not provided, the output defaults to 720p.

  `gemini-omni-1.1-flash-preview` supports the following values:

  - `"360p"`
  - `"720p"`
  - `"1080p"`
  - `"4k"`

  `gemini-omni-flash-preview` only supports `"720p"` .

- `CLOUD_STORAGE_OUTPUT_URI` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer TOKEN" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions"
```

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content
```

The response contains an interaction which includes the model thoughts and an output video.

```
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
```

### Synchronous: stateful

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.

- `MODEL_ID` : A string representing the model ID to use. The following are accepted values:
  - `"gemini-omni-flash-preview"`
  - `"gemini-omni-1.1-flash-preview"`

- `TEXT_PROMPT` : The text prompt used to guide video generation.

- `CLOUD_STORAGE_VIDEO_URI` : A string representing the Cloud Storage bucket that contains the input video. For example: `"gs://video-bucket/input/"` .

- `VIDEO_MIME` : A string representing a video MIME type. The following are accepted values:
  - `video/3gpp`
  - `video/mp4`
  - `video/mpeg`
  - `video/quicktime`
  - `video/webm`
  - `video/x-flv`
  - `video/x-ms-wmv`

- `OUTPUT_RESOLUTION` :

  Optional: A string representing the video output resolution. If not provided, the output defaults to 720p.

  `gemini-omni-1.1-flash-preview` supports the following values:

  - `"360p"`
  - `"720p"`
  - `"1080p"`
  - `"4k"`

  `gemini-omni-flash-preview` only supports `"720p"` .

- `CLOUD_STORAGE_OUTPUT_URI` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions
```

Request JSON body:

```
{
  "model": "MODEL_ID",
  "background": false,
  "store": true,
  "stream": false,
  "input": [
    {
      "type": "user_input",
      "content": [
        {
          "type": "text",
          "text": "TEXT_PROMPT"
        },
        {
          "type": "video",
          "uri": "CLOUD_STORAGE_VIDEO_URI",
          "mime_type": "VIDEO_MIME"
        }
      ]
    }
  ],
  "response_format": [
    {
      "type": "video",
      "delivery": "uri",
      "resolution": "OUTPUT_RESOLUTION",
      "gcs_uri": "CLOUD_STORAGE_OUTPUT_URI"
    }
  ]
}
```

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer TOKEN" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions"
```

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content
```

The response contains an interaction which includes the model thoughts and an output video.

```
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
```

Use the ` INTERACTION_ID ` to get the generated video:

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.
- `INTERACTION_ID` : The interaction ID from the asynchronous request.

HTTP method and URL:

```
GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID
```

To send your request, choose one of these options:

#### curl

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer TOKEN" \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID"
```

#### PowerShell

Execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID" | Select-Object -Expand Content
```

The response is in a format similar to the following:

```
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
```

### Synchronous: stateful streaming

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.

- `MODEL_ID` : A string representing the model ID to use. The following are accepted values:
  - `"gemini-omni-flash-preview"`
  - `"gemini-omni-1.1-flash-preview"`

- `TEXT_PROMPT` : The text prompt used to guide video generation.

- `CLOUD_STORAGE_VIDEO_URI` : A string representing the Cloud Storage bucket that contains the input video. For example: `"gs://video-bucket/input/"` .

- `VIDEO_MIME` : A string representing a video MIME type. The following are accepted values:
  - `video/3gpp`
  - `video/mp4`
  - `video/mpeg`
  - `video/quicktime`
  - `video/webm`
  - `video/x-flv`
  - `video/x-ms-wmv`

- `OUTPUT_RESOLUTION` :

  Optional: A string representing the video output resolution. If not provided, the output defaults to 720p.

  `gemini-omni-1.1-flash-preview` supports the following values:

  - `"360p"`
  - `"720p"`
  - `"1080p"`
  - `"4k"`

  `gemini-omni-flash-preview` only supports `"720p"` .

- `CLOUD_STORAGE_OUTPUT_URI` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions
```

Request JSON body:

```
{
  "model": "MODEL_ID",
  "background": false,
  "store": true,
  "stream": true,
  "input": [
    {
      "type": "user_input",
      "content": [
        {
          "type": "text",
          "text": "TEXT_PROMPT"
        },
        {
          "type": "video",
          "uri": "CLOUD_STORAGE_VIDEO_URI",
          "mime_type": "VIDEO_MIME"
        }
      ]
    }
  ],
  "response_format": [
    {
      "type": "video",
      "delivery": "uri",
      "resolution": "OUTPUT_RESOLUTION",
      "gcs_uri": "CLOUD_STORAGE_OUTPUT_URI"
    }
  ]
}
```

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer TOKEN" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions"
```

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content
```

The response contains an interaction which includes the model thoughts and an output video.

```
event: interaction.created
data: {"interaction":{"id":"INTERACTION_ID","status":"in_progress","object":"interaction","model":"gemini-omni-flash-preview"},"event_type":"interaction.created"}

event: interaction.status_update
data: {"interaction_id":"INTERACTION_ID","status":"in_progress","event_type":"interaction.status_update"}

event: step.start
data: {"index":0,"step":{"type":"thought"},"event_type":"step.start"}

event: step.delta
data: {"index":0,"delta":{"content":{"text":"MODEL THOUGHTS","type":"text"},"type":"thought_summary"},"event_id":"EVENT_ID","event_type":"step.delta"}

event: step.delta
data: {"index":0,"delta":{"content":{"text":"MODEL THOUGHTS","type":"text"},"type":"thought_summary"},"event_id":"EVENT_ID","event_type":"step.delta"}

event: step.delta
data: {"index":0,"delta":{"signature":"...","type":"thought_signature"},"event_type":"step.delta"}

event: step.stop
data: {"index":0,"event_type":"step.stop"}

event: step.start
data: {"index":1,"step":{"type":"model_output"},"event_type":"step.start"}

event: step.delta
data: {"index":1,"delta":{"mime_type":"video/mp4","uri":"gs://some/output_path/123.mp4","type":"video"},"event_id":"EVENT_ID","event_type":"step.delta"}

event: step.stop
data: {"index":1,"event_type":"step.stop"}

event: interaction.completed
data: {"interaction":{"id":"INTERACTION_ID","status":"completed","usage":{"total_tokens":17812,"total_input_tokens":21,"input_tokens_by_modality":[{"modality":"text","tokens":21}],"total_output_tokens":17376,"output_tokens_by_modality":[{"modality":"video","tokens":17376}],"total_thought_tokens":415},"created":"2026-08-12T21:26:20Z","updated":"2026-08-12T21:26:20Z","event_id":"EVENT_ID","object":"interaction","model":"gemini-omni-flash-preview"},"event_id":"EVENT_ID","event_type":"interaction.completed"}

event: done
data: [DONE]
```

Use the ` INTERACTION_ID ` with \`?stream=true\` to stream the stored interaction and generated video:

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.
- `INTERACTION_ID` : The interaction ID from the request.

HTTP method and URL:

```
GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID?stream=true
```

To send your request, choose one of these options:

#### curl

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer TOKEN" \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID?stream=true"
```

#### PowerShell

Execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID?stream=true" | Select-Object -Expand Content
```

The response is a stream of Server-Sent Events (SSE) in a format similar to the following:

```
event: interaction.created
data: {"interaction":{"id":"INTERACTION_ID","status":"in_progress","object":"interaction","model":"gemini-omni-flash-preview"},"event_type":"interaction.created"}

event: interaction.status_update
data: {"interaction_id":"INTERACTION_ID","status":"in_progress","event_type":"interaction.status_update"}

event: step.start
data: {"index":0,"step":{"type":"thought"},"event_type":"step.start"}

event: step.delta
data: {"index":0,"delta":{"content":{"text":"MODEL THOUGHTS","type":"text"},"type":"thought_summary"},"event_id":"EVENT_ID","event_type":"step.delta"}

event: step.delta
data: {"index":0,"delta":{"content":{"text":"MODEL THOUGHTS","type":"text"},"type":"thought_summary"},"event_id":"EVENT_ID","event_type":"step.delta"}

event: step.delta
data: {"index":0,"delta":{"signature":"...","type":"thought_signature"},"event_type":"step.delta"}

event: step.stop
data: {"index":0,"event_type":"step.stop"}

event: step.start
data: {"index":1,"step":{"type":"model_output"},"event_type":"step.start"}

event: step.delta
data: {"index":1,"delta":{"mime_type":"video/mp4","uri":"gs://some/output_path/123.mp4","type":"video"},"event_id":"EVENT_ID","event_type":"step.delta"}

event: step.stop
data: {"index":1,"event_type":"step.stop"}

event: interaction.completed
data: {"interaction":{"id":"INTERACTION_ID","status":"completed","usage":{"total_tokens":17664,"total_input_tokens":21,"input_tokens_by_modality":[{"modality":"text","tokens":21}],"total_output_tokens":17376,"output_tokens_by_modality":[{"modality":"video","tokens":17376}],"total_thought_tokens":267},"created":"2026-08-12T21:33:08Z","updated":"2026-08-12T21:33:08Z","event_id":"EVENT_ID","object":"interaction","model":"gemini-omni-flash-preview"},"event_id":"EVENT_ID","event_type":"interaction.completed"}

event: done
data: [DONE]
```

### Asynchronous

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.

- `MODEL_ID` : A string representing the model ID to use. The following are accepted values:
  - `"gemini-omni-1.1-flash-preview"`
  - `"gemini-omni-flash-preview"`

- `TEXT_PROMPT` : The text prompt used to guide video generation.

- `CLOUD_STORAGE_VIDEO_URI` : A string representing the Cloud Storage bucket that contains the input video. For example: `"gs://video-bucket/input/"` .

- `VIDEO_MIME` : A string representing a video MIME type. The following are accepted values:
  - `video/3gpp`
  - `video/mp4`
  - `video/mpeg`
  - `video/quicktime`
  - `video/webm`
  - `video/x-flv`
  - `video/x-ms-wmv`

- `OUTPUT_RESOLUTION` :

  Optional: A string representing the video output resolution. If not provided, the output defaults to 720p.

  `gemini-omni-1.1-flash-preview` supports the following values:

  - `"360p"`
  - `"720p"`
  - `"1080p"`
  - `"4k"`

  `gemini-omni-flash-preview` only supports `"720p"` .

- `CLOUD_STORAGE_OUTPUT_URI` : Optional: A string representing the Cloud Storage bucket to store the output videos. If not provided, video bytes are returned in the response. For example: `"gs://video-bucket/output/"` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer TOKEN" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions"
```

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content
```

The response contains an interaction ID, which you'll use to get the video you generated.

```
{
  "id":"INTERACTION_ID",
  "status":"in_progress",
  "object":"interaction"
}
```

Later, use the ` INTERACTION_ID ` to get the generated video:

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : A string representing your Google Cloud project ID.
- `INTERACTION_ID` : The interaction ID from the asynchronous request.

HTTP method and URL:

```
GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID
```

To send your request, choose one of these options:

#### curl

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer TOKEN" \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID"
```

#### PowerShell

Execute the following command:

```
$headers = @{ "Authorization" = "Bearer TOKEN" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID" | Select-Object -Expand Content
```

The response is in a format similar to the following:

```
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
```

## What's next

- [Video generation prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide)

- [Best practices for generating videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/best-practice)

- [Generate videos from text prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)

- [Generate videos from an image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)

- [Generate videos using first and last video frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)

- [Generate videos from references](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references)

- [Understand responsible AI and usage guidelines for Veo on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/responsible-ai-and-usage-guidelines)
