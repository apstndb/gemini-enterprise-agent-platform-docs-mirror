---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs
title: Structured outputs with Anthropic Claude models
description: Constrain Anthropic Claude model responses on Gemini Enterprise Agent Platform to a specific JSON schema using structured outputs and strict tool use.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . You can process personal data for this feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Structured outputs let you constrain a Claude model's generated output to conform exactly to a specific JSON schema. This is useful for ensuring that responses from your Claude models are always in the precise format required for downstream applications, databases, and processing pipelines.

Structured outputs provide two complementary features that you can use independently or together in the same request:

  - **JSON outputs** ( `output_config.format` ): Constrain the model's text response to a JSON object that matches a schema you provide. Use this when you need to extract structured data from text, generate structured reports, or format API responses.
  - **Strict tool use** ( `tools[].strict` ): Guarantee that the arguments the model passes to a tool match the tool's `input_schema` . Use this when you need type-safe function calls in agentic workflows.

For more information, see Anthropic's [Building with Claude: Structured Outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs) and [Strict tool use](https://platform.claude.com/docs/en/agents-and-tools/tool-use/strict-tool-use) documentation.

## Supported Anthropic Claude models

Gemini Enterprise Agent Platform supports structured outputs for the following Anthropic Claude models:

  - Claude Opus 4.7
  - Claude Sonnet 4.6
  - Claude Opus 4.6
  - (Coming soon) Claude Opus 4.5
  - (Coming soon) Claude Sonnet 4.5
  - (Coming soon) Claude Haiku 4.5

## Control access to structured outputs

By default, structured outputs are disabled by the organization policy constraint `constraints/vertexai.allowedPartnerModelFeatures` . To enable structured outputs, you must configure this constraint to explicitly allow the `structured_outputs` feature.

Additionally, you can configure the organization policy constraint `constraints/vertexai.allowedModels` to restrict access to Claude models.

For detailed instructions on configuring organization policy constraints, see [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

## Send a structured output request

To request a JSON output, send a POST request to the publisher model endpoint and include the `output_config` parameter in your request body. The `output_config` parameter specifies the JSON schema that the model's response must conform to.

### REST

The following sample shows how to send a request to the Agent Platform API that extracts structured contact information from an unstructured email. The response is constrained to a JSON object with `name` , `email` , `plan_interest` , and `demo_requested` fields.

Before using any of the request data, make the following replacements:

  - LOCATION : A [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs#regions) that supports Anthropic Claude models. To use the global endpoint, see [Specify the global endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/use-partner-models#global) .

  - MODEL : A [supported Claude model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs#models) , for example `claude-opus-4-7` .

  - ROLE : The role associated with a message. You can specify a `user` or an `assistant` . The first message must use the `user` role. Claude models operate with alternating `user` and `assistant` turns. If the final message uses the `assistant` role, then the response content continues immediately from the content in that message. You can use this to constrain part of the model's response.

  - CONTENT : The content, such as text, of the `user` or `assistant` message. For example, `Extract the key information from this email: John Smith (john@example.com) is interested in our Enterprise plan and wants to schedule a demo for next Tuesday at 2pm.`

  - MAX\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately 3.5 characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

  - STREAM : A boolean that specifies whether the response is streamed or not. Set to `true` to stream the response and `false` to return the response all at once. Structured outputs are typically returned with `false` .

The example uses the following structured output fields. For details on each field, see the [Request fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs#request-fields) section.

  - `output_config` : The top-level configuration block that controls the structure of the model's response.
  - `output_config.format.type` : Set to `json_schema` to constrain the response to a JSON object that conforms to the provided schema.
  - `output_config.format.schema` : A JSON schema that defines the required structure of the model's response. The schema must conform to the [supported JSON Schema subset](https://platform.claude.com/docs/en/build-with-claude/structured-outputs#json-schema-limitations) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/MODEL:rawPredict

Request JSON body:

    {
      "anthropic_version": "vertex-2023-10-16",
      "messages": [
        {
          "role": "ROLE",
          "content": "CONTENT"
        }
      ],
      "max_tokens": MAX_TOKENS,
      "stream": STREAM,
      "output_config": {
        "format": {
          "type": "json_schema",
          "schema": {
            "type": "object",
            "properties": {
              "name": {"type": "string"},
              "email": {"type": "string"},
              "plan_interest": {"type": "string"},
              "demo_requested": {"type": "boolean"}
            },
            "required": ["name", "email", "plan_interest", "demo_requested"],
            "additionalProperties": false
          }
        }
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/MODEL:rawPredict"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/MODEL:rawPredict" | Select-Object -Expand Content

You should receive a JSON response similar to the following. The `text` field of the `content` block contains a JSON string that conforms to the schema you specified in `output_config` .

#### Response

    {
      "id": "msg_vrtx_01ABcdEFghIJklMNopQRstUV",
      "type": "message",
      "role": "assistant",
      "model": "claude-opus-4-7",
      "content": [
        {
          "type": "text",
          "text": "{\"name\": \"John Smith\", \"email\": \"john@example.com\", \"plan_interest\": \"Enterprise\", \"demo_requested\": true}"
        }
      ],
      "stop_reason": "end_turn",
      "stop_sequence": null,
      "usage": {
        "input_tokens": 78,
        "output_tokens": 42
      }
    }

### Request fields

The following fields are specific to JSON outputs. For information about the other request fields, see the [Claude messages API reference](https://docs.anthropic.com/claude/reference/messages_post) .

  - `output_config` : The top-level configuration block that controls the structure of the model's response.

  - `output_config.format` : The format definition for the output. Only the `json_schema` type is supported.

  - `output_config.format.type` : The type of output format to enforce. Set this to `json_schema` to constrain the response to a JSON object.

  - `output_config.format.schema` : A JSON schema that defines the required structure of the model's response. Structured outputs support standard JSON Schema with some limitations, such as requiring `additionalProperties` to be set to `false` for objects and not supporting numerical or string-length constraints. For the full list of supported and unsupported features, see Anthropic's [JSON Schema limitations](https://platform.claude.com/docs/en/build-with-claude/structured-outputs#json-schema-limitations) documentation. Within the schema, you typically specify:
    
      - `type` : The JSON type of the value at this level (most commonly `object` for the root schema).
      - `properties` : A map of field names to their type definitions, which describe each field that the model must return.
      - `required` : A list of property names that the model must include in its response.
      - `additionalProperties` : A boolean that, when set to `false` , prevents the model from including any fields that aren't declared in `properties` .

## Use strict tool use

Strict tool use ensures that the arguments the model passes to a tool match the tool's `input_schema` . Without strict mode, the model might call a tool with incorrectly-typed arguments (for example, `"2"` instead of `2` ) or omit required fields, which can break your downstream functions and require retry logic. With strict mode enabled, the API uses grammar-constrained sampling to ensure that:

  - The tool `name` is always one of the tools you provided.
  - The tool `input` always conforms to the tool's `input_schema` .

Use strict tool use when you need to validate tool parameters, build agentic workflows, ensure type-safe function calls, or handle complex tools with nested properties.

To enable strict tool use, set `"strict": true` as a top-level field in your tool definition, alongside `name` , `description` , and `input_schema` .

### REST

The following sample shows how to send a request to the Agent Platform API that defines a strict `get_weather` tool. The model is guaranteed to call the tool with a `location` string and an optional `unit` that is either `celsius` or `fahrenheit` .

Before using any of the request data, make the following replacements:

  - LOCATION : A [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs#regions) that supports Anthropic Claude models. To use the global endpoint, see [Specify the global endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/use-partner-models#global) .

  - MODEL : A [supported Claude model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs#models) , for example `claude-opus-4-7` .

  - ROLE : The role associated with a message. The first message must use the `user` role.

  - CONTENT : The content, such as text, of the `user` or `assistant` message. For example, `What is the weather in San Francisco?`

  - MAX\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately 3.5 characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

  - STREAM : A boolean that specifies whether the response is streamed or not. Set to `true` to stream the response and `false` to return the response all at once.

The example uses the following strict tool use fields. For details on each field, see the [Strict tool use fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/structured-outputs#strict-tool-use-fields) section.

  - `tools[].strict` : A boolean that, when set to `true` , enables grammar-constrained sampling for the tool. The model is guaranteed to call the tool with arguments that match the `input_schema` .
  - `tools[].input_schema` : A JSON schema that defines the arguments that the model can pass to the tool. When `strict` is `true` , the schema must conform to the same [supported JSON Schema subset](https://platform.claude.com/docs/en/build-with-claude/structured-outputs#json-schema-limitations) as the `output_config` schema for JSON outputs.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/MODEL:rawPredict

Request JSON body:

    {
      "anthropic_version": "vertex-2023-10-16",
      "messages": [
        {
          "role": "ROLE",
          "content": "CONTENT"
        }
      ],
      "max_tokens": MAX_TOKENS,
      "stream": STREAM,
      "tools": [
        {
          "name": "get_weather",
          "description": "Get the current weather in a given location",
          "strict": true,
          "input_schema": {
            "type": "object",
            "properties": {
              "location": {
                "type": "string",
                "description": "The city and state, for example San Francisco, CA"
              },
              "unit": {
                "type": "string",
                "enum": ["celsius", "fahrenheit"]
              }
            },
            "required": ["location"],
            "additionalProperties": false
          }
        }
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/MODEL:rawPredict"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/MODEL:rawPredict" | Select-Object -Expand Content

You should receive a JSON response similar to the following. The `tool_use` content block contains an `input` field whose keys and value types are guaranteed to match the tool's `input_schema` .

#### Response

    {
      "id": "msg_vrtx_01ABcdEFghIJklMNopQRstUV",
      "type": "message",
      "role": "assistant",
      "model": "claude-opus-4-7",
      "content": [
        {
          "type": "tool_use",
          "id": "toolu_vrtx_01TAJCTkxe8HhRoaQ69N4ouP",
          "name": "get_weather",
          "input": {
            "location": "San Francisco, CA",
            "unit": "fahrenheit"
          }
        }
      ],
      "stop_reason": "tool_use",
      "stop_sequence": null,
      "usage": {
        "input_tokens": 412,
        "output_tokens": 64
      }
    }

### Strict tool use fields

The following fields are specific to strict tool use. For information about the other tool definition fields, see Anthropic's [Define tools](https://platform.claude.com/docs/en/agents-and-tools/tool-use/define-tools) documentation.

  - `tools[].strict` : A boolean that, when set to `true` , enables grammar-constrained sampling for the tool. When `strict` is `true` , the model's tool input is constrained to match the schema in `input_schema` . The default value is `false` .

  - `tools[].input_schema` : A JSON schema that defines the arguments the model can pass to the tool. When `strict` is `true` , the schema must conform to the same JSON Schema subset that JSON outputs use. In particular, you must:
    
      - Set `additionalProperties` to `false` on every object in the schema.
      - List every property in the `required` array.
    
    For the full list of supported and unsupported features, see Anthropic's [JSON Schema limitations](https://platform.claude.com/docs/en/build-with-claude/structured-outputs#json-schema-limitations) documentation.
