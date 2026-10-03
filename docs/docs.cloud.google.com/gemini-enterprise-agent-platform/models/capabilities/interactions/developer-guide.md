---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide
title: Interactions API developer guide
description: Learn how to authenticate, connect to, and use the stateful Interactions API on Gemini Enterprise Agent Platform for multi-turn conversations, streaming, structured output, function calling, and long-running agent tasks.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> To see an example of how to use the Interactions API, run the "Gemini API: Getting started with Interactions API" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_interactions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_interactions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_interactions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_interactions_api.ipynb)

The Interactions API provides a unified, stateful interface for building generative AI applications with Gemini models and autonomous agents on Gemini Enterprise Agent Platform. Use the Interactions API to run multi-turn conversations, stream real-time responses, enforce structured outputs, execute function calls, and orchestrate long-running background tasks.

This guide shows you how to install the Google Gen AI SDK, authenticate your client, and implement common interaction workflows. For conceptual details about the interaction lifecycle, see the [Interactions API overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) .

## Before you begin

Before you send requests to the Interactions API, set up your Google Cloud project and development environment:

### Key concepts

Review the following concepts to understand how the Interactions API manages state and responses:

- **`Interaction`** : The Interactions API centers around a core resource: an `Interaction` . An `Interaction` represents a complete turn in a conversation or task, tracking the chronology of model thoughts, tool calls, and final outputs. It provides a unified envelope for prompt-response interactions and complex, multi-step agent workflows.
- **Stateful retention** : Interactions are stored server-side by default ( `store=True` in Python or `store: true` in TypeScript/JavaScript). Stored interactions persist for 7 days and are automatically deleted after that time. Setting `store=False` opts into stateless mode, which disables server-side retention and is Zero Data Retention (ZDR) compliant. Stateless mode also disables `previous_interaction_id` chaining and asynchronous execution ( `background=True` ).
- **Response helpers** : Google Gen AI SDK version `2.3.0` and later provides convenience properties on the interaction response, including `interaction.output_text` , `interaction.output_image` , and `interaction.output_audio` . Use `interaction.output_text` to read text responses instead of manually indexing into the steps array (such as `interaction.steps[-1].content[0].text` ).

### Requirements

Ensure your environment and requests meet the following requirements before integrating with the Interactions API:

- **SDK version support** : Use the unified Google Gen AI SDK ( `>= 2.3.0` for Python or `@google/genai >= 2.3.0` for TypeScript and JavaScript).

  - Version `2.3.0` or later is required for response helper properties and agent capabilities, while version 2.0.0 supports the base `steps` schema.
  - Legacy SDKs ( `google-cloud-aiplatform` , `@google-cloud/vertexai` , and `google-generativeai` ) don't support the Interactions API.

- **Supported models** : Use supported Gemini 3 models or later. Earlier model families don't support this API. For a complete list of supported models, see [Supported models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions#supported-models) and [Migrate to the latest model versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate) .

- **Turn-scoped parameters** : Configuration parameters such as `tools` , `system_instruction` , and `generation_config` apply only to the current turn. Pass these parameters on each subsequent interaction turn if your workflow requires them across a multi-turn conversation.

> **Tip:** If you use an AI coding assistant, you can install the Interactions API agent skill from the [`google/skills` GitHub repository](https://github.com/google/skills/blob/main/skills/cloud/gemini-interactions-api/SKILL.md) .

## Install the Google Gen AI SDK

Install or upgrade the Google Gen AI SDK ( `>= 2.3.0` ) for your preferred language:

### Python

```
pip install --upgrade "google-genai>=2.3.0"
```

### TypeScript / JavaScript

```
npm install "@google/genai>=2.3.0"
```

## Authenticate your client

You can connect to the Interactions API on Agent Platform using either of the following authentication methods:

- [Google Cloud project with Application Default Credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#connect-adc)
- [Express mode with an API key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#connect-api-key)

### Connect using a Google Cloud project with Application Default Credentials (ADC)

We recommend using this authentication method for enterprise workloads and production deployments on Google Cloud. To authenticate with Application Default Credentials (ADC), initialize the client with the following properties:

- `enterprise=True`
- `project= Google Cloud project ID`
- `location="global"`

If you haven't configured local credentials yet, run `gcloud auth application-default login` .

In the following code sample, replace ` PROJECT_ID ` with your Google Cloud project ID.

> **Note:** The code samples use `gemini-3.8-flash` as an example. For the most appropriate model identifier for your use case, see [Supported models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions#supported-models) .

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

interaction = client.interactions.create(
    model="gemini-3.8-flash",
    input="Explain serverless computing in one sentence.",
)

print(interaction.output_text)
```

### TypeScript / JavaScript

```
import { GoogleGenAI } from "@google/genai";

const ai = new GoogleGenAI({
    enterprise: true,
    project: "PROJECT_ID",
    location: "global",
});

const interaction = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "Explain serverless computing in one sentence.",
});

console.log(interaction.output_text);
```

### REST

```
curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": [{
      "role": "user",
      "content": [{
        "type": "text",
        "text": "Explain serverless computing in one sentence."
      }]
    }]
  }'
```

> **Tip:** You can also configure the SDK using environment variables so that `genai.Client()` resolves your project settings automatically without inline arguments: `export GOOGLE_GENAI_USE_ENTERPRISE=true` , `export GOOGLE_CLOUD_PROJECT=" `` PROJECT_ID `` "` , and `export GOOGLE_CLOUD_LOCATION="global"` .

### Connect using express mode (API key)

We recommend using this authentication method for rapid prototyping, lightweight scripts, or environments that authenticate with an API key. Pass your API key when initializing the client or in the `x-goog-api-key` HTTP header.

In the following code sample, replace ` API_KEY ` with your API key.

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    api_key="API_KEY",
)

interaction = client.interactions.create(
    model="gemini-3.8-flash",
    input="Explain serverless computing in one sentence.",
)

print(interaction.output_text)
```

### TypeScript / JavaScript

```
import { GoogleGenAI } from "@google/genai";

const ai = new GoogleGenAI({
    enterprise: true,
    apiKey: "API_KEY",
});

const interaction = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "Explain serverless computing in one sentence.",
});

console.log(interaction.output_text);
```

### REST

```
curl -X POST "https://aiplatform.googleapis.com/v1beta1/locations/global/interactions" \
  -H "x-goog-api-key: API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": [{
      "role": "user",
      "content": [{
        "type": "text",
        "text": "Explain serverless computing in one sentence."
      }]
    }]
  }'
```

## Common interaction workflows

After you configure your client, you can use the `interactions.create` method to build multi-turn conversations, stream output tokens in real time, generate schema-validated JSON, call external functions, and run autonomous agents.

### Manage stateful multi-turn conversations

Unlike stateless chat APIs that require you to resend the full message history with every request, the Interactions API manages conversation state on the server by default ( `store=True` in Python or `store: true` in TypeScript/JavaScript).

To continue an existing conversation, pass the `id` of the preceding interaction to the `previous_interaction_id` parameter. Agent Platform automatically retrieves the stored conversation context and appends the new turn. If you set `store=False` ( `store: false` in TypeScript/JavaScript), server-side persistence is disabled and you can't chain subsequent turns with `previous_interaction_id` .

### Python

```
# Turn 1: Start a conversation (store=True by default)
turn1 = client.interactions.create(
    model="gemini-3.8-flash",
    input="Hi! My name is John. I am working on AI agents.",
    store=True,
)
print(f"Turn 1: {turn1.output_text}")

# Turn 2: Reference the stored conversation state using previous_interaction_id
turn2 = client.interactions.create(
    model="gemini-3.8-flash",
    input="What is my name?",
    previous_interaction_id=turn1.id,
)
print(f"Turn 2: {turn2.output_text}")
```

### TypeScript / JavaScript

```
// Turn 1: Start a conversation (store: true by default)
const turn1 = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "Hi! My name is John. I am working on AI agents.",
    store: true,
});
console.log(`Turn 1: ${turn1.output_text}`);

// Turn 2: Reference the stored conversation state using previous_interaction_id
const turn2 = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "What is my name?",
    previous_interaction_id: turn1.id,
});
console.log(`Turn 2: ${turn2.output_text}`);
```

### Stream responses in real time

To reduce perceived latency for interactive applications, you can stream model responses as they are generated. Set `stream=True` ( `stream: true` in TypeScript/JavaScript) when calling `interactions.create` to receive an iterable stream of server-sent events. Filter for `step.delta` events to render incremental text chunks as they arrive:

### Python

```
response = client.interactions.create(
    model="gemini-3.8-flash",
    input="Write a short poem about debugging.",
    stream=True,
)

for event in response:
    if event.event_type == "step.delta" and hasattr(event.delta, "text"):
        print(event.delta.text, end="", flush=True)
print()
```

### TypeScript / JavaScript

```
const responseStream = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "Write a short poem about debugging.",
    stream: true,
});

for await (const event of responseStream) {
    if (event.event_type === "step.delta" && event.delta && "text" in event.delta) {
        process.stdout.write(event.delta.text);
    }
}
console.log();
```

### Generate structured output

When your application requires responses in a predictable, machine-readable format, you can constrain the model output to match a specific JSON schema. Pass your target schema—such as a Pydantic model JSON schema in Python or a `Type` schema object in TypeScript/JavaScript—directly to the polymorphic `response_format` parameter:

### Python

```
from pydantic import BaseModel, Field

class Book(BaseModel):
    title: str = Field(description="The title of the book")
    author: str = Field(description="The book's author")
    year_published: int

interaction = client.interactions.create(
    model="gemini-3.8-flash",
    input="Recommend one famous sci-fi book.",
    response_format=Book.model_json_schema(),
)

# The output text is valid JSON matching the Book schema
print(interaction.output_text)
```

### TypeScript / JavaScript

```
import { Type } from "@google/genai";

const BookSchema = {
    type: Type.OBJECT,
    properties: {
        title: { type: Type.STRING, description: "The title of the book" },
        author: { type: Type.STRING, description: "The book's author" },
        yearPublished: { type: Type.INTEGER },
    },
    required: ["title", "author", "yearPublished"],
};

const interaction = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "Recommend one famous sci-fi book.",
    response_format: BookSchema,
});

console.log(interaction.output_text);
```

### Use function calling (tool use)

Function calling lets a model request the execution of custom functions or external APIs to gather information before formulating a final response. In a stateful interaction workflow, function calling follows a two-turn pattern:

1.  **Declare and pass tools** : Provide your function declarations in the `tools` parameter on the initial request.
2.  **Execute and return results** : Inspect the response steps ( `interaction.steps` ) for `function_call` steps, run your local function using the model-supplied `arguments` , and send a follow-up interaction containing a `function_result` item linked by `call_id` and `previous_interaction_id` .

### Python

```
# Define a declarative function tool schema
stock_tool = {
    "type": "function",
    "name": "get_stock_price",
    "description": "Gets the stock price for a given ticker symbol.",
    "parameters": {
        "type": "object",
        "properties": {
            "ticker": {"type": "string", "description": "The stock ticker symbol"}
        },
        "required": ["ticker"],
    },
}

def get_stock_price(ticker: str) -> float:
    """Executes the local tool function."""
    if ticker.upper() == "GOOG":
        return 175.50
    return 100.0

# Turn 1: Pass the tool declaration to the model
interaction = client.interactions.create(
    model="gemini-3.8-flash",
    input="What is the stock price of GOOG?",
    tools=[stock_tool],
)

# Inspect the interaction steps for function call requests
for step in interaction.steps:
    if step.type == "function_call" and step.name == "get_stock_price":
        ticker_arg = step.arguments.get("ticker")
        price = get_stock_price(ticker_arg)

        # Turn 2: Submit the function execution result to the conversation
        final_turn = client.interactions.create(
            model="gemini-3.8-flash",
            input=[{
                "type": "function_result",
                "call_id": step.id,
                "result": {"price": price},
            }],
            previous_interaction_id=interaction.id,
        )
        print(final_turn.output_text)
```

### TypeScript / JavaScript

```
// Define a declarative function tool schema
const stockTool = {
    type: "function",
    name: "getStockPrice",
    description: "Gets the stock price for a given ticker symbol.",
    parameters: {
        type: "object",
        properties: {
            ticker: { type: "string", description: "The stock ticker symbol" },
        },
        required: ["ticker"],
    },
};

function getStockPrice({ ticker }: { ticker: string }): number {
    if (ticker.toUpperCase() === "GOOG") return 175.50;
    return 100.00;
}

// Turn 1: Pass the tool declaration to the model
const interaction = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: "What is the stock price of GOOG?",
    tools: [stockTool],
});

// Inspect the interaction steps for function call requests
for (const step of interaction.steps ?? []) {
    if (step.type === "function_call" && step.name === "getStockPrice") {
        const tickerArg = step.arguments.ticker as string;
        const price = getStockPrice({ ticker: tickerArg });

        // Turn 2: Submit the function execution result to the conversation
        const finalTurn = await ai.interactions.create({
            model: "gemini-3.8-flash",
            input: [{
                type: "function_result",
                call_id: step.id,
                result: { price },
            }],
            previous_interaction_id: interaction.id,
        });
        console.log(finalTurn.output_text);
    }
}
```

### Run agents and long-running background tasks

In addition to foundation models, the Interactions API lets you invoke specialized autonomous agents using the `agent` parameter:

- **`antigravity-preview-05-2026`** : General-purpose managed agent with code execution, file management, and web browsing in a secure sandboxed Linux environment. For more information, see [Interact with agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents) .
- **`deep-research-preview-04-2026`** : Gemini Deep Research Agent, which plans and executes multi-step web research tasks and synthesizes findings from multiple sources into comprehensive reports. For more information, see [Use the Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .
- **Custom agents** : Custom agent resources configured and provisioned with `client.agents.create()` .

> **Note:** Managed agents run autonomously in secure cloud execution environments with access to multi-step search, reasoning, and execution tools.

Because agent workflows often take several minutes to complete, run them asynchronously in the background by setting `background=True` . The API immediately returns an `Interaction` object with an `id` that you can poll using `client.interactions.get()` until `interaction.status` transitions to `completed` :

Before trying this sample, replace ` PROJECT_ID ` with your Google Cloud project ID.

```
import time
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

interaction = client.interactions.create(
    input="Analyze competitive positioning for solar energy providers.",
    agent="deep-research-preview-04-2026",
    background=True,
)

print(f"Research started: {interaction.id}")

while True:
    interaction = client.interactions.get(interaction.id)
    if interaction.status == "completed":
        print(interaction.output_text)
        break
    elif interaction.status in ("failed", "cancelled"):
        print(f"Research ended with status: {interaction.status}")
        break
    time.sleep(10)
```

### Access uploaded Cloud Storage files

You can use the Interactions API to access uploaded Cloud Storage files. See the following example:

```
from google import genai

# Credentials must belong to an identity with storage.objects.get permissions
client = genai.Client()

interaction = client.interactions.create(
    model="gemini-3.8-flash",
    input=[
        {"type": "text", "text": "Summarize the attached document:"},
        {
            "type": "document",
            "uri": "gs://my-secure-bucket/quarterly_report.pdf",
            "mime_type": "application/pdf"
        }
    ],
)

print(interaction.output_text)
```

When passing Cloud Storage URIs (for example, `gs://bucket-name/path/to/file` ) to the Interactions API, requests are evaluated using end-user credentials (EUC). The API fetches Cloud Storage objects using the identity of the authenticated caller rather than a background project service agent.

To pass Cloud Storage files in an interaction request, the calling principal (user account, service account, or federated identity) must hold the `storage.objects.get` permission for all referenced objects.

#### Configure IAM roles for accessing Cloud Storage files

Grant one of the standard predefined roles that include the `storage.objects.get` permission:

- Storage Object Viewer ( `roles/storage.objectViewer` ): Read access to objects (recommended).
- Storage Object User ( `roles/storage.objectUser` ): Read and write access to objects.

To grant access to a user account by using the Google Cloud CLI, use the following command:

```
gcloud storage buckets add-iam-policy-binding gs://BUCKET_NAME \
    --member="user:user-email@example.com" \
    --role="roles/storage.objectViewer"
```

To grant access to a specific calling service account, use the following command:

```
gcloud storage buckets add-iam-policy-binding gs://BUCKET_NAME \
    --member="serviceAccount:sa-name@PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/storage.objectViewer"
```

#### Troubleshoot Cloud Storage file access

If the calling principal lacks sufficient permissions, the Interactions API returns a `403 Forbidden` error similar to the following:

```
Access error:
PERMISSION_DENIED - 403 Forbidden: Calling principal lacks
storage.objects.get on one or more Cloud Storage URIs.
```

To resolve this issue, grant the Storage Object Viewer role ( `roles/storage.objectViewer` ) on the bucket or object to the authenticated caller.

If the specified object doesn't exist, or if bucket permissions prevent the caller from seeing whether the object exists, the Interactions API returns a `404 Not Found` error similar to the following:

```
Access error:
NOT_FOUND - 404 Not Found: The object does not exist, or bucket
permissions prevent revealing object existence.
```

To resolve this issue, verify that the Cloud Storage URI is correct and confirm that the authenticated caller has read access to the bucket.

## Advanced REST workflows

For shell-based automation, CI/CD pipelines, or environments without a Python or TypeScript/JavaScript runtime, you can call the Interactions API directly over HTTP using `curl` .

### REST endpoint

Send `POST` requests to the following Interactions API endpoint:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/interactions
```

Replace the following variables in your requests:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` LOCATION ` : Set to `global` (or a supported custom region if required by your configuration).

### Set environment variables and authentication

Before running the `curl` examples in the following sections, export your project ID, target model or agent ID, and an OAuth 2.0 access token generated from Application Default Credentials:

```
PROJECT_ID="PROJECT_ID"
MODEL_ID="gemini-3.8-flash"
AGENT_ID="deep-research-preview-04-2026"
ACCESS_TOKEN=$(gcloud auth print-access-token)
```

### Synchronous response format

A synchronous `POST` request returns a JSON `interaction` object that includes the unique interaction `id` , execution `status` , conversation `steps` , and token `usage` metadata:

```
{
  "id": "your-interaction-id",
  "status": "completed",
  "steps": [
    {
      "type": "model_output",
      "content": [
        {
          "type": "text",
          "text": "Serverless computing is a cloud execution model where the cloud provider dynamically manages the allocation and provisioning of servers, charging customers based on actual usage rather than pre-purchased capacity."
        }
      ]
    }
  ],
  "usage": {
    "total_tokens": 24751,
    "total_input_tokens": 23894,
    "total_output_tokens": 857
  },
  "created": "2026-05-08T10:44:43Z",
  "updated": "2026-05-08T10:44:43Z",
  "environment_id": "your-environment-id",
  "object": "interaction"
}
```

### Continue a multi-turn stateful interaction

To continue a stored conversation over REST, pass the `id` from a previous response in the `previous_interaction_id` field of the JSON request body.

Before trying this sample, replace ` PREVIOUS_INTERACTION_ID ` with the `id` returned by a previous interaction.

```
curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/global/interactions" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "'"${MODEL_ID}"'",
    "store": true,
    "previous_interaction_id": "PREVIOUS_INTERACTION_ID",
    "input": [{
      "role": "user",
      "content": [{
        "type": "text",
        "text": "Can you elaborate on that?"
      }]
    }]
  }'
```

### Stream output with server-sent events

To stream incremental updates over REST, include `"stream": true` in the JSON request body:

```
curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/global/interactions" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "'"${MODEL_ID}"'",
    "stream": true,
    "input": [{
      "role": "user",
      "content": [{
        "type": "text",
        "text": "Write a long story about space travel."
      }]
    }]
  }'
```

When `"stream": true` is set, the server responds with `Transfer-Encoding: chunked` and `Content-Type: text/event-stream` (Server-Sent Events). Each event in the stream includes a `data:` prefix containing a JSON payload with the `event_type` and step delta contents. `curl` automatically keeps the HTTP connection open and writes incoming chunks to `stdout` in real time until the interaction completes.

### Run a managed agent in the background

To start a long-running managed agent task asynchronously over REST, specify the target `agent` , set `"background": true` , and configure `"environment": "remote"` :

```
curl -X POST "https://aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/global/interactions" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "agent": "'"${AGENT_ID}"'",
    "environment": "remote",
    "background": true,
    "input": [{
      "role": "user",
      "content": [{
        "type": "text",
        "text": "Analyze competitive positioning for commercial solar energy providers."
      }]
    }]
  }'
```

## What's next

- Learn more about key concepts in the [Interactions API overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) .
- Explore request and response schemas in the [Interactions API reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .
- Learn how to [interact with managed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents) and [use the Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .
