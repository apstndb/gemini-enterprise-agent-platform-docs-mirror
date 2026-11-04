---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.learning.vertex.api.interactions.v1
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.learning.vertex.api.interactions.v1
title: Package google.learning.vertex.api.interactions.v1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

- [`InteractionsService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.learning.vertex.api.interactions.v1#google.learning.vertex.api.interactions.v1.InteractionsService) (interface)

## InteractionsService

API that allows users to interact with models and agents.

**CancelInteraction**

`rpc CancelInteraction( `[`CancelInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CancelInteractionRequest)` ) returns ( `[`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction)` )`

Cancels an interaction.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `aiplatform.interactions.cancel`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**CancelInteractionHttp**

`rpc CancelInteractionHttp( `[`CancelInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CancelInteractionRequest)` ) returns ( `[`HttpBody`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.api#google.api.HttpBody)` )`

Cancels an interaction by id. This only applies to background interactions that are still running.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateInteraction**

`rpc CreateInteraction( `[`CreateInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CreateInteractionRequest)` ) returns ( `[`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction)` )`

Creates an interaction.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `aiplatform.interactions.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**CreateInteractionHttp**

`rpc CreateInteractionHttp( `[`CreateInteractionHttpRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CreateInteractionHttpRequest)` ) returns ( `[`HttpBody`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.api#google.api.HttpBody)` )`

Creates a new interaction.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `aiplatform.interactions.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**CreateInteractionStream**

`rpc CreateInteractionStream( `[`CreateInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CreateInteractionRequest)` ) returns ( `[`InteractionStreamingEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionStreamingEvent)` )`

Creates an interaction and streams the response.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `aiplatform.interactions.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**DeleteInteraction**

> This item is deprecated!

`rpc DeleteInteraction( `[`DeleteInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeleteInteractionRequest)` ) returns ( `[`DeleteInteractionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeleteInteractionResponse)` )`

Deletes an interaction.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `aiplatform.interactions.delete`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**GetInteraction**

`rpc GetInteraction( `[`GetInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GetInteractionRequest)` ) returns ( `[`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction)` )`

Fully typed proto, unary version of GetInteraction that returns Interaction proto.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `aiplatform.interactions.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**GetInteractionHttp**

`rpc GetInteractionHttp( `[`GetInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GetInteractionRequest)` ) returns ( `[`HttpBody`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.api#google.api.HttpBody)` )`

Retrieves the full details of a single interaction based on its `Interaction.id` .

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetInteractionStream**

`rpc GetInteractionStream( `[`GetInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GetInteractionRequest)` ) returns ( `[`InteractionStreamingEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionStreamingEvent)` )`

Fully typed proto, streaming version of GetInteraction that returns Interaction proto.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `aiplatform.interactions.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**ListInteractions**

`rpc ListInteractions( `[`ListInteractionsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListInteractionsRequest)` ) returns ( `[`ListInteractionsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListInteractionsResponse)` )`

List interactions.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `aiplatform.interactions.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**ListInteractionsHttp**

`rpc ListInteractionsHttp( `[`ListInteractionsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListInteractionsRequest)` ) returns ( `[`HttpBody`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.api#google.api.HttpBody)` )`

List interactions.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `aiplatform.interactions.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
