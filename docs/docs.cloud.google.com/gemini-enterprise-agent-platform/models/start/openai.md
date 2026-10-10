---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/openai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/openai
title: OpenAI compatibility
description: Integrate Gemini models using OpenAI libraries and REST API. Implement Google Cloud auth, thinking, streaming, function calling, and multimodal features.
data_source: docs.cloud.google.com
---

Gemini models are accessible using the OpenAI libraries (Python, TypeScript, and JavaScript) along with the REST API. Only Google Cloud Auth is supported using the OpenAI library in Gemini Enterprise Agent Platform. If you aren't already using the OpenAI libraries, call the [Gemini API](https://ai.google.dev/gemini-api/docs/quickstart) directly. If you are using OpenAI libraries and want to migrate to Agent Platform SDKs, see [Migrate from OpenAI SDK to Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/migrate-code) .

### Python

```
import openai
from google.auth import default
import google.auth.transport.requests

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token
)

response = client.chat.completions.create(
  model="google/gemini-3.5-flash",
  messages=[
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Explain to me how AI works"}
  ]
)

print(response.choices[0].message)
```

Note the following differences from standard OpenAI client configuration:

- **`api_key=credentials.token`** : Uses an OAuth access token obtained from Google Cloud Application Default Credentials.

- **`base_url`** : Directs the OpenAI library to send requests to the Agent Platform OpenAI-compatible endpoint instead of the default URL.

- **`model="google/gemini-3.5-flash"`** : Selects a compatible Gemini model hosted on Agent Platform.

## Thinking

Gemini 3 models generate an internal reasoning process before returning a response, improving performance on complex multi-step tasks. In the Gemini API, the [`thinking_level` parameter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#gemini-3-and-later-models) controls reasoning depth across discrete tiers ( `MINIMAL` , `LOW` , `MEDIUM` , and `HIGH` ).

In the OpenAI-compatible Chat Completions API, you control reasoning depth with the `reasoning_effort` parameter ( `"minimal"` , `"low"` , `"medium"` , or `"high"` ), which maps to the corresponding `thinking_level` setting for Gemini 3 models.

Omitting `reasoning_effort` uses the model's default thinking configuration.

For direct control over thinking configuration parameters from the OpenAI-compatible API, use [`extra_body.google.thinking_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview#gemini-specific-parameters) .

### Python

```
import openai
from google.auth import default
import google.auth.transport.requests

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token
)

response = client.chat.completions.create(
  model="google/gemini-3.5-flash",
  reasoning_effort="low",
  messages=[
      {"role": "system", "content": "You are a helpful assistant."},
      {
          "role": "user",
          "content": "Explain to me how AI works"
      }
  ]
)
print(response.choices[0].message)
```

## Streaming

The Gemini API supports [streaming responses](https://ai.google.dev/gemini-api/docs/text-generation?lang=python#generate-a-text-stream) .

### Python

```
import openai
from google.auth import default
import google.auth.transport.requests

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token
)
response = client.chat.completions.create(
  model="google/gemini-3.5-flash",
  messages=[
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ],
  stream=True
)

for chunk in response:
  print(chunk.choices[0].delta)
```

## Function calling

Function calling makes it easier to get structured data outputs from generative models and is [supported in the Gemini API](https://ai.google.dev/gemini-api/docs/function-calling/tutorial) .

### Python

```
import openai
from google.auth import default
import google.auth.transport.requests

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token
)

tools = [
  {
    "type": "function",
    "function": {
      "name": "get_weather",
      "description": "Get the weather in a given location",
      "parameters": {
        "type": "object",
        "properties": {
          "location": {
            "type": "string",
            "description": "The city and state, e.g. Chicago, IL",
          },
          "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]},
        },
        "required": ["location"],
      },
    }
  }
]

messages = [{"role": "user", "content": "What's the weather like in Chicago today?"}]
response = client.chat.completions.create(
  model="google/gemini-3.5-flash",
  messages=messages,
  tools=tools,
  tool_choice="auto"
)

print(response)
```

## Image understanding

Gemini models are natively multimodal and support [many common vision tasks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-understanding) .

### Python

```
from google.auth import default
import google.auth.transport.requests

import base64
from openai import OpenAI

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token,
)

# Function to encode the image
def encode_image(image_path):
  with open(image_path, "rb") as image_file:
    return base64.b64encode(image_file.read()).decode('utf-8')

# Getting the base64 string
# base64_image = encode_image("Path/to/image.jpeg")

response = client.chat.completions.create(
  model="google/gemini-3.5-flash",
  messages=[
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "What is in this image?",
        },
        {
          "type": "image_url",
          "image_url": {
            "url":  f"data:image/jpeg;base64,{base64_image}"
          },
        },
      ],
    }
  ],
)

print(response.choices[0])
```

## Generate an image

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
cat > request.json << 'EOF'
{
  "model": "google/gemini-3.1-flash-image",
  "messages": [{
    "role": "user",
    "content": "Generate an image of a banana."
  }],
  "modalities": ["image", "text"]
}
EOF
```

Then execute the following command to send your REST request:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/chat/completions"
```

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
@'
{
  "model": "google/gemini-3.1-flash-image",
  "messages": [{
    "role": "user",
    "content": "Generate an image of a banana."
  }],
  "modalities": ["image", "text"]
}
'@  | Out-File -FilePath request.json -Encoding utf8
```

Then execute the following command to send your REST request:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/chat/completions" | Select-Object -Expand Content
```

You should receive a JSON response similar to the following:

```
{
  "choices": [{
    "finish_reason": "stop",
    "index": 0,
    "image": {
      "data":"IMAGE_DATA",
      "extra_content": {
        "google": {
          "mime_type":"image/png"
        }
      }
    },
    "content":"Here is an image of a banana: ",
    "role":"assistant"
  }],
  "created":1757099999,
  "id":"sample_response_id",
  "model":"google/gemini-3.1-flash-image",
  "object":"chat.completion",
  "system_fingerprint":"",
  "usage": {
    "completion_tokens":1299,
    "prompt_tokens":7,
    "total_tokens":1306
  }
}
```

## Audio understanding

The following sample shows how to analyze audio input:

### Python

```
from google.auth import default
import google.auth.transport.requests

import base64
from openai import OpenAI

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token,
)

with open("/path/to/your/audio/file.wav", "rb") as audio_file:
  base64_audio = base64.b64encode(audio_file.read()).decode('utf-8')

response = client.chat.completions.create(
  model="google/gemini-3.5-flash",
  messages=[
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "Transcribe this audio",
        },
        {
              "type": "input_audio",
              "input_audio": {
                "data": base64_audio,
                "format": "wav"
          }
        }
      ],
    }
  ],
)

print(response.choices[0].message.content)
```

## Structured output

Gemini models can output JSON objects in any [structure you define](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output#googlegenaisdk_ctrlgen_with_resp_schema-python_genai_sdk) .

### Python

```
from google.auth import default
import google.auth.transport.requests

from pydantic import BaseModel
from openai import OpenAI

# TODO(developer): Update and un-comment below lines
# project_id = "PROJECT_ID"
# location = "global"

# Programmatically get an access token
credentials, _ = default(scopes=["https://www.googleapis.com/auth/cloud-platform"])
credentials.refresh(google.auth.transport.requests.Request())

# OpenAI Client
client = openai.OpenAI(
  base_url=f"https://aiplatform.googleapis.com/v1/projects/{project_id}/locations/{location}/endpoints/openapi",
  api_key=credentials.token,
)

class CalendarEvent(BaseModel):
  name: str
  date: str
  participants: list[str]

completion = client.beta.chat.completions.parse(
  model="google/gemini-3.5-flash",
  messages=[
      {"role": "system", "content": "Extract the event information."},
      {"role": "user", "content": "John and Susan are going to an AI conference on Friday."},
  ],
  response_format=CalendarEvent,
)

print(completion.choices[0].message.parsed)
```

## Current limitations

Consider the following limitation when using the OpenAI-compatible API:

- Access tokens live for 1 hour by default. After expiration, they must be refreshed. For more information, see [Refresh your credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials#refresh-credentials) .

## What's next

- Use the [Google Gen AI Libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries) to call Gemini models directly.

- See more examples using the [Chat Completions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/examples) with the OpenAI-compatible syntax.

- See supported Gemini models and parameters in [Using OpenAI libraries with Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview) .
