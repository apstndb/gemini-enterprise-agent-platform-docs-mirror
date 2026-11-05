---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide
title: Interactions API developer guide
description: Learn how to authenticate, connect to, and use the stateful Interactions API on Gemini Enterprise Agent Platform for session storage, multi-turn conversations, streaming, structured output, built-in tools, grounding, function calling, and long-running agent tasks.
data_source: docs.cloud.google.com
---

> To see an example of how to use the Interactions API, run the "Gemini API: Getting started with Interactions API" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_interactions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_interactions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fgetting-started%2Fintro_interactions_api.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_interactions_api.ipynb)

The Interactions API provides a unified, stateful interface for building generative AI applications with Gemini models and autonomous agents on Gemini Enterprise Agent Platform. Use the Interactions API to manage session storage and multi-turn conversations, stream real-time responses, enforce structured outputs, invoke built-in tools and grounding, execute function calls, and orchestrate long-running background tasks.

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

- **SDK version support** : Use one of the [Supported Google Gen AI SDK libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions#sdks) .

- **Supported models** : Use supported Gemini 3 models or later. Earlier model families don't support this API. For a complete list of supported models, see [Supported models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions#supported-models) and [Migrate to the latest model versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate) .

- **Turn-scoped parameters** : Configuration parameters such as `tools` , `system_instruction` , and `generation_config` apply only to the current turn. Pass these parameters on each subsequent interaction turn if your workflow requires them across a multi-turn conversation.

> **Tip:** If you use an AI coding assistant, you can install the Interactions API agent skill from the [`google/skills` GitHub repository](https://github.com/google/skills/blob/main/skills/cloud/gemini-interactions-api/SKILL.md) .

## Install the Google Gen AI SDK

Install or upgrade the Google Gen AI SDK for your preferred language:

### Python

```
pip install --upgrade "google-genai>=2.3.0"
```

### TypeScript / JavaScript

```
npm install "@google/genai>=2.3.0"
```

### Go

```
go get google.golang.org/genai
```

### Java

```
<dependencies>
  <dependency>
    <groupId>com.google.genai</groupId>
    <artifactId>google-genai</artifactId>
    <version>1.78.0</version>
  </dependency>
</dependencies>
```

## Authenticate your client

You can connect to the Interactions API on Agent Platform using either of the following authentication methods:

- [Google Cloud project with Application Default Credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#connect-adc)
- [Express mode with an API key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#connect-api-key)

### Connect using a Google Cloud project with Application Default Credentials (ADC)

Use this authentication method for enterprise workloads and production deployments on Google Cloud. To authenticate with Application Default Credentials (ADC), initialize the client with the following properties:

- `enterprise=True`
- `project=" `` PROJECT_ID `` "`
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
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": [{
      "type": "user_input",
      "content": [{
        "type": "text",
        "text": "Explain serverless computing in one sentence."
      }]
    }]
  }'
```

> **Tip:** You can also configure the SDK using environment variables so that `genai.Client()` resolves your project settings automatically without inline arguments: `export GOOGLE_GENAI_USE_ENTERPRISE=true` , `export GOOGLE_CLOUD_PROJECT=" `` PROJECT_ID `` "` , and `export GOOGLE_CLOUD_LOCATION="global"` .

### Connect using express mode (API key)

Use this authentication method for rapid prototyping, lightweight scripts, or environments that authenticate with an API key. Pass your API key when initializing the client or in the `x-goog-api-key` HTTP header.

In the following code sample, replace ` API_KEY ` with your API key and ` PROJECT_ID ` with your Google Cloud project ID.

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
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "x-goog-api-key: API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": [{
      "type": "user_input",
      "content": [{
        "type": "text",
        "text": "Explain serverless computing in one sentence."
      }]
    }]
  }'
```

## Common interaction workflows

After you configure your client, you can use the `interactions.create` method to manage session storage and multi-turn conversations, stream output tokens in real time, generate schema-validated JSON, invoke built-in tools and grounding, call external functions, and run autonomous agents.

### Manage session storage and conversation state

The Interactions API supports both server-side stateful storage ( `store=True` , default) and client-managed stateless execution ( `store=False` ). The following table compares stateful and stateless interaction modes:

| Feature                                        | Stateful mode ( `store=true` , default)                                                                                                                                                                                                                                                 | Stateless mode ( `store=false` )                                                                                                                                                                                 |
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Server-side persistence**                    | Stores inputs, intermediate steps, and outputs on the server for 7 days.                                                                                                                                                                                                                | Disables server-side interaction storage to support [Zero Data Retention (ZDR)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention#customer-data-retention) workflows. |
| **Multi-turn context**                         | Chains turns by passing the preceding interaction `id` in `previous_interaction_id` .                                                                                                                                                                                                   | Requires passing the full array of prior conversation `steps` in `input` on each turn. Passing `previous_interaction_id` returns a `400 Bad Request` error.                                                      |
| **Background execution ( `background=true` )** | Supported for long-running model and agent interactions.                                                                                                                                                                                                                                | Not supported. Asynchronous background execution requires server-side state persistence.                                                                                                                         |
| **Session lifecycle methods**                  | Supports retrieving ( `get` ), listing ( `list` ), canceling ( `cancel` ), and deleting ( `delete` ) interactions.                                                                                                                                                                      | Not retrievable after the synchronous or streaming response completes.                                                                                                                                           |
| **Encryption at rest**                         | Encrypted by default with a Google-owned and Google-managed encryption key, or with [customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#cmek) in the `us` and `eu` multi-regions. | No interaction state is stored at rest.                                                                                                                                                                          |

#### Run stateful multi-turn conversations

By default, the Interactions API stores conversation state on the server ( `store=True` in Python or `store: true` in TypeScript/JavaScript). To continue an existing conversation, pass the `id` of the preceding interaction to the `previous_interaction_id` parameter. Agent Platform retrieves the stored conversation context, appends the new turn, and reuses cached prefix tokens.

When chaining interactions across endpoints, observe the following location rules:

- **Same location** : You can chain interactions within the same location (such as `global` to `global` , `us` to `us` , or `eu` to `eu` ).

- **Across different locations** : Chaining across different endpoint locations (between `global` and `us` or `eu` , or between `us` and `eu` ) isn't supported. Each endpoint stores interaction state in isolated storage, so referencing an interaction ID created in another location returns a `404 Not Found` error.

In the following example, replace ` PROJECT_ID ` with your Google Cloud project ID:

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

# Turn 1: Start a stateful conversation (store=True by default)
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
import { GoogleGenAI } from "@google/genai";

const ai = new GoogleGenAI({
    enterprise: true,
    project: "PROJECT_ID",
    location: "global",
});

// Turn 1: Start a stateful conversation (store: true by default)
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

### Java

```
import com.google.genai.Client;
import com.google.genai.gaos.models.interactions.CreateModelInteraction;
import com.google.genai.gaos.models.interactions.Interaction;
import com.google.genai.gaos.models.interactions.InteractionsInput;
import com.google.genai.gaos.models.interactions.Model;
import com.google.genai.gaos.models.operations.CreateInteractionRequestBody;

Client client =
    Client.builder()
        .enterprise(true)
        .project("PROJECT_ID")
        .location("global")
        .build();

// Turn 1: Start a stateful conversation (store is true by default)
CreateModelInteraction req1 =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .input(InteractionsInput.of("Hi! My name is John. I am working on AI agents."))
        .store(true)
        .build();

Interaction turn1 =
    client.interactions.create(CreateInteractionRequestBody.of(req1)).interaction().orElseThrow();
System.out.println("Turn 1: " + turn1.outputText().orElse(""));

// Turn 2: Reference the stored conversation state using previousInteractionId
CreateModelInteraction req2 =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .previousInteractionId(turn1.id().orElseThrow())
        .input(InteractionsInput.of("What is my name?"))
        .build();

Interaction turn2 =
    client.interactions.create(CreateInteractionRequestBody.of(req2)).interaction().orElseThrow();
System.out.println("Turn 2: " + turn2.outputText().orElse(""));
```

### REST

```
# Turn 1: Start a stateful conversation
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "store": true,
    "input": "Hi! My name is John. I am working on AI agents."
  }'

# Turn 2: Pass the interaction ID from Turn 1 in previous_interaction_id
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "previous_interaction_id": "PREVIOUS_INTERACTION_ID",
    "input": "What is my name?"
  }'
```

#### Run stateless multi-turn conversations

If your workload requires [Zero Data Retention (ZDR)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention#customer-data-retention) , explicitly set `store=False` ( `store: false` in TypeScript/JavaScript or `"store": false` in REST) on every request.

In stateless mode, you manage conversation history on the client by maintaining a list of [`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api#Resource:Step) objects ( `user_input` , `thought` , `function_call` , `function_result` , and `model_output` ) and sending the accumulated `steps` array in `input` on each turn:

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

history = [
    {
        "type": "user_input",
        "content": [{"type": "text", "text": "Hi! My name is John."}],
    }
]

# Turn 1: Stateless request (store=False)
turn1 = client.interactions.create(
    model="gemini-3.8-flash",
    input=history,
    store=False,
)
print(f"Turn 1: {turn1.output_text}")

# Append the model's generated steps and the next user turn to local history
history.extend(turn1.steps)
history.append(
    {
        "type": "user_input",
        "content": [{"type": "text", "text": "What is my name?"}],
    }
)

# Turn 2: Send the full step history with store=False
turn2 = client.interactions.create(
    model="gemini-3.8-flash",
    input=history,
    store=False,
)
print(f"Turn 2: {turn2.output_text}")
```

### TypeScript / JavaScript

```
import { GoogleGenAI, Step } from "@google/genai";

const ai = new GoogleGenAI({
    enterprise: true,
    project: "PROJECT_ID",
    location: "global",
});

const history: Step[] = [
    {
        type: "user_input",
        content: [{ type: "text", text: "Hi! My name is John." }],
    },
];

// Turn 1: Stateless request (store: false)
const turn1 = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: history,
    store: false,
});
console.log(`Turn 1: ${turn1.output_text}`);

// Append the model's generated steps and the next user turn to local history
if (turn1.steps) {
    history.push(...turn1.steps);
}
history.push({
    type: "user_input",
    content: [{ type: "text", text: "What is my name?" }],
});

// Turn 2: Send the full step history with store: false
const turn2 = await ai.interactions.create({
    model: "gemini-3.8-flash",
    input: history,
    store: false,
});
console.log(`Turn 2: ${turn2.output_text}`);
```

### Java

```
import com.google.genai.Client;
import com.google.genai.gaos.models.interactions.CreateModelInteraction;
import com.google.genai.gaos.models.interactions.Interaction;
import com.google.genai.gaos.models.interactions.InteractionsInput;
import com.google.genai.gaos.models.interactions.Model;
import com.google.genai.gaos.models.interactions.Step;
import com.google.genai.gaos.models.interactions.TextContent;
import com.google.genai.gaos.models.interactions.UserInputContent;
import com.google.genai.gaos.models.interactions.UserInputStep;
import com.google.genai.gaos.models.operations.CreateInteractionRequestBody;
import java.util.ArrayList;
import java.util.List;

Client client =
    Client.builder()
        .enterprise(true)
        .project("PROJECT_ID")
        .location("global")
        .build();

List<Step> history = new ArrayList<>();
history.add(
    Step.of(
        UserInputStep.builder()
            .content(
                List.of(
                    UserInputContent.of(
                        TextContent.builder().text("Hi! My name is John.").build())))
            .build()));

// Turn 1: Stateless request (store(false))
CreateModelInteraction req1 =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .input(InteractionsInput.ofSteps(history))
        .store(false)
        .build();

Interaction turn1 =
    client.interactions.create(CreateInteractionRequestBody.of(req1)).interaction().orElseThrow();
System.out.println("Turn 1: " + turn1.outputText().orElse(""));

// Append the model's generated steps and the next user turn to local history
turn1.steps().ifPresent(history::addAll);
history.add(
    Step.of(
        UserInputStep.builder()
            .content(
                List.of(
                    UserInputContent.of(
                        TextContent.builder().text("What is my name?").build())))
            .build()));

// Turn 2: Send the full step history with store(false)
CreateModelInteraction req2 =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .input(InteractionsInput.ofSteps(history))
        .store(false)
        .build();

Interaction turn2 =
    client.interactions.create(CreateInteractionRequestBody.of(req2)).interaction().orElseThrow();
System.out.println("Turn 2: " + turn2.outputText().orElse(""));
```

### REST

```
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "store": false,
    "input": [
      {
        "type": "user_input",
        "content": [{"type": "text", "text": "Hi! My name is John."}]
      },
      {
        "type": "model_output",
        "content": [{"type": "text", "text": "Hello John! How can I help you today?"}]
      },
      {
        "type": "user_input",
        "content": [{"type": "text", "text": "What is my name?"}]
      }
    ]
  }'
```

#### Retention and session lifecycle

Stored interactions ( `store=True` ) follow these retention and branching rules:

- **7-day time-to-live (TTL)** : Each stored interaction persists for 7 days from its `created` timestamp and is automatically deleted when the 7-day TTL expires.

- **Independent parent and child storage** : When you chain a new turn using `previous_interaction_id` , Agent Platform copies the ancestor conversation history into the new interaction record. Because each turn stores its own copy of the conversation history, expiring or deleting an earlier turn has the following effects:

  - **Continuing from a later turn succeeds** : If Turn 1 ( `interaction_1` ) expires or is deleted after Turn 2 ( `interaction_2` ) has already been created, you can still create Turn 3 using `previous_interaction_id=interaction_2.id` until `interaction_2` itself expires or is deleted.

  - **Branching from an expired or deleted turn fails** : Attempting to create a new interaction directly referencing an expired or deleted interaction ID in `previous_interaction_id` returns a `400 Bad Request` ( `Previous Interaction ID not found` ) error.

#### Retrieve, list, cancel, and delete stored interactions

You can inspect and manage stored interactions throughout their lifecycle using the following methods:

- **Retrieve an interaction ( [`interactions.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api#getInteractionById) )** : Fetches the complete `Interaction` resource by `id` , including `user_input` steps, intermediate `thought` and tool steps, and `model_output` steps. Set `stream=True` (and optional `last_event_id` ) to stream or resume an in-progress interaction.

- **List interactions ( [`interactions.list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api#listInteractions) )** : Queries stored interaction IDs in your project over REST using `page_size` (default `10` , maximum `500` ) and `page_token` . Returns a list of [`InteractionMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api#Resource:InteractionMetadata) resources.

- **Cancel an in-progress interaction ( [`interactions.cancel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api#cancelInteractionById) )** : Halts an asynchronous background interaction ( `background=True` ) that is in the `in_progress` or `requires_action` state and transitions its status to `cancelled` . You are billed for any tokens generated prior to cancellation.

- **Delete a stored interaction ( [`interactions.delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api#deleteInteraction) )** : Permanently removes a stored interaction before its 7-day TTL expires. Only interactions in a terminal state ( `completed` , `failed` , or `cancelled` ) can be deleted; if an interaction is still running in the background, cancel it before deleting it.

In the following example, replace ` PROJECT_ID ` with your Google Cloud project ID and ` INTERACTION_ID ` with the target interaction ID:

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

# Retrieve a stored interaction by ID
interaction = client.interactions.get(id="INTERACTION_ID")
print(f"Status: {interaction.status}")

# Cancel an in-progress background interaction
cancelled = client.interactions.cancel(id="INTERACTION_ID")
print(f"After cancel: {cancelled.status}")

# Delete a completed, failed, or cancelled interaction before its 7-day TTL
client.interactions.delete(id="INTERACTION_ID")
print("Interaction deleted.")
```

### TypeScript / JavaScript

```
import { GoogleGenAI } from "@google/genai";

const ai = new GoogleGenAI({
    enterprise: true,
    project: "PROJECT_ID",
    location: "global",
});

// Retrieve a stored interaction by ID
const interaction = await ai.interactions.get("INTERACTION_ID");
console.log(`Status: ${interaction.status}`);

// Cancel an in-progress background interaction
const cancelled = await ai.interactions.cancel("INTERACTION_ID");
console.log(`After cancel: ${cancelled.status}`);

// Delete a completed, failed, or cancelled interaction before its 7-day TTL
await ai.interactions.delete("INTERACTION_ID");
console.log("Interaction deleted.");
```

### Java

```
import com.google.genai.Client;
import com.google.genai.gaos.models.interactions.Interaction;
import com.google.genai.gaos.models.interactions.InteractionStatus;
import com.google.genai.gaos.models.operations.CancelInteractionByIdResponse;
import com.google.genai.gaos.models.operations.GetInteractionByIdRequest;
import com.google.genai.gaos.models.operations.GetInteractionByIdResponse;

Client client =
    Client.builder()
        .enterprise(true)
        .project("PROJECT_ID")
        .location("global")
        .build();

String interactionId = "INTERACTION_ID";

// Retrieve a stored interaction by ID
GetInteractionByIdResponse getResponse =
    client.interactions.get(new GetInteractionByIdRequest(interactionId));
Interaction interaction = getResponse.interaction().orElseThrow();
System.out.println("Status: " + interaction.status().map(InteractionStatus::value).orElse(""));

// Cancel an in-progress background interaction
CancelInteractionByIdResponse cancelResponse = client.interactions.cancel(interactionId);
Interaction cancelled = cancelResponse.interaction().orElseThrow();
System.out.println("After cancel: " + cancelled.status().map(InteractionStatus::value).orElse(""));

// Delete a completed, failed, or cancelled interaction before its 7-day TTL
client.interactions.delete(interactionId);
System.out.println("Interaction deleted.");
```

### REST

```
# Retrieve a stored interaction by ID
curl -X GET "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)"

# List stored interactions (up to 500 per page)
curl -X GET "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions?page_size=10" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)"

# Cancel an in-progress background interaction
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID/cancel" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)"

# Delete a completed, failed, or cancelled interaction
curl -X DELETE "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)"
```

#### Stateful storage quotas and limits

In addition to model token and request rate limits, stateful interactions ( `store=True` ) are subject to the following project-level storage and concurrency limits:

| Quota or system limit                                  | Default limit (per project)   | Description                                                                                                                                                                     |
|--------------------------------------------------------|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Stateful interactions creation throughput per day**  | `240 GiB` per day             | Maximum total volume of interaction data written to server-side storage per day across `interactions.create` requests with `store=true` .                                       |
| **Stateful interactions retrieval throughput per day** | `480 GiB` per day             | Maximum total volume of stored interaction data read per day across `interactions.get` requests and multi-turn requests that load prior turns using `previous_interaction_id` . |
| **Concurrent stateful interactions**                   | `500` concurrent interactions | Maximum number of active stateful interactions executing concurrently in a project.                                                                                             |

For more information about viewing and managing quotas on Agent Platform, see [Quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas) .

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

### Use built-in tools

In addition to client-side [function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#function-calling) , the Interactions API supports built-in server-side tools for Gemini 3 models. When you enable a built-in tool in the `tools` parameter, Agent Platform executes the tool on the server during a single `interactions.create` call and records the tool invocation ( `*_call` ) and output ( `*_result` ) steps in `interaction.steps` .

The Interactions API supports the following built-in tools:

- **[Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#code-execution)** ( `{"type": "code_execution"}` ): Generates and executes Python code in a sandboxed environment to perform calculations, data analysis, and code-based reasoning. For supported libraries, billing, and limitations, see [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution) .

- **[URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#url-context)** ( `{"type": "url_context"}` ): Retrieves and analyzes content from public web URLs included in your prompt. For details on index caching, live fetches, and combining URL context with search, see [URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context) .

- **[Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#grounding)** ( `{"type": "google_search"}` ): Grounds model responses in real-time web information and returns inline citations. See [Ground responses with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#grounding) .

- **[Computer use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use)** ( `{"type": "computer_use"}` ): Enables browser and user-interface automation workflows. For configuration and safety controls, see [Computer use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use) .

#### Execute Python code

To enable code execution, include `{"type": "code_execution"}` in the `tools` list. The returned `interaction.steps` array contains `code_execution_call` steps (with `arguments.code` and `arguments.language` ), `code_execution_result` steps (with `result` and `is_error` ), and the final `model_output` step.

In the following example, replace ` PROJECT_ID ` with your Google Cloud project ID:

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
    input="Calculate the 50th Fibonacci number and find its closest prime.",
    tools=[{"type": "code_execution"}],
)

for step in interaction.steps:
    if step.type == "code_execution_call":
        print(f"Generated code:\n{step.arguments.code}")
    elif step.type == "code_execution_result":
        print(f"Execution result:\n{step.result}")
    elif step.type == "model_output":
        for content in step.content:
            if content.type == "text":
                print(content.text)
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
    input: "Calculate the 50th Fibonacci number and find its closest prime.",
    tools: [{ type: "code_execution" }],
});

for (const step of interaction.steps ?? []) {
    if (step.type === "code_execution_call") {
        console.log(`Generated code:\n${step.arguments?.code}`);
    } else if (step.type === "code_execution_result") {
        console.log(`Execution result:\n${step.result}`);
    } else if (step.type === "model_output") {
        for (const content of step.content ?? []) {
            if (content.type === "text") {
                console.log(content.text);
            }
        }
    }
}
```

### Java

```
import com.google.genai.Client;
import com.google.genai.gaos.models.interactions.CodeExecution;
import com.google.genai.gaos.models.interactions.CodeExecutionCallStep;
import com.google.genai.gaos.models.interactions.CodeExecutionResultStep;
import com.google.genai.gaos.models.interactions.CreateModelInteraction;
import com.google.genai.gaos.models.interactions.Interaction;
import com.google.genai.gaos.models.interactions.InteractionsInput;
import com.google.genai.gaos.models.interactions.Model;
import com.google.genai.gaos.models.interactions.Step;
import com.google.genai.gaos.models.operations.CreateInteractionRequestBody;
import java.util.List;

Client client =
    Client.builder()
        .enterprise(true)
        .project("PROJECT_ID")
        .location("global")
        .build();

CreateModelInteraction request =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .input(
            InteractionsInput.of(
                "Calculate the 50th Fibonacci number and find its closest prime."))
        .tools(List.of(CodeExecution.builder().build()))
        .build();

Interaction interaction =
    client.interactions.create(CreateInteractionRequestBody.of(request)).interaction().orElseThrow();

for (Step step : interaction.steps().orElse(List.of())) {
    if (step instanceof CodeExecutionCallStep callStep) {
        callStep
            .arguments()
            .flatMap(args -> args.code())
            .ifPresent(code -> System.out.println("Generated code:\n" + code));
    } else if (step instanceof CodeExecutionResultStep resultStep) {
        resultStep
            .result()
            .ifPresent(res -> System.out.println("Execution result:\n" + res));
    }
}
System.out.println(interaction.outputText().orElse(""));
```

### REST

```
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": "Calculate the 50th Fibonacci number and find its closest prime.",
    "tools": [{"type": "code_execution"}]
  }'
```

#### Retrieve web page content with URL context

To enable the model to fetch and analyze web pages referenced in your prompt, include `{"type": "url_context"}` in the `tools` list. The API records the fetched URLs in `url_context_call` and `url_context_result` steps and attaches `url_citation` annotations to the generated text in `model_output` .

In the following example, replace ` PROJECT_ID ` with your Google Cloud project ID and ` YOUR_URL_1 ` and ` YOUR_URL_2 ` with the public URLs to compare:

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
    input="Compare the key findings from YOUR_URL_1 and YOUR_URL_2.",
    tools=[{"type": "url_context"}],
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
    input: "Compare the key findings from YOUR_URL_1 and YOUR_URL_2.",
    tools: [{ type: "url_context" }],
});

console.log(interaction.output_text);
```

### Java

```
import com.google.genai.Client;
import com.google.genai.gaos.models.interactions.CreateModelInteraction;
import com.google.genai.gaos.models.interactions.Interaction;
import com.google.genai.gaos.models.interactions.InteractionsInput;
import com.google.genai.gaos.models.interactions.Model;
import com.google.genai.gaos.models.interactions.URLContext;
import com.google.genai.gaos.models.operations.CreateInteractionRequestBody;
import java.util.List;

Client client =
    Client.builder()
        .enterprise(true)
        .project("PROJECT_ID")
        .location("global")
        .build();

CreateModelInteraction request =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .input(
            InteractionsInput.of(
                "Compare the key findings from YOUR_URL_1 and YOUR_URL_2."))
        .tools(List.of(URLContext.builder().build()))
        .build();

Interaction interaction =
    client.interactions.create(CreateInteractionRequestBody.of(request)).interaction().orElseThrow();

System.out.println(interaction.outputText().orElse(""));
```

### REST

```
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": "Compare the key findings from YOUR_URL_1 and YOUR_URL_2.",
    "tools": [{"type": "url_context"}]
  }'
```

### Ground responses with Google Search

Grounding connects Gemini models to verifiable external sources to reduce hallucinations and provide up-to-date answers with citations. For an overview of grounding options on Agent Platform, see the [Grounding overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview) , [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search) , and [Web Grounding for Enterprise](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/web-grounding-enterprise) .

When you enable Grounding with Google Search by passing `{"type": "google_search"}` in the `tools` list, the Interactions API returns search and attribution data directly in the `interaction.steps` timeline:

- **`google_search_call`** : Contains the search queries issued by the model ( `step.arguments.queries` ).

- **`google_search_result`** : Contains search suggestions ( `result[].search_suggestions` ), an HTML/CSS snippet used for rendering search suggestions in user interfaces. Web resources with source URLs and titles are provided as inline `url_citation` annotations on `model_output` text blocks.

- **Inline `url_citation` annotations** : Each `text` content block ( `TextContent` ) inside a `model_output` step can include an `annotations` array. Each `url_citation` annotation identifies the character or byte span ( `start_index` and `end_index` ) in the response text along with the source `title` and `url` .

In the following example, replace ` PROJECT_ID ` with your Google Cloud project ID:

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
    input="Who won the 2026 Super Bowl?",
    tools=[{"type": "google_search"}],
)

print(interaction.output_text)

# Parse inline url_citation annotations from model_output steps
print("\nSources:")
for step in interaction.steps:
    if step.type == "model_output" and step.content:
        for content in step.content:
            if content.type == "text" and getattr(content, "annotations", None):
                for annotation in content.annotations:
                    if annotation.type == "url_citation":
                        span = content.text[annotation.start_index:annotation.end_index]
                        print(f"- [{annotation.title}]({annotation.url}) (cited text: {span!r})")
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
    input: "Who won the 2026 Super Bowl?",
    tools: [{ type: "google_search" }],
});

console.log(interaction.output_text);

// Parse inline url_citation annotations from model_output steps
console.log("\nSources:");
for (const step of interaction.steps ?? []) {
    if (step.type === "model_output") {
        for (const content of step.content ?? []) {
            if (content.type === "text" && content.annotations) {
                for (const annotation of content.annotations) {
                    if (annotation.type === "url_citation") {
                        const span = content.text.slice(
                            annotation.start_index,
                            annotation.end_index,
                        );
                        console.log(
                            `- [${annotation.title}](${annotation.url}) (cited text: "${span}")`,
                        );
                    }
                }
            }
        }
    }
}
```

### Java

```
import com.google.genai.Client;
import com.google.genai.gaos.models.interactions.Annotation;
import com.google.genai.gaos.models.interactions.Content;
import com.google.genai.gaos.models.interactions.CreateModelInteraction;
import com.google.genai.gaos.models.interactions.GoogleSearch;
import com.google.genai.gaos.models.interactions.Interaction;
import com.google.genai.gaos.models.interactions.InteractionsInput;
import com.google.genai.gaos.models.interactions.Model;
import com.google.genai.gaos.models.interactions.ModelOutputStep;
import com.google.genai.gaos.models.interactions.Step;
import com.google.genai.gaos.models.interactions.TextContent;
import com.google.genai.gaos.models.interactions.URLCitation;
import com.google.genai.gaos.models.operations.CreateInteractionRequestBody;
import java.util.List;

Client client =
    Client.builder()
        .enterprise(true)
        .project("PROJECT_ID")
        .location("global")
        .build();

CreateModelInteraction request =
    CreateModelInteraction.builder()
        .model(Model.of("gemini-3.8-flash"))
        .input(InteractionsInput.of("Who won the 2026 Super Bowl?"))
        .tools(List.of(GoogleSearch.builder().build()))
        .build();

Interaction interaction =
    client.interactions.create(CreateInteractionRequestBody.of(request)).interaction().orElseThrow();

System.out.println(interaction.outputText().orElse(""));

// Parse inline URLCitation annotations from ModelOutputStep blocks
System.out.println("\nSources:");
for (Step step : interaction.steps().orElse(List.of())) {
    if (step instanceof ModelOutputStep outputStep) {
        for (Content content : outputStep.content().orElse(List.of())) {
            if (content instanceof TextContent textContent) {
                for (Annotation annotation : textContent.annotations().orElse(List.of())) {
                    if (annotation instanceof URLCitation citation) {
                        System.out.printf(
                            "- %s: %s (span: %d..%d)%n",
                            citation.title().orElse(""),
                            citation.url().orElse(""),
                            citation.startIndex().orElse(0L),
                            citation.endIndex().orElse(0L));
                    }
                }
            }
        }
    }
}
```

### REST

```
# Request
curl -X POST "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.8-flash",
    "input": "Who won the 2026 Super Bowl?",
    "tools": [{"type": "google_search"}]
  }'
```

The response includes `google_search_call` , `google_search_result` , and `model_output` steps with inline `url_citation` annotations:

```
{
  "id": "v1_ChdPU0F4YWFtNkFwS2kxZThQZ05lbXdROA",
  "model": "gemini-3.8-flash",
  "status": "completed",
  "steps": [
    {
      "type": "google_search_call",
      "id": "search_call_1",
      "arguments": {
        "queries": ["2026 Super Bowl winner"]
      }
    },
    {
      "type": "google_search_result",
      "call_id": "search_call_1",
      "result": [
        {
          "search_suggestions": "<!-- HTML and CSS for search suggestions -->"
        }
      ]
    },
    {
      "type": "model_output",
      "content": [
        {
          "type": "text",
          "text": "The Seattle Seahawks won Super Bowl LX on February 8, 2026.",
          "annotations": [
            {
              "type": "url_citation",
              "start_index": 0,
              "end_index": 59,
              "title": "Super Bowl LX",
              "url": "https://example.com/super-bowl-lx"
            }
          ]
        }
      ]
    }
  ]
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

You can use the Interactions API to access uploaded Cloud Storage files. In the following example, replace ` PROJECT_ID ` with your Google Cloud project ID:

```
from google import genai

# Credentials must belong to an identity with storage.objects.get permissions
client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

interaction = client.interactions.create(
    model="gemini-3.8-flash",
    input=[
        {
            "type": "user_input",
            "content": [
                {"type": "text", "text": "Summarize the attached document:"},
                {
                    "type": "document",
                    "uri": "gs://my-secure-bucket/quarterly_report.pdf",
                    "mime_type": "application/pdf",
                },
            ],
        }
    ],
)

print(interaction.output_text)
```

When passing Cloud Storage URIs (for example, `gs://bucket-name/path/to/file` ) to the Interactions API, requests verify read access using the caller's credentials before the calling project's Agent Platform Service Agent ( `service- `` PROJECT_NUMBER `` @gcp-sa-aiplatform.iam.gserviceaccount.com` ) fetches the object from Cloud Storage.

To pass Cloud Storage files in an interaction request, the calling principal (user account, service account, or federated identity) must hold the `storage.objects.get` permission for all referenced objects. For cross-project Cloud Storage buckets or Cloud Storage buckets with custom IAM policies, grant read access to both the calling principal and the calling project's service agent.

Each standard Gemini model interaction request supports up to 100 distinct Cloud Storage ( `gs://` ) URIs (up to 2 GiB minus 500 KiB per file). When you chain stateful turns using `previous_interaction_id` , Agent Platform counts distinct `gs://` URIs cumulatively across the conversation history and the current turn. Managed agent interactions (requests that set `agent` instead of `model` ), Gemini Omni models, and Lyria 3 models are excluded from this 100-URI limit.

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

To resolve this issue, grant the Storage Object Viewer role ( `roles/storage.objectViewer` ) on the Cloud Storage bucket or object to the authenticated caller (and to the calling project's Agent Platform Service Agent for cross-project or custom-IAM Cloud Storage buckets).

If the specified object doesn't exist, or if bucket permissions prevent the caller from seeing whether the object exists, the Interactions API returns a `404 Not Found` error similar to the following:

```
Access error:
NOT_FOUND - 404 Not Found: The object does not exist, or bucket
permissions prevent revealing object existence.
```

To resolve this issue, verify that the Cloud Storage URI is correct and confirm that the authenticated caller has read access to the bucket.

If a model interaction request references more than 100 distinct Cloud Storage URIs across the current turn and any linked `previous_interaction_id` history, the Interactions API returns a `400 Bad Request` error similar to the following:

```
INVALID_ARGUMENT - 400 Bad Request: Request references 101 distinct gs:// URIs, which exceeds the maximum of 100.
```

To resolve this issue, do one of the following:

- Start a new interaction without `previous_interaction_id` when files from earlier turns are no longer needed.
- Combine smaller documents or pass additional files inline within the request payload limit (256 MiB compressed for synchronous or streaming requests, or 9.75 MiB uncompressed when `service_tier` is set to `deferred` with `background` and `store` set to `true` ).
- Use [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference) for requests that reference `gs://` URIs up to the per-modality model item limits (3,000 images and PDFs combined, 1,000 audio files, and 10 videos, or up to 6,500 files when including plain-text files).

### Encrypt interaction data with CMEK

Stateful interactions ( `store=True` in Python or `store: true` in TypeScript/JavaScript) store interaction data at rest for up to 7 days. To protect that data with your own encryption key instead of a Google-owned and Google-managed encryption key, use a *serving profile* . A serving profile links a Cloud Key Management Service key to a project, location, and API scope. While a serving profile exists, Agent Platform encrypts stored interaction data automatically—your interaction request format doesn't change.

Serving profile CMEK for the Interactions API is supported in the `us` and `eu` multi-regions. The `global` region isn't supported.

To set up CMEK for the Interactions API, do the following:

1.  Enable the Cloud KMS API and the Agent Platform API on your project. See [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#serving-profile-before-you-begin) .

2.  Create a Cloud KMS key in the `us` or `eu` multi-region. See [Create a key ring and key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#creating-key-ring-and-key) .

3.  Grant the Gemini Enterprise Agent Platform service agent the `roles/cloudkms.cryptoKeyEncrypterDecrypter` role on the key. See [Grant Agent Platform permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#grant-permissions) .

4.  Create a serving profile in the same multi-region ( `us` or `eu` ) that sets `scope` to `INTERACTIONS_API` and `cmekConfig.encryptionSpec.kmsKeyName` to your key:

    ```
    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.LOCATION.rep.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/servingProfiles?servingProfileId=SERVING_PROFILE_ID" \
      -d '{
        "displayName": "Interactions API CMEK profile",
        "description": "CMEK for Interactions API",
        "scope": "INTERACTIONS_API",
        "cmekConfig": {
          "encryptionSpec": {
            "kmsKeyName": "projects/KMS_PROJECT_ID/locations/LOCATION/keyRings/KEY_RING_NAME/cryptoKeys/KEY_NAME"
          }
        }
      }'
    ```

    Wait for the long-running create operation to complete ( `"done": true` ). For more details on managing, updating, or deleting serving profiles, see [Create a serving profile](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#serving-profile-create) .

5.  Send your interaction requests to the same `us` or `eu` multi-region as your serving profile. Serving profile CMEK isn't available on the `global` endpoint.

    - **Google Gen AI SDK** : Initialize the client with `location="us"` or `location="eu"` ( `location: "us"` or `location: "eu"` in TypeScript/JavaScript).
    - **REST** : Send requests to the multi-region endpoint `https://aiplatform. `` LOCATION `` .rep.googleapis.com/v1/projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /interactions` , where ` LOCATION ` is `us` or `eu` .

    If you disable the key or revoke the service agent's access, requests that create or read stored interactions fail with a `FAILED_PRECONDITION` error.

> **Note:** Data stored before you create the serving profile isn't retroactively re-encrypted with your key.

## Advanced REST workflows

For shell-based automation, CI/CD pipelines, or environments without a Python or TypeScript/JavaScript runtime, you can call the Interactions API directly over HTTP using `curl` .

### REST endpoint

Send `POST` requests to the following Interactions API endpoint:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/interactions
```

Replace the following variables in your requests:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` LOCATION ` : Set to `global` (or `us` or `eu` with the multi-region host `https://aiplatform. `` LOCATION `` .rep.googleapis.com` for [data residency](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency) or [CMEK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#cmek) ).

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
curl -X POST "https://aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/global/interactions" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "'"${MODEL_ID}"'",
    "store": true,
    "previous_interaction_id": "PREVIOUS_INTERACTION_ID",
    "input": [{
      "type": "user_input",
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
curl -X POST "https://aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/global/interactions" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "'"${MODEL_ID}"'",
    "stream": true,
    "input": [{
      "type": "user_input",
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
curl -X POST "https://aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/global/interactions" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "agent": "'"${AGENT_ID}"'",
    "environment": "remote",
    "background": true,
    "input": [{
      "type": "user_input",
      "content": [{
        "type": "text",
        "text": "Analyze competitive positioning for commercial solar energy providers."
      }]
    }]
  }'
```

## What's next

Explore the following resources to learn more about the Interactions API, built-in tools, and grounding:

- Learn more about key concepts in the [Interactions API overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) .

- Explore request and response schemas in the [Interactions API reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .

- Learn more about [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution) , [URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context) , and [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search) .

- Learn how to [interact with managed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents) and [use the Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .
