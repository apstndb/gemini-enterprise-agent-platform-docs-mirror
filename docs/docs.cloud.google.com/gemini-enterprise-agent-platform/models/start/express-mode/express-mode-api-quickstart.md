---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/express-mode-api-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/express-mode-api-quickstart
title: 'Tutorial: Agent Platform API in express mode'
description: Agent Platform API in express mode
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> To see an example of Agent Platform in Express Mode, run the "Getting started with Gemini using Agent Platform in Express Mode" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_express.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_gemini_express.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_gemini_express.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_express.ipynb)

Gemini Enterprise Agent Platform in [express mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/overview) lets you try core generative AI features available on Agent Platform. This tutorial shows you how to complete the following tasks by using the Agent Platform API in express mode:

- Install and initialize the Google Gen AI SDK for express mode.

- Send a request to the Gemini for Google Cloud API, including the following:

  - Streaming request
  - Non-streaming request
  - Function calling request

## Before you begin

Before performing the tasks described in this document, [sign up for express mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/overview#eligibility) .

## Install and initialize the SDK for express mode

The Google Gen AI SDK lets you use Google generative AI models and features to build AI-powered applications. When using Agent Platform in express mode, install and initialize the `google-genai` package to authenticate using your generated API key.

### Install

To install the Google Gen AI SDK for express mode, run the following commands:

```
# Developer TODO: If you're using Colab, uncomment the following lines:
# from google.colab import auth
# auth.authenticate_user()

!pip install --upgrade google-genai
```

If you're using Colaboratory, restart the runtime after installation if prompted.

### Initialize

Configure the API key for express mode and initialize the client with `enterprise=True` . For details about getting an API key, see [Agent Platform in express mode overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/overview) .

```
from google import genai
from google.genai import types

# Developer TODO: Replace YOUR_API_KEY with your API key.
API_KEY = "YOUR_API_KEY"

client = genai.Client(
    enterprise=True, api_key=API_KEY
)
```

## Send a request to the Gemini for Google Cloud API

You can send either streaming or non-streaming requests to the Gemini for Google Cloud API. Streaming requests return the response in chunks as the request is processed. Non-streaming requests return the complete response after processing finishes.

### Streaming request

To send a streaming request, call `client.models.generate_content_stream()` and print each chunk as it arrives:

```
from google import genai
from google.genai import types

def generate():
  client = genai.Client(enterprise=True, api_key="YOUR_API_KEY")

  config = types.GenerateContentConfig(
      thinking_config=types.ThinkingConfig(
          thinking_level="MEDIUM",
      ),
      seed=5,
      max_output_tokens=1024,
      stop_sequences=["STOP!"],
      safety_settings=[
          types.SafetySetting(
              category="HARM_CATEGORY_HATE_SPEECH",
              threshold="BLOCK_ONLY_HIGH",
          )
      ],
  )
  for chunk in client.models.generate_content_stream(
      model="gemini-3.8-flash",
      contents="Explain bubble sort to me",
      config=config,
  ):
    print(chunk.text, end="")

generate()
```

### Non-streaming request

The following code sample defines a function that sends a non-streaming request to Gemini 3.8 Flash ( `gemini-3.8-flash` ). It shows you how to configure thinking level, output parameters, and safety settings:

```
from google import genai
from google.genai import types

def generate():
  client = genai.Client(enterprise=True, api_key="YOUR_API_KEY")

  config = types.GenerateContentConfig(
      thinking_config=types.ThinkingConfig(
          thinking_level="MEDIUM",
      ),
      seed=5,
      max_output_tokens=1024,
      stop_sequences=["STOP!"],
      safety_settings=[
          types.SafetySetting(
              category="HARM_CATEGORY_HATE_SPEECH",
              threshold="BLOCK_ONLY_HIGH",
          )
      ],
  )
  response = client.models.generate_content(
      model="gemini-3.8-flash",
      contents="Explain bubble sort to me",
      config=config,
  )
  print(response.text)

generate()
```

### Function calling request

The following code sample declares a function tool, sends an initial prompt to 3.8 Flash, receives a function call part in the response, and then sends the matching `FunctionResponse` back to the model to generate a final response:

```
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, api_key="YOUR_API_KEY")

get_weather_declaration = types.FunctionDeclaration(
    name="get_current_weather",
    description="Gets the current weather in a given city.",
    parameters={
        "type": "OBJECT",
        "properties": {
            "location": {
                "type": "STRING",
                "description": "The city and state, such as Boston, MA.",
            },
            "unit": {
                "type": "STRING",
                "enum": ["C", "F"],
            },
        },
        "required": ["location"],
    },
)
tools = [types.Tool(function_declarations=[get_weather_declaration])]

prompt = "What is the weather in Boston?"
first_response = client.models.generate_content(
    model="gemini-3.8-flash",
    contents=prompt,
    config=types.GenerateContentConfig(tools=tools),
)

function_call = first_response.function_calls[0]
contents = [
    types.Content(role="user", parts=[types.Part(text=prompt)]),
    first_response.candidates[0].content,
    types.Content(
        role="user",
        parts=[
            types.Part(
                function_response=types.FunctionResponse(
                    id=function_call.id,
                    name=function_call.name,
                    response={"weather": "sunny", "temperature": "72F"},
                )
            )
        ],
    ),
]

response = client.models.generate_content(
    model="gemini-3.8-flash",
    contents=contents,
    config=types.GenerateContentConfig(tools=tools),
)
print(response.text)
```

## Clean up

This tutorial does not create any Google Cloud resources, so no cleanup is required to avoid charges.

## What's next

- Try the [Agent Studio tutorial](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/studio-express-mode-quickstart) for Agent Platform in express mode.
- See the complete [API reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/api-reference) for Agent Platform in express mode.
