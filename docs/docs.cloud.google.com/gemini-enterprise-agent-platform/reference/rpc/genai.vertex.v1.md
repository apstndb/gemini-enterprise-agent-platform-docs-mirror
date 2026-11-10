---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1
title: Package genai.vertex.v1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

- [`AgentInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AgentInteraction) (message)
- [`AllowedTools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AllowedTools) (message)
- [`ArgumentsDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ArgumentsDelta) (message)
- [`AudioContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioContent) (message)
- [`AudioContent.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioContent.MimeType) (enum)
- [`AudioDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioDelta) (message)
- [`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioResponseFormat) (message)
- [`AudioResponseFormat.Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioResponseFormat.Delivery) (enum)
- [`AudioResponseFormat.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioResponseFormat.MimeType) (enum)
- [`CancelInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CancelInteractionRequest) (message)
- [`CodeExecution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecution) (message)
- [`CodeExecutionCallContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallContent) (message) **(deprecated)**
- [`CodeExecutionCallContent.CodeExecutionCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallContent.CodeExecutionCallArguments) (message)
- [`CodeExecutionCallContent.CodeExecutionCallArguments.Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallContent.CodeExecutionCallArguments.Language) (enum)
- [`CodeExecutionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallDelta) (message)
- [`CodeExecutionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallStep) (message)
- [`CodeExecutionCallStep.CodeExecutionCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallStep.CodeExecutionCallStepArguments) (message)
- [`CodeExecutionCallStep.CodeExecutionCallStepArguments.Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallStep.CodeExecutionCallStepArguments.Language) (enum)
- [`CodeExecutionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionResultDelta) (message)
- [`CodeExecutionResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionResultStep) (message)
- [`CodeMenderAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig) (message)
- [`CodeMenderAgentConfig.FileContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FileContent) (message)
- [`CodeMenderAgentConfig.FindRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FindRequest) (message)
- [`CodeMenderAgentConfig.FindRequest.Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FindRequest.Mode) (enum)
- [`CodeMenderAgentConfig.FixRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FixRequest) (message)
- [`CodeMenderAgentConfig.SessionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.SessionConfig) (message)
- [`ComputerUse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ComputerUse) (message)
- [`ComputerUse.Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ComputerUse.Environment) (enum)
- [`ComputerUse.SafetyPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ComputerUse.SafetyPolicy) (enum)
- [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) (message)
- [`ContentDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentDelta) (message)
- [`ContentDeltaData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentDeltaData) (message)
- [`ContentList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentList) (message)
- [`ContentStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentStart) (message)
- [`ContentStop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentStop) (message)
- [`CreateInteractionHttpRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CreateInteractionHttpRequest) (message)
- [`CreateInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CreateInteractionRequest) (message)
- [`DeepResearchAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeepResearchAgentConfig) (message)
- [`DeepResearchAgentConfig.VisualizationMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeepResearchAgentConfig.VisualizationMode) (enum)
- [`DeleteInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeleteInteractionRequest) (message)
- [`DeleteInteractionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeleteInteractionResponse) (message)
- [`DocumentContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentContent) (message)
- [`DocumentContent.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentContent.MimeType) (enum)
- [`DocumentDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentDelta) (message)
- [`DynamicAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DynamicAgentConfig) (message)
- [`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Error) (message)
- [`ErrorEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ErrorEvent) (message)
- [`ExaAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ExaAISearchConfig) (message)
- [`Field`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Field) (message)
- [`FileCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileCitation) (message)
- [`FileSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearch) (message)
- [`FileSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchCallDelta) (message)
- [`FileSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchCallStep) (message)
- [`FileSearchResultContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultContent) (message) **(deprecated)**
- [`FileSearchResultContent.FileSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultContent.FileSearchResult) (message)
- [`FileSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultDelta) (message)
- [`FileSearchResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultStep) (message)
- [`Function`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Function) (message)
- [`FunctionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionCallDelta) (message)
- [`FunctionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionCallStep) (message)
- [`FunctionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionResultDelta) (message)
- [`FunctionResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionResultStep) (message)
- [`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GenerationConfig) (message)
- [`GetInteractionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GetInteractionRequest) (message)
- [`GoogleMaps`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMaps) (message)
- [`GoogleMapsCallContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallContent) (message) **(deprecated)**
- [`GoogleMapsCallContent.GoogleMapsCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallContent.GoogleMapsCallArguments) (message)
- [`GoogleMapsCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallDelta) (message)
- [`GoogleMapsCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallStep) (message)
- [`GoogleMapsCallStep.GoogleMapsCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallStep.GoogleMapsCallStepArguments) (message)
- [`GoogleMapsResultContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultContent) (message) **(deprecated)**
- [`GoogleMapsResultContent.GoogleMapsResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultContent.GoogleMapsResult) (message)
- [`GoogleMapsResultContent.GoogleMapsResult.Places`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultContent.GoogleMapsResult.Places) (message)
- [`GoogleMapsResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultDelta) (message)
- [`GoogleMapsResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultStep) (message)
- [`GoogleMapsResultStep.GoogleMapsResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultStep.GoogleMapsResultItem) (message)
- [`GoogleMapsResultStep.GoogleMapsResultItem.GoogleMapsResultPlaces`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultStep.GoogleMapsResultItem.GoogleMapsResultPlaces) (message)
- [`GoogleSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearch) (message)
- [`GoogleSearch.SearchType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearch.SearchType) (enum)
- [`GoogleSearchCallContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallContent) (message) **(deprecated)**
- [`GoogleSearchCallContent.GoogleSearchCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallContent.GoogleSearchCallArguments) (message)
- [`GoogleSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallDelta) (message)
- [`GoogleSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallStep) (message)
- [`GoogleSearchCallStep.GoogleSearchCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallStep.GoogleSearchCallStepArguments) (message)
- [`GoogleSearchResultContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultContent) (message) **(deprecated)**
- [`GoogleSearchResultContent.GoogleSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultContent.GoogleSearchResult) (message)
- [`GoogleSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultDelta) (message)
- [`GoogleSearchResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultStep) (message)
- [`GoogleSearchResultStep.GoogleSearchResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultStep.GoogleSearchResultItem) (message)
- [`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.HarmCategory) (enum)
- [`ImageContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageContent) (message)
- [`ImageContent.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageContent.MimeType) (enum)
- [`ImageDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageDelta) (message)
- [`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat) (message)
- [`ImageResponseFormat.AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.AspectRatio) (enum)
- [`ImageResponseFormat.Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.Delivery) (enum)
- [`ImageResponseFormat.ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.ImageSize) (enum)
- [`ImageResponseFormat.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.MimeType) (enum)
- [`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction) (message)
- [`Interaction.Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Status) (enum)
- [`Interaction.Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage) (message)
- [`Interaction.Usage.GroundingToolCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.GroundingToolCount) (message)
- [`Interaction.Usage.GroundingToolCount.Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.GroundingToolCount.Type) (enum)
- [`Interaction.Usage.ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.ModalityTokens) (message)
- [`InteractionCompletedSseEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionCompletedSseEvent) (message)
- [`InteractionCreatedSseEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionCreatedSseEvent) (message)
- [`InteractionMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionMetadata) (message)
- [`InteractionStatusUpdate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionStatusUpdate) (message)
- [`InteractionStreamingEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionStreamingEvent) (message)
- [`ListInteractionsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListInteractionsRequest) (message)
- [`ListInteractionsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListInteractionsResponse) (message)
- [`ListValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListValue) (message)
- [`McpServer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.McpServer) (message)
- [`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.MediaResolution) (enum)
- [`ModelInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ModelInteraction) (message)
- [`ModelOutputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ModelOutputStep) (message)
- [`ParallelAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ParallelAISearchConfig) (message)
- [`PlaceCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.PlaceCitation) (message)
- [`RagStoreConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig) (message)
- [`RagStoreConfig.RagResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagResource) (message)
- [`RagStoreConfig.RagRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig) (message)
- [`RagStoreConfig.RagRetrievalConfig.Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.Filter) (message)
- [`RagStoreConfig.RagRetrievalConfig.HybridSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.HybridSearch) (message)
- [`RagStoreConfig.RagRetrievalConfig.Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.Ranking) (message)
- [`RagStoreConfig.RagRetrievalConfig.Ranking.RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.Ranking.RankService) (message)
- [`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseFormat) (message)
- [`ResponseFormatList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseFormatList) (message)
- [`ResponseModality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseModality) (enum)
- [`Retrieval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Retrieval) (message)
- [`Retrieval.RetrievalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Retrieval.RetrievalType) (enum)
- [`RetrievalCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallDelta) (message)
- [`RetrievalCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallStep) (message)
- [`RetrievalCallStep.RetrievalStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallStep.RetrievalStepArguments) (message)
- [`RetrievalResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalResultDelta) (message)
- [`RetrievalResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalResultStep) (message)
- [`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ReviewSnippet) (message)
- [`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.SafetySetting) (message)
- [`SafetySetting.HarmBlockMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.SafetySetting.HarmBlockMethod) (enum)
- [`SafetySetting.HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.SafetySetting.HarmBlockThreshold) (enum)
- [`ServerToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ServerToolCallDelta) (message)
- [`ServerToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ServerToolResultDelta) (message)
- [`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Step) (message)
- [`StepDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepDelta) (message)
- [`StepDeltaData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepDeltaData) (message)
- [`StepList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepList) (message)
- [`StepStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepStart) (message)
- [`StepStop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepStop) (message)
- [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) (message)
- [`TextAnnotationDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextAnnotationDelta) (message)
- [`TextContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextContent) (message)
- [`TextContent.Annotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextContent.Annotation) (message)
- [`TextDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextDelta) (message)
- [`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextResponseFormat) (message)
- [`TextResponseFormat.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextResponseFormat.MimeType) (enum)
- [`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThinkingLevel) (enum)
- [`ThinkingSummaries`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThinkingSummaries) (enum)
- [`ThoughtSignatureDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtSignatureDelta) (message)
- [`ThoughtStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtStep) (message)
- [`ThoughtSummaryDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtSummaryDelta) (message)
- [`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Tool) (message)
- [`ToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolCallDelta) (message)
- [`ToolCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolCallStep) (message)
- [`ToolChoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolChoiceConfig) (message)
- [`ToolChoiceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolChoiceType) (enum)
- [`ToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolResultDelta) (message)
- [`ToolResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolResultStep) (message)
- [`TranscriptionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TranscriptionConfig) (message)
- [`UrlCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlCitation) (message)
- [`UrlContext`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContext) (message)
- [`UrlContextCallContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallContent) (message) **(deprecated)**
- [`UrlContextCallContent.UrlContextCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallContent.UrlContextCallArguments) (message)
- [`UrlContextCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallDelta) (message)
- [`UrlContextCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallStep) (message)
- [`UrlContextCallStep.UrlContextCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallStep.UrlContextCallStepArguments) (message)
- [`UrlContextResultContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultContent) (message) **(deprecated)**
- [`UrlContextResultContent.UrlContextResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultContent.UrlContextResult) (message)
- [`UrlContextResultContent.UrlContextResult.Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultContent.UrlContextResult.Status) (enum)
- [`UrlContextResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultDelta) (message)
- [`UrlContextResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultStep) (message)
- [`UrlContextResultStep.UrlContextResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultStep.UrlContextResultItem) (message)
- [`UrlContextResultStep.UrlContextResultItem.Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultStep.UrlContextResultItem.Status) (enum)
- [`UserInputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UserInputStep) (message)
- [`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Value) (message)
- [`VertexAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VertexAISearchConfig) (message)
- [`VideoConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoConfig) (message)
- [`VideoConfig.Task`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoConfig.Task) (enum)
- [`VideoContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent) (message)
- [`VideoContent.MediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.MediaProcessing) (message)
- [`VideoContent.MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.MimeType) (enum)
- [`VideoContent.Processing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.Processing) (enum)
- [`VideoContent.StaticMediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.StaticMediaProcessing) (message)
- [`VideoDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoDelta) (message)
- [`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat) (message)
- [`VideoResponseFormat.AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat.AspectRatio) (enum)
- [`VideoResponseFormat.Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat.Delivery) (enum)
- [`VideoResponseFormat.Resolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat.Resolution) (enum)
- [`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.WordInfo) (message)

## AgentInteraction

Interaction for generating the completion using agents.

| Fields                                                                                                                            |                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `agent`                                                                                                                           | `string` The name of the `Agent` used for generating the completion.                                                                                              |
| Union field `agent_config` . Configuration parameters for the agent interaction. `agent_config` can be only one of the following: |                                                                                                                                                                   |
| `dynamic_config`                                                                                                                  | [`DynamicAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DynamicAgentConfig)           |
| `deep_research_config`                                                                                                            | [`DeepResearchAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeepResearchAgentConfig) |
| `code_mender_config`                                                                                                              | [`CodeMenderAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig)     |

## AllowedTools

The configuration for allowed tools.

| Fields    |                                                                                                                                                                              |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode`    | [`ToolChoiceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolChoiceType) The mode of the tool choice. |
| `tools[]` | `string` The names of the allowed tools.                                                                                                                                     |

## ArgumentsDelta

| Fields      |          |
|-------------|----------|
| `arguments` | `string` |

## AudioContent

An audio content block.

| Fields                                                                                         |                                                                                                                                                                      |
|------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type_string`                                                                             | `string` Flexible MIME type string of the audio, superseding mime_type = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mime_type" JSON key. |
| `channels`                                                                                     | `int32` The number of audio channels.                                                                                                                                |
| `sample_rate`                                                                                  | `int32` The sample rate of the audio.                                                                                                                                |
| Union field `data_or_uri` . The audio content. `data_or_uri` can be only one of the following: |                                                                                                                                                                      |
| `data`                                                                                         | `bytes` The audio content.                                                                                                                                           |
| `uri`                                                                                          | `string` The URI of the audio.                                                                                                                                       |

## MimeType

| Enums                    |                                     |
|--------------------------|-------------------------------------|
| `TYPE_UNSPECIFIED`       |                                     |
| `TYPE_WAV`               | WAV audio format                    |
| `TYPE_MP3`               | MP3 audio format                    |
| `TYPE_AIFF`              | AIFF audio format                   |
| `TYPE_AAC`               | AAC audio format                    |
| `TYPE_OGG`               | OGG audio format                    |
| `TYPE_FLAC`              | FLAC audio format                   |
| `TYPE_MPEG`              | MPEG audio format                   |
| `TYPE_M4A`               | M4A audio format                    |
| `TYPE_L16`               | L16 audio format                    |
| `TYPE_S16LE`             | S16LE audio format                  |
| `TYPE_OPUS`              | OPUS audio format                   |
| `TYPE_ALAW`              | ALAW audio format                   |
| `TYPE_MULAW`             | MULAW audio format                  |
| `TYPE_VIDEO_AUDIO_S16LE` | Video audio S16LE format (internal) |
| `TYPE_WEBM`              | WEBM audio format                   |

## AudioDelta

| Fields                                                                      |                                                                                                                                                  |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type`                                                                 | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioContent.MimeType) |
| `sample_rate`                                                               | `int32` The sample rate of the audio.                                                                                                            |
| `channels`                                                                  | `int32` The number of audio channels.                                                                                                            |
| Union field `data_or_uri` . `data_or_uri` can be only one of the following: |                                                                                                                                                  |
| `data`                                                                      | `bytes`                                                                                                                                          |
| `uri`                                                                       | `string`                                                                                                                                         |

## AudioResponseFormat

Configuration for audio output format.

| Fields        |                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type`   | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioResponseFormat.MimeType) The MIME type of the audio output.      |
| `delivery`    | [`Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioResponseFormat.Delivery) The delivery mode for the audio output. |
| `sample_rate` | `int32` Sample rate in Hz.                                                                                                                                                                      |
| `bit_rate`    | `int32` Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).                                                                                                  |

## Delivery

Delivery mode for audio output.

| Enums                  |                                                |
|------------------------|------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.           |
| `INLINE`               | Audio data is returned inline in the response. |
| `URI`                  | Audio data is returned as a URI.               |

## MimeType

Supported MIME types for audio output.

| Enums              |                                      |
|--------------------|--------------------------------------|
| `TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `TYPE_MP3`         | MP3 audio format.                    |
| `TYPE_OGG_OPUS`    | OGG Opus audio format.               |
| `TYPE_L16`         | Raw PCM (L16) audio format.          |
| `TYPE_WAV`         | WAV audio format.                    |
| `TYPE_ALAW`        | A-law audio format.                  |
| `TYPE_MULAW`       | Mu-law audio format.                 |

## CancelInteractionRequest

| Fields |                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The name of the interaction to cancel. Format: `interactions/{interaction}` . |

## CodeExecution

This type has no fields.

A tool that can be used by the model to execute code.

## CodeExecutionCallContent

This type has no fields.

> This item is deprecated!

Code execution content.

## CodeExecutionCallArguments

The arguments to pass to the code execution.

| Fields     |                                                                                                                                                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `language` | [`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallContent.CodeExecutionCallArguments.Language) Programming language of the `code` . |
| `code`     | `string` The code to be executed.                                                                                                                                                                                            |

## Language

Supported programming languages for the generated code.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `LANGUAGE_UNSPECIFIED` | Unspecified language. This value should not be used. |
| `PYTHON`               | Python \>= 3.10, with numpy and simpy available.     |

## CodeExecutionCallDelta

| Fields      |                                                                                                                                                                                                  |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`CodeExecutionCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallContent.CodeExecutionCallArguments) |

## CodeExecutionCallStep

Code execution call step.

| Fields      |                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`CodeExecutionCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallStep.CodeExecutionCallStepArguments) Required. The arguments to pass to the code execution. |

## CodeExecutionCallStepArguments

The arguments to pass to the code execution.

| Fields     |                                                                                                                                                                                                                               |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `language` | [`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallStep.CodeExecutionCallStepArguments.Language) Programming language of the `code` . |
| `code`     | `string` The code to be executed.                                                                                                                                                                                             |

## Language

Supported programming languages for the generated code.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `LANGUAGE_UNSPECIFIED` | Unspecified language. This value should not be used. |
| `PYTHON`               | Python \>= 3.10, with numpy and simpy available.     |

## CodeExecutionResultDelta

| Fields     |          |
|------------|----------|
| `result`   | `string` |
| `is_error` | `bool`   |

## CodeExecutionResultStep

Code execution result step.

| Fields                                                                                              |                                                         |
|-----------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `is_error`                                                                                          | `bool` Whether the code execution resulted in an error. |
| Union field `output` . The output of the code execution. `output` can be only one of the following: |                                                         |
| `result`                                                                                            | `string` Required. The output of the code execution.    |

## CodeMenderAgentConfig

Configuration for the CodeMender agent.

| Fields                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                                                                                                                                                                                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `session_id`                                                                                                                                                                                                                                                                                                                                                                                                | `string` Parameter for grouping multiple interactions that belong to the same CodeMender session.                                                                                                                                                |
| `session_config`                                                                                                                                                                                                                                                                                                                                                                                            | [`SessionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.SessionConfig) Optional session-specific configurations to override default agent behavior. |
| `model`                                                                                                                                                                                                                                                                                                                                                                                                     | `string` The name of the model to use for the CodeMender agent. One CodeMender session will only use one model.                                                                                                                                  |
| Union field `request` . CodeMender's request type. Set exactly one of find_request/fix_request only on the first round to start a session; on subsequent rounds (e.g. submitting tool results), leave this unset and identify the session via session_id. This oneof is intentionally not a subtype_source discriminator so it can be omitted on resume rounds. `request` can be only one of the following: |                                                                                                                                                                                                                                                  |
| `find_request`                                                                                                                                                                                                                                                                                                                                                                                              | [`FindRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FindRequest) Parameters for finding vulnerabilities.                                          |
| `fix_request`                                                                                                                                                                                                                                                                                                                                                                                               | [`FixRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FixRequest) Parameters for fixing vulnerabilities.                                             |

## FileContent

Content of a single file in the codebase.

| Fields    |                                                               |
|-----------|---------------------------------------------------------------|
| `path`    | `string` The relative path of the file from the project root. |
| `content` | `string` The UTF-8 encoded text content of the file.          |

## FindRequest

Request parameters specific to FIND sessions, used for discovering vulnerabilities in a codebase.

| Fields           |                                                                                                                                                                                                                            |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `source_files[]` | [`FileContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FileContent) A list of source files to provide as context for the scan. |
| `finding_id`     | `string` The identifier of a specific finding to verify. This is primarily used in VERIFY mode to focus the agent's execution-based validation on a single vulnerability.                                                  |
| `description`    | `string` Additional context or custom instructions provided by the user to guide the vulnerability analysis.                                                                                                               |
| `mode`           | [`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FindRequest.Mode) The mode of the find session.                                |

## Mode

Defines the depth and thoroughness of the find session.

| Enums              |                                                             |
|--------------------|-------------------------------------------------------------|
| `MODE_UNSPECIFIED` | Default value. This value is unused.                        |
| `MODE_SCAN`        | Fast scan using only the initial classifier.                |
| `MODE_VERIFY`      | Performs classification followed by detailed investigation. |

## FixRequest

Request parameters specific to FIX sessions, used for generating and validating security patches.

| Fields           |                                                                                                                                                                                                                                                                                                           |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `source_files[]` | [`FileContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeMenderAgentConfig.FileContent) A list of source files providing context for the remediation. These files are typically the ones containing the identified vulnerability. |
| `finding_id`     | `string` The identifier of the specific security finding to be remediated. This ID maps to a previously discovered vulnerability.                                                                                                                                                                         |
| `description`    | `string` Additional context or custom instructions provided by the user to guide the patch generation process.                                                                                                                                                                                            |

## SessionConfig

The configuration of CodeMender sessions.

| Fields       |                                                                                                             |
|--------------|-------------------------------------------------------------------------------------------------------------|
| `max_rounds` | `int32` The maximum number of interaction rounds the agent is allowed to perform before reaching a timeout. |

## ComputerUse

A tool that can be used by the model to interact with the computer.

| Fields                              |                                                                                                                                                                                                              |
|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `environment`                       | [`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ComputerUse.Environment) The environment being operated.                        |
| `excluded_predefined_functions[]`   | `string` The list of predefined functions that are excluded from the model call.                                                                                                                             |
| `enable_prompt_injection_detection` | `bool` Whether enable the prompt injection detection check on computer-use request.                                                                                                                          |
| `disabled_safety_policies[]`        | [`SafetyPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ComputerUse.SafetyPolicy) Optional. Disabled safety policies for computer use. |

## Environment

Represents the environment being operated, such as a web browser.

| Enums                     |                                    |
|---------------------------|------------------------------------|
| `ENVIRONMENT_UNSPECIFIED` | Defaults to browser.               |
| `BROWSER`                 | Operates in a web browser.         |
| `MOBILE`                  | Operates in a mobile environment.  |
| `DESKTOP`                 | Operates in a desktop environment. |

## SafetyPolicy

| Enums                         |                                                                 |
|-------------------------------|-----------------------------------------------------------------|
| `SAFETY_POLICY_UNSPECIFIED`   | Unspecified safety policy.                                      |
| `FINANCIAL_TRANSACTIONS`      | Safety policy for financial transactions.                       |
| `SENSITIVE_DATA_MODIFICATION` | Safety policy for sensitive data modification.                  |
| `COMMUNICATION_TOOL`          | Safety policy for communication tools (e.g. Gmail, Chat, Meet). |
| `ACCOUNT_CREATION`            | Safety policy for account creation.                             |
| `DATA_MODIFICATION`           | Safety policy for data modification.                            |
| `USER_CONSENT_MANAGEMENT`     | Safety policy for user consent management.                      |
| `LEGAL_TERMS_AND_AGREEMENTS`  | Safety policy for legal terms and agreements.                   |

## Content

The content of the response.

| Fields                                                        |                                                                                                                                                   |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                   |
| `text`                                                        | [`TextContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextContent)         |
| `image`                                                       | [`ImageContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageContent)       |
| `audio`                                                       | [`AudioContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioContent)       |
| `document`                                                    | [`DocumentContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentContent) |
| `video`                                                       | [`VideoContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent)       |

## ContentDelta

| Fields  |                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `index` | `int32`                                                                                                                                             |
| `delta` | [`ContentDeltaData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentDeltaData) |

## ContentDeltaData

The delta content data for a content block.

| Fields                                                                                       |                                                                                                                                                               |
|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . The type of the delta content. `type` can be only one of the following: |                                                                                                                                                               |
| `text`                                                                                       | [`TextDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextDelta)                         |
| `image`                                                                                      | [`ImageDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageDelta)                       |
| `audio`                                                                                      | [`AudioDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioDelta)                       |
| `document`                                                                                   | [`DocumentDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentDelta)                 |
| `video`                                                                                      | [`VideoDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoDelta)                       |
| `thought_summary`                                                                            | [`ThoughtSummaryDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtSummaryDelta)     |
| `thought_signature`                                                                          | [`ThoughtSignatureDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtSignatureDelta) |
| `tool_call`                                                                                  | [`ToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolCallDelta)                 |
| `tool_result`                                                                                | [`ToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolResultDelta)             |
| `text_annotation`                                                                            | [`TextAnnotationDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextAnnotationDelta)     |

## ContentList

A list of Content.

| Fields       |                                                                                                                                                             |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contents[]` | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) The contents of the list. |

## ContentStart

| Fields    |                                                                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| `index`   | `int32`                                                                                                                           |
| `content` | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) |

## ContentStop

| Fields  |         |
|---------|---------|
| `index` | `int32` |

## CreateInteractionHttpRequest

Request message for \[InteractionsService.CreateInteractionHttp\].

| Fields      |                                                                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`    | `string` Required. The parent resource where this interaction will be created. Format: `projects/{project}/locations/{location}` Supported only by the Vertex API only. |
| `http_body` | [`HttpBody`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.api#google.api.HttpBody) Required. The interaction to create.          |

## CreateInteractionRequest

Configuration parameters for creating an interaction.

| Fields        |                                                                                                                                                                      |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stream`      | `bool` Input only. Whether the interaction will be streamed.                                                                                                         |
| `store`       | `bool` Input only. Whether to store the response and request for later retrieval.                                                                                    |
| `interaction` | [`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction) The interaction to create. |
| `background`  | `bool` Input only. Whether to run the model interaction in the background.                                                                                           |

## DeepResearchAgentConfig

Configuration for the Deep Research agent.

| Fields                   |                                                                                                                                                                                                                                               |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `thinking_summaries`     | [`ThinkingSummaries`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThinkingSummaries) Whether to include thought summaries in the response.                                   |
| `visualization`          | [`VisualizationMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DeepResearchAgentConfig.VisualizationMode) Whether to include visualizations in the response.              |
| `collaborative_planning` | `bool` Enables human-in-the-loop planning for the Deep Research agent. If set to true, the Deep Research agent will provide a research plan in its response. The agent will then proceed only if the user confirms the plan in the next turn. |
| `enable_bigquery_tool`   | `bool` Enables bigquery tool for the Deep Research agent.                                                                                                                                                                                     |

## VisualizationMode

Enum for visualization mode. Eventually we will support an interactive mode where the user can choose whether to include HTML visualizations in the response.

| Enums         |                                                       |
|---------------|-------------------------------------------------------|
| `UNSPECIFIED` | The default visualization mode. Will default to AUTO. |
| `OFF`         | Do not include visualizations.                        |
| `AUTO`        | Automatically include visualizations.                 |

## DeleteInteractionRequest

Request for InteractionService.DeleteInteraction.

| Fields |                                                                                              |
|--------|----------------------------------------------------------------------------------------------|
| `name` | `string` Required. The name of the interaction to delete. Format: interactions/{interaction} |

## DeleteInteractionResponse

This type has no fields.

Response for InteractionService.DeleteInteraction.

## DocumentContent

A document content block.

| Fields                                                                                            |                                                                                                                                                                         |
|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type_string`                                                                                | `string` Flexible MIME type string of the document, superseding mime_type = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mime_type" JSON key. |
| Union field `data_or_uri` . The document content. `data_or_uri` can be only one of the following: |                                                                                                                                                                         |
| `data`                                                                                            | `bytes` The document content.                                                                                                                                           |
| `uri`                                                                                             | `string` The URI of the document.                                                                                                                                       |

## MimeType

| Enums              |                     |
|--------------------|---------------------|
| `TYPE_UNSPECIFIED` |                     |
| `TYPE_PDF`         | PDF document format |
| `TYPE_CSV`         | CSV document format |

## DocumentDelta

| Fields                                                                      |                                                                                                                                                     |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type`                                                                 | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentContent.MimeType) |
| Union field `data_or_uri` . `data_or_uri` can be only one of the following: |                                                                                                                                                     |
| `data`                                                                      | `bytes`                                                                                                                                             |
| `uri`                                                                       | `string`                                                                                                                                            |

## DynamicAgentConfig

Configuration for dynamic agents.

| Fields   |                                                                                                                                                                                                     |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `config` | [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) For agents that are not supported statically in the API definition. |

## Error

Error message from an interaction.

| Fields    |                                                |
|-----------|------------------------------------------------|
| `code`    | `string` A URI that identifies the error type. |
| `message` | `string` A human-readable error message.       |

## ErrorEvent

| Fields  |                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| `error` | [`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Error) |

## ExaAISearchConfig

Used to specify configuration for ExaAISearch.

| Fields          |                                                                                                                                                                |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_key`       | `string` Required. The API key for ExaAiSearch.                                                                                                                |
| `custom_config` | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) Optional. This field can be used to pass any parameter from the Exa.ai Search API. |

## Field

Represents a single field in a struct.

| Fields  |                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string`                                                                                                                      |
| `value` | [`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Value) |

## FileCitation

A file citation annotation.

| Fields            |                                                                                                                                 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------|
| `document_uri`    | `string` The URI of the file.                                                                                                   |
| `file_name`       | `string` The name of the file.                                                                                                  |
| `source`          | `string` Source attributed for a portion of the text.                                                                           |
| `custom_metadata` | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) User provided metadata about the retrieved context. |
| `page_number`     | `int32` Page number of the cited document, if applicable.                                                                       |
| `media_id`        | `string` Media ID in-case of image citations, if applicable.                                                                    |

## FileSearch

A tool that can be used by the model to search files.

| Fields                      |                                                                                   |
|-----------------------------|-----------------------------------------------------------------------------------|
| `file_search_store_names[]` | `string` The file search store names to search.                                   |
| `top_k`                     | `int32` The number of semantic retrieval chunks to retrieve.                      |
| `metadata_filter`           | `string` Metadata filter to apply to the semantic retrieval documents and chunks. |

## FileSearchCallDelta

This type has no fields.

## FileSearchCallStep

This type has no fields.

File Search call step.

## FileSearchResultContent

This type has no fields.

> This item is deprecated!

File Search result content.

## FileSearchResult

This type has no fields.

The result of the File Search.

## FileSearchResultDelta

| Fields     |                                                                                                                                                                             |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`FileSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultContent.FileSearchResult) |

## FileSearchResultStep

This type has no fields.

File Search result step.

## Function

A tool that can be used by the model.

| Fields        |                                                                                                                                                                                                                                                                                                                                                                             |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`        | `string` The name of the function.                                                                                                                                                                                                                                                                                                                                          |
| `description` | `string` A description of the function.                                                                                                                                                                                                                                                                                                                                     |
| `parameters`  | [`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Value) The JSON Schema for the function's parameters. Supports a subset of JSON Schema. `minLength` , `maxLength` , `minProperties` , `maxProperties` , `uniqueItems` , `contains` , `minContains` , and `maxContains` are ignored and not enforced. |

## FunctionCallDelta

| Fields      |                                                                                                                                 |
|-------------|---------------------------------------------------------------------------------------------------------------------------------|
| `name`      | `string`                                                                                                                        |
| `arguments` | [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) |

## FunctionCallStep

A function tool call step.

| Fields      |                                                                                                                                                                                  |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`      | `string` Required. The name of the tool to call.                                                                                                                                 |
| `arguments` | [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) Required. The arguments to pass to the function. |

## FunctionResultDelta

| Fields     |                                                                                                                               |
|------------|-------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string`                                                                                                                      |
| `is_error` | `bool`                                                                                                                        |
| `result`   | [`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Value) |

## FunctionResultStep

Result of a function tool call.

| Fields     |                                                                                                                                                                      |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` The name of the tool that was called.                                                                                                                       |
| `is_error` | `bool` Whether the tool call resulted in an error.                                                                                                                   |
| `result`   | [`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Value) Required. The result of the tool call. |

## GenerationConfig

Configuration parameters for model interactions.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>temperature </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>float</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Controls the randomness of the output.</p></td>
</tr>
<tr class="even">
<td><code>top_p </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>float</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The maximum cumulative probability of tokens to consider when sampling.</p></td>
</tr>
<tr class="odd">
<td><code>seed</code></td>
<td><p><code>int32</code></p>
<p>Seed used in decoding for reproducibility.</p></td>
</tr>
<tr class="even">
<td><code>stop_sequences[]</code></td>
<td><p><code>string</code></p>
<p>A list of character sequences that will stop output interaction.</p></td>
</tr>
<tr class="odd">
<td><code>thinking_level</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThinkingLevel"><code>ThinkingLevel</code></a></p>
<p>The level of thought tokens that the model should generate.</p></td>
</tr>
<tr class="even">
<td><code>thinking_summaries</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThinkingSummaries"><code>ThinkingSummaries</code></a></p>
<p>Whether to include thought summaries in the response.</p></td>
</tr>
<tr class="odd">
<td><code>max_output_tokens</code></td>
<td><p><code>int32</code></p>
<p>The maximum number of tokens to include in the response.</p></td>
</tr>
<tr class="even">
<td><code>video_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoConfig"><code>VideoConfig</code></a></p>
<p>Configuration for video generation.</p></td>
</tr>
<tr class="odd">
<td><code>transcription_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TranscriptionConfig"><code>TranscriptionConfig</code></a></p>
<p>Optional. Configuration for speech recognition (transcription). If present, ASR is enabled.</p></td>
</tr>
<tr class="even">
<td>Union field <code>tool_choice</code> . The tool choice configuration. <code>tool_choice</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>tool_choice_mode</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolChoiceType"><code>ToolChoiceType</code></a></p>
<p>The mode of the tool choice.</p></td>
</tr>
<tr class="even">
<td><code>tool_choice_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolChoiceConfig"><code>ToolChoiceConfig</code></a></p>
<p>The config for the tool choice.</p></td>
</tr>
</tbody>
</table>

## GetInteractionRequest

Request for InteractionService.GetInteraction.

| Fields          |                                                                                                                                              |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Required. The name of the interaction to retrieve. Format: interactions/{interaction}                                               |
| `stream`        | `bool` If true, streams the interaction events as Server-Sent Events.                                                                        |
| `last_event_id` | `string` If set, resumes the interaction stream from the chunk after the event marked by the event id. Can only be used if `stream` is true. |

## GoogleMaps

A tool that can be used by the model to call Google Maps.

| Fields          |                                                                                          |
|-----------------|------------------------------------------------------------------------------------------|
| `enable_widget` | `bool` Whether to return a widget context token in the tool call result of the response. |
| `latitude`      | `double` The latitude of the user's location.                                            |
| `longitude`     | `double` The longitude of the user's location.                                           |

## GoogleMapsCallContent

This type has no fields.

> This item is deprecated!

Google Maps content.

## GoogleMapsCallArguments

The arguments to pass to the Google Maps tool.

| Fields      |                                      |
|-------------|--------------------------------------|
| `queries[]` | `string` The queries to be executed. |

## GoogleMapsCallDelta

| Fields      |                                                                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`GoogleMapsCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallContent.GoogleMapsCallArguments) The arguments to pass to the Google Maps tool. |

## GoogleMapsCallStep

Google Maps call step.

| Fields      |                                                                                                                                                                                                                                             |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`GoogleMapsCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallStep.GoogleMapsCallStepArguments) The arguments to pass to the Google Maps tool. |

## GoogleMapsCallStepArguments

The arguments to pass to the Google Maps tool.

| Fields      |                                      |
|-------------|--------------------------------------|
| `queries[]` | `string` The queries to be executed. |

## GoogleMapsResultContent

This type has no fields.

> This item is deprecated!

Google Maps result content.

## GoogleMapsResult

The result of the Google Maps.

| Fields                 |                                                                                                                                                                                                      |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `places[]`             | [`Places`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultContent.GoogleMapsResult.Places) The places that were found. |
| `widget_context_token` | `string` Resource name of the Google Maps widget context token.                                                                                                                                      |

## Places

| Fields              |                                                                                                                                                                                                                                                         |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `place_id`          | `string` The ID of the place, in `places/{place_id}` format.                                                                                                                                                                                            |
| `name`              | `string` Title of the place.                                                                                                                                                                                                                            |
| `url`               | `string` URI reference of the place.                                                                                                                                                                                                                    |
| `review_snippets[]` | [`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ReviewSnippet) Snippets of reviews that are used to generate answers about the features of a given place in Google Maps. |

## GoogleMapsResultDelta

| Fields     |                                                                                                                                                                                                             |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`GoogleMapsResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultContent.GoogleMapsResult) The results of the Google Maps. |

## GoogleMapsResultStep

Google Maps result step.

| Fields     |                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`GoogleMapsResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultStep.GoogleMapsResultItem) |

## GoogleMapsResultItem

The result of the Google Maps.

| Fields                 |                                                                                                                                                                                                           |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `places[]`             | [`GoogleMapsResultPlaces`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultStep.GoogleMapsResultItem.GoogleMapsResultPlaces) |
| `widget_context_token` | `string`                                                                                                                                                                                                  |

## GoogleMapsResultPlaces

| Fields              |                                                                                                                                               |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `place_id`          | `string`                                                                                                                                      |
| `name`              | `string`                                                                                                                                      |
| `url`               | `string`                                                                                                                                      |
| `review_snippets[]` | [`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ReviewSnippet) |

## GoogleSearch

A tool that can be used by the model to search Google.

| Fields           |                                                                                                                                                                                               |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `search_types[]` | [`SearchType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearch.SearchType) The types of search grounding to enable. |

## SearchType

The types of search grounding to enable.

| Enums                               |                                                                        |
|-------------------------------------|------------------------------------------------------------------------|
| `SEARCH_TYPE_UNSPECIFIED`           | Unspecified search type. This value should not be used.                |
| `SEARCH_TYPE_WEB_SEARCH`            | Setting this field enables web search. Only text results are returned. |
| `SEARCH_TYPE_IMAGE_SEARCH`          | Setting this field enables image search. Image bytes are returned.     |
| `SEARCH_TYPE_ENTERPRISE_WEB_SEARCH` | Setting this field enables enterprise web search.                      |

## GoogleSearchCallContent

This type has no fields.

> This item is deprecated!

Google Search content.

## GoogleSearchCallArguments

The arguments to pass to Google Search.

| Fields      |                                                              |
|-------------|--------------------------------------------------------------|
| `queries[]` | `string` Web search queries for the following-up web search. |

## GoogleSearchCallDelta

| Fields      |                                                                                                                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`GoogleSearchCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallContent.GoogleSearchCallArguments) |

## GoogleSearchCallStep

Google Search call step.

| Fields        |                                                                                                                                                                                                                                                      |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments`   | [`GoogleSearchCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallStep.GoogleSearchCallStepArguments) Required. The arguments to pass to Google Search. |
| `search_type` | [`SearchType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearch.SearchType) The type of search grounding enabled.                                                           |

## GoogleSearchCallStepArguments

The arguments to pass to Google Search.

| Fields      |                                                              |
|-------------|--------------------------------------------------------------|
| `queries[]` | `string` Web search queries for the following-up web search. |

## GoogleSearchResultContent

This type has no fields.

> This item is deprecated!

Google Search result content.

## GoogleSearchResult

The result of the Google Search.

| Fields               |                                                                                    |
|----------------------|------------------------------------------------------------------------------------|
| `search_suggestions` | `string` Web content snippet that can be embedded in a web page or an app webview. |

## GoogleSearchResultDelta

| Fields     |                                                                                                                                                                                   |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`GoogleSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultContent.GoogleSearchResult) |
| `is_error` | `bool`                                                                                                                                                                            |

## GoogleSearchResultStep

Google Search result step.

| Fields     |                                                                                                                                                                                                                                    |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`GoogleSearchResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultStep.GoogleSearchResultItem) Required. The results of the Google Search. |
| `is_error` | `bool` Whether the Google Search resulted in an error.                                                                                                                                                                             |

## GoogleSearchResultItem

The result of the Google Search.

| Fields               |                                                                                    |
|----------------------|------------------------------------------------------------------------------------|
| `search_suggestions` | `string` Web content snippet that can be embedded in a web page or an app webview. |

## HarmCategory

Harm categories that can be detected in user input and model responses.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>HARM_CATEGORY_UNSPECIFIED</code></td>
<td>Default value. This value is unused.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_HATE_SPEECH</code></td>
<td>Content that promotes violence or incites hatred against individuals or groups based on certain attributes.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_DANGEROUS_CONTENT</code></td>
<td>Content that promotes, facilitates, or enables dangerous activities.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_HARASSMENT</code></td>
<td>Abusive, threatening, or content intended to bully, torment, or ridicule.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_SEXUALLY_EXPLICIT</code></td>
<td>Content that contains sexually explicit material.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_CIVIC_INTEGRITY</code></td>
<td><p>Deprecated: Election filter is not longer supported. The harm category is civic integrity.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_IMAGE_HATE</code></td>
<td>Images that contain hate speech.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_IMAGE_DANGEROUS_CONTENT</code></td>
<td>Images that contain dangerous content.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_IMAGE_HARASSMENT</code></td>
<td>Images that contain harassment.</td>
</tr>
<tr class="even">
<td><code>HARM_CATEGORY_IMAGE_SEXUALLY_EXPLICIT</code></td>
<td>Images that contain sexually explicit content.</td>
</tr>
<tr class="odd">
<td><code>HARM_CATEGORY_JAILBREAK</code></td>
<td>Prompts designed to bypass safety filters.</td>
</tr>
</tbody>
</table>

## ImageContent

An image content block.

| Fields                                                                                         |                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type_string`                                                                             | `string` Flexible MIME type string of the image, superseding mime_type = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mime_type" JSON key.           |
| `resolution`                                                                                   | [`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.MediaResolution) The resolution of the media. |
| Union field `data_or_uri` . The image content. `data_or_uri` can be only one of the following: |                                                                                                                                                                                |
| `data`                                                                                         | `bytes` The image content.                                                                                                                                                     |
| `uri`                                                                                          | `string` The URI of the image.                                                                                                                                                 |

## MimeType

| Enums                       |                                             |
|-----------------------------|---------------------------------------------|
| `TYPE_UNSPECIFIED`          |                                             |
| `TYPE_PNG`                  | PNG image format                            |
| `TYPE_JPEG`                 | JPEG image format                           |
| `TYPE_WEBP`                 | WebP image format                           |
| `TYPE_HEIC`                 | HEIC image format                           |
| `TYPE_HEIF`                 | HEIF image format                           |
| `TYPE_GIF`                  | GIF image format                            |
| `TYPE_BMP`                  | BMP image format                            |
| `TYPE_TIFF`                 | TIFF image format                           |
| `TYPE_VIDEO_FRAME_JPEG2000` | Video frame JPEG2000 format (internal)      |
| `TYPE_VIDEO_JPEG2000`       | Video only frame JPEG2000 format (internal) |

## ImageDelta

| Fields                                                                      |                                                                                                                                                                                |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type`                                                                 | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageContent.MimeType)                               |
| `resolution`                                                                | [`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.MediaResolution) The resolution of the media. |
| Union field `data_or_uri` . `data_or_uri` can be only one of the following: |                                                                                                                                                                                |
| `data`                                                                      | `bytes`                                                                                                                                                                        |
| `uri`                                                                       | `string`                                                                                                                                                                       |

## ImageResponseFormat

Configuration for image output format.

| Fields         |                                                                                                                                                                                                      |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type`    | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.MimeType) The MIME type of the image output.           |
| `delivery`     | [`Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.Delivery) The delivery mode for the image output.      |
| `aspect_ratio` | [`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.AspectRatio) The aspect ratio for the image output. |
| `image_size`   | [`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat.ImageSize) The size of the image output.              |

## AspectRatio

Supported aspect ratios for image output.

| Enums                             |                                      |
|-----------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`        | Default value. This value is unused. |
| `ASPECT_RATIO_ONE_BY_ONE`         | 1:1 aspect ratio.                    |
| `ASPECT_RATIO_TWO_BY_THREE`       | 2:3 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_TWO`       | 3:2 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_FOUR`      | 3:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_THREE`      | 4:3 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_FIVE`       | 4:5 aspect ratio.                    |
| `ASPECT_RATIO_FIVE_BY_FOUR`       | 5:4 aspect ratio.                    |
| `ASPECT_RATIO_NINE_BY_SIXTEEN`    | 9:16 aspect ratio.                   |
| `ASPECT_RATIO_SIXTEEN_BY_NINE`    | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_TWENTY_ONE_BY_NINE` | 21:9 aspect ratio.                   |
| `ASPECT_RATIO_ONE_BY_EIGHT`       | 1:8 aspect ratio.                    |
| `ASPECT_RATIO_EIGHT_BY_ONE`       | 8:1 aspect ratio.                    |
| `ASPECT_RATIO_ONE_BY_FOUR`        | 1:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_ONE`        | 4:1 aspect ratio.                    |

## Delivery

Delivery mode for image output.

| Enums                  |                                                |
|------------------------|------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.           |
| `INLINE`               | Image data is returned inline in the response. |
| `URI`                  | Image data is returned as a URI.               |

## ImageSize

Supported image sizes for image output.

| Enums                    |                                      |
|--------------------------|--------------------------------------|
| `IMAGE_SIZE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_SIZE_FIVE_TWELVE` | 512px image size.                    |
| `IMAGE_SIZE_ONE_K`       | 1K image size.                       |
| `IMAGE_SIZE_TWO_K`       | 2K image size.                       |
| `IMAGE_SIZE_FOUR_K`      | 4K image size.                       |

## MimeType

Supported MIME types for image output.

| Enums              |                                      |
|--------------------|--------------------------------------|
| `TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `TYPE_JPEG`        | JPEG image format.                   |

## Interaction

Response for InteractionService.CreateInteraction.

| Fields                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                                                                                                                                                                                                                                      | `string` Required. Output only. A unique identifier for the interaction completion.                                                                                                                                                                                                                                                                    |
| `status`                                                                                                                                                                                                                                  | [`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Status) Required. Output only. The status of the interaction.                                                                                                                                                      |
| `created`                                                                                                                                                                                                                                 | `string` Required. Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).                                                                                                                                                                                                                                  |
| `updated`                                                                                                                                                                                                                                 | `string` Required. Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).                                                                                                                                                                                                                             |
| `system_instruction`                                                                                                                                                                                                                      | `string` System instruction for the interaction.                                                                                                                                                                                                                                                                                                       |
| `tools[]`                                                                                                                                                                                                                                 | [`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Tool) A list of tool declarations the model may call during interaction.                                                                                                                                                         |
| `usage`                                                                                                                                                                                                                                   | [`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage) Output only. Statistics on the interaction request's token usage.                                                                                                                                            |
| `previous_interaction_id`                                                                                                                                                                                                                 | `string` The ID of the previous interaction, if any.                                                                                                                                                                                                                                                                                                   |
| `environment_id`                                                                                                                                                                                                                          | `string` Output only. The environment ID for the interaction. Only populated if environment config is set in the request.                                                                                                                                                                                                                              |
| `steps[]`                                                                                                                                                                                                                                 | [`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Step) Required. Output only. The steps that make up the interaction, when included in the response.                                                                                                                              |
| `safety_settings[]`                                                                                                                                                                                                                       | [`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.SafetySetting) Safety settings for the interaction.                                                                                                                                                                     |
| `labels`                                                                                                                                                                                                                                  | `map<string, string>` The labels with user-defined metadata for the request. Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter. |
| `errors[]`                                                                                                                                                                                                                                | [`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Error) Output only. Diagnostic faults / platform errors recorded on the interaction.                                                                                                                                            |
| Union field `input` . The input for the interaction. `input` can be only one of the following:                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                        |
| `string_content`                                                                                                                                                                                                                          | `string` A string input for the interaction, it will be processed as a single text input.                                                                                                                                                                                                                                                              |
| `step_list`                                                                                                                                                                                                                               | [`StepList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepList) Input only. The steps for the interaction.                                                                                                                                                                         |
| `content`                                                                                                                                                                                                                                 | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) The content for the interaction.                                                                                                                                                                                     |
| Union field `response_format_config` . Enforces that the generated response is a JSON object that complies with the JSON schema specified in this field. `response_format_config` can be only one of the following:                       |                                                                                                                                                                                                                                                                                                                                                        |
| `response_format_list`                                                                                                                                                                                                                    | [`ResponseFormatList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseFormatList)                                                                                                                                                                                                |
| `response_format_singleton`                                                                                                                                                                                                               | [`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseFormat)                                                                                                                                                                                                        |
| Union field `request_type` . The request type for the interaction. `request_type` can be only one of the following:                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                        |
| `model_interaction`                                                                                                                                                                                                                       | [`ModelInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ModelInteraction) Interaction for generating the completion using models.                                                                                                                                            |
| `agent_interaction`                                                                                                                                                                                                                       | [`AgentInteraction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AgentInteraction) Interaction for generating the completion using agents.                                                                                                                                            |
| Union field `environment` . The environment configuration for the interaction. Can be an object specifying remote environment sources or a string referencing an existing environment ID. `environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                        |
| `env_id`                                                                                                                                                                                                                                  | `string` The environment ID for the interaction. Can be 'remote' for default environment.                                                                                                                                                                                                                                                              |

## Status

The status of the interaction.

| Enums             |                                                                                          |
|-------------------|------------------------------------------------------------------------------------------|
| `UNSPECIFIED`     | Default value. This value is unused.                                                     |
| `IN_PROGRESS`     | The interaction is in progress.                                                          |
| `REQUIRES_ACTION` | The interaction requires action/input from the user.                                     |
| `COMPLETED`       | The interaction is completed.                                                            |
| `FAILED`          | The interaction failed.                                                                  |
| `CANCELLED`       | The interaction was cancelled.                                                           |
| `INCOMPLETE`      | The interaction is completed, but contains incomplete results (e.g. hitting max_tokens). |
| `QUEUED`          | The interaction is queued, waiting for processing (e.g. waiting for off-peak capacity).  |

## Usage

Statistics on the interaction request's token usage.

| Fields                          |                                                                                                                                                                                                                    |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `total_input_tokens`            | `int32` Number of tokens in the prompt (context).                                                                                                                                                                  |
| `input_tokens_by_modality[]`    | [`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.ModalityTokens) A breakdown of input token usage by modality.    |
| `total_cached_tokens`           | `int32` Number of tokens in the cached part of the prompt (the cached content).                                                                                                                                    |
| `cached_tokens_by_modality[]`   | [`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.ModalityTokens) A breakdown of cached token usage by modality.   |
| `total_output_tokens`           | `int32` Total number of tokens across all the generated responses.                                                                                                                                                 |
| `output_tokens_by_modality[]`   | [`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.ModalityTokens) A breakdown of output token usage by modality.   |
| `total_tool_use_tokens`         | `int32` Number of tokens present in tool-use prompt(s).                                                                                                                                                            |
| `tool_use_tokens_by_modality[]` | [`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.ModalityTokens) A breakdown of tool-use token usage by modality. |
| `total_thought_tokens`          | `int32` Number of tokens of thoughts for thinking models.                                                                                                                                                          |
| `total_tokens`                  | `int32` Total token count for the interaction request (prompt + responses + other internal tokens).                                                                                                                |
| `grounding_tool_count[]`        | [`GroundingToolCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.GroundingToolCount) Grounding tool count.                    |

## GroundingToolCount

The number of grounding tool counts.

| Fields  |                                                                                                                                                                                                                     |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`  | [`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage.GroundingToolCount.Type) The grounding tool type associated with the count. |
| `count` | `int32` The number of grounding tool counts.                                                                                                                                                                        |

## Type

The type of grounding tool.

| Enums              |                                                                                    |
|--------------------|------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Default value. This value is unused.                                               |
| `GOOGLE_SEARCH`    | Grounding with Google Web Search and Image Search, & Web Grounding for Enterprise. |
| `GOOGLE_MAPS`      | Grounding with Google Maps.                                                        |
| `RETRIEVAL`        | Grounding with customer's data, for example, VertexAISearch.                       |

## ModalityTokens

The token count for a single response modality.

| Fields     |                                                                                                                                                                                                   |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modality` | [`ResponseModality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseModality) The modality associated with the token count. |
| `tokens`   | `int32` Number of tokens for the modality.                                                                                                                                                        |

## InteractionCompletedSseEvent

Signals that the Interaction completed. Sent when the Interaction receives Complete/Cancel or naturally terminates. No more input can be sent to the Interaction after this.

| Fields        |                                                                                                                                                                                                                              |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `interaction` | [`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction) Required. Partial completed interaction resource emitted at the end of the stream. |

## InteractionCreatedSseEvent

Server response confirming that a new interaction was created.

| Fields        |                                                                                                                                                                                                                      |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `interaction` | [`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction) Required. Partial interaction resource emitted when the stream is created. |

## InteractionMetadata

Metadata for an interaction, used for listing interactions.

| Fields    |                                                                                                                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`      | `string` Output only. A unique identifier for the interaction completion.                                                                                                               |
| `status`  | [`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Status) Output only. The status of the interaction. |
| `created` | `string` Output only. The time at which the response was created in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).                                                                             |
| `updated` | `string` Output only. The time at which the response was last updated in ISO 8601 format (YYYY-MM-DDThh:mm:ssZ).                                                                        |

## InteractionStatusUpdate

| Fields           |                                                                                                                                             |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| `interaction_id` | `string`                                                                                                                                    |
| `status`         | [`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Status) |

## InteractionStreamingEvent

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>event_id</code></td>
<td><p><code>string</code></p>
<p>The event_id token to be used to resume the interaction stream, from this event.</p></td>
</tr>
<tr class="even">
<td>Union field <code>event_type</code> . The event data. <code>event_type</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>interaction_created_event</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionCreatedSseEvent"><code>InteractionCreatedSseEvent</code></a></p>
<p>The interaction data, used for interaction.created events. Used when steps are enabled.</p></td>
</tr>
<tr class="even">
<td><code>interaction_completed_event</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionCompletedSseEvent"><code>InteractionCompletedSseEvent</code></a></p>
<p>The interaction data, used for interaction.completed events. Used when steps are enabled.</p></td>
</tr>
<tr class="odd">
<td><code>interaction_status_update</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionStatusUpdate"><code>InteractionStatusUpdate</code></a></p>
<p>The interaction status data, used for interaction.status_update events.</p></td>
</tr>
<tr class="even">
<td><code>content_start </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentStart"><code>ContentStart</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The content block start data, used for content.start events. Legacy content-based streaming event, used when steps are disabled.</p></td>
</tr>
<tr class="odd">
<td><code>content_delta </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentDelta"><code>ContentDelta</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The content block delta data, used for content.delta events. Legacy content-based streaming event, used when steps are disabled.</p></td>
</tr>
<tr class="even">
<td><code>content_stop </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentStop"><code>ContentStop</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The content block stop data, used for content.stop events. Legacy content-based streaming event, used when steps are disabled.</p></td>
</tr>
<tr class="odd">
<td><code>error_event</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ErrorEvent"><code>ErrorEvent</code></a></p>
<p>The error event data, used for error events.</p></td>
</tr>
<tr class="even">
<td><code>step_start</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepStart"><code>StepStart</code></a></p>
<p>The step start data, used for step.start events. Step-based streaming event, used when steps are enabled.</p></td>
</tr>
<tr class="odd">
<td><code>step_delta</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepDelta"><code>StepDelta</code></a></p>
<p>The step delta data, used for step.delta events. Step-based streaming event, used when steps are enabled.</p></td>
</tr>
<tr class="even">
<td><code>step_stop</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepStop"><code>StepStop</code></a></p>
<p>The step stop data, used for step.stop events. Step-based streaming event, used when steps are enabled.</p></td>
</tr>
</tbody>
</table>

## ListInteractionsRequest

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`     | `string` Required. The parent, which owns this collection of interactions. Format: `projects/{project}/locations/{location}` Supported only by the Agent Platform Platform.                                                                                                                                                                                                           |
| `page_size`  | `int32` The maximum number of `Interactions` to return (per page). The service may return fewer `Interactions` . If unspecified, at most 10 `Interactions` will be returned. The maximum size limit is 20 `Interactions` per page. Note: Vertex API does supports page size up to 500.                                                                                                |
| `page_token` | `string` A page token, received from a previous `ListInteractions` call. Provide the `next_page_token` returned in the response as an argument to the next request to retrieve the next page. When paginating, all other parameters provided to `ListInteractions` must match the call that provided the page token. Note: Vertex API does not enforce this requirement on page_size. |

## ListInteractionsResponse

| Fields                    |                                                                                                                                                                                                                    |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `interaction_metadatas[]` | [`InteractionMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.InteractionMetadata) The `InteractionMetadata` from the specified collection. |
| `next_page_token`         | `string` A token, which can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.                                                                            |

## ListValue

`ListValue` is a wrapper around a repeated field of values.

| Fields     |                                                                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | [`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Value) Repeated field of dynamically typed values. |

## McpServer

A MCPServer is a server that can be called by the model to perform actions.

| Fields                                                                  |                                                                                                                                                                |
|-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                  | `string` The name of the MCPServer.                                                                                                                            |
| `headers`                                                               | `map<string, string>` Optional: Fields for authentication headers, timeouts, etc., if needed.                                                                  |
| `allowed_tools[]`                                                       | [`AllowedTools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AllowedTools) The allowed tools. |
| Union field `transport` . `transport` can be only one of the following: |                                                                                                                                                                |
| `url`                                                                   | `string` The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"                                                                       |

## MediaResolution

Resolution for input media (images/video).

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `MEDIA_RESOLUTION_UNSPECIFIED` | Default value. This value is unused. |
| `LOW`                          | Low resolution.                      |
| `MEDIUM`                       | Medium resolution.                   |
| `HIGH`                         | High resolution.                     |
| `ULTRA_HIGH`                   | Ultra high resolution.               |

## ModelInteraction

Interaction for generating the completion using models.

| Fields              |                                                                                                                                                                                                                     |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `model`             | `string` The name of the `Model` used for generating the completion.                                                                                                                                                |
| `generation_config` | [`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GenerationConfig) Input only. Configuration parameters for the model interaction. |

## ModelOutputStep

Output generated by the model.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>content[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content"><code>Content</code></a></p></td>
</tr>
<tr class="even">
<td><code>error </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.rpc#google.rpc.Status"><code>Status</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The error result of the operation in case of failure or cancellation.</p></td>
</tr>
</tbody>
</table>

## ParallelAISearchConfig

Used to specify configuration for ParallelAISearch.

| Fields          |                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------|
| `api_key`       | `string` Optional. The API key for ParallelAiSearch.                                                                       |
| `custom_config` | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) Optional. Custom configs for ParallelAiSearch. |

## PlaceCitation

A place citation annotation.

| Fields              |                                                                                                                                                                                                                                                         |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `place_id`          | `string` The ID of the place, in `places/{place_id}` format.                                                                                                                                                                                            |
| `name`              | `string` Title of the place.                                                                                                                                                                                                                            |
| `url`               | `string` URI reference of the place.                                                                                                                                                                                                                    |
| `review_snippets[]` | [`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ReviewSnippet) Snippets of reviews that are used to generate answers about the features of a given place in Google Maps. |

## RagStoreConfig

Use to specify configuration for RAG Store.

| Fields                 |                                                                                                                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rag_resources[]`      | [`RagResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagResource) Optional. The representation of the rag source.                 |
| `rag_retrieval_config` | [`RagRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig) Optional. The retrieval config for the Rag query. |

## RagResource

The definition of the Rag resource.

| Fields           |                                                                                                     |
|------------------|-----------------------------------------------------------------------------------------------------|
| `rag_corpus`     | `string` Optional. RagCorpora resource name.                                                        |
| `rag_file_ids[]` | `string` Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field. |

## RagRetrievalConfig

Specifies the context retrieval config.

| Fields          |                                                                                                                                                                                                                   |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `top_k`         | `int32` Optional. The number of contexts to retrieve.                                                                                                                                                             |
| `hybrid_search` | [`HybridSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.HybridSearch) Optional. Config for Hybrid Search. |
| `filter`        | [`Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.Filter) Optional. Config for filters.                   |
| `ranking`       | [`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.Ranking) Optional. Config for ranking and reranking.   |

## Filter

Config for filters.

| Fields                                                                                                                                                                                         |                                                                                            |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| `metadata_filter`                                                                                                                                                                              | `string` Optional. String for metadata filtering.                                          |
| Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following: |                                                                                            |
| `vector_distance_threshold`                                                                                                                                                                    | `double` Optional. Only returns contexts with vector distance smaller than the threshold.  |
| `vector_similarity_threshold`                                                                                                                                                                  | `double` Optional. Only returns contexts with vector similarity larger than the threshold. |

## HybridSearch

Config for Hybrid Search.

| Fields  |                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------|
| `alpha` | `float` Optional. Alpha value controls the weight between dense and sparse vector search results. |

## Ranking

Config for ranking and reranking.

| Fields                                                                                                        |                                                                                                                                                                                                              |
|---------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `ranking_config` . Config options for ranking. `ranking_config` can be only one of the following: |                                                                                                                                                                                                              |
| `rank_service`                                                                                                | [`RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig.RagRetrievalConfig.Ranking.RankService) Config for Rank Service. |

## RankService

Config for Rank Service.

| Fields       |                                                        |
|--------------|--------------------------------------------------------|
| `model_name` | `string` Optional. The model name of the rank service. |

## ResponseFormat

| Fields                                                        |                                                                                                                                                                                       |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                                       |
| `audio`                                                       | [`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioResponseFormat)                             |
| `text`                                                        | [`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextResponseFormat)                               |
| `image`                                                       | [`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageResponseFormat)                             |
| `video`                                                       | [`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat)                             |
| `struct_value`                                                | [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) Multi-discriminator values is already enabled in GAOS |

## ResponseFormatList

| Fields               |                                                                                                                                                 |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `response_formats[]` | [`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ResponseFormat) |

## ResponseModality

The modality of the response.

| Enums                           |                                              |
|---------------------------------|----------------------------------------------|
| `RESPONSE_MODALITY_UNSPECIFIED` | Default value. This value is unused.         |
| `TEXT`                          | Indicates the model should return text.      |
| `IMAGE`                         | Indicates the model should return images.    |
| `AUDIO`                         | Indicates the model should return audio.     |
| `VIDEO`                         | Indicates the model should return video.     |
| `DOCUMENT`                      | Indicates the model should return documents. |

## Retrieval

A tool that can be used by the model to retrieve files.

| Fields                      |                                                                                                                                                                                                                     |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `retrieval_types[]`         | [`RetrievalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Retrieval.RetrievalType) The types of file retrieval to enable.                      |
| `vertex_ai_search_config`   | [`VertexAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VertexAISearchConfig) Used to specify configuration for VertexAISearch.       |
| `exa_ai_search_config`      | [`ExaAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ExaAISearchConfig) Used to specify configuration for ExaAISearch.                |
| `parallel_ai_search_config` | [`ParallelAISearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ParallelAISearchConfig) Used to specify configuration for ParallelAISearch. |
| `rag_store_config`          | [`RagStoreConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RagStoreConfig) Used to specify configuration for RagStore.                         |

## RetrievalType

The types of file retrieval to enable.

| Enums                               |     |
|-------------------------------------|-----|
| `RETRIEVAL_TYPE_UNSPECIFIED`        |     |
| `RETRIEVAL_TYPE_VERTEX_AI_SEARCH`   |     |
| `RETRIEVAL_TYPE_RAG_STORE`          |     |
| `RETRIEVAL_TYPE_EXA_AI_SEARCH`      |     |
| `RETRIEVAL_TYPE_PARALLEL_AI_SEARCH` |     |

## RetrievalCallDelta

Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. RetrievalType decides which tool is used.

| Fields           |                                                                                                                                                                                                                                          |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments`      | [`RetrievalStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallStep.RetrievalStepArguments) Required. The arguments to pass to the Retrieval tool. |
| `retrieval_type` | [`RetrievalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Retrieval.RetrievalType) The type of retrieval tools.                                                     |

## RetrievalCallStep

Retrieval call step. Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. RetrievalType decides which tool is used.

| Fields           |                                                                                                                                                                                                                                          |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments`      | [`RetrievalStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallStep.RetrievalStepArguments) Required. The arguments to pass to the retrieval tool. |
| `retrieval_type` | [`RetrievalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Retrieval.RetrievalType) The type of retrieval tools.                                                     |

## RetrievalStepArguments

The arguments to pass to Retrieval tools.

| Fields      |                                             |
|-------------|---------------------------------------------|
| `queries[]` | `string` Queries for Retrieval information. |

## RetrievalResultDelta

Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. ToolResultDelta.type

| Fields     |                                                    |
|------------|----------------------------------------------------|
| `is_error` | `bool` Whether the retrieval resulted in an error. |

## RetrievalResultStep

Vertex Retrieval result step. Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc.

| Fields     |                                                    |
|------------|----------------------------------------------------|
| `is_error` | `bool` Whether the retrieval resulted in an error. |

## ReviewSnippet

Encapsulates a snippet of a user review that answers a question about the features of a specific place in Google Maps.

| Fields      |                                                                     |
|-------------|---------------------------------------------------------------------|
| `title`     | `string` Title of the review.                                       |
| `url`       | `string` A link that corresponds to the user review on Google Maps. |
| `review_id` | `string` The ID of the review snippet.                              |

## SafetySetting

A safety setting that affects the safety-blocking behavior.

A `SafetySetting` consists of a harm `category` and a `threshold` for that category.

| Fields      |                                                                                                                                                                                                                                                                                                  |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | [`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.HarmCategory) Required. The type of harm category to be blocked.                                                                                                   |
| `threshold` | [`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.SafetySetting.HarmBlockThreshold) Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked. |
| `method`    | [`HarmBlockMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.SafetySetting.HarmBlockMethod) Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.               |

## HarmBlockMethod

The method for blocking content.

| Enums                           |                                                                  |
|---------------------------------|------------------------------------------------------------------|
| `HARM_BLOCK_METHOD_UNSPECIFIED` | The harm block method is unspecified.                            |
| `SEVERITY`                      | The harm block method uses both probability and severity scores. |
| `PROBABILITY`                   | The harm block method uses the probability score.                |

## HarmBlockThreshold

Thresholds for blocking content based on harm probability.

| Enums                              |                                                               |
|------------------------------------|---------------------------------------------------------------|
| `HARM_BLOCK_THRESHOLD_UNSPECIFIED` | The harm block threshold is unspecified.                      |
| `BLOCK_LOW_AND_ABOVE`              | Block content with a low harm probability or higher.          |
| `BLOCK_MEDIUM_AND_ABOVE`           | Block content with a medium harm probability or higher.       |
| `BLOCK_ONLY_HIGH`                  | Block content with a high harm probability.                   |
| `BLOCK_NONE`                       | Do not block any content, regardless of its harm probability. |
| `OFF`                              | Turn off the safety filter entirely.                          |

## ServerToolCallDelta

| Fields                                                        |                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `signature`                                                   | `bytes` A signature hash for backend validation.                                                                                                                |
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                 |
| `code_execution_call`                                         | [`CodeExecutionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallDelta) |
| `url_context_call`                                            | [`UrlContextCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallDelta)       |
| `google_search_call`                                          | [`GoogleSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallDelta)   |
| `file_search_call`                                            | [`FileSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchCallDelta)       |
| `google_maps_call`                                            | [`GoogleMapsCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallDelta)       |
| `retrieval_call`                                              | [`RetrievalCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallDelta)         |

## ServerToolResultDelta

| Fields                                                        |                                                                                                                                                                     |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `signature`                                                   | `bytes` A signature hash for backend validation.                                                                                                                    |
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                     |
| `code_execution_result`                                       | [`CodeExecutionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionResultDelta) |
| `url_context_result`                                          | [`UrlContextResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultDelta)       |
| `google_search_result`                                        | [`GoogleSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultDelta)   |
| `file_search_result`                                          | [`FileSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultDelta)       |
| `google_maps_result`                                          | [`GoogleMapsResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultDelta)       |
| `retrieval_result`                                            | [`RetrievalResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalResultDelta)         |

## Step

A step in the interaction.

| Fields                                                        |                                                                                                                                                                                        |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                                        |
| `thought`                                                     | [`ThoughtStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtStep)                                              |
| `tool_call`                                                   | [`ToolCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolCallStep)                                            |
| `tool_result`                                                 | [`ToolResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ToolResultStep)                                        |
| `user_input`                                                  | [`UserInputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UserInputStep) DO NOT USE -- These are for 3P JSON only |
| `model_output`                                                | [`ModelOutputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ModelOutputStep)                                      |

## StepDelta

| Fields  |                                                                                                                                               |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `index` | `int32`                                                                                                                                       |
| `delta` | [`StepDeltaData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.StepDeltaData) |

## StepDeltaData

| Fields                                                        |                                                                                                                                                               |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                               |
| `text`                                                        | [`TextDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextDelta)                         |
| `image`                                                       | [`ImageDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ImageDelta)                       |
| `audio`                                                       | [`AudioDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AudioDelta)                       |
| `document`                                                    | [`DocumentDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.DocumentDelta)                 |
| `video`                                                       | [`VideoDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoDelta)                       |
| `thought_summary`                                             | [`ThoughtSummaryDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtSummaryDelta)     |
| `thought_signature`                                           | [`ThoughtSignatureDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ThoughtSignatureDelta) |
| `text_annotation_delta`                                       | [`TextAnnotationDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextAnnotationDelta)     |
| `arguments_delta`                                             | [`ArgumentsDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ArgumentsDelta)               |
| `server_tool_call`                                            | [`ServerToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ServerToolCallDelta)     |
| `server_tool_result`                                          | [`ServerToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ServerToolResultDelta) |
| `function_result`                                             | [`FunctionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionResultDelta)     |

## StepList

A list of Steps.

| Fields    |                                                                                                                                                    |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `steps[]` | [`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Step) The steps of the list. |

## StepStart

| Fields  |                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| `index` | `int32`                                                                                                                     |
| `step`  | [`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Step) |

## StepStop

| Fields       |                                                                                                                                                                                                       |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `index`      | `int32`                                                                                                                                                                                               |
| `usage`      | [`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage) Cumulative model usage stats from the start of the session. |
| `step_usage` | [`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Interaction.Usage) Model usage stats for this specific step.                   |

## Struct

`Struct` represents a structured data value, consisting of fields which map to dynamically typed values.

| Fields     |                                                                                                                                                                                                                                                             |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | [`Field`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Field) Dynamically typed fields. List instead of map because LLMs are sensitive to ordering, and we want to give users full control. |

## TextAnnotationDelta

| Fields          |                                                                                                                                                                                                       |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `annotations[]` | [`Annotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextContent.Annotation) Citation information for model-generated content. |

## TextContent

A text content block.

| Fields          |                                                                                                                                                                                                       |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`          | `string` Required. The text content.                                                                                                                                                                  |
| `annotations[]` | [`Annotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextContent.Annotation) Citation information for model-generated content. |

## Annotation

Citation information for model-generated content.

| Fields                                                                                |                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_index`                                                                         | `int32` Start of segment of the response that is attributed to this source. Index indicates the start of the segment, measured in bytes.                                                                                                        |
| `end_index`                                                                           | `int32` End of the attributed segment, exclusive.                                                                                                                                                                                               |
| Union field `type` . The type of annotation. `type` can be only one of the following: |                                                                                                                                                                                                                                                 |
| `url_citation`                                                                        | [`UrlCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlCitation) NOTE: We use these instead of the Citation message for historical reasons. A URL citation annotation. |
| `file_citation`                                                                       | [`FileCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileCitation) A file citation annotation.                                                                         |
| `place_citation`                                                                      | [`PlaceCitation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.PlaceCitation) A place citation annotation.                                                                      |
| `word_info`                                                                           | [`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.WordInfo) Word-level ASR annotation with timing and speaker info.                                                     |

## TextDelta

| Fields |          |
|--------|----------|
| `text` | `string` |

## TextResponseFormat

Configuration for text output format.

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type` | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.TextResponseFormat.MimeType) The MIME type of the text output.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `schema`    | [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) The JSON schema that the output should conform to. Only applicable when mime_type is application/json. Supports a subset of JSON Schema. `minLength` , `maxLength` , `minProperties` , `maxProperties` , `uniqueItems` , `contains` , `minContains` , and `maxContains` are ignored and not enforced; validate these in your application. `minItems` and `maxItems` are enforced. Schemas that are too complex to enforce (for example, large `maxItems` on nested arrays) return a 400 INVALID_ARGUMENT error. |

## MimeType

Supported MIME types for text output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `TYPE_UNSPECIFIED`      | Default value. This value is unused. |
| `TYPE_APPLICATION_JSON` | JSON output format.                  |
| `TYPE_TEXT_PLAIN`       | Plain text output format.            |

## ThinkingLevel

The level of thought tokens that the model should generate.

| Enums                        |                                      |
|------------------------------|--------------------------------------|
| `THINKING_LEVEL_UNSPECIFIED` | Default value. This value is unused. |
| `THINKING_LEVEL_MINIMAL`     | Little to no thinking.               |
| `THINKING_LEVEL_LOW`         | Low thinking level.                  |
| `THINKING_LEVEL_MEDIUM`      | Medium thinking level.               |
| `THINKING_LEVEL_HIGH`        | High thinking level.                 |

## ThinkingSummaries

Whether to include thought summaries in the response.

| Enums                            |                                      |
|----------------------------------|--------------------------------------|
| `THINKING_SUMMARIES_UNSPECIFIED` | Default value. This value is unused. |
| `THINKING_SUMMARIES_AUTO`        | Auto thinking summaries.             |
| `THINKING_SUMMARIES_NONE`        | No thinking summaries.               |

## ThoughtSignatureDelta

| Fields      |                                                                             |
|-------------|-----------------------------------------------------------------------------|
| `signature` | `bytes` Signature to match the backend source to be part of the generation. |

## ThoughtStep

A thought step.

| Fields      |                                                                                                                                                             |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `signature` | `bytes` A signature hash for backend validation.                                                                                                            |
| `summary[]` | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) A summary of the thought. |

## ThoughtSummaryDelta

| Fields    |                                                                                                                                                                                  |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `content` | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) A new summary item to be added to the thought. |

## Tool

A tool that can be used by the model.

| Fields                                                                         |                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . The tool to use. `type` can be only one of the following: |                                                                                                                                                                                                                   |
| `function`                                                                     | [`Function`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Function) A function that can be used by the model.                                     |
| `code_execution`                                                               | [`CodeExecution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecution) A tool that can be used by the model to execute code.               |
| `url_context`                                                                  | [`UrlContext`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContext) A tool that can be used by the model to fetch URL context.                |
| `computer_use`                                                                 | [`ComputerUse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ComputerUse) Tool to support the model interacting directly with the computer.       |
| `mcp_server`                                                                   | [`McpServer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.McpServer) A MCPServer is a server that can be called by the model to perform actions. |
| `google_search`                                                                | [`GoogleSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearch) A tool that can be used by the model to search Google.                |
| `file_search`                                                                  | [`FileSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearch) A tool that can be used by the model to search files.                     |
| `google_maps`                                                                  | [`GoogleMaps`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMaps) A tool that can be used by the model to search Google Maps.               |
| `retrieval`                                                                    | [`Retrieval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Retrieval) A tool that can be used by the model to retrieve files.                     |

## ToolCallDelta

| Fields                                                        |                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                                                          | `string` Required. A unique ID for this specific tool call.                                                                                                     |
| `signature`                                                   | `bytes` A signature hash for backend validation.                                                                                                                |
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                 |
| `function_call`                                               | [`FunctionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionCallDelta)           |
| `code_execution_call`                                         | [`CodeExecutionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallDelta) |
| `url_context_call`                                            | [`UrlContextCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallDelta)       |
| `google_search_call`                                          | [`GoogleSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallDelta)   |
| `file_search_call`                                            | [`FileSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchCallDelta)       |
| `google_maps_call`                                            | [`GoogleMapsCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallDelta)       |

## ToolCallStep

Tool call step.

| Fields                                                        |                                                                                                                                                               |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                                                          | `string` Required. A unique ID for this specific tool call.                                                                                                   |
| `signature`                                                   | `bytes` A signature hash for backend validation.                                                                                                              |
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                               |
| `function_call`                                               | [`FunctionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionCallStep)           |
| `code_execution_call`                                         | [`CodeExecutionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionCallStep) |
| `url_context_call`                                            | [`UrlContextCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallStep)       |
| `google_search_call`                                          | [`GoogleSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchCallStep)   |
| `file_search_call`                                            | [`FileSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchCallStep)       |
| `google_maps_call`                                            | [`GoogleMapsCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsCallStep)       |
| `retrieval_call`                                              | [`RetrievalCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalCallStep)         |

## ToolChoiceConfig

The tool choice configuration containing allowed tools.

| Fields          |                                                                                                                                                                |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `allowed_tools` | [`AllowedTools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.AllowedTools) The allowed tools. |

## ToolChoiceType

The type of tool choice.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `TOOL_CHOICE_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `AUTO`                         | Auto tool choice.                    |
| `ANY`                          | Any tool choice.                     |
| `NONE`                         | No tool choice.                      |
| `VALIDATED`                    | Validated tool choice.               |

## ToolResultDelta

| Fields                                                        |                                                                                                                                                                     |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `call_id`                                                     | `string` Required. ID to match the ID from the function call block.                                                                                                 |
| `signature`                                                   | `bytes` A signature hash for backend validation.                                                                                                                    |
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                     |
| `function_result`                                             | [`FunctionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionResultDelta)           |
| `code_execution_result`                                       | [`CodeExecutionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionResultDelta) |
| `url_context_result`                                          | [`UrlContextResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultDelta)       |
| `google_search_result`                                        | [`GoogleSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultDelta)   |
| `file_search_result`                                          | [`FileSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultDelta)       |
| `google_maps_result`                                          | [`GoogleMapsResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultDelta)       |

## ToolResultStep

Tool result step.

| Fields                                                        |                                                                                                                                                                   |
|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `call_id`                                                     | `string` Required. ID to match the ID from the function call block.                                                                                               |
| `signature`                                                   | `bytes` A signature hash for backend validation.                                                                                                                  |
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                   |
| `function_result`                                             | [`FunctionResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FunctionResultStep)           |
| `code_execution_result`                                       | [`CodeExecutionResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.CodeExecutionResultStep) |
| `url_context_result`                                          | [`UrlContextResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultStep)       |
| `google_search_result`                                        | [`GoogleSearchResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleSearchResultStep)   |
| `file_search_result`                                          | [`FileSearchResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.FileSearchResultStep)       |
| `google_maps_result`                                          | [`GoogleMapsResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.GoogleMapsResultStep)       |
| `retrieval_result`                                            | [`RetrievalResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.RetrievalResultStep)         |

## TranscriptionConfig

Configuration for speech recognition (transcription).

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>language_codes[]</code></td>
<td><p><code>string</code></p>
<p>Optional. BCP-47 language codes providing hints about the languages present in the audio. If omitted or empty, defaults to automatic language detection.</p></td>
</tr>
<tr class="even">
<td><code>custom_vocabulary[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.</p></td>
</tr>
<tr class="odd">
<td><code>timestamp_granularities[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. The granularity of timestamps to include in the transcription output. Supported values: "word". If empty, no timestamps are generated.</p></td>
</tr>
<tr class="even">
<td><code>diarization_mode </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Configures speaker diarization. Supported values: "speaker".</p></td>
</tr>
<tr class="odd">
<td><code>adaptation_phrases[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. A list of phrases to bias the ASR model towards.</p></td>
</tr>
</tbody>
</table>

## UrlCitation

A URL citation annotation.

| Fields  |                                |
|---------|--------------------------------|
| `url`   | `string` The URL.              |
| `title` | `string` The title of the URL. |

## UrlContext

This type has no fields.

A tool that can be used by the model to fetch URL context.

## UrlContextCallContent

This type has no fields.

> This item is deprecated!

URL context content.

## UrlContextCallArguments

The arguments to pass to the URL context.

| Fields   |                             |
|----------|-----------------------------|
| `urls[]` | `string` The URLs to fetch. |

## UrlContextCallDelta

| Fields      |                                                                                                                                                                                         |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`UrlContextCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallContent.UrlContextCallArguments) |

## UrlContextCallStep

URL context call step.

| Fields      |                                                                                                                                                                                                                                                  |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arguments` | [`UrlContextCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextCallStep.UrlContextCallStepArguments) Required. The arguments to pass to the URL context. |

## UrlContextCallStepArguments

The arguments to pass to the URL context.

| Fields   |                             |
|----------|-----------------------------|
| `urls[]` | `string` The URLs to fetch. |

## UrlContextResultContent

This type has no fields.

> This item is deprecated!

URL context result content.

## UrlContextResult

The result of the URL context.

| Fields   |                                                                                                                                                                                                           |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `url`    | `string` The URL that was fetched.                                                                                                                                                                        |
| `status` | [`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultContent.UrlContextResult.Status) The status of the URL retrieval. |

## Status

The status of the URL retrieval.

| Enums                |                                                                |
|----------------------|----------------------------------------------------------------|
| `STATUS_UNSPECIFIED` | Unspecified status. This value should not be used.             |
| `SUCCESS`            | Url retrieval is successful.                                   |
| `ERROR`              | Url retrieval is failed due to error.                          |
| `PAYWALL`            | Url retrieval is failed because the content is behind paywall. |
| `UNSAFE`             | Url retrieval is failed because the content is unsafe.         |

## UrlContextResultDelta

| Fields     |                                                                                                                                                                             |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`UrlContextResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultContent.UrlContextResult) |
| `is_error` | `bool`                                                                                                                                                                      |

## UrlContextResultStep

URL context result step.

| Fields     |                                                                                                                                                                                                                            |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `result[]` | [`UrlContextResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultStep.UrlContextResultItem) Required. The results of the URL context. |
| `is_error` | `bool` Whether the URL context resulted in an error.                                                                                                                                                                       |

## UrlContextResultItem

The result of the URL context.

| Fields   |                                                                                                                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `url`    | `string` The URL that was fetched.                                                                                                                                                                         |
| `status` | [`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.UrlContextResultStep.UrlContextResultItem.Status) The status of the URL retrieval. |

## Status

The status of the URL retrieval.

| Enums                |     |
|----------------------|-----|
| `STATUS_UNSPECIFIED` |     |
| `SUCCESS`            |     |
| `ERROR`              |     |
| `PAYWALL`            |     |
| `UNSAFE`             |     |

## UserInputStep

Input provided by the user.

| Fields                                                              |                                                                                                                                                                                                 |
|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `content` . `content` can be only one of the following: |                                                                                                                                                                                                 |
| `content_list`                                                      | [`ContentList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ContentList) The content of the step. An array of Content objects. |
| `content_string`                                                    | `string` The content of the step. A single string.                                                                                                                                              |

## Value

`Value` represents a dynamically typed value which can be either null, a number, a string, a boolean, a recursive struct value, or a list of values. A producer of value is expected to set one of these variants. Absence of any variant indicates an error.

| Fields                                                                           |                                                                                                                                                                                |
|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                |
| `null_value`                                                                     | [`NullValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#null-value) Represents a null value.                                                                    |
| `number_value`                                                                   | `double` Represents a double value.                                                                                                                                            |
| `string_value`                                                                   | `string` Represents a string value.                                                                                                                                            |
| `bool_value`                                                                     | `bool` Represents a boolean value.                                                                                                                                             |
| `struct_value`                                                                   | [`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Struct) Represents a structured value.                 |
| `list_value`                                                                     | [`ListValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.ListValue) Represents a repeated `Value` .          |
| `content_value`                                                                  | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.Content) Represents rich content (text, image, etc.). |

## VertexAISearchConfig

Used to specify configuration for VertexAISearch.

| Fields         |                                                                      |
|----------------|----------------------------------------------------------------------|
| `engine`       | `string` Optional. Used to specify Agent Platform Search engine.     |
| `datastores[]` | `string` Optional. Used to specify Agent Platform Search datastores. |

## VideoConfig

Configuration options for video generation.

| Fields |                                                                                                                                                                                                                                                                                                               |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `task` | [`Task`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoConfig.Task) Optional task mode for video generation. If not specified, the model automatically determines the appropriate mode based on the provided text prompt and input media. |

## Task

Supported video generation tasks.

| Enums                |                                                                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `TASK_UNSPECIFIED`   | Unspecified task. The task is inferred from the input prompt and media.                                                                            |
| `TEXT_TO_VIDEO`      | Generates video solely from a text prompt.                                                                                                         |
| `IMAGE_TO_VIDEO`     | Generates video from one or two source images. The first image defines the starting frame, and the optional second image defines the ending frame. |
| `REFERENCE_TO_VIDEO` | Generates video using reference media (such as images, audio, or video).                                                                           |
| `EDIT`               | Modifies an existing input video.                                                                                                                  |
| `EXTEND`             | Extends an existing input video.                                                                                                                   |

## VideoContent

A video content block.

| Fields                                                                                                                          |                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type_string`                                                                                                              | `string` Flexible MIME type string of the video, superseding mime_type = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mime_type" JSON key.           |
| `resolution`                                                                                                                    | [`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.MediaResolution) The resolution of the media. |
| `name`                                                                                                                          | `string` A user-defined name for this content block. Can be referenced by the model in the final response.                                                                     |
| Union field `data_or_uri` . The video content. `data_or_uri` can be only one of the following:                                  |                                                                                                                                                                                |
| `data`                                                                                                                          | `bytes` The video content.                                                                                                                                                     |
| `uri`                                                                                                                           | `string` The URI of the video.                                                                                                                                                 |
| Union field `processing` . How the model processes this video for understanding. `processing` can be only one of the following: |                                                                                                                                                                                |
| `processing_type`                                                                                                               | [`Processing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.Processing)                           |
| `processing_config`                                                                                                             | [`MediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.MediaProcessing)                 |

## MediaProcessing

| Fields                                                        |                                                                                                                                                                            |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `type` . `type` can be only one of the following: |                                                                                                                                                                            |
| `static`                                                      | [`StaticMediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.StaticMediaProcessing) |

## MimeType

| Enums              |                                 |
|--------------------|---------------------------------|
| `TYPE_UNSPECIFIED` |                                 |
| `TYPE_MP4`         | MP4 video format                |
| `TYPE_MPEG`        | MPEG video format               |
| `TYPE_MPG`         | MPG video format                |
| `TYPE_MOV`         | MOV video format                |
| `TYPE_AVI`         | AVI video format                |
| `TYPE_X_FLV`       | FLV video format                |
| `TYPE_WEBM`        | WebM video format               |
| `TYPE_WMV`         | WMV video format                |
| `TYPE_3GPP`        | 3GPP video format               |
| `TYPE_YT_BEYOND`   | YouTube video format (internal) |
| `TYPE_JPEG2000`    | JPEG 2000 video format          |

## Processing

How the model processes input media for understanding.

| Enums                    |                                                                                           |
|--------------------------|-------------------------------------------------------------------------------------------|
| `PROCESSING_UNSPECIFIED` | Default. Uses model-specific processing (3.5 Pro+ --\> AGENTIC, older models --\> STATIC) |
| `STATIC`                 | Fixed-rate frame extraction. All frames placed in context.                                |
| `AGENTIC`                | Model-driven dynamic navigation.                                                          |

## StaticMediaProcessing

| Fields         |                                                                                                                                                                                                                                                                             |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_offset` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Optional. Segment start time. Specified as a decimal number of seconds followed by an 's' suffix, e.g., "10.5s". Must be non-negative.                                                      |
| `end_offset`   | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Optional. Segment end time. Specified as a decimal number of seconds followed by an 's' suffix, e.g., "30s". Must be non-negative and greater than `start_offset` if `start_offset` is set. |
| `fps`          | `double` Optional. Video frame-rate sampling density.                                                                                                                                                                                                                       |

## VideoDelta

| Fields                                                                      |                                                                                                                                                                                |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mime_type`                                                                 | [`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoContent.MimeType)                               |
| `resolution`                                                                | [`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.MediaResolution) The resolution of the media. |
| Union field `data_or_uri` . `data_or_uri` can be only one of the following: |                                                                                                                                                                                |
| `data`                                                                      | `bytes`                                                                                                                                                                        |
| `uri`                                                                       | `string`                                                                                                                                                                       |

## VideoResponseFormat

Configuration for video output format.

| Fields         |                                                                                                                                                                                                            |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`     | [`Delivery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat.Delivery) The delivery mode for the video output.            |
| `gcs_uri`      | `string` The Cloud Storage URI to store the video output. Required for Vertex if delivery mode is URI.                                                                                                     |
| `aspect_ratio` | [`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat.AspectRatio) The aspect ratio for the video output.       |
| `duration`     | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) The duration for the video output.                                                                                         |
| `resolution`   | [`Resolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/genai.vertex.v1#genai.vertex.v1.VideoResponseFormat.Resolution) The video output resolution. Defaults to 720p. |

## AspectRatio

Supported aspect ratios for video output.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`     | Default value. This value is unused. |
| `ASPECT_RATIO_SIXTEEN_BY_NINE` | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_NINE_BY_SIXTEEN` | 9:16 aspect ratio.                   |

## Delivery

Delivery mode for video output.

| Enums                  |                                                |
|------------------------|------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.           |
| `INLINE`               | Video data is returned inline in the response. |
| `URI`                  | Video data is returned as a URI.               |

## Resolution

Supported resolutions for video output.

| Enums                       |                                      |
|-----------------------------|--------------------------------------|
| `RESOLUTION_UNSPECIFIED`    | Default value. This value is unused. |
| `RESOLUTION_THREE_SIXTY_P`  | 360p resolution.                     |
| `RESOLUTION_SEVEN_TWENTY_P` | 720p resolution.                     |
| `RESOLUTION_TEN_EIGHTY_P`   | 1080p resolution.                    |
| `RESOLUTION_FOUR_K`         | 4K resolution.                       |

## WordInfo

Word-level ASR annotation for transcription output. Carries the word text, optional timing, and optional speaker attribution.

| Fields         |                                                                                                                                                                                                            |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`         | `string` The transcribed word.                                                                                                                                                                             |
| `start_offset` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Start offset in time of the word relative to the start of the audio. Present when timestamp_granularities contains "word". |
| `end_offset`   | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) End offset in time of the word relative to the start of the audio. Present when timestamp_granularities contains "word".   |
| `speaker`      | `string` Optional. Speaker label for this word (e.g. "spk_1", "spk_2"). Present when diarization_mode is set in TranscriptionConfig.                                                                       |
