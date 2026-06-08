---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc
title: Agent Platform API
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Agent Platform API lets you manage Agent Platform resources in Google Cloud.

## Service: aiplatform.googleapis.com

The Service name `aiplatform.googleapis.com` is needed to create RPC client stubs.

## `        google.cloud.aiplatform.v1.DataFoundryService       `

Methods

`  GenerateSyntheticData  `

Generates synthetic (artificial) data based on a description

## `        google.cloud.aiplatform.v1.DatasetService       `

Methods

`  CreateDataset  `

Creates a Dataset.

`  CreateDatasetVersion  `

Create a version from a Dataset.

`  DeleteDataset  `

Deletes a Dataset.

`  DeleteDatasetVersion  `

Deletes a Dataset version.

`  DeleteSavedQuery  `

Deletes a SavedQuery.

`  ExportData  `

Exports data from a Dataset.

`  GetAnnotationSpec  `

Gets an AnnotationSpec.

`  GetDataset  `

Gets a Dataset.

`  GetDatasetVersion  `

Gets a Dataset version.

`  ImportData  `

Imports data into a Dataset.

`  ListAnnotations  `

Lists Annotations belongs to a dataitem.

`  ListDataItems  `

Lists DataItems in a Dataset.

`  ListDatasetVersions  `

Lists DatasetVersions in a Dataset.

`  ListDatasets  `

Lists Datasets in a Location.

`  ListSavedQueries  `

Lists SavedQueries in a Dataset.

`  RestoreDatasetVersion  `

Restores a dataset version.

`  SearchDataItems  `

Searches DataItems in a Dataset.

`  UpdateDataset  `

Updates a Dataset.

`  UpdateDatasetVersion  `

Updates a DatasetVersion.

## `        google.cloud.aiplatform.v1.DeploymentResourcePoolService       `

Methods

`  CreateDeploymentResourcePool  `

Create a DeploymentResourcePool.

`  DeleteDeploymentResourcePool  `

Delete a DeploymentResourcePool.

`  GetDeploymentResourcePool  `

Get a DeploymentResourcePool.

`  ListDeploymentResourcePools  `

List DeploymentResourcePools in a location.

`  QueryDeployedModels  `

List DeployedModels that have been deployed on this DeploymentResourcePool.

`  UpdateDeploymentResourcePool  `

Update a DeploymentResourcePool.

## `        google.cloud.aiplatform.v1.EndpointService       `

Methods

`  CreateEndpoint  `

Creates an Endpoint.

`  DeleteEndpoint  `

Deletes an Endpoint.

`  DeployModel  `

Deploys a Model into this Endpoint, creating a DeployedModel within it.

`  GetEndpoint  `

Gets an Endpoint.

`  ListEndpoints  `

Lists Endpoints in a Location.

`  MutateDeployedModel  `

Updates an existing deployed model.

`  UndeployModel  `

Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

`  UpdateEndpoint  `

Updates an Endpoint.

`  UpdateEndpointLongRunning  `

Updates an Endpoint with a long running operation.

## `        google.cloud.aiplatform.v1.EvaluationService       `

Methods

`  EvaluateInstances  `

Evaluates instances based on a given metric.

## `        google.cloud.aiplatform.v1.FeatureOnlineStoreAdminService       `

Methods

`  CreateFeatureOnlineStore  `

Creates a new FeatureOnlineStore in a given project and location.

`  CreateFeatureView  `

Creates a new FeatureView in a given FeatureOnlineStore.

`  DeleteFeatureOnlineStore  `

Deletes a single FeatureOnlineStore.

`  DeleteFeatureView  `

Deletes a single FeatureView.

`  GetFeatureOnlineStore  `

Gets details of a single FeatureOnlineStore.

`  GetFeatureView  `

Gets details of a single FeatureView.

`  GetFeatureViewSync  `

Gets details of a single FeatureViewSync.

`  ListFeatureOnlineStores  `

Lists FeatureOnlineStores in a given project and location.

`  ListFeatureViewSyncs  `

Lists FeatureViewSyncs in a given FeatureView.

`  ListFeatureViews  `

Lists FeatureViews in a given FeatureOnlineStore.

`  SyncFeatureView  `

Triggers on-demand sync for the FeatureView.

`  UpdateFeatureOnlineStore  `

Updates the parameters of a single FeatureOnlineStore.

`  UpdateFeatureView  `

Updates the parameters of a single FeatureView.

## `        google.cloud.aiplatform.v1.FeatureOnlineStoreService       `

Methods

`  FeatureViewDirectWrite  `

Bidirectional streaming RPC to directly write to feature values in a feature view.

`  FetchFeatureValues  `

Fetch feature values under a FeatureView.

`  GenerateFetchAccessToken  `

RPC to generate an access token for the given feature view.

`  SearchNearestEntities  `

Search the nearest entities under a FeatureView.

## `        google.cloud.aiplatform.v1.FeatureRegistryService       `

Methods

`  BatchCreateFeatures  `

Creates a batch of Features in a given FeatureGroup.

`  CreateFeature  `

Creates a new Feature in a given FeatureGroup.

`  CreateFeatureGroup  `

Creates a new FeatureGroup in a given project and location.

`  DeleteFeature  `

Deletes a single Feature.

`  DeleteFeatureGroup  `

Deletes a single FeatureGroup.

`  GetFeature  `

Gets details of a single Feature.

`  GetFeatureGroup  `

Gets details of a single FeatureGroup.

`  ListFeatureGroups  `

Lists FeatureGroups in a given project and location.

`  ListFeatures  `

Lists Features in a given FeatureGroup.

`  UpdateFeature  `

Updates the parameters of a single Feature.

`  UpdateFeatureGroup  `

Updates the parameters of a single FeatureGroup.

## `        google.cloud.aiplatform.v1.FeaturestoreOnlineServingService       `

Methods

`  ReadFeatureValues  `

Reads Feature values of a specific entity of an EntityType.

`  StreamingReadFeatureValues  `

Reads Feature values for multiple entities.

`  WriteFeatureValues  `

Writes Feature values of one or more entities of an EntityType.

## `        google.cloud.aiplatform.v1.FeaturestoreService       `

Methods

`  BatchCreateFeatures  `

Creates a batch of Features in a given EntityType.

`  BatchReadFeatureValues  `

Batch reads Feature values from a Featurestore.

`  CreateEntityType  `

Creates a new EntityType in a given Featurestore.

`  CreateFeature  `

Creates a new Feature in a given EntityType.

`  CreateFeaturestore  `

Creates a new Featurestore in a given project and location.

`  DeleteEntityType  `

Deletes a single EntityType.

`  DeleteFeature  `

Deletes a single Feature.

`  DeleteFeatureValues  `

Delete Feature values from Featurestore.

`  DeleteFeaturestore  `

Deletes a single Featurestore.

`  ExportFeatureValues  `

Exports Feature values from all the entities of a target EntityType.

`  GetEntityType  `

Gets details of a single EntityType.

`  GetFeature  `

Gets details of a single Feature.

`  GetFeaturestore  `

Gets details of a single Featurestore.

`  ImportFeatureValues  `

Imports Feature values into the Featurestore from a source storage.

`  ListEntityTypes  `

Lists EntityTypes in a given Featurestore.

`  ListFeatures  `

Lists Features in a given EntityType.

`  ListFeaturestores  `

Lists Featurestores in a given project and location.

`  SearchFeatures  `

Searches Features matching a query in a given project.

`  UpdateEntityType  `

Updates the parameters of a single EntityType.

`  UpdateFeature  `

Updates the parameters of a single Feature.

`  UpdateFeaturestore  `

Updates the parameters of a single Featurestore.

## `        google.cloud.aiplatform.v1.GenAiCacheService       `

Methods

`  CreateCachedContent  `

Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

`  DeleteCachedContent  `

Deletes cached content

`  GetCachedContent  `

Gets cached content configurations

`  ListCachedContents  `

Lists cached contents in a project

`  UpdateCachedContent  `

Updates cached content configurations

## `        google.cloud.aiplatform.v1.GenAiTuningService       `

Methods

`  CancelTuningJob  `

Cancels a tuning job.

`  CreateTuningJob  `

Creates a tuning job.

`  GetTuningJob  `

Gets a tuning job.

`  ListTuningJobs  `

Lists tuning jobs in a location.

`  RebaseTunedModel  `

Rebase a tuned model.

## `        google.cloud.aiplatform.v1.IndexEndpointService       `

Methods

`  CreateIndexEndpoint  `

Creates an IndexEndpoint.

`  DeleteIndexEndpoint  `

Deletes an IndexEndpoint.

`  DeployIndex  `

Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it.

`  GetIndexEndpoint  `

Gets an IndexEndpoint.

`  ListIndexEndpoints  `

Lists IndexEndpoints in a Location.

`  MutateDeployedIndex  `

Update an existing DeployedIndex under an IndexEndpoint.

`  UndeployIndex  `

Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

`  UpdateIndexEndpoint  `

Updates an IndexEndpoint.

## `        google.cloud.aiplatform.v1.IndexService       `

Methods

`  CreateIndex  `

Creates an Index.

`  DeleteIndex  `

Deletes an Index.

`  GetIndex  `

Gets an Index.

`  ListIndexes  `

Lists Indexes in a Location.

`  RemoveDatapoints  `

Remove Datapoints from an Index.

`  UpdateIndex  `

Updates an Index.

`  UpsertDatapoints  `

Add/update Datapoints into an Index.

## `        google.cloud.aiplatform.v1.JobService       `

Methods

`  CancelBatchPredictionJob  `

Cancels a BatchPredictionJob.

`  CancelCustomJob  `

Cancels a CustomJob.

`  CancelHyperparameterTuningJob  `

Cancels a HyperparameterTuningJob.

`  CancelNasJob  `

Cancels a NasJob.

`  CreateBatchPredictionJob  `

Creates a BatchPredictionJob.

`  CreateCustomJob  `

Creates a CustomJob.

`  CreateHyperparameterTuningJob  `

Creates a HyperparameterTuningJob

`  CreateModelDeploymentMonitoringJob  `

Creates a ModelDeploymentMonitoringJob.

`  CreateNasJob  `

Creates a NasJob

`  DeleteBatchPredictionJob  `

Deletes a BatchPredictionJob.

`  DeleteCustomJob  `

Deletes a CustomJob.

`  DeleteHyperparameterTuningJob  `

Deletes a HyperparameterTuningJob.

`  DeleteModelDeploymentMonitoringJob  `

Deletes a ModelDeploymentMonitoringJob.

`  DeleteNasJob  `

Deletes a NasJob.

`  GetBatchPredictionJob  `

Gets a BatchPredictionJob

`  GetCustomJob  `

Gets a CustomJob.

`  GetHyperparameterTuningJob  `

Gets a HyperparameterTuningJob

`  GetModelDeploymentMonitoringJob  `

Gets a ModelDeploymentMonitoringJob.

`  GetNasJob  `

Gets a NasJob

`  GetNasTrialDetail  `

Gets a NasTrialDetail.

`  ListBatchPredictionJobs  `

Lists BatchPredictionJobs in a Location.

`  ListCustomJobs  `

Lists CustomJobs in a Location.

`  ListHyperparameterTuningJobs  `

Lists HyperparameterTuningJobs in a Location.

`  ListModelDeploymentMonitoringJobs  `

Lists ModelDeploymentMonitoringJobs in a Location.

`  ListNasJobs  `

Lists NasJobs in a Location.

`  ListNasTrialDetails  `

List top NasTrialDetails of a NasJob.

`  PauseModelDeploymentMonitoringJob  `

Pauses a ModelDeploymentMonitoringJob.

`  ResumeModelDeploymentMonitoringJob  `

Resumes a paused ModelDeploymentMonitoringJob.

`  SearchModelDeploymentMonitoringStatsAnomalies  `

Searches Model Monitoring Statistics generated within a given time window.

`  UpdateModelDeploymentMonitoringJob  `

Updates a ModelDeploymentMonitoringJob.

## `        google.cloud.aiplatform.v1.LlmUtilityService       `

Methods

`  ComputeTokens  `

Return a list of tokens based on the input text.

`  CountTokens  `

Perform a token counting.

## `        google.cloud.aiplatform.v1.MatchService       `

Methods

## `        google.cloud.aiplatform.v1.MetadataService       `

Methods

`  AddContextArtifactsAndExecutions  `

Adds a set of Artifacts and Executions to a Context.

`  AddContextChildren  `

Adds a set of Contexts as children to a parent Context.

`  AddExecutionEvents  `

Adds Events to the specified Execution.

`  CreateArtifact  `

Creates an Artifact associated with a MetadataStore.

`  CreateContext  `

Creates a Context associated with a MetadataStore.

`  CreateExecution  `

Creates an Execution associated with a MetadataStore.

`  CreateMetadataSchema  `

Creates a MetadataSchema.

`  CreateMetadataStore  `

Initializes a MetadataStore, including allocation of resources.

`  DeleteArtifact  `

Deletes an Artifact.

`  DeleteContext  `

Deletes a stored Context.

`  DeleteExecution  `

Deletes an Execution.

`  DeleteMetadataStore  `

Deletes a single MetadataStore and all its child resources (Artifacts, Executions, and Contexts).

`  GetArtifact  `

Retrieves a specific Artifact.

`  GetContext  `

Retrieves a specific Context.

`  GetExecution  `

Retrieves a specific Execution.

`  GetMetadataSchema  `

Retrieves a specific MetadataSchema.

`  GetMetadataStore  `

Retrieves a specific MetadataStore.

`  ListArtifacts  `

Lists Artifacts in the MetadataStore.

`  ListContexts  `

Lists Contexts on the MetadataStore.

`  ListExecutions  `

Lists Executions in the MetadataStore.

`  ListMetadataSchemas  `

Lists MetadataSchemas.

`  ListMetadataStores  `

Lists MetadataStores for a Location.

`  PurgeArtifacts  `

Purges Artifacts.

`  PurgeContexts  `

Purges Contexts.

`  PurgeExecutions  `

Purges Executions.

`  QueryArtifactLineageSubgraph  `

Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.

`  QueryContextLineageSubgraph  `

Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.

`  QueryExecutionInputsAndOutputs  `

Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting Events.

`  RemoveContextChildren  `

Remove a set of children contexts from a parent Context.

`  UpdateArtifact  `

Updates a stored Artifact.

`  UpdateContext  `

Updates a stored Context.

`  UpdateExecution  `

Updates a stored Execution.

## `        google.cloud.aiplatform.v1.MigrationService       `

Methods

`  BatchMigrateResources  `

Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Agent Platform.

`  SearchMigratableResources  `

Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Agent Platform's given location.

## `        google.cloud.aiplatform.v1.ModelGardenService       `

Methods

`  Deploy  `

Deploys a model to a new endpoint.

`  GetPublisherModel  `

Gets a Model Garden publisher model.

## `        google.cloud.aiplatform.v1.ModelService       `

Methods

`  BatchImportEvaluatedAnnotations  `

Imports a list of externally generated EvaluatedAnnotations.

`  BatchImportModelEvaluationSlices  `

Imports a list of externally generated ModelEvaluationSlice.

`  CopyModel  `

Copies an already existing Agent Platform Model into the specified Location.

`  DeleteModel  `

Deletes a Model.

`  DeleteModelVersion  `

Deletes a Model version.

`  ExportModel  `

Exports a trained, exportable Model to a location specified by the user.

`  GetModel  `

Gets a Model.

`  GetModelEvaluation  `

Gets a ModelEvaluation.

`  GetModelEvaluationSlice  `

Gets a ModelEvaluationSlice.

`  ImportModelEvaluation  `

Imports an externally generated ModelEvaluation.

`  ListModelEvaluationSlices  `

Lists ModelEvaluationSlices in a ModelEvaluation.

`  ListModelEvaluations  `

Lists ModelEvaluations in a Model.

`  ListModelVersionCheckpoints  `

Lists checkpoints of the specified model version.

`  ListModelVersions  `

Lists versions of the specified model.

`  ListModels  `

Lists Models in a Location.

`  MergeVersionAliases  `

Merges a set of aliases for a Model version.

`  UpdateExplanationDataset  `

Incrementally update the dataset used for an examples model.

`  UpdateModel  `

Updates a Model.

`  UploadModel  `

Uploads a Model artifact into Agent Platform.

## `        google.cloud.aiplatform.v1.NotebookService       `

Methods

`  AssignNotebookRuntime  `

Assigns a NotebookRuntime to a user for a particular Notebook file.

`  CreateNotebookExecutionJob  `

Creates a NotebookExecutionJob.

`  CreateNotebookRuntimeTemplate  `

Creates a NotebookRuntimeTemplate.

`  DeleteNotebookExecutionJob  `

Deletes a NotebookExecutionJob.

`  DeleteNotebookRuntime  `

Deletes a NotebookRuntime.

`  DeleteNotebookRuntimeTemplate  `

Deletes a NotebookRuntimeTemplate.

`  GetNotebookExecutionJob  `

Gets a NotebookExecutionJob.

`  GetNotebookRuntime  `

Gets a NotebookRuntime.

`  GetNotebookRuntimeTemplate  `

Gets a NotebookRuntimeTemplate.

`  ListNotebookExecutionJobs  `

Lists NotebookExecutionJobs in a Location.

`  ListNotebookRuntimeTemplates  `

Lists NotebookRuntimeTemplates in a Location.

`  ListNotebookRuntimes  `

Lists NotebookRuntimes in a Location.

`  StartNotebookRuntime  `

Starts a NotebookRuntime.

`  StopNotebookRuntime  `

Stops a NotebookRuntime.

`  UpdateNotebookRuntimeTemplate  `

Updates a NotebookRuntimeTemplate.

`  UpgradeNotebookRuntime  `

Upgrades a NotebookRuntime.

## `        google.cloud.aiplatform.v1.PersistentResourceService       `

Methods

`  CreatePersistentResource  `

Creates a PersistentResource.

`  DeletePersistentResource  `

Deletes a PersistentResource.

`  GetPersistentResource  `

Gets a PersistentResource.

`  ListPersistentResources  `

Lists PersistentResources in a Location.

`  RebootPersistentResource  `

Reboots a PersistentResource.

`  UpdatePersistentResource  `

Updates a PersistentResource.

## `        google.cloud.aiplatform.v1.PipelineService       `

Methods

`  BatchCancelPipelineJobs  `

Batch cancel PipelineJobs.

`  BatchDeletePipelineJobs  `

Batch deletes PipelineJobs The Operation is atomic.

`  CancelPipelineJob  `

Cancels a PipelineJob.

`  CancelTrainingPipeline  `

Cancels a TrainingPipeline.

`  CreatePipelineJob  `

Creates a PipelineJob.

`  CreateTrainingPipeline  `

Creates a TrainingPipeline.

`  DeletePipelineJob  `

Deletes a PipelineJob.

`  DeleteTrainingPipeline  `

Deletes a TrainingPipeline.

`  GetPipelineJob  `

Gets a PipelineJob.

`  GetTrainingPipeline  `

Gets a TrainingPipeline.

`  ListPipelineJobs  `

Lists PipelineJobs in a Location.

`  ListTrainingPipelines  `

Lists TrainingPipelines in a Location.

## `        google.cloud.aiplatform.v1.PredictionService       `

Methods

`  DirectPredict  `

Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

`  DirectRawPredict  `

Perform an unary online prediction request to a gRPC model server for custom containers.

`  EmbedContent  `

Embed content with multimodal inputs.

`  Explain  `

Perform an online explanation.

`  GenerateContent  `

Generate content with multimodal inputs.

`  Predict  `

Perform an online inference.

`  RawPredict  `

Perform an online prediction with an arbitrary HTTP payload.

`  ServerStreamingPredict  `

Perform a server-side streaming online prediction request for Vertex LLM streaming.

`  StreamDirectPredict  `

Perform a streaming online prediction request to a gRPC model server for Vertex first-party products and frameworks.

`  StreamDirectRawPredict  `

Perform a streaming online prediction request to a gRPC model server for custom containers.

`  StreamGenerateContent  `

Generate content with multimodal inputs with streaming support.

`  StreamRawPredict  `

Perform a streaming online prediction with an arbitrary HTTP payload.

`  StreamingPredict  `

Perform a streaming online prediction request for Vertex first-party products and frameworks.

`  StreamingRawPredict  `

Perform a streaming online prediction request through gRPC.

## `        google.cloud.aiplatform.v1.ReasoningEngineExecutionService       `

Methods

`  AsyncQueryReasoningEngine  `

Async query using a reasoning engine.

`  BidiInvokeReasoningEngine  `

Invokes reasoning engine with arbitrary WebSocket requests for bidi streaming

`  CancelAsyncQueryReasoningEngine  `

Cancels an AsyncQueryReasoningEngine operation.

`  InvokeReasoningEngine  `

Invokes reasoning engine with arbitrary HTTP requests for both unary and server-side streaming cases.

`  QueryReasoningEngine  `

Queries using a reasoning engine.

`  StreamQueryReasoningEngine  `

Streams queries using a reasoning engine.

## `        google.cloud.aiplatform.v1.ReasoningEngineService       `

Methods

`  CreateReasoningEngine  `

Creates a reasoning engine.

`  DeleteReasoningEngine  `

Deletes a reasoning engine.

`  GetReasoningEngine  `

Gets a reasoning engine.

`  ListReasoningEngines  `

Lists reasoning engines in a location.

`  UpdateReasoningEngine  `

Updates a reasoning engine.

## `        google.cloud.aiplatform.v1.ScheduleService       `

Methods

`  CreateSchedule  `

Creates a Schedule.

`  DeleteSchedule  `

Deletes a Schedule.

`  GetSchedule  `

Gets a Schedule.

`  ListSchedules  `

Lists Schedules in a Location.

`  PauseSchedule  `

Pauses a Schedule.

`  ResumeSchedule  `

Resumes a paused Schedule to start scheduling new runs.

`  UpdateSchedule  `

Updates an active or paused Schedule.

## `        google.cloud.aiplatform.v1.SessionService       `

Methods

`  AppendEvent  `

Appends an event to a given session.

`  CreateSession  `

Creates a new `  Session  ` .

`  DeleteSession  `

Deletes details of the specific `  Session  ` .

`  GetSession  `

Gets details of the specific `  Session  ` .

`  ListEvents  `

Lists `  Events  ` in a given session.

`  ListSessions  `

Lists `  Sessions  ` in a given reasoning engine.

`  UpdateSession  `

Updates the specific `  Session  ` .

## `        google.cloud.aiplatform.v1.SpecialistPoolService       `

Methods

`  CreateSpecialistPool  `

Creates a SpecialistPool.

`  DeleteSpecialistPool  `

Deletes a SpecialistPool as well as all Specialists in the pool.

`  GetSpecialistPool  `

Gets a SpecialistPool.

`  ListSpecialistPools  `

Lists SpecialistPools in a Location.

`  UpdateSpecialistPool  `

Updates a SpecialistPool.

## `        google.cloud.aiplatform.v1.TensorboardService       `

Methods

`  BatchCreateTensorboardRuns  `

Batch create TensorboardRuns.

`  BatchCreateTensorboardTimeSeries  `

Batch create TensorboardTimeSeries that belong to a TensorboardExperiment.

`  BatchReadTensorboardTimeSeriesData  `

Reads multiple TensorboardTimeSeries' data.

`  CreateTensorboard  `

Creates a Tensorboard.

`  CreateTensorboardExperiment  `

Creates a TensorboardExperiment.

`  CreateTensorboardRun  `

Creates a TensorboardRun.

`  CreateTensorboardTimeSeries  `

Creates a TensorboardTimeSeries.

`  DeleteTensorboard  `

Deletes a Tensorboard.

`  DeleteTensorboardExperiment  `

Deletes a TensorboardExperiment.

`  DeleteTensorboardRun  `

Deletes a TensorboardRun.

`  DeleteTensorboardTimeSeries  `

Deletes a TensorboardTimeSeries.

`  ExportTensorboardTimeSeriesData  `

Exports a TensorboardTimeSeries' data.

`  GetTensorboard  `

Gets a Tensorboard.

`  GetTensorboardExperiment  `

Gets a TensorboardExperiment.

`  GetTensorboardRun  `

Gets a TensorboardRun.

`  GetTensorboardTimeSeries  `

Gets a TensorboardTimeSeries.

`  ListTensorboardExperiments  `

Lists TensorboardExperiments in a Location.

`  ListTensorboardRuns  `

Lists TensorboardRuns in a Location.

`  ListTensorboardTimeSeries  `

Lists TensorboardTimeSeries in a Location.

`  ListTensorboards  `

Lists Tensorboards in a Location.

`  ReadTensorboardBlobData  `

Gets bytes of TensorboardBlobs.

`  ReadTensorboardSize  `

Returns the storage size for a given TensorBoard instance.

`  ReadTensorboardTimeSeriesData  `

Reads a TensorboardTimeSeries' data.

`  ReadTensorboardUsage  `

Returns a list of monthly active users for a given TensorBoard instance.

`  UpdateTensorboard  `

Updates a Tensorboard.

`  UpdateTensorboardExperiment  `

Updates a TensorboardExperiment.

`  UpdateTensorboardRun  `

Updates a TensorboardRun.

`  UpdateTensorboardTimeSeries  `

Updates a TensorboardTimeSeries.

`  WriteTensorboardExperimentData  `

Write time series data points of multiple TensorboardTimeSeries in multiple TensorboardRun's.

`  WriteTensorboardRunData  `

Write time series data points into multiple TensorboardTimeSeries under a TensorboardRun.

## `        google.cloud.aiplatform.v1.VertexRagDataService       `

Methods

`  CreateRagCorpus  `

Creates a RagCorpus.

`  DeleteRagCorpus  `

Deletes a RagCorpus.

`  DeleteRagFile  `

Deletes a RagFile.

`  GetRagCorpus  `

Gets a RagCorpus.

`  GetRagEngineConfig  `

Gets a RagEngineConfig.

`  GetRagFile  `

Gets a RagFile.

`  ImportRagFiles  `

Import files from Google Cloud Storage or Google Drive into a RagCorpus.

`  ListRagCorpora  `

Lists RagCorpora in a Location.

`  ListRagFiles  `

Lists RagFiles in a RagCorpus.

`  UpdateRagCorpus  `

Updates a RagCorpus.

`  UpdateRagEngineConfig  `

Updates a RagEngineConfig.

## `        google.cloud.aiplatform.v1.VertexRagService       `

Methods

`  AskContexts  `

Agentic Retrieval Ask API for RAG.

`  AsyncRetrieveContexts  `

Asynchronous API to retrieves relevant contexts for a query.

`  AugmentPrompt  `

Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

`  CorroborateContent  `

Given an input text, it returns a score that evaluates the factuality of the text.

`  RetrieveContexts  `

Retrieves relevant contexts for a query.

## `        google.cloud.aiplatform.v1.VizierService       `

Methods

`  AddTrialMeasurement  `

Adds a measurement of the objective metrics to a Trial.

`  CheckTrialEarlyStoppingState  `

Checks whether a Trial should stop or not.

`  CompleteTrial  `

Marks a Trial as complete.

`  CreateStudy  `

Creates a Study.

`  CreateTrial  `

Adds a user provided Trial to a Study.

`  DeleteStudy  `

Deletes a Study.

`  DeleteTrial  `

Deletes a Trial.

`  GetStudy  `

Gets a Study by name.

`  GetTrial  `

Gets a Trial.

`  ListOptimalTrials  `

Lists the pareto-optimal Trials for multi-objective Study or the optimal Trials for single-objective Study.

`  ListStudies  `

Lists all the studies in a region for an associated project.

`  ListTrials  `

Lists the Trials associated with a Study.

`  LookupStudy  `

Looks a study up using the user-defined display\_name field instead of the fully qualified resource name.

`  StopTrial  `

Stops a Trial.

`  SuggestTrials  `

Adds one or more Trials to a Study, with parameter values suggested by Agent Platform Vizier.

## `        google.cloud.aiplatform.v1beta1.AgentService       `

Methods

`  CreateAgent  `

Creates an agent.

`  DeleteAgent  `

Deletes an agent.

`  GetAgent  `

Retrieves an agent.

`  ListAgents  `

Lists agents in a location.

`  UpdateAgent  `

Updates an agent.

## `        google.cloud.aiplatform.v1beta1.DataFoundryService       `

Methods

`  GenerateSyntheticData  `

Generates synthetic (artificial) data based on a description

## `        google.cloud.aiplatform.v1beta1.DatasetService       `

Methods

`  AssembleData  `

Assembles each row of a multimodal dataset and writes the result into a BigQuery table.

`  AssessData  `

Assesses the state or validity of the dataset with respect to a given use case.

`  CreateDataset  `

Creates a Dataset.

`  CreateDatasetVersion  `

Create a version from a Dataset.

`  DeleteDataset  `

Deletes a Dataset.

`  DeleteDatasetVersion  `

Deletes a Dataset version.

`  DeleteSavedQuery  `

Deletes a SavedQuery.

`  ExportData  `

Exports data from a Dataset.

`  GetAnnotationSpec  `

Gets an AnnotationSpec.

`  GetDataset  `

Gets a Dataset.

`  GetDatasetVersion  `

Gets a Dataset version.

`  ImportData  `

Imports data into a Dataset.

`  ListAnnotations  `

Lists Annotations belongs to a dataitem.

`  ListDataItems  `

Lists DataItems in a Dataset.

`  ListDatasetVersions  `

Lists DatasetVersions in a Dataset.

`  ListDatasets  `

Lists Datasets in a Location.

`  ListSavedQueries  `

Lists SavedQueries in a Dataset.

`  RestoreDatasetVersion  `

Restores a dataset version.

`  SearchDataItems  `

Searches DataItems in a Dataset.

`  UpdateDataset  `

Updates a Dataset.

`  UpdateDatasetVersion  `

Updates a DatasetVersion.

## `        google.cloud.aiplatform.v1beta1.DeploymentResourcePoolService       `

Methods

`  CreateDeploymentResourcePool  `

Create a DeploymentResourcePool.

`  DeleteDeploymentResourcePool  `

Delete a DeploymentResourcePool.

`  GetDeploymentResourcePool  `

Get a DeploymentResourcePool.

`  ListDeploymentResourcePools  `

List DeploymentResourcePools in a location.

`  QueryDeployedModels  `

List DeployedModels that have been deployed on this DeploymentResourcePool.

`  UpdateDeploymentResourcePool  `

Update a DeploymentResourcePool.

## `        google.cloud.aiplatform.v1beta1.EndpointService       `

Methods

`  CreateEndpoint  `

Creates an Endpoint.

`  DeleteEndpoint  `

Deletes an Endpoint.

`  DeployModel  `

Deploys a Model into this Endpoint, creating a DeployedModel within it.

`  FetchPublisherModelConfig  `

Fetches the configs of publisher models.

`  GetEndpoint  `

Gets an Endpoint.

`  ListEndpoints  `

Lists Endpoints in a Location.

`  MutateDeployedModel  `

Updates an existing deployed model.

`  SetPublisherModelConfig  `

Sets (creates or updates) configs of publisher models.

`  UndeployModel  `

Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

`  UpdateEndpoint  `

Updates an Endpoint.

`  UpdateEndpointLongRunning  `

Updates an Endpoint with a long running operation.

## `        google.cloud.aiplatform.v1beta1.EvaluationAnalyticsService       `

Methods

`  GenerateLossClusters  `

Generates loss clusters from evaluation results.

## `        google.cloud.aiplatform.v1beta1.EvaluationService       `

Methods

`  EvaluateDataset  `

Evaluates a dataset based on a set of given metrics.

`  EvaluateInstances  `

Evaluates instances based on a given metric.

`  GenerateInstanceRubrics  `

Generates rubrics for a given prompt.

## `        google.cloud.aiplatform.v1beta1.ExampleStoreService       `

Methods

`  CreateExampleStore  `

Create an ExampleStore.

`  DeleteExampleStore  `

Delete an ExampleStore.

`  FetchExamples  `

Get Examples from the Example Store.

`  GetExampleStore  `

Get an ExampleStore.

`  ListExampleStores  `

List ExampleStores in a Location.

`  RemoveExamples  `

Remove Examples from the Example Store.

`  SearchExamples  `

Search for similar Examples for given selection criteria.

`  UpdateExampleStore  `

Update an ExampleStore.

`  UpsertExamples  `

Create or update Examples in the Example Store.

## `        google.cloud.aiplatform.v1beta1.ExtensionExecutionService       `

Methods

`  ExecuteExtension  `

Executes the request against a given extension.

`  QueryExtension  `

Queries an extension with a default controller.

## `        google.cloud.aiplatform.v1beta1.ExtensionRegistryService       `

Methods

`  DeleteExtension  `

Deletes an Extension.

`  GetExtension  `

Gets an Extension.

`  ImportExtension  `

Imports an Extension.

`  ListExtensions  `

Lists Extensions in a location.

`  UpdateExtension  `

Updates an Extension.

## `        google.cloud.aiplatform.v1beta1.FeatureOnlineStoreAdminService       `

Methods

`  CreateFeatureOnlineStore  `

Creates a new FeatureOnlineStore in a given project and location.

`  CreateFeatureView  `

Creates a new FeatureView in a given FeatureOnlineStore.

`  DeleteFeatureOnlineStore  `

Deletes a single FeatureOnlineStore.

`  DeleteFeatureView  `

Deletes a single FeatureView.

`  GetFeatureOnlineStore  `

Gets details of a single FeatureOnlineStore.

`  GetFeatureView  `

Gets details of a single FeatureView.

`  GetFeatureViewSync  `

Gets details of a single FeatureViewSync.

`  ListFeatureOnlineStores  `

Lists FeatureOnlineStores in a given project and location.

`  ListFeatureViewSyncs  `

Lists FeatureViewSyncs in a given FeatureView.

`  ListFeatureViews  `

Lists FeatureViews in a given FeatureOnlineStore.

`  SyncFeatureView  `

Triggers on-demand sync for the FeatureView.

`  UpdateFeatureOnlineStore  `

Updates the parameters of a single FeatureOnlineStore.

`  UpdateFeatureView  `

Updates the parameters of a single FeatureView.

## `        google.cloud.aiplatform.v1beta1.FeatureOnlineStoreService       `

Methods

`  FeatureViewDirectWrite  `

Bidirectional streaming RPC to directly write to feature values in a feature view.

`  FetchFeatureValues  `

Fetch feature values under a FeatureView.

`  GenerateFetchAccessToken  `

RPC to generate an access token for the given feature view.

`  SearchNearestEntities  `

Search the nearest entities under a FeatureView.

`  StreamingFetchFeatureValues  `

Bidirectional streaming RPC to fetch feature values under a FeatureView.

## `        google.cloud.aiplatform.v1beta1.FeatureRegistryService       `

Methods

`  BatchCreateFeatures  `

Creates a batch of Features in a given FeatureGroup.

`  CreateFeature  `

Creates a new Feature in a given FeatureGroup.

`  CreateFeatureGroup  `

Creates a new FeatureGroup in a given project and location.

`  CreateFeatureMonitor  `

Creates a new FeatureMonitor in a given project, location and FeatureGroup.

`  CreateFeatureMonitorJob  `

Creates a new feature monitor job.

`  DeleteFeature  `

Deletes a single Feature.

`  DeleteFeatureGroup  `

Deletes a single FeatureGroup.

`  DeleteFeatureMonitor  `

Deletes a single FeatureMonitor.

`  GetFeature  `

Gets details of a single Feature.

`  GetFeatureGroup  `

Gets details of a single FeatureGroup.

`  GetFeatureMonitor  `

Gets details of a single FeatureMonitor.

`  GetFeatureMonitorJob  `

Get a feature monitor job.

`  ListFeatureGroups  `

Lists FeatureGroups in a given project and location.

`  ListFeatureMonitorJobs  `

List feature monitor jobs.

`  ListFeatureMonitors  `

Lists FeatureGroups in a given project and location.

`  ListFeatures  `

Lists Features in a given FeatureGroup.

`  UpdateFeature  `

Updates the parameters of a single Feature.

`  UpdateFeatureGroup  `

Updates the parameters of a single FeatureGroup.

`  UpdateFeatureMonitor  `

Updates the parameters of a single FeatureMonitor.

## `        google.cloud.aiplatform.v1beta1.FeaturestoreOnlineServingService       `

Methods

`  ReadFeatureValues  `

Reads Feature values of a specific entity of an EntityType.

`  StreamingReadFeatureValues  `

Reads Feature values for multiple entities.

`  WriteFeatureValues  `

Writes Feature values of one or more entities of an EntityType.

## `        google.cloud.aiplatform.v1beta1.FeaturestoreService       `

Methods

`  BatchCreateFeatures  `

Creates a batch of Features in a given EntityType.

`  BatchReadFeatureValues  `

Batch reads Feature values from a Featurestore.

`  CreateEntityType  `

Creates a new EntityType in a given Featurestore.

`  CreateFeature  `

Creates a new Feature in a given EntityType.

`  CreateFeaturestore  `

Creates a new Featurestore in a given project and location.

`  DeleteEntityType  `

Deletes a single EntityType.

`  DeleteFeature  `

Deletes a single Feature.

`  DeleteFeatureValues  `

Delete Feature values from Featurestore.

`  DeleteFeaturestore  `

Deletes a single Featurestore.

`  ExportFeatureValues  `

Exports Feature values from all the entities of a target EntityType.

`  GetEntityType  `

Gets details of a single EntityType.

`  GetFeature  `

Gets details of a single Feature.

`  GetFeaturestore  `

Gets details of a single Featurestore.

`  ImportFeatureValues  `

Imports Feature values into the Featurestore from a source storage.

`  ListEntityTypes  `

Lists EntityTypes in a given Featurestore.

`  ListFeatures  `

Lists Features in a given EntityType.

`  ListFeaturestores  `

Lists Featurestores in a given project and location.

`  SearchFeatures  `

Searches Features matching a query in a given project.

`  UpdateEntityType  `

Updates the parameters of a single EntityType.

`  UpdateFeature  `

Updates the parameters of a single Feature.

`  UpdateFeaturestore  `

Updates the parameters of a single Featurestore.

## `        google.cloud.aiplatform.v1beta1.GenAiCacheService       `

Methods

`  CreateCachedContent  `

Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

`  DeleteCachedContent  `

Deletes cached content

`  GetCachedContent  `

Gets cached content configurations

`  ListCachedContents  `

Lists cached contents in a project

`  UpdateCachedContent  `

Updates cached content configurations

## `        google.cloud.aiplatform.v1beta1.GenAiTuningService       `

Methods

`  CancelTuningJob  `

Cancels a tuning job.

`  CreateTuningJob  `

Creates a tuning job.

`  GetTuningJob  `

Gets a tuning job.

`  ListTuningJobs  `

Lists tuning jobs in a location.

`  RebaseTunedModel  `

Rebase a tuned model.

## `        google.cloud.aiplatform.v1beta1.IndexEndpointService       `

Methods

`  CreateIndexEndpoint  `

Creates an IndexEndpoint.

`  DeleteIndexEndpoint  `

Deletes an IndexEndpoint.

`  DeployIndex  `

Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it.

`  GetIndexEndpoint  `

Gets an IndexEndpoint.

`  ListIndexEndpoints  `

Lists IndexEndpoints in a Location.

`  MutateDeployedIndex  `

Update an existing DeployedIndex under an IndexEndpoint.

`  UndeployIndex  `

Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

`  UpdateIndexEndpoint  `

Updates an IndexEndpoint.

## `        google.cloud.aiplatform.v1beta1.IndexService       `

Methods

`  CreateIndex  `

Creates an Index.

`  DeleteIndex  `

Deletes an Index.

`  GetIndex  `

Gets an Index.

`  ImportIndex  `

Imports an Index from an external source (e.g., BigQuery).

`  ListIndexes  `

Lists Indexes in a Location.

`  RemoveDatapoints  `

Remove Datapoints from an Index.

`  UpdateIndex  `

Updates an Index.

`  UpsertDatapoints  `

Add/update Datapoints into an Index.

## `        google.cloud.aiplatform.v1beta1.JobService       `

Methods

`  CancelBatchPredictionJob  `

Cancels a BatchPredictionJob.

`  CancelCustomJob  `

Cancels a CustomJob.

`  CancelHyperparameterTuningJob  `

Cancels a HyperparameterTuningJob.

`  CreateBatchPredictionJob  `

Creates a BatchPredictionJob.

`  CreateCustomJob  `

Creates a CustomJob.

`  CreateHyperparameterTuningJob  `

Creates a HyperparameterTuningJob

`  CreateModelDeploymentMonitoringJob  `

Creates a ModelDeploymentMonitoringJob.

`  DeleteBatchPredictionJob  `

Deletes a BatchPredictionJob.

`  DeleteCustomJob  `

Deletes a CustomJob.

`  DeleteHyperparameterTuningJob  `

Deletes a HyperparameterTuningJob.

`  DeleteModelDeploymentMonitoringJob  `

Deletes a ModelDeploymentMonitoringJob.

`  GetBatchPredictionJob  `

Gets a BatchPredictionJob

`  GetCustomJob  `

Gets a CustomJob.

`  GetHyperparameterTuningJob  `

Gets a HyperparameterTuningJob

`  GetModelDeploymentMonitoringJob  `

Gets a ModelDeploymentMonitoringJob.

`  ListBatchPredictionJobs  `

Lists BatchPredictionJobs in a Location.

`  ListCustomJobs  `

Lists CustomJobs in a Location.

`  ListHyperparameterTuningJobs  `

Lists HyperparameterTuningJobs in a Location.

`  ListModelDeploymentMonitoringJobs  `

Lists ModelDeploymentMonitoringJobs in a Location.

`  PauseModelDeploymentMonitoringJob  `

Pauses a ModelDeploymentMonitoringJob.

`  ResumeModelDeploymentMonitoringJob  `

Resumes a paused ModelDeploymentMonitoringJob.

`  SearchModelDeploymentMonitoringStatsAnomalies  `

Searches Model Monitoring Statistics generated within a given time window.

`  UpdateModelDeploymentMonitoringJob  `

Updates a ModelDeploymentMonitoringJob.

## `        google.cloud.aiplatform.v1beta1.LlmUtilityService       `

Methods

`  ComputeTokens  `

Return a list of tokens based on the input text.

## `        google.cloud.aiplatform.v1beta1.MatchService       `

Methods

## `        google.cloud.aiplatform.v1beta1.MemoryBankService       `

Methods

`  CreateMemory  `

Create a Memory.

`  DeleteMemory  `

Delete a Memory.

`  GenerateMemories  `

Generate memories.

`  GetMemory  `

Get a Memory.

`  IngestEvents  `

Ingests events for a Memory Bank.

`  ListMemories  `

List Memories.

`  RetrieveMemories  `

Retrieve memories.

`  RetrieveProfiles  `

Retrieves profiles.

`  UpdateMemory  `

Update a Memory.

## `        google.cloud.aiplatform.v1beta1.MetadataService       `

Methods

`  AddContextArtifactsAndExecutions  `

Adds a set of Artifacts and Executions to a Context.

`  AddContextChildren  `

Adds a set of Contexts as children to a parent Context.

`  AddExecutionEvents  `

Adds Events to the specified Execution.

`  CreateArtifact  `

Creates an Artifact associated with a MetadataStore.

`  CreateContext  `

Creates a Context associated with a MetadataStore.

`  CreateExecution  `

Creates an Execution associated with a MetadataStore.

`  CreateMetadataSchema  `

Creates a MetadataSchema.

`  CreateMetadataStore  `

Initializes a MetadataStore, including allocation of resources.

`  DeleteArtifact  `

Deletes an Artifact.

`  DeleteContext  `

Deletes a stored Context.

`  DeleteExecution  `

Deletes an Execution.

`  DeleteMetadataStore  `

Deletes a single MetadataStore and all its child resources (Artifacts, Executions, and Contexts).

`  GetArtifact  `

Retrieves a specific Artifact.

`  GetContext  `

Retrieves a specific Context.

`  GetExecution  `

Retrieves a specific Execution.

`  GetMetadataSchema  `

Retrieves a specific MetadataSchema.

`  GetMetadataStore  `

Retrieves a specific MetadataStore.

`  ListArtifacts  `

Lists Artifacts in the MetadataStore.

`  ListContexts  `

Lists Contexts on the MetadataStore.

`  ListExecutions  `

Lists Executions in the MetadataStore.

`  ListMetadataSchemas  `

Lists MetadataSchemas.

`  ListMetadataStores  `

Lists MetadataStores for a Location.

`  PurgeArtifacts  `

Purges Artifacts.

`  PurgeContexts  `

Purges Contexts.

`  PurgeExecutions  `

Purges Executions.

`  QueryArtifactLineageSubgraph  `

Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.

`  QueryContextLineageSubgraph  `

Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.

`  QueryExecutionInputsAndOutputs  `

Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting Events.

`  RemoveContextChildren  `

Remove a set of children contexts from a parent Context.

`  UpdateArtifact  `

Updates a stored Artifact.

`  UpdateContext  `

Updates a stored Context.

`  UpdateExecution  `

Updates a stored Execution.

## `        google.cloud.aiplatform.v1beta1.MigrationService       `

Methods

`  BatchMigrateResources  `

Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Agent Platform.

`  SearchMigratableResources  `

Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Agent Platform's given location.

## `        google.cloud.aiplatform.v1beta1.ModelGardenService       `

Methods

`  AcceptPublisherModelEula  `

Accepts the EULA acceptance status of a publisher model.

`  CheckPublisherModelEulaAcceptance  `

Checks the EULA acceptance status of a publisher model.

`  Deploy  `

Deploys a model to a new endpoint.

`  DeployPublisherModel  `  
**(deprecated)**

Deploys publisher models.

`  ExportPublisherModel  `

Exports a publisher model to a user provided Google Cloud Storage bucket.

`  GetPublisherModel  `

Gets a Model Garden publisher model.

`  ListPublisherModels  `

Lists publisher models in Model Garden.

## `        google.cloud.aiplatform.v1beta1.ModelMonitoringService       `

Methods

`  CreateModelMonitor  `

Creates a ModelMonitor.

`  CreateModelMonitoringJob  `

Creates a ModelMonitoringJob.

`  DeleteModelMonitor  `

Deletes a ModelMonitor.

`  DeleteModelMonitoringJob  `

Deletes a ModelMonitoringJob.

`  GetModelMonitor  `

Gets a ModelMonitor.

`  GetModelMonitoringJob  `

Gets a ModelMonitoringJob.

`  ListModelMonitoringJobs  `

Lists ModelMonitoringJobs.

`  ListModelMonitors  `

Lists ModelMonitors in a Location.

`  SearchModelMonitoringAlerts  `

Returns the Model Monitoring alerts.

`  SearchModelMonitoringStats  `

Searches Model Monitoring Stats generated within a given time window.

`  UpdateModelMonitor  `

Updates a ModelMonitor.

## `        google.cloud.aiplatform.v1beta1.ModelService       `

Methods

`  BatchImportEvaluatedAnnotations  `

Imports a list of externally generated EvaluatedAnnotations.

`  BatchImportModelEvaluationSlices  `

Imports a list of externally generated ModelEvaluationSlice.

`  CopyModel  `

Copies an already existing Agent Platform Model into the specified Location.

`  DeleteModel  `

Deletes a Model.

`  DeleteModelVersion  `

Deletes a Model version.

`  ExportModel  `

Exports a trained, exportable Model to a location specified by the user.

`  GetModel  `

Gets a Model.

`  GetModelEvaluation  `

Gets a ModelEvaluation.

`  GetModelEvaluationSlice  `

Gets a ModelEvaluationSlice.

`  ImportModelEvaluation  `

Imports an externally generated ModelEvaluation.

`  ListModelEvaluationSlices  `

Lists ModelEvaluationSlices in a ModelEvaluation.

`  ListModelEvaluations  `

Lists ModelEvaluations in a Model.

`  ListModelVersionCheckpoints  `

Lists checkpoints of the specified model version.

`  ListModelVersions  `

Lists versions of the specified model.

`  ListModels  `

Lists Models in a Location.

`  MergeVersionAliases  `

Merges a set of aliases for a Model version.

`  RecommendSpec  `

Gets a Model's spec recommendations.

`  UpdateExplanationDataset  `

Incrementally update the dataset used for an examples model.

`  UpdateModel  `

Updates a Model.

`  UploadModel  `

Uploads a Model artifact into Agent Platform.

## `        google.cloud.aiplatform.v1beta1.NotebookService       `

Methods

`  AssignNotebookRuntime  `

Assigns a NotebookRuntime to a user for a particular Notebook file.

`  CreateNotebookExecutionJob  `

Creates a NotebookExecutionJob.

`  CreateNotebookRuntimeTemplate  `

Creates a NotebookRuntimeTemplate.

`  DeleteNotebookExecutionJob  `

Deletes a NotebookExecutionJob.

`  DeleteNotebookRuntime  `

Deletes a NotebookRuntime.

`  DeleteNotebookRuntimeTemplate  `

Deletes a NotebookRuntimeTemplate.

`  GetNotebookExecutionJob  `

Gets a NotebookExecutionJob.

`  GetNotebookRuntime  `

Gets a NotebookRuntime.

`  GetNotebookRuntimeTemplate  `

Gets a NotebookRuntimeTemplate.

`  ListNotebookExecutionJobs  `

Lists NotebookExecutionJobs in a Location.

`  ListNotebookRuntimeTemplates  `

Lists NotebookRuntimeTemplates in a Location.

`  ListNotebookRuntimes  `

Lists NotebookRuntimes in a Location.

`  StartNotebookRuntime  `

Starts a NotebookRuntime.

`  StopNotebookRuntime  `

Stops a NotebookRuntime.

`  UpdateNotebookRuntimeTemplate  `

Updates a NotebookRuntimeTemplate.

`  UpgradeNotebookRuntime  `

Upgrades a NotebookRuntime.

## `        google.cloud.aiplatform.v1beta1.OnlineEvaluatorService       `

Methods

`  ActivateOnlineEvaluator  `

Activates an OnlineEvaluator.

`  CreateOnlineEvaluator  `

Creates an OnlineEvaluator in the given project and location.

`  DeleteOnlineEvaluator  `

Deletes an OnlineEvaluator.

`  GetOnlineEvaluator  `

Gets details of an OnlineEvaluator.

`  ListOnlineEvaluators  `

Lists the OnlineEvaluators for the given project and location.

`  SuspendOnlineEvaluator  `

Suspends an OnlineEvaluator.

`  UpdateOnlineEvaluator  `

Updates the fields of an OnlineEvaluator.

## `        google.cloud.aiplatform.v1beta1.PersistentResourceService       `

Methods

`  CreatePersistentResource  `

Creates a PersistentResource.

`  DeletePersistentResource  `

Deletes a PersistentResource.

`  GetPersistentResource  `

Gets a PersistentResource.

`  ListPersistentResources  `

Lists PersistentResources in a Location.

`  RebootPersistentResource  `

Reboots a PersistentResource.

`  UpdatePersistentResource  `

Updates a PersistentResource.

## `        google.cloud.aiplatform.v1beta1.PipelineService       `

Methods

`  BatchCancelPipelineJobs  `

Batch cancel PipelineJobs.

`  BatchDeletePipelineJobs  `

Batch deletes PipelineJobs The Operation is atomic.

`  CancelPipelineJob  `

Cancels a PipelineJob.

`  CancelTrainingPipeline  `

Cancels a TrainingPipeline.

`  CreatePipelineJob  `

Creates a PipelineJob.

`  CreateTrainingPipeline  `

Creates a TrainingPipeline.

`  DeletePipelineJob  `

Deletes a PipelineJob.

`  DeleteTrainingPipeline  `

Deletes a TrainingPipeline.

`  GetPipelineJob  `

Gets a PipelineJob.

`  GetTrainingPipeline  `

Gets a TrainingPipeline.

`  ListPipelineJobs  `

Lists PipelineJobs in a Location.

`  ListTrainingPipelines  `

Lists TrainingPipelines in a Location.

## `        google.cloud.aiplatform.v1beta1.PredictionService       `

Methods

`  ChatCompletions  `

Exposes an OpenAI-compatible endpoint for chat completions.

`  CountTokens  `

Perform a token counting.

`  DeleteResponse  `

Deletes the response from the endpoint.

`  DirectPredict  `

Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

`  DirectRawPredict  `

Perform an unary online prediction request to a gRPC model server for custom containers.

`  EmbedContent  `

Embed content with multimodal inputs.

`  Explain  `

Perform an online explanation.

`  GenerateContent  `

Generate content with multimodal inputs.

`  GetResponse  `

Gets the response from the endpoint.

`  Predict  `

Perform an online inference.

`  PredictLongRunning  `

`  RawPredict  `

Perform an online prediction with an arbitrary HTTP payload.

`  ServerStreamingPredict  `

Perform a server-side streaming online prediction request for Vertex LLM streaming.

`  StreamDirectPredict  `

Perform a streaming online prediction request to a gRPC model server for Vertex first-party products and frameworks.

`  StreamDirectRawPredict  `

Perform a streaming online prediction request to a gRPC model server for custom containers.

`  StreamGenerateContent  `

Generate content with multimodal inputs with streaming support.

`  StreamRawPredict  `

Perform a streaming online prediction with an arbitrary HTTP payload.

`  StreamingPredict  `

Perform a streaming online prediction request for Vertex first-party products and frameworks.

`  StreamingRawPredict  `

Perform a streaming online prediction request through gRPC.

## `        google.cloud.aiplatform.v1beta1.ReasoningEngineExecutionService       `

Methods

`  AsyncQueryReasoningEngine  `

Async query using a reasoning engine.

`  BidiInvokeReasoningEngine  `

Invokes reasoning engine with arbitrary WebSocket requests for bidi streaming

`  CancelAsyncQueryReasoningEngine  `

Cancels an AsyncQueryReasoningEngine operation.

`  InvokeReasoningEngine  `

Invokes reasoning engine with arbitrary HTTP requests for both unary and server-side streaming cases.

`  QueryReasoningEngine  `

Queries using a reasoning engine.

`  StreamQueryReasoningEngine  `

Streams queries using a reasoning engine.

## `        google.cloud.aiplatform.v1beta1.ReasoningEngineRuntimeRevisionService       `

Methods

`  DeleteReasoningEngineRuntimeRevision  `

Deletes a reasoning engine revision.

`  GetReasoningEngineRuntimeRevision  `

Gets a reasoning engine runtime revision.

`  ListReasoningEngineRuntimeRevisions  `

Lists runtime revisions in a reasoning engine.

## `        google.cloud.aiplatform.v1beta1.ReasoningEngineService       `

Methods

`  CreateReasoningEngine  `

Creates a reasoning engine.

`  DeleteReasoningEngine  `

Deletes a reasoning engine.

`  GetReasoningEngine  `

Gets a reasoning engine.

`  ListReasoningEngines  `

Lists reasoning engines in a location.

`  UpdateReasoningEngine  `

Updates a reasoning engine.

## `        google.cloud.aiplatform.v1beta1.ScheduleService       `

Methods

`  CreateSchedule  `

Creates a Schedule.

`  DeleteSchedule  `

Deletes a Schedule.

`  GetSchedule  `

Gets a Schedule.

`  ListSchedules  `

Lists Schedules in a Location.

`  PauseSchedule  `

Pauses a Schedule.

`  ResumeSchedule  `

Resumes a paused Schedule to start scheduling new runs.

`  UpdateSchedule  `

Updates an active or paused Schedule.

## `        google.cloud.aiplatform.v1beta1.SessionService       `

Methods

`  AppendEvent  `

Appends an event to a given session.

`  CreateSession  `

Creates a new `  Session  ` .

`  DeleteSession  `

Deletes details of the specific `  Session  ` .

`  GetSession  `

Gets details of the specific `  Session  ` .

`  ListEvents  `

Lists `  Events  ` in a given session.

`  ListSessions  `

Lists `  Sessions  ` in a given reasoning engine.

`  UpdateSession  `

Updates the specific `  Session  ` .

## `        google.cloud.aiplatform.v1beta1.SkillRegistryService       `

Methods

`  CreateSkill  `

Create a Skill.

`  DeleteSkill  `

Delete a Skill.

`  GetSkill  `

Get a Skill.

`  GetSkillRevision  `

Get a Skill Revision.

`  ListSkillRevisions  `

List Skill Revisions for a Skill.

`  ListSkills  `

List Skills.

`  RetrieveSkills  `

Retrieves skills.

`  UpdateSkill  `

Update a Skill.

## `        google.cloud.aiplatform.v1beta1.SpecialistPoolService       `

Methods

`  CreateSpecialistPool  `

Creates a SpecialistPool.

`  DeleteSpecialistPool  `

Deletes a SpecialistPool as well as all Specialists in the pool.

`  GetSpecialistPool  `

Gets a SpecialistPool.

`  ListSpecialistPools  `

Lists SpecialistPools in a Location.

`  UpdateSpecialistPool  `

Updates a SpecialistPool.

## `        google.cloud.aiplatform.v1beta1.TensorboardService       `

Methods

`  BatchCreateTensorboardRuns  `

Batch create TensorboardRuns.

`  BatchCreateTensorboardTimeSeries  `

Batch create TensorboardTimeSeries that belong to a TensorboardExperiment.

`  BatchReadTensorboardTimeSeriesData  `

Reads multiple TensorboardTimeSeries' data.

`  CreateTensorboard  `

Creates a Tensorboard.

`  CreateTensorboardExperiment  `

Creates a TensorboardExperiment.

`  CreateTensorboardRun  `

Creates a TensorboardRun.

`  CreateTensorboardTimeSeries  `

Creates a TensorboardTimeSeries.

`  DeleteTensorboard  `

Deletes a Tensorboard.

`  DeleteTensorboardExperiment  `

Deletes a TensorboardExperiment.

`  DeleteTensorboardRun  `

Deletes a TensorboardRun.

`  DeleteTensorboardTimeSeries  `

Deletes a TensorboardTimeSeries.

`  ExportTensorboardTimeSeriesData  `

Exports a TensorboardTimeSeries' data.

`  GetTensorboard  `

Gets a Tensorboard.

`  GetTensorboardExperiment  `

Gets a TensorboardExperiment.

`  GetTensorboardRun  `

Gets a TensorboardRun.

`  GetTensorboardTimeSeries  `

Gets a TensorboardTimeSeries.

`  ListTensorboardExperiments  `

Lists TensorboardExperiments in a Location.

`  ListTensorboardRuns  `

Lists TensorboardRuns in a Location.

`  ListTensorboardTimeSeries  `

Lists TensorboardTimeSeries in a Location.

`  ListTensorboards  `

Lists Tensorboards in a Location.

`  ReadTensorboardBlobData  `

Gets bytes of TensorboardBlobs.

`  ReadTensorboardSize  `

Returns the storage size for a given TensorBoard instance.

`  ReadTensorboardTimeSeriesData  `

Reads a TensorboardTimeSeries' data.

`  ReadTensorboardUsage  `

Returns a list of monthly active users for a given TensorBoard instance.

`  UpdateTensorboard  `

Updates a Tensorboard.

`  UpdateTensorboardExperiment  `

Updates a TensorboardExperiment.

`  UpdateTensorboardRun  `

Updates a TensorboardRun.

`  UpdateTensorboardTimeSeries  `

Updates a TensorboardTimeSeries.

`  WriteTensorboardExperimentData  `

Write time series data points of multiple TensorboardTimeSeries in multiple TensorboardRun's.

`  WriteTensorboardRunData  `

Write time series data points into multiple TensorboardTimeSeries under a TensorboardRun.

## `        google.cloud.aiplatform.v1beta1.VertexRagDataService       `

Methods

`  BatchCreateRagDataSchemas  `

Batch Create one or more RagDataSchemas

`  BatchCreateRagMetadata  `

Batch Create one or more RagMetadatas

`  BatchDeleteRagDataSchemas  `

Batch Deletes one or more RagDataSchemas

`  BatchDeleteRagMetadata  `

Batch Deletes one or more RagMetadata.

`  CreateRagCorpus  `

Creates a RagCorpus.

`  CreateRagDataSchema  `

Creates a RagDataSchema.

`  CreateRagMetadata  `

Creates a RagMetadata.

`  DeleteRagCorpus  `

Deletes a RagCorpus.

`  DeleteRagDataSchema  `

Deletes a RagDataSchema.

`  DeleteRagFile  `

Deletes a RagFile.

`  DeleteRagMetadata  `

Deletes a RagMetadata.

`  GetRagCorpus  `

Gets a RagCorpus.

`  GetRagDataSchema  `

Gets a RagDataSchema.

`  GetRagEngineConfig  `

Gets a RagEngineConfig.

`  GetRagFile  `

Gets a RagFile.

`  GetRagMetadata  `

Gets a RagMetadata.

`  ImportRagFiles  `

Import files from Google Cloud Storage or Google Drive into a RagCorpus.

`  ListRagCorpora  `

Lists RagCorpora in a Location.

`  ListRagDataSchemas  `

Lists RagDataSchemas in a Location.

`  ListRagFiles  `

Lists RagFiles in a RagCorpus.

`  ListRagMetadata  `

Lists RagMetadata in a RagFile.

`  UpdateRagCorpus  `

Updates a RagCorpus.

`  UpdateRagEngineConfig  `

Updates a RagEngineConfig.

`  UpdateRagMetadata  `

Updates a RagMetadata.

## `        google.cloud.aiplatform.v1beta1.VertexRagService       `

Methods

`  AskContexts  `

Agentic Retrieval Ask API for RAG.

`  AsyncRetrieveContexts  `

Asynchronous API to retrieves relevant contexts for a query.

`  AugmentPrompt  `

Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

`  CorroborateContent  `

Given an input text, it returns a score that evaluates the factuality of the text.

`  RetrieveContexts  `

Retrieves relevant contexts for a query.

## `        google.cloud.aiplatform.v1beta1.VizierService       `

Methods

`  AddTrialMeasurement  `

Adds a measurement of the objective metrics to a Trial.

`  CheckTrialEarlyStoppingState  `

Checks whether a Trial should stop or not.

`  CompleteTrial  `

Marks a Trial as complete.

`  CreateStudy  `

Creates a Study.

`  CreateTrial  `

Adds a user provided Trial to a Study.

`  DeleteStudy  `

Deletes a Study.

`  DeleteTrial  `

Deletes a Trial.

`  GetStudy  `

Gets a Study by name.

`  GetTrial  `

Gets a Trial.

`  ListOptimalTrials  `

Lists the pareto-optimal Trials for multi-objective Study or the optimal Trials for single-objective Study.

`  ListStudies  `

Lists all the studies in a region for an associated project.

`  ListTrials  `

Lists the Trials associated with a Study.

`  LookupStudy  `

Looks a study up using the user-defined display\_name field instead of the fully qualified resource name.

`  StopTrial  `

Stops a Trial.

`  SuggestTrials  `

Adds one or more Trials to a Study, with parameter values suggested by Agent Platform Vizier.

## `        google.iam.v1.IAMPolicy       `

Methods

`  GetIamPolicy  `

Gets the access control policy for a resource.

`  SetIamPolicy  `

Sets the access control policy on the specified resource.

`  TestIamPermissions  `

Returns permissions that a caller has on the specified resource.

## `        google.longrunning.Operations       `

Methods

`  CancelOperation  `

Starts asynchronous cancellation on a long-running operation.

`  DeleteOperation  `

Deletes a long-running operation.

`  GetOperation  `

Gets the latest state of a long-running operation.

`  ListOperations  `

Lists operations that match the specified filter in the request.

`  WaitOperation  `

Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.
