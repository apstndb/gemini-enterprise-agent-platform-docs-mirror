---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.interactions/createStream
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.interactions/createStream
title: 'Method: interactions.createStream'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.interactions.createStream

Creates an interaction and streams the response.

### Endpoint

post `https: / /{service-endpoint} /v1 /projects /* /locations /* /interactions:createStream`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Request body

The request body contains data with the following structure:

Fields

`stream` `boolean`

Input only. Whether the interaction will be streamed.

`store` `boolean`

Input only. Whether to store the response and request for later retrieval.

`interaction.id` `string`

Required. Output only. A unique identifier for the interaction completion.

`interaction.status` `enum ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Status)` )`

Required. Output only. The status of the interaction.

`interaction.created` `string`

Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`interaction.updated` `string`

Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).

`interaction.systemInstruction` `string`

System instruction for the interaction.

`interaction.tools[].function.name` `string`

The name of the function.

`interaction.tools[].function.description` `string`

A description of the function.

`interaction.stepList.steps[].toolCall.id` `string`

Required. A unique id for this specific tool call.

`interaction.stepList.steps[].toolCall.signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`interaction.stepList.steps[].toolCall.functionCall.name` `string`

Required. The name of the tool to call.

`interaction.stepList.steps[].toolCall.functionCall.arguments` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Struct)` )`

Required. The arguments to pass to the function.

`interaction.usage` `object ( `[`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Usage)` )`

Output only. Statistics on the interaction request's token usage.

`interaction.previousInteractionId` `string`

The id of the previous interaction, if any.

`interaction.environmentId` `string`

Output only. The environment id for the interaction. Only populated if environment config is set in the request.

`interaction.steps[]` `object ( `[`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step)` )`

Required. Output only. The steps that make up the interaction, when included in the response.

`interaction.safetySettings[]` `object ( `[`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#SafetySetting)` )`

Safety settings for the interaction.

`interaction.labels` `map (key: string, value: string)`

The labels with user-defined metadata for the request.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`interaction.errors[]` `object ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Error)` )`

Output only. Diagnostic faults / platform errors recorded on the interaction.

`background` `boolean`

Input only. Whether to run the model interaction in the background.

`kind` `Union type`

The kind of value. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.tools[].function.parameters.nullValue` `null`

Represents a null value.

`interaction.tools[].function.parameters.numberValue` `number`

Represents a double value.

`interaction.tools[].function.parameters.stringValue` `string`

Represents a string value.

`interaction.tools[].function.parameters.boolValue` `boolean`

Represents a boolean value.

`interaction.tools[].function.parameters.structValue` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Struct)` )`

Represents a structured value.

`interaction.tools[].function.parameters.listValue` `object ( `[`ListValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Value#ListValue)` )`

Represents a repeated `value` .

`interaction.tools[].function.parameters.contentValue` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Represents rich content (text, image, etc.).

End of mutually exclusive fields.

`type` `Union type`

The tool to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.tools[].function` `object ( `[`Function`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#Function)` )`

A function that can be used by the model.

`interaction.tools[].codeExecution` `object ( `[`CodeExecution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#CodeExecution)` )`

A tool that can be used by the model to execute code.

`interaction.tools[].urlContext` `object ( `[`UrlContext`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#UrlContext)` )`

A tool that can be used by the model to fetch URL context.

`interaction.tools[].computerUse` `object ( `[`ComputerUse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ComputerUse)` )`

Tool to support the model interacting directly with the computer.

`interaction.tools[].mcpServer` `object ( `[`McpServer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#McpServer)` )`

A MCPServer is a server that can be called by the model to perform actions.

`interaction.tools[].googleSearch` `object ( `[`GoogleSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#GoogleSearch)` )`

A tool that can be used by the model to search Google.

`interaction.tools[].fileSearch` `object ( `[`FileSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#FileSearch)` )`

A tool that can be used by the model to search files.

`interaction.tools[].googleMaps` `object ( `[`GoogleMaps`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#GoogleMaps)` )`

A tool that can be used by the model to search Google Maps.

`interaction.tools[].retrieval` `object ( `[`Retrieval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#Retrieval)` )`

A tool that can be used by the model to retrieve files.

End of mutually exclusive fields.

`input` `Union type`

The input for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stringContent` `string`

A string input for the interaction, it will be processed as a single text input.

`interaction.stepList` `object ( `[`StepList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#StepList)` )`

Input only. The steps for the interaction.

`interaction.content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

The content for the interaction.

End of mutually exclusive fields.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].thought` `object ( `[`ThoughtStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ThoughtStep)` )`

`interaction.stepList.steps[].toolCall` `object ( `[`ToolCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ToolCallStep)` )`

`interaction.stepList.steps[].toolResult` `object ( `[`ToolResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ToolResultStep)` )`

`interaction.stepList.steps[].userInput` `object ( `[`UserInputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#UserInputStep)` )`

DO NOT USE -- These are for 3P JSON only

`interaction.stepList.steps[].modelOutput` `object ( `[`ModelOutputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#ModelOutputStep)` )`

End of mutually exclusive fields.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.stepList.steps[].toolCall.functionCall` `object ( `[`FunctionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#FunctionCallStep)` )`

`interaction.stepList.steps[].toolCall.codeExecutionCall` `object ( `[`CodeExecutionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#CodeExecutionCallStep)` )`

`interaction.stepList.steps[].toolCall.urlContextCall` `object ( `[`UrlContextCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#UrlContextCallStep)` )`

`interaction.stepList.steps[].toolCall.googleSearchCall` `object ( `[`GoogleSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#GoogleSearchCallStep)` )`

`interaction.stepList.steps[].toolCall.fileSearchCall` `object ( `[`FileSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#FileSearchCallStep)` )`

`interaction.stepList.steps[].toolCall.googleMapsCall` `object ( `[`GoogleMapsCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#GoogleMapsCallStep)` )`

`interaction.stepList.steps[].toolCall.retrievalCall` `object ( `[`RetrievalCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Step#RetrievalCallStep)` )`

End of mutually exclusive fields.

`response_format_config` `Union type`

Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.responseFormatList` `object ( `[`ResponseFormatList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ResponseFormatList)` )`

`interaction.responseFormatSingleton` `object ( `[`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ResponseFormat)` )`

End of mutually exclusive fields.

`request_type` `Union type`

The request type for the interaction. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.modelInteraction` `object ( `[`ModelInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#ModelInteraction)` )`

Interaction for generating the completion using models.

`interaction.agentInteraction` `object ( `[`AgentInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Interaction#AgentInteraction)` )`

Interaction for generating the completion using agents.

End of mutually exclusive fields.

`environment` `Union type`

The environment configuration for the interaction. Can be an object specifying remote environment sources or a string referencing an existing environment ID. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interaction.envId` `string`

The environment id for the interaction. Can be 'remote' for default environment.

End of mutually exclusive fields.

### Response body

If successful, the response body contains a stream of [`InteractionStreamingEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/InteractionStreamingEvent) instances.

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `aiplatform.interactions.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
