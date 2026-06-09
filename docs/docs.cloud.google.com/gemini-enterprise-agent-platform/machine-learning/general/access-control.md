---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control
title: Agent Platform access control with IAM
description: Control access to Agent Platform resources with IAM.
data_source: docs.cloud.google.com
---

This page describes how to use [Identity and Access Management (IAM)](https://docs.cloud.google.com/iam) to manage access to Gemini Enterprise Agent Platform resources. To manage access to Vertex AI Workbench instances, see [Vertex AI Workbench instances access control](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam) .

## Overview

Agent Platform uses IAM to manage access to resources. When you plan access control for your resources, consider the following:

  - You can manage access at the project level or resource level. Project-level access applies to all of the resources in that project. Access to a specific resource only applies to that resource. See [Project-level versus resource-level access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#resource-policy) .

  - You grant access by assigning IAM roles to principals. Predefined roles are available to make it easier to set up access, but custom roles are recommended because you create them, so you can limit their access to only the permissions that are required. See [IAM roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#roles) .

<span id="project-roles"></span>

## IAM roles

There are different types of IAM roles that can be used in Agent Platform:

  - [Custom roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#custom-roles) let you choose a specific set of permissions, create your own role with those permissions, and grant the role to users in your organization.

  - [Predefined roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) let you grant a set of related permissions to your Agent Platform resources at the project level.

  - [Basic roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#basic-roles) (Owner, Editor, and Viewer) provide access control to your Agent Platform resources at the project level, and are common to all Google Cloud services.

To add, update, or remove these roles in your Agent Platform project, see the documentation on [granting, changing, and revoking access](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Custom roles

Custom roles let you choose a specific set of permissions, create your own role with those permissions, and grant the role to users in your organization. For more information, see [Understanding IAM custom roles](https://docs.cloud.google.com/iam/docs/roles-overview#custom) .

### Use custom roles to grant least-privilege permissions

Predefined roles often contain more permissions than you need. You can create custom roles to grant your principals only the specific permissions that are required.

For example, you can create a custom role with the `aiplatform.endpoints.predict` permission, and then assign the role to a service account on an endpoint. This grants the service account the ability to call the endpoint for predictions, but not the ability of controlling the endpoint.

> **Note:** When using custom roles, granting the `aiplatform.endpoints.deploy` permission might allow a user to export other deployed or deployable models from the project. If you want to grant the ability to deploy specific models but not others, we recommend using separate projects.

### Predefined roles for Agent Platform

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><h4 id="aiplatform.admin" class="role-title add-link" data-text="Agent Platform Administrator" tabindex="-1">Agent Platform Administrator</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.admin</code> )</p>
<p>Grants full access to all resources in Agent Platform.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotationSpecs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.cacheConfigs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cacheConfigs.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.consents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.consents.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextArtifactsAndExecutions</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextChildren</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  queryDeployedModels</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeviceDebugInfo.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.explain</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  endpoints.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></li>
<li><code dir="ltr" translate="no">aiplatform.  endpoints.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.endpoints.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  readExample</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  writeExample</code></li>
<li><code dir="ltr" translate="no">aiplatform.  executions.  addExecutionEvents</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  executions.  queryExecutionInputsAndOutputs</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  directWrite</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.featurestores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.featurestores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.humanInTheLoops.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  queryAnnotationStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  send</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  migratableResources.  migrate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  migratableResources.  search</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  pause</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  resume</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  searchStatsAnomalies</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  exportEvaluatedDataItems</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringAlerts</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.upload</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasTrialDetails.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  nasTrialDetails.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.operations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  split</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.upload</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  query</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.run</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.specialistPools.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  write</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  write</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboards.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboards.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboards.  recordAccess</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboards.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  optimizePrompt</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  validateReinforcementTuningReward</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  vertexTune</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.editor" class="role-title add-link" data-text="Aiplatform Editor" tabindex="-1">Aiplatform Editor</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.editor</code> )</p>
<p>Editor role for aiplatform</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.agentExamples.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.agents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.agents.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotationSpecs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotationSpecs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.annotations.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.apps.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.apps.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.artifacts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.artifacts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.cacheConfigs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.cacheConfigs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cacheConfigs.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.cachedContents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.consents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.consents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.consents.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.contexts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextArtifactsAndExecutions</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextChildren</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.customJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.customJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.dataItems.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataLabelingJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasetVersions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.datasets.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  queryDeployedModels</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeviceDebugInfo.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.edgeDevices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.endpoints.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.explain</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  endpoints.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.undeploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationSets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.exampleStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  readExample</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  writeExample</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.executions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  executions.  addExecutionEvents</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  executions.  queryExecutionInputsAndOutputs</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.extensions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.extensions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViews.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  directWrite</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.humanInTheLoops.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.humanInTheLoops.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  queryAnnotationStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  send</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.indexes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataSchemas.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  migratableResources.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  migratableResources.  migrate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  migratableResources.  search</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  pause</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  resume</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  searchStatsAnomalies</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelEvaluations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  exportEvaluatedDataItems</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringAlerts</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.models.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.models.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasTrialDetails.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasTrialDetails.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  nasTrialDetails.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.onlineEvaluators.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  persistentResources.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  split</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.ragEngineConfigs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  query</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.sessions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.run</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.specialistPools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.specialistPools.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.studies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.studies.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboardRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.trainingPipelines.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.trials.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.trials.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  optimizePrompt</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  validateReinforcementTuningReward</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  vertexTune</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.expressUser" class="role-title add-link" data-text="Agent Platform Express User Beta" tabindex="-1">Agent Platform Express User <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.expressUser</code> )</p>
<p>Grants user access to Agent Platform Express.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.datasetVersions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasets.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.update</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.user" class="role-title add-link" data-text="Agent Platform User" tabindex="-1">Agent Platform User</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.user</code> )</p>
<p>Grants access to use all resource in Agent Platform.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.agentExamples.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.agents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.agents.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotationSpecs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotationSpecs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.annotations.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.apps.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.apps.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.artifacts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.artifacts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.cacheConfigs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.cachedContents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.consents.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.contexts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextArtifactsAndExecutions</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextChildren</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.customJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.customJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.dataItems.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataLabelingJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasetVersions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.datasets.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  queryDeployedModels</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeviceDebugInfo.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.edgeDevices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.endpoints.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.explain</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.undeploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationSets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.exampleStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  readExample</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  writeExample</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.executions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  executions.  addExecutionEvents</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  executions.  queryExecutionInputsAndOutputs</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.extensions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.extensions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViews.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  directWrite</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.humanInTheLoops.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.humanInTheLoops.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  queryAnnotationStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  send</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.indexes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataSchemas.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  pause</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  resume</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  searchStatsAnomalies</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelEvaluations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  exportEvaluatedDataItems</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringAlerts</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.models.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.models.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasTrialDetails.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasTrialDetails.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  nasTrialDetails.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.onlineEvaluators.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  query</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.sessions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.run</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.specialistPools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.specialistPools.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.studies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.studies.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboardRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.trainingPipelines.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.trials.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.trials.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  optimizePrompt</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  validateReinforcementTuningReward</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  vertexTune</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.viewer" class="role-title add-link" data-text="Agent Platform Viewer" tabindex="-1">Agent Platform Viewer</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.viewer</code> )</p>
<p>Grants access to view all resource in Agent Platform.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.agentExamples.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.agentExamples.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.agents.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.agents.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.annotationSpecs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.annotations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.annotations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.apps.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.apps.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.artifacts.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.artifacts.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.cacheConfigs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.cachedContents.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.cachedContents.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.consents.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.contexts.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.contexts.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></p>
<p><code dir="ltr" translate="no">aiplatform.customJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.customJobs.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.dataItems.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.dataItems.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  queryDeployedModels</code></p>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeviceDebugInfo.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.edgeDevices.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.edgeDevices.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.evaluationItems.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationItems.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.evaluationSets.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.evaluationSets.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.exampleStores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.exampleStores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  exampleStores.  readExample</code></p>
<p><code dir="ltr" translate="no">aiplatform.executions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.executions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  executions.  queryExecutionInputsAndOutputs</code></p>
<p><code dir="ltr" translate="no">aiplatform.extensions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.extensions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.humanInTheLoops.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></p>
<p><code dir="ltr" translate="no">aiplatform.indexes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.indexes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.locations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  searchStatsAnomalies</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.modelMonitors.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.modelMonitors.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringAlerts</code></p>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringStats</code></p>
<p><code dir="ltr" translate="no">aiplatform.models.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.models.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.nasJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.nasJobs.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.nasTrialDetails.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasTrialDetails.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  nasTrialDetails.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.specialistPools.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  specialistPools.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  specialistPools.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.studies.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.studies.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.trials.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.trials.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.colabEnterpriseAdmin" class="role-title add-link" data-text="Colab Enterprise Admin" tabindex="-1">Colab Enterprise Admin</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.colabEnterpriseAdmin</code> )</p>
<p>Admin role of using colab enterprise.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">dataform.*</code></p>
<ul>
<li><code dir="ltr" translate="no">dataform.commentThreads.create</code></li>
<li><code dir="ltr" translate="no">dataform.commentThreads.delete</code></li>
<li><code dir="ltr" translate="no">dataform.commentThreads.get</code></li>
<li><code dir="ltr" translate="no">dataform.commentThreads.list</code></li>
<li><code dir="ltr" translate="no">dataform.commentThreads.update</code></li>
<li><code dir="ltr" translate="no">dataform.comments.create</code></li>
<li><code dir="ltr" translate="no">dataform.comments.delete</code></li>
<li><code dir="ltr" translate="no">dataform.comments.get</code></li>
<li><code dir="ltr" translate="no">dataform.comments.list</code></li>
<li><code dir="ltr" translate="no">dataform.comments.update</code></li>
<li><code dir="ltr" translate="no">dataform.  compilationResults.  create</code></li>
<li><code dir="ltr" translate="no">dataform.  compilationResults.  get</code></li>
<li><code dir="ltr" translate="no">dataform.  compilationResults.  list</code></li>
<li><code dir="ltr" translate="no">dataform.  compilationResults.  query</code></li>
<li><code dir="ltr" translate="no">dataform.config.get</code></li>
<li><code dir="ltr" translate="no">dataform.config.update</code></li>
<li><code dir="ltr" translate="no">dataform.folders.addContents</code></li>
<li><code dir="ltr" translate="no">dataform.folders.create</code></li>
<li><code dir="ltr" translate="no">dataform.folders.delete</code></li>
<li><code dir="ltr" translate="no">dataform.folders.deleteTree</code></li>
<li><code dir="ltr" translate="no">dataform.folders.get</code></li>
<li><code dir="ltr" translate="no">dataform.folders.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.folders.move</code></li>
<li><code dir="ltr" translate="no">dataform.folders.queryContents</code></li>
<li><code dir="ltr" translate="no">dataform.folders.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.folders.update</code></li>
<li><code dir="ltr" translate="no">dataform.locations.get</code></li>
<li><code dir="ltr" translate="no">dataform.locations.list</code></li>
<li><code dir="ltr" translate="no">dataform.operations.cancel</code></li>
<li><code dir="ltr" translate="no">dataform.operations.delete</code></li>
<li><code dir="ltr" translate="no">dataform.operations.get</code></li>
<li><code dir="ltr" translate="no">dataform.operations.list</code></li>
<li><code dir="ltr" translate="no">dataform.releaseConfigs.create</code></li>
<li><code dir="ltr" translate="no">dataform.releaseConfigs.delete</code></li>
<li><code dir="ltr" translate="no">dataform.releaseConfigs.get</code></li>
<li><code dir="ltr" translate="no">dataform.releaseConfigs.list</code></li>
<li><code dir="ltr" translate="no">dataform.releaseConfigs.update</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.commit</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  computeAccessTokenStatus</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.create</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.delete</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  fetchHistory</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  fetchRemoteBranches</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.get</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.list</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.move</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  queryDirectoryContents</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.readFile</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  scheduleRelease</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  scheduleWorkflow</code></li>
<li><code dir="ltr" translate="no">dataform.  repositories.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.repositories.update</code></li>
<li><code dir="ltr" translate="no">dataform.teamFolders.create</code></li>
<li><code dir="ltr" translate="no">dataform.teamFolders.delete</code></li>
<li><code dir="ltr" translate="no">dataform.  teamFolders.  deleteTree</code></li>
<li><code dir="ltr" translate="no">dataform.teamFolders.get</code></li>
<li><code dir="ltr" translate="no">dataform.  teamFolders.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.  teamFolders.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.teamFolders.update</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowConfigs.  create</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowConfigs.  delete</code></li>
<li><code dir="ltr" translate="no">dataform.workflowConfigs.get</code></li>
<li><code dir="ltr" translate="no">dataform.workflowConfigs.list</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowConfigs.  update</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowInvocations.  cancel</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowInvocations.  create</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowInvocations.  delete</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowInvocations.  get</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowInvocations.  list</code></li>
<li><code dir="ltr" translate="no">dataform.  workflowInvocations.  query</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.commit</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.create</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.delete</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  fetchFileDiff</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  fetchFileGitStatuses</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  fetchGitAheadBehind</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.get</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  installNpmPackages</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.list</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  makeDirectory</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  moveDirectory</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.moveFile</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.pull</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.push</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  queryDirectoryContents</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.readFile</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  removeDirectory</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.removeFile</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.reset</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  searchFiles</code></li>
<li><code dir="ltr" translate="no">dataform.  workspaces.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">dataform.workspaces.writeFile</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.colabEnterpriseUser" class="role-title add-link" data-text="Colab Enterprise User" tabindex="-1">Colab Enterprise User</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.colabEnterpriseUser</code> )</p>
<p>User role of using colab enterprise.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">dataform.commentThreads.get</code></p>
<p><code dir="ltr" translate="no">dataform.commentThreads.list</code></p>
<p><code dir="ltr" translate="no">dataform.comments.get</code></p>
<p><code dir="ltr" translate="no">dataform.comments.list</code></p>
<p><code dir="ltr" translate="no">dataform.folders.create</code></p>
<p><code dir="ltr" translate="no">dataform.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">dataform.locations.get</code></li>
<li><code dir="ltr" translate="no">dataform.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">dataform.repositories.create</code></p>
<p><code dir="ltr" translate="no">dataform.repositories.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.entityTypeOwner" class="role-title add-link" data-text="Agent Platform Feature Store EntityType owner" tabindex="-1">Agent Platform Feature Store EntityType owner</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.entityTypeOwner</code> )</p>
<p>Provides full access to all permissions for a particular entity type resource.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Entity type</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  setIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.expressAdmin" class="role-title add-link" data-text="Agent Platform Express Admin Beta" tabindex="-1">Agent Platform Express Admin <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.expressAdmin</code> )</p>
<p>Grants admin access to Agent Platform Express.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasetVersions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasets.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.datasets.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.update</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.featurestoreAdmin" class="role-title add-link" data-text="Agent Platform Feature Store Admin" tabindex="-1">Agent Platform Feature Store Admin</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.featurestoreAdmin</code> )</p>
<p>Grants full access to all resources in Agent Platform Feature Store.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Entity type</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.entityTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureGroups.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViews.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.featureViews.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  directWrite</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViews.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureViews.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featurestores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.featurestores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.featurestores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.featurestoreDataViewer" class="role-title add-link" data-text="Agent Platform Feature Store Data Viewer" tabindex="-1">Agent Platform Feature Store Data Viewer</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.featurestoreDataViewer</code> )</p>
<p>This role provides permissions to read Feature data.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Entity type</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.featurestoreDataWriter" class="role-title add-link" data-text="Agent Platform Feature Store Data Writer" tabindex="-1">Agent Platform Feature Store Data Writer</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.featurestoreDataWriter</code> )</p>
<p>This role provides permissions to read and write Feature data.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Entity type</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.featurestoreInstanceCreator" class="role-title add-link" data-text="Agent Platform Feature Store Instance Creator" tabindex="-1">Agent Platform Feature Store Instance Creator</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.featurestoreInstanceCreator</code> )</p>
<p>Administrator of Featurestore resources, but not the child resources under Featurestores.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Featurestore</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.featurestoreResourceViewer" class="role-title add-link" data-text="Agent Platform Feature Store Resource Viewer" tabindex="-1">Agent Platform Feature Store Resource Viewer</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.featurestoreResourceViewer</code> )</p>
<p>Viewer of all resources in Agent Platform Feature Store but cannot make changes.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Entity type</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.featurestoreUser" class="role-title add-link" data-text="Agent Platform Feature Store User Beta" tabindex="-1">Agent Platform Feature Store User <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.featurestoreUser</code> )</p>
<p>Deprecated. Use featurestoreAdmin instead.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.entityTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featurestores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.featurestores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.featurestores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.memoryEditor" class="role-title add-link" data-text="Agent Platform Memory Bank Editor Role" tabindex="-1">Agent Platform Memory Bank Editor Role</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.memoryEditor</code> )</p>
<p>Grants edit access to Agent Platform Memory Bank.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.memories.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.generate</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.memoryUser" class="role-title add-link" data-text="Agent Platform Memory Bank User Role" tabindex="-1">Agent Platform Memory Bank User Role</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.memoryUser</code> )</p>
<p>Grants full user access to Agent Platform Memory Bank.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.memoryViewer" class="role-title add-link" data-text="Agent Platform Memory Bank Viewer Role" tabindex="-1">Agent Platform Memory Bank Viewer Role</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.memoryViewer</code> )</p>
<p>Grants viewer access to Agent Platform Memory Bank.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.memories.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></p>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.migrator" class="role-title add-link" data-text="Agent Platform Migration Service User" tabindex="-1">Agent Platform Migration Service User</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.migrator</code> )</p>
<p>Grants access to use migration service in Agent Platform</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  migratableResources.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  migratableResources.  migrate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  migratableResources.  search</code></li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.notebookExecutorUser" class="role-title add-link" data-text="Notebook Executor User Beta" tabindex="-1">Notebook Executor User <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.notebookExecutorUser</code> )</p>
<p>Grants users full access to schedules and notebook execution jobs.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.notebookRuntimeAdmin" class="role-title add-link" data-text="Notebook Runtime Admin" tabindex="-1">Notebook Runtime Admin</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.notebookRuntimeAdmin</code> )</p>
<p>Grants full access to all runtime templates and runtimes in Notebook Service.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.notebookRuntimeUser" class="role-title add-link" data-text="Notebook Runtime User" tabindex="-1">Notebook Runtime User</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.notebookRuntimeUser</code> )</p>
<p>Grants users permissions to create runtime resources using a runtime template and manage the runtime resources they created.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.provisionedThroughputAdmin" class="role-title add-link" data-text="Vertex AI Platform Provisioned Throughput Admin Beta" tabindex="-1">Vertex AI Platform Provisioned Throughput Admin <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.provisionedThroughputAdmin</code> )</p>
<p>Grants access to use all resources related to Vertex AI Provisioned Throughput</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  split</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.publisherProvisionedThroughputAdmin" class="role-title add-link" data-text="Vertex AI Platform Publisher Provisioned Throughput Admin Beta" tabindex="-1">Vertex AI Platform Publisher Provisioned Throughput Admin <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.publisherProvisionedThroughputAdmin</code> )</p>
<p>Grants Publisher access to use all resources related to Vertex AI Provisioned Throughput Orders</p></td>
<td></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.publisherProvisionedThroughputViewer" class="role-title add-link" data-text="Vertex AI Platform Publisher Provisioned Throughput Viewer Beta" tabindex="-1">Vertex AI Platform Publisher Provisioned Throughput Viewer <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.publisherProvisionedThroughputViewer</code> )</p>
<p>Grants Publisher access to view all resources related to Vertex AI Provisioned Throughput Orders</p></td>
<td></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.sessionEditor" class="role-title add-link" data-text="Agent Platform Sessions Editor Role" tabindex="-1">Agent Platform Sessions Editor Role</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.sessionEditor</code> )</p>
<p>Grants edit access to Agent Platform Sessions.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.update</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.sessionUser" class="role-title add-link" data-text="Agent Platform Sessions User Role" tabindex="-1">Agent Platform Sessions User Role</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.sessionUser</code> )</p>
<p>Grants full user access to Agent Platform Sessions.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.update</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.sessionViewer" class="role-title add-link" data-text="Agent Platform Sessions Viewer Role" tabindex="-1">Agent Platform Sessions Viewer Role</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.sessionViewer</code> )</p>
<p>Grants viewer access to Agent Platform Sessions</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.tensorboardWebAppUser" class="role-title add-link" data-text="Agent Platform Tensorboard Web App User Beta" tabindex="-1">Agent Platform Tensorboard Web App User <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.tensorboardWebAppUser</code> )</p>
<p>Grants access to the Vertex AI TensorBoard web app.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  tensorboards.  recordAccess</code></p></td>
</tr>
</tbody>
</table>

### Service agent roles

Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><h4 id="aiplatform.agentSandboxServiceAgent" class="role-title add-link" data-text="Vertex AI Agent Sandbox Service Agent" tabindex="-1">Vertex AI Agent Sandbox Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.agentSandboxServiceAgent</code> )</p>
<p>Vertex AI Service Agent used to access Agent Sandbox managed resources in consumer project with restricted permissions.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">artifactregistry.  repositories.  downloadArtifacts</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.objects.create</code></p>
<p><code dir="ltr" translate="no">storage.objects.delete</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.batchPredictionServiceAgent" class="role-title add-link" data-text="Vertex AI Batch Prediction Service Agent" tabindex="-1">Vertex AI Batch Prediction Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.batchPredictionServiceAgent</code> )</p>
<p>Vertex AI Batch Prediction Service Agent for serving batch prediction requests.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">bigquery.datasets.create</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.get</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.create</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.models.create</code></p>
<p><code dir="ltr" translate="no">bigquery.models.export</code></p>
<p><code dir="ltr" translate="no">bigquery.models.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.create</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.create</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.createSnapshot</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.deleteSnapshot</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.export</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.  tables.  restoreSnapshot</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.update</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.updateData</code></p>
<p><code dir="ltr" translate="no">storage.buckets.create</code></p>
<p><code dir="ltr" translate="no">storage.buckets.delete</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.buckets.update</code></p>
<p><code dir="ltr" translate="no">storage.objects.create</code></p>
<p><code dir="ltr" translate="no">storage.objects.delete</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.update</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.colabServiceAgent" class="role-title add-link" data-text="Vertex AI Colab Service Agent" tabindex="-1">Vertex AI Colab Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.colabServiceAgent</code> )</p>
<p>Gives Vertex AI Colab the proper permissions to function.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></p>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.addresses.use</code></p>
<p><code dir="ltr" translate="no">compute.addresses.useInternal</code></p>
<p><code dir="ltr" translate="no">compute.disks.create</code></p>
<p><code dir="ltr" translate="no">compute.disks.createSnapshot</code></p>
<p><code dir="ltr" translate="no">compute.disks.createTagBinding</code></p>
<p><code dir="ltr" translate="no">compute.disks.delete</code></p>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.setLabels</code></p>
<p><code dir="ltr" translate="no">compute.disks.use</code></p>
<p><code dir="ltr" translate="no">compute.disks.useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.instances.attachDisk</code></p>
<p><code dir="ltr" translate="no">compute.instances.create</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  createTagBinding</code></p>
<p><code dir="ltr" translate="no">compute.instances.delete</code></p>
<p><code dir="ltr" translate="no">compute.instances.detachDisk</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.reset</code></p>
<p><code dir="ltr" translate="no">compute.instances.setLabels</code></p>
<p><code dir="ltr" translate="no">compute.instances.setMetadata</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  setServiceAccount</code></p>
<p><code dir="ltr" translate="no">compute.instances.setTags</code></p>
<p><code dir="ltr" translate="no">compute.instances.start</code></p>
<p><code dir="ltr" translate="no">compute.instances.stop</code></p>
<p><code dir="ltr" translate="no">compute.instances.useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.networks.use</code></p>
<p><code dir="ltr" translate="no">compute.networks.useExternalIp</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.create</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.delete</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.use</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  useExternalIp</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.actAs</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.create</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.get</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.customCodeServiceAgent" class="role-title add-link" data-text="Vertex AI Custom Code Service Agent" tabindex="-1">Vertex AI Custom Code Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.customCodeServiceAgent</code> )</p>
<p>Gives Vertex AI Custom Code the proper permissions. The aiplatform.customJobs.create IAM permission is highly privileged. Through Vertex AI Custom Training jobs, it effectively grants editor-level access to other services activated for the consumer project, such as GCS and BigQuery.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.agentExamples.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.agents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.agents.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotationSpecs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotationSpecs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.annotations.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.apps.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.apps.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.artifacts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.artifacts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.cacheConfigs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.cachedContents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.consents.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.contexts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextArtifactsAndExecutions</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextChildren</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.customJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.customJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.dataItems.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataLabelingJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasetVersions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.datasets.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  queryDeployedModels</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeviceDebugInfo.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.edgeDevices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.endpoints.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.explain</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.undeploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationSets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.exampleStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  readExample</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  writeExample</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.executions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  executions.  addExecutionEvents</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  executions.  queryExecutionInputsAndOutputs</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.extensions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.extensions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViews.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  directWrite</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.humanInTheLoops.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.humanInTheLoops.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  queryAnnotationStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  send</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.indexes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataSchemas.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  pause</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  resume</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  searchStatsAnomalies</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelEvaluations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  exportEvaluatedDataItems</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringAlerts</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.models.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.models.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasTrialDetails.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasTrialDetails.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  nasTrialDetails.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.onlineEvaluators.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  query</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.sessions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.run</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.specialistPools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.specialistPools.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.studies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.studies.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboardRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.trainingPipelines.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.trials.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.trials.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  optimizePrompt</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  validateReinforcementTuningReward</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  vertexTune</code></li>
</ul>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  downloadArtifacts</code></p>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  get</code></p>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  list</code></p>
<p><code dir="ltr" translate="no">artifactregistry.tags.get</code></p>
<p><code dir="ltr" translate="no">artifactregistry.versions.get</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.create</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.get</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.create</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.create</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.create</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.export</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.update</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.updateData</code></p>
<p><code dir="ltr" translate="no">cloudtrace.traces.list</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.get</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getAccessToken</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getOpenIdToken</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  implicitDelegation</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.list</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.signBlob</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.signJwt</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">logging.views.access</code></p>
<p><code dir="ltr" translate="no">logging.views.get</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  create</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  get</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  list</code></p>
<p><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  get</code></li>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">monitoring.timeSeries.create</code></p>
<p><code dir="ltr" translate="no">observability.views.access</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">servicemanagement.  services.  report</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.buckets.create</code></p>
<p><code dir="ltr" translate="no">storage.buckets.delete</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.create</code></p>
<p><code dir="ltr" translate="no">storage.objects.delete</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.update</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.extensionCustomCodeServiceAgent" class="role-title add-link" data-text="Vertex AI Extension Custom Code Service Agent" tabindex="-1">Vertex AI Extension Custom Code Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.extensionCustomCodeServiceAgent</code> )</p>
<p>Gives Vertex AI Extension that executes custom code the permissions it needs to function.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">monitoring.timeSeries.create</code></p>
<p><code dir="ltr" translate="no">orgpolicy.policy.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">storage.folders.*</code></p>
<ul>
<li><code dir="ltr" translate="no">storage.folders.create</code></li>
<li><code dir="ltr" translate="no">storage.folders.delete</code></li>
<li><code dir="ltr" translate="no">storage.folders.get</code></li>
<li><code dir="ltr" translate="no">storage.folders.list</code></li>
<li><code dir="ltr" translate="no">storage.folders.rename</code></li>
</ul>
<p><code dir="ltr" translate="no">storage.managedFolders.create</code></p>
<p><code dir="ltr" translate="no">storage.managedFolders.delete</code></p>
<p><code dir="ltr" translate="no">storage.managedFolders.get</code></p>
<p><code dir="ltr" translate="no">storage.managedFolders.list</code></p>
<p><code dir="ltr" translate="no">storage.multipartUploads.*</code></p>
<ul>
<li><code dir="ltr" translate="no">storage.multipartUploads.abort</code></li>
<li><code dir="ltr" translate="no">storage.  multipartUploads.  create</code></li>
<li><code dir="ltr" translate="no">storage.multipartUploads.list</code></li>
<li><code dir="ltr" translate="no">storage.  multipartUploads.  listParts</code></li>
</ul>
<p><code dir="ltr" translate="no">storage.objects.*</code></p>
<ul>
<li><code dir="ltr" translate="no">storage.objects.create</code></li>
<li><code dir="ltr" translate="no">storage.objects.createContext</code></li>
<li><code dir="ltr" translate="no">storage.objects.delete</code></li>
<li><code dir="ltr" translate="no">storage.objects.deleteContext</code></li>
<li><code dir="ltr" translate="no">storage.objects.get</code></li>
<li><code dir="ltr" translate="no">storage.objects.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">storage.objects.list</code></li>
<li><code dir="ltr" translate="no">storage.objects.move</code></li>
<li><code dir="ltr" translate="no">storage.  objects.  overrideUnlockedRetention</code></li>
<li><code dir="ltr" translate="no">storage.objects.restore</code></li>
<li><code dir="ltr" translate="no">storage.objects.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">storage.objects.setRetention</code></li>
<li><code dir="ltr" translate="no">storage.objects.update</code></li>
<li><code dir="ltr" translate="no">storage.objects.updateContext</code></li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.extensionServiceAgent" class="role-title add-link" data-text="Vertex AI Extension Service Agent" tabindex="-1">Vertex AI Extension Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.extensionServiceAgent</code> )</p>
<p>Gives Vertex AI Extension the permissions it needs to function.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></p>
<p><code dir="ltr" translate="no">discoveryengine.  servingConfigs.  search</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getAccessToken</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getOpenIdToken</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.modelMonitoringServiceAgent" class="role-title add-link" data-text="Vertex AI Model Monitoring Service Agent" tabindex="-1">Vertex AI Model Monitoring Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.modelMonitoringServiceAgent</code> )</p>
<p>Gives Vertex AI Model Monitoring the permissions it needs to function.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.create</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.get</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.create</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.create</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.export</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.update</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.updateData</code></p>
<p><code dir="ltr" translate="no">monitoring.  notificationChannels.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.buckets.create</code></p>
<p><code dir="ltr" translate="no">storage.buckets.delete</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.buckets.update</code></p>
<p><code dir="ltr" translate="no">storage.objects.create</code></p>
<p><code dir="ltr" translate="no">storage.objects.delete</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.update</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.notebookServiceAgent" class="role-title add-link" data-text="Vertex AI Notebook Service Agent" tabindex="-1">Vertex AI Notebook Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.notebookServiceAgent</code> )</p>
<p>Vertex AI Service Agent used to run Notebook managed resources in user project with restricted permissions.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  create</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  get</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  list</code></p>
<p><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  get</code></li>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">monitoring.timeSeries.create</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.onlinePredictionServiceAgent" class="role-title add-link" data-text="Vertex AI Online Prediction Service Agent" tabindex="-1">Vertex AI Online Prediction Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.onlinePredictionServiceAgent</code> )</p>
<p>Gives Vertex AI Online Prediction the permissions it needs to function.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">gkehub.features.get</code></p>
<p><code dir="ltr" translate="no">gkehub.features.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">gkehub.features.list</code></p>
<p><code dir="ltr" translate="no">gkehub.fleet.get</code></p>
<p><code dir="ltr" translate="no">gkehub.gateway.delete</code></p>
<p><code dir="ltr" translate="no">gkehub.  gateway.  generateCredentials</code></p>
<p><code dir="ltr" translate="no">gkehub.gateway.get</code></p>
<p><code dir="ltr" translate="no">gkehub.gateway.patch</code></p>
<p><code dir="ltr" translate="no">gkehub.gateway.post</code></p>
<p><code dir="ltr" translate="no">gkehub.gateway.put</code></p>
<p><code dir="ltr" translate="no">gkehub.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">gkehub.locations.get</code></li>
<li><code dir="ltr" translate="no">gkehub.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">gkehub.memberships.get</code></p>
<p><code dir="ltr" translate="no">gkehub.  memberships.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">gkehub.memberships.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.ragServiceAgent" class="role-title add-link" data-text="Vertex AI RAG Data Service Agent" tabindex="-1">Vertex AI RAG Data Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.ragServiceAgent</code> )</p>
<p>Vertex AI Service Agent used by Vertex RAG to access user imported data, Vertex AI, Document AI processors, and Vector Search in the project</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.indexes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.models.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.create</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.get</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.create</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.create</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.create</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.createSnapshot</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.deleteSnapshot</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.export</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.  tables.  restoreSnapshot</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.update</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.updateData</code></p>
<p><code dir="ltr" translate="no">documentai.  processorVersions.  processOnline</code></p>
<p><code dir="ltr" translate="no">documentai.processors.get</code></p>
<p><code dir="ltr" translate="no">documentai.  processors.  processOnline</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">vectorsearch.collections.*</code></p>
<ul>
<li><code dir="ltr" translate="no">vectorsearch.  collections.  create</code></li>
<li><code dir="ltr" translate="no">vectorsearch.  collections.  delete</code></li>
<li><code dir="ltr" translate="no">vectorsearch.collections.get</code></li>
<li><code dir="ltr" translate="no">vectorsearch.collections.list</code></li>
<li><code dir="ltr" translate="no">vectorsearch.  collections.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">vectorsearch.dataObjects.*</code></p>
<ul>
<li><code dir="ltr" translate="no">vectorsearch.  dataObjects.  create</code></li>
<li><code dir="ltr" translate="no">vectorsearch.  dataObjects.  delete</code></li>
<li><code dir="ltr" translate="no">vectorsearch.dataObjects.get</code></li>
<li><code dir="ltr" translate="no">vectorsearch.  dataObjects.  import</code></li>
<li><code dir="ltr" translate="no">vectorsearch.dataObjects.query</code></li>
<li><code dir="ltr" translate="no">vectorsearch.  dataObjects.  search</code></li>
<li><code dir="ltr" translate="no">vectorsearch.  dataObjects.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">vectorsearch.indexes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">vectorsearch.indexes.create</code></li>
<li><code dir="ltr" translate="no">vectorsearch.indexes.delete</code></li>
<li><code dir="ltr" translate="no">vectorsearch.indexes.get</code></li>
<li><code dir="ltr" translate="no">vectorsearch.indexes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">vectorsearch.operations.get</code></p>
<p><code dir="ltr" translate="no">vectorsearch.operations.list</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.rapidevalServiceAgent" class="role-title add-link" data-text="Vertex AI Rapid Eval Service Agent" tabindex="-1">Vertex AI Rapid Eval Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.rapidevalServiceAgent</code> )</p>
<p>Vertex AI Service Agent used by GenAI Rapid Evaluation Service to access publisher model endpoints in the user project</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.reasoningEngineServiceAgent" class="role-title add-link" data-text="Vertex AI Reasoning Engine Service Agent" tabindex="-1">Vertex AI Reasoning Engine Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.reasoningEngineServiceAgent</code> )</p>
<p>Gives Vertex AI Reasoning Engine the proper permissions to function. The aiplatform.reasoningEngines.create IAM permission implies read access to the GCS objects of the consumer project through this service agent.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.endpoints.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.explain</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.undeploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.sessions.update</code></p>
<p><code dir="ltr" translate="no">cloudapiregistry.*</code></p>
<ul>
<li><code dir="ltr" translate="no">cloudapiregistry.locations.get</code></li>
<li><code dir="ltr" translate="no">cloudapiregistry.  locations.  list</code></li>
<li><code dir="ltr" translate="no">cloudapiregistry.  mcpServers.  get</code></li>
<li><code dir="ltr" translate="no">cloudapiregistry.  mcpServers.  list</code></li>
<li><code dir="ltr" translate="no">cloudapiregistry.mcpTools.get</code></li>
<li><code dir="ltr" translate="no">cloudapiregistry.mcpTools.list</code></li>
</ul>
<p><code dir="ltr" translate="no">cloudtrace.traces.patch</code></p>
<p><code dir="ltr" translate="no">developerconnect.  connections.  get</code></p>
<p><code dir="ltr" translate="no">developerconnect.  gitRepositoryLinks.  fetchReadToken</code></p>
<p><code dir="ltr" translate="no">developerconnect.  gitRepositoryLinks.  get</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">modelarmor.callouts.invoke</code></p>
<p><code dir="ltr" translate="no">modelarmor.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">modelarmor.locations.get</code></li>
<li><code dir="ltr" translate="no">modelarmor.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">modelarmor.  templates.  useToSanitizeInput</code></p>
<p><code dir="ltr" translate="no">modelarmor.  templates.  useToSanitizeModelResponse</code></p>
<p><code dir="ltr" translate="no">modelarmor.  templates.  useToSanitizeOutput</code></p>
<p><code dir="ltr" translate="no">modelarmor.  templates.  useToSanitizeUserPrompt</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  create</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  get</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  list</code></p>
<p><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  get</code></li>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">monitoring.timeSeries.create</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">telemetry.traces.write</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.serviceAgent" class="role-title add-link" data-text="Vertex AI Service Agent" tabindex="-1">Vertex AI Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.serviceAgent</code> )</p>
<p>Gives Vertex AI the permissions it needs to function.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.agentExamples.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agentExamples.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  agentExamples.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.agents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.agents.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.agents.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotationSpecs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotationSpecs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  annotationSpecs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.annotations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.annotations.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.annotations.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.apps.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.apps.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.apps.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.artifacts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.artifacts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.cacheConfigs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.cachedContents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.cachedContents.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  cachedContents.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.consents.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.contexts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextArtifactsAndExecutions</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextChildren</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.customJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.customJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.customJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.dataItems.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.dataItems.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.dataLabelingJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  dataLabelingJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasetVersions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasetVersions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  datasetVersions.  restore</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.datasets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.datasets.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.datasets.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  queryDeployedModels</code></li>
<li><code dir="ltr" translate="no">aiplatform.  deploymentResourcePools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  edgeDeploymentJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  edgeDeviceDebugInfo.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.edgeDevices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.edgeDevices.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.endpoints.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.explain</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.undeploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  deleteFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  exportFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  importFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  readFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  streamingReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.entityTypes.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  entityTypes.  writeFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationExperiments.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationItems.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationItems.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationItems.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationRuns.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.evaluationSets.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.evaluationSets.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  evaluationSets.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.exampleStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.exampleStores.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  readExample</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  exampleStores.  writeExample</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.executions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  executions.  addExecutionEvents</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  executions.  queryExecutionInputsAndOutputs</code></li>
<li><code dir="ltr" translate="no">aiplatform.executions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.extensions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.extensions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.extensions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureGroups.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureGroups.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitorJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.featureMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureOnlineStores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViewSyncs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  featureViewSyncs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.featureViews.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  directWrite</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  fetchFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featureViews.  searchNearestEntities</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.sync</code></p>
<p><code dir="ltr" translate="no">aiplatform.featureViews.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.features.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.features.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.features.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  batchReadFeatureValues</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  exportFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  importFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.featurestores.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  readFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  featurestores.  writeFeatures</code></p>
<p><code dir="ltr" translate="no">aiplatform.humanInTheLoops.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.humanInTheLoops.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  queryAnnotationStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  send</code></li>
<li><code dir="ltr" translate="no">aiplatform.  humanInTheLoops.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  hyperparameterTuningJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexEndpoints.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  deploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexEndpoints.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  queryVectors</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  undeploy</code></li>
<li><code dir="ltr" translate="no">aiplatform.  indexEndpoints.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.indexes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.indexes.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.indexes.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memories.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memories.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.generate</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.retrieve</code></li>
<li><code dir="ltr" translate="no">aiplatform.memories.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.memoryRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.memoryRevisions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  memoryRevisions.  rollback</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataSchemas.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  pause</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  resume</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  searchStatsAnomalies</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelDeploymentMonitoringJobs.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluationSlices.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelEvaluations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  exportEvaluatedDataItems</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  import</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelEvaluations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitoringJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.modelMonitors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.modelMonitors.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringAlerts</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  searchModelMonitoringStats</code></li>
<li><code dir="ltr" translate="no">aiplatform.  modelMonitors.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.models.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.models.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.export</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.update</code></li>
<li><code dir="ltr" translate="no">aiplatform.models.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.nasJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.nasTrialDetails.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.nasTrialDetails.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  nasTrialDetails.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  apply</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimeTemplates.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  assign</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  start</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  upgrade</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.onlineEvaluators.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  onlineEvaluators.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  persistentResources.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  provisionedThroughputRevisions.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  provisionedThroughputs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragCorpora.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.query</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragCorpora.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  ragEngineConfigs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.ragFiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.import</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.ragFiles.upload</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  reasoningEngineRuntimeRevisions.  query</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  query</code></p>
<p><code dir="ltr" translate="no">aiplatform.  reasoningEngines.  update</code></p>
<p><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  execute</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  sandboxEnvironments.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicies.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  semanticGovernancePolicyEngine.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessionEvents.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  sessionEvents.  append</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessionEvents.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.sessions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.sessions.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.run</code></li>
<li><code dir="ltr" translate="no">aiplatform.sessions.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.specialistPools.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.specialistPools.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  specialistPools.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.studies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.studies.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.studies.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboardRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.trainingPipelines.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  trainingPipelines.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.trials.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.trials.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.trials.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.cancel</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  optimizePrompt</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  validateReinforcementTuningReward</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tuningJobs.  vertexTune</code></li>
</ul>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  create</code></p>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  downloadArtifacts</code></p>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  get</code></p>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  list</code></p>
<p><code dir="ltr" translate="no">artifactregistry.  repositories.  uploadArtifacts</code></p>
<p><code dir="ltr" translate="no">artifactregistry.tags.get</code></p>
<p><code dir="ltr" translate="no">artifactregistry.versions.get</code></p>
<p><code dir="ltr" translate="no">automl.datasets.export</code></p>
<p><code dir="ltr" translate="no">automl.datasets.get</code></p>
<p><code dir="ltr" translate="no">automl.datasets.list</code></p>
<p><code dir="ltr" translate="no">automl.modelEvaluations.list</code></p>
<p><code dir="ltr" translate="no">automl.models.get</code></p>
<p><code dir="ltr" translate="no">automl.models.list</code></p>
<p><code dir="ltr" translate="no">automl.operations.get</code></p>
<p><code dir="ltr" translate="no">automl.tableSpecs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.create</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.get</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.create</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.models.create</code></p>
<p><code dir="ltr" translate="no">bigquery.models.export</code></p>
<p><code dir="ltr" translate="no">bigquery.models.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.objectRefs.read</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.create</code></p>
<p><code dir="ltr" translate="no">bigquery.readsessions.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.create</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.export</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.list</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.update</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.updateData</code></p>
<p><code dir="ltr" translate="no">bigtable.tables.get</code></p>
<p><code dir="ltr" translate="no">bigtable.tables.list</code></p>
<p><code dir="ltr" translate="no">bigtable.tables.readRows</code></p>
<p><code dir="ltr" translate="no">binaryauthorization.  policy.  evaluatePolicy</code></p>
<p><code dir="ltr" translate="no">cloudtrace.traces.get</code></p>
<p><code dir="ltr" translate="no">cloudtrace.traces.list</code></p>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.addresses.use</code></p>
<p><code dir="ltr" translate="no">compute.addresses.useInternal</code></p>
<p><code dir="ltr" translate="no">compute.disks.create</code></p>
<p><code dir="ltr" translate="no">compute.disks.createSnapshot</code></p>
<p><code dir="ltr" translate="no">compute.disks.createTagBinding</code></p>
<p><code dir="ltr" translate="no">compute.disks.delete</code></p>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.setLabels</code></p>
<p><code dir="ltr" translate="no">compute.disks.use</code></p>
<p><code dir="ltr" translate="no">compute.disks.useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.instances.attachDisk</code></p>
<p><code dir="ltr" translate="no">compute.instances.create</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  createTagBinding</code></p>
<p><code dir="ltr" translate="no">compute.instances.delete</code></p>
<p><code dir="ltr" translate="no">compute.instances.detachDisk</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.list</code></p>
<p><code dir="ltr" translate="no">compute.instances.setLabels</code></p>
<p><code dir="ltr" translate="no">compute.instances.setMetadata</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  setServiceAccount</code></p>
<p><code dir="ltr" translate="no">compute.instances.setTags</code></p>
<p><code dir="ltr" translate="no">compute.instances.start</code></p>
<p><code dir="ltr" translate="no">compute.instances.stop</code></p>
<p><code dir="ltr" translate="no">compute.instances.update</code></p>
<p><code dir="ltr" translate="no">compute.instances.useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.get</code></p>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.networks.use</code></p>
<p><code dir="ltr" translate="no">compute.networks.useExternalIp</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.create</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.delete</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.use</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  useExternalIp</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">dataflow.jobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">dataflow.jobs.cancel</code></li>
<li><code dir="ltr" translate="no">dataflow.jobs.create</code></li>
<li><code dir="ltr" translate="no">dataflow.jobs.get</code></li>
<li><code dir="ltr" translate="no">dataflow.jobs.list</code></li>
<li><code dir="ltr" translate="no">dataflow.jobs.snapshot</code></li>
<li><code dir="ltr" translate="no">dataflow.jobs.updateContents</code></li>
</ul>
<p><code dir="ltr" translate="no">dataflow.messages.list</code></p>
<p><code dir="ltr" translate="no">dataflow.metrics.get</code></p>
<p><code dir="ltr" translate="no">dataflow.snapshots.*</code></p>
<ul>
<li><code dir="ltr" translate="no">dataflow.snapshots.delete</code></li>
<li><code dir="ltr" translate="no">dataflow.snapshots.get</code></li>
<li><code dir="ltr" translate="no">dataflow.snapshots.list</code></li>
</ul>
<p><code dir="ltr" translate="no">datalabeling.  annotateddatasets.  get</code></p>
<p><code dir="ltr" translate="no">datalabeling.datasets.export</code></p>
<p><code dir="ltr" translate="no">datalabeling.datasets.get</code></p>
<p><code dir="ltr" translate="no">datalabeling.datasets.list</code></p>
<p><code dir="ltr" translate="no">datalabeling.operations.get</code></p>
<p><code dir="ltr" translate="no">hypercomputecluster.clusters.*</code></p>
<ul>
<li><code dir="ltr" translate="no">hypercomputecluster.  clusters.  create</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  clusters.  delete</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  clusters.  get</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  clusters.  list</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  clusters.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">hypercomputecluster.  locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">hypercomputecluster.  locations.  get</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  locations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">hypercomputecluster.  operations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">hypercomputecluster.  operations.  cancel</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  operations.  delete</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  operations.  get</code></li>
<li><code dir="ltr" translate="no">hypercomputecluster.  operations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">iam.serviceAccounts.actAs</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getAccessToken</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getOpenIdToken</code></p>
<p><code dir="ltr" translate="no">logging.links.*</code></p>
<ul>
<li><code dir="ltr" translate="no">logging.links.create</code></li>
<li><code dir="ltr" translate="no">logging.links.delete</code></li>
<li><code dir="ltr" translate="no">logging.links.get</code></li>
<li><code dir="ltr" translate="no">logging.links.list</code></li>
</ul>
<p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">logging.views.access</code></p>
<p><code dir="ltr" translate="no">logging.views.get</code></p>
<p><code dir="ltr" translate="no">ml.models.list</code></p>
<p><code dir="ltr" translate="no">ml.operations.get</code></p>
<p><code dir="ltr" translate="no">ml.versions.get</code></p>
<p><code dir="ltr" translate="no">ml.versions.list</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  create</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  get</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  list</code></p>
<p><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  get</code></li>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">monitoring.  notificationChannels.  get</code></p>
<p><code dir="ltr" translate="no">monitoring.timeSeries.create</code></p>
<p><code dir="ltr" translate="no">networkservices.  agentGateways.  get</code></p>
<p><code dir="ltr" translate="no">networkservices.  agentGateways.  use</code></p>
<p><code dir="ltr" translate="no">networkservices.operations.get</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.create</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.get</code></p>
<p><code dir="ltr" translate="no">observability.links.create</code></p>
<p><code dir="ltr" translate="no">observability.links.delete</code></p>
<p><code dir="ltr" translate="no">observability.links.get</code></p>
<p><code dir="ltr" translate="no">observability.links.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">run.executions.delete</code></p>
<p><code dir="ltr" translate="no">run.executions.get</code></p>
<p><code dir="ltr" translate="no">run.jobs.create</code></p>
<p><code dir="ltr" translate="no">run.jobs.delete</code></p>
<p><code dir="ltr" translate="no">run.jobs.get</code></p>
<p><code dir="ltr" translate="no">run.jobs.run</code></p>
<p><code dir="ltr" translate="no">run.jobs.update</code></p>
<p><code dir="ltr" translate="no">run.operations.delete</code></p>
<p><code dir="ltr" translate="no">run.operations.get</code></p>
<p><code dir="ltr" translate="no">run.routes.invoke</code></p>
<p><code dir="ltr" translate="no">run.services.create</code></p>
<p><code dir="ltr" translate="no">run.services.delete</code></p>
<p><code dir="ltr" translate="no">run.services.get</code></p>
<p><code dir="ltr" translate="no">servicemanagement.  services.  report</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.buckets.create</code></p>
<p><code dir="ltr" translate="no">storage.buckets.delete</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.create</code></p>
<p><code dir="ltr" translate="no">storage.objects.delete</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.update</code></p></td>
</tr>
<tr class="even">
<td><h4 id="aiplatform.telemetryServiceAgent" class="role-title add-link" data-text="Vertex AI Telemetry Service Agent" tabindex="-1">Vertex AI Telemetry Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.telemetryServiceAgent</code> )</p>
<p>Allows Vertex AI Telemetry Service Agent to access telemetry data.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">logging.logEntries.create</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.list</code></p>
<p><code dir="ltr" translate="no">logging.logEntries.route</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  create</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  get</code></p>
<p><code dir="ltr" translate="no">monitoring.  metricDescriptors.  list</code></p>
<p><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.*</code></p>
<ul>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  get</code></li>
<li><code dir="ltr" translate="no">monitoring.  monitoredResourceDescriptors.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">monitoring.timeSeries.*</code></p>
<ul>
<li><code dir="ltr" translate="no">monitoring.timeSeries.create</code></li>
<li><code dir="ltr" translate="no">monitoring.timeSeries.list</code></li>
</ul>
<p><code dir="ltr" translate="no">servicemanagement.  services.  report</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="aiplatform.tuningServiceAgent" class="role-title add-link" data-text="Vertex AI Tuning Service Agent" tabindex="-1">Vertex AI Tuning Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  aiplatform.tuningServiceAgent</code> )</p>
<p>Vertex AI Service Agent used for tuning in user project.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.artifacts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.artifacts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.artifacts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  cancel</code></p>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.  batchPredictionJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.contexts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextArtifactsAndExecutions</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  addContextChildren</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  contexts.  queryContextLineageSubgraph</code></li>
<li><code dir="ltr" translate="no">aiplatform.contexts.update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.endpoints.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.deploy</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.endpoints.predict</code></p>
<p><code dir="ltr" translate="no">aiplatform.  evaluationRuns.  create</code></p>
<p><code dir="ltr" translate="no">aiplatform.evaluationRuns.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  locations.  evaluateInstances</code></p>
<p><code dir="ltr" translate="no">aiplatform.locations.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.metadataSchemas.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataSchemas.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataSchemas.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.metadataStores.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  metadataStores.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.metadataStores.list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.models.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.models.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.models.upload</code></p>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardExperiments.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboardRuns.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.tensorboardRuns.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  update</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardRuns.  write</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchCreate</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  batchRead</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  list</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  read</code></li>
<li><code dir="ltr" translate="no">aiplatform.  tensorboardTimeSeries.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.tensorboards.update</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.cancel</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.delete</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.tuningJobs.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  tuningJobs.  vertexTune</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.create</code></p>
<p><code dir="ltr" translate="no">bigquery.datasets.get</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.create</code></p>
<p><code dir="ltr" translate="no">bigquery.jobs.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.create</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.delete</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.get</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.getData</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.list</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.update</code></p>
<p><code dir="ltr" translate="no">bigquery.tables.updateData</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.use</code></p>
<p><code dir="ltr" translate="no">storage.buckets.create</code></p>
<p><code dir="ltr" translate="no">storage.buckets.get</code></p>
<p><code dir="ltr" translate="no">storage.buckets.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">storage.buckets.list</code></p>
<p><code dir="ltr" translate="no">storage.buckets.update</code></p>
<p><code dir="ltr" translate="no">storage.objects.create</code></p>
<p><code dir="ltr" translate="no">storage.objects.delete</code></p>
<p><code dir="ltr" translate="no">storage.objects.get</code></p>
<p><code dir="ltr" translate="no">storage.objects.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">storage.objects.list</code></p>
<p><code dir="ltr" translate="no">storage.objects.update</code></p></td>
</tr>
</tbody>
</table>

<span id="primitive-roles"></span>

### Basic roles

The older Google Cloud [basic roles](https://docs.cloud.google.com/iam/docs/roles-overview#basic) are common to all Google Cloud services. These roles are Owner, Editor, and Viewer.

> Basic roles include thousands of permissions across all Google Cloud services. In production environments, don't grant basic roles unless there is no alternative. Instead, grant the most limited [predefined roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) or [custom roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#custom-roles) that meet your needs.

## Project-level versus resource-level access

You can manage access at the project level or resource level. You might also have the ability to manage access at a folder or organization level.

For most Agent Platform resources, access can only be controlled by the project, folder, and organization. Access to individual resources can be granted only for specific resource types, for example, an endpoint or a featurestore.

Users share control of all resources they can access. For example, if a user registers a model, all other authorized users in the project can access, change, and delete the model.

To grant access to resources at the project level, assign one or more [roles](https://docs.cloud.google.com/iam/docs/understanding-roles) to a principal (user, group, or [service account](https://docs.cloud.google.com/iam/docs/overview#service_account) ).

For Agent Platform resources that let you grant access at the resource level, you set an IAM policy on that resource. The policy defines which roles are assigned to which principals.

Setting a [policy](https://docs.cloud.google.com/iam/docs/policies#structure) at the resource level doesn't affect project-level policies. A resource inherits all policies from its ancestry. You can use these two levels of granularity to customize permissions. For example, you can grant users read permissions at the project level so that they can read all resources in the project, and then you can grant users write permissions per resource (at the resource level).

Not all Agent Platform predefined roles and resources support resource-level policies. To identify which roles can be used on which resources, see the [Predefined roles table](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) .

### Supported resources

Agent Platform supports Vertex AI Feature Store featurestore, entity type, and Model Registry resources. For more information, see [Control access to Vertex AI Feature Store resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/resource-policy) and [Control access to Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/access-control) .

After granting or revoking access to a resource, those changes take time to propagate. For more information, see [Access change propagation](https://docs.cloud.google.com/iam/docs/access-change-propagation) .

## Resources, service accounts, and service agents

Agent Platform services often manage long-running resources that perform actions, such as running a training job that reads training data, or serving a machine learning (ML) model that reads model weight. Such standalone resources have their own resource identity when performing actions. This identity is distinct from the identity of the principal that created the resource. Permissions granted to the resource identity define which data and other resources that the resource identity can access, not the permissions of the principal that created the resource.

By default, Agent Platform resources use service accounts managed by Agent Platform as a resource identity. These service accounts are called Agent Platform service agents, and they are attached to the project where the resource is created. Users with specific Agent Platform permissions can create resources that use Agent Platform service agents. For some services, you can specify a service account to attach to the resource. The resource uses this service account to access other resources and services. To learn more about service accounts, see [service accounts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-accounts) .

Agent Platform uses different service agents depending on the APIs being called. Each service agent has specific IAM permissions on the project to which they are tied. These permissions are used by the resource identity to perform actions, and the permissions can include read-only access to all Cloud Storage resources and BigQuery data in the project.

### Service accounts

A [service account](https://docs.cloud.google.com/iam/docs/service-account-overview) is a special account used by an application or a virtual machine (VM) instance, not a person. You can create and assign permissions to service accounts to provide specific permissions to a resource or application.

For information about using a service account to customize the permissions available to a custom training container or a container that serves online predictions for a custom-trained model, read [Use a custom service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account) .

Service accounts are identified by an email address.

### Service agents

[Service agents](https://docs.cloud.google.com/iam/docs/service-agents) are automatically provided; they enable a service to access resources on your behalf.

> **Note:** Don't remove default roles and permissions of service agents unless you are sure that they are unnecessary.

When a service agent is created, the service agent is granted a predefined role for your project. The following table lists Agent Platform service agents, their email addresses, and their respective roles:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Used for</th>
<th>Email address</th>
<th>Role</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Agent Platform Service Agent</td>
<td>Agent Platform capabilities</td>
<td><code dir="ltr" translate="no">service-         PROJECT_NUMBER        @gcp-sa-aiplatform.iam.gserviceaccount.com</code></td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.serviceAgent"><code dir="ltr" translate="no">roles/aiplatform.serviceAgent</code></a></td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform RAG Data Service Agent</td>
<td>Agent Platform RAG accesses user-imported data, Agent Platform, Document AI processors in the project</td>
<td><code dir="ltr" translate="no">service-         PROJECT_NUMBER        @gcp-sa-vertex-rag.iam.gserviceaccount.com</code></td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.ragServiceAgent"><code dir="ltr" translate="no">roles/  aiplatform.ragServiceAgent</code></a></td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Custom Code Service Agent</td>
<td><p>Custom training code</p>
<p>Ray on Agent Platform application code</p></td>
<td><code dir="ltr" translate="no">service-         PROJECT_NUMBER        @gcp-sa-aiplatform-cc.iam.gserviceaccount.com</code></td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.customCodeServiceAgent"><code dir="ltr" translate="no">roles/aiplatform.customCodeServiceAgent</code></a></td>
</tr>
<tr class="even">
<td>Agent Platform Extension Service Agent</td>
<td>Vertex Extensions</td>
<td><code dir="ltr" translate="no">service-         PROJECT_NUMBER        @gcp-sa-vertex-ex.iam.gserviceaccount.com</code></td>
<td><code dir="ltr" translate="no"> roles/aiplatform.extensionServiceAgent</code></td>
</tr>
<tr class="odd">
<td>Cloud AI Platform Notebooks Service Account</td>
<td>Vertex AI Workbench capabilities</td>
<td><code dir="ltr" translate="no">service-         PROJECT_NUMBER        @gcp-sa-notebooks.iam.gserviceaccount.com</code></td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#notebooks.serviceAgent"><code dir="ltr" translate="no">roles/notebooks.serviceAgent</code></a></td>
</tr>
</tbody>
</table>

The Gemini Enterprise Agent Platform Custom Code Service Agent is created only if you run custom training code to train a custom-trained model.

> For Agent Platform to perform tasks like training a model using data from a Cloud Storage bucket, it needs permission to read that data. To handle this securely, Agent Platform uses a Google-managed service account called a [Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) to access your resources. When you use the Agent Platform API, this Service Agent is automatically granted IAM roles (like [Storage Object Viewer](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) ) on your project. This is expected and necessary for the service to function. This mechanism allows Agent Platform to access the data it needs for tasks you initiate, while your data remains under your project's access control policies.

#### Service agent roles and permissions

See the following roles and permissions that are granted to [Agent Platform service agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) .

Role

Permissions

#### Vertex AI Service Agent

( `roles/ aiplatform.serviceAgent` )

Gives Vertex AI the permissions it needs to function.

> **Warning:** Do not grant service agent roles to any principals except [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

`aiplatform.agentExamples.*`

  - `aiplatform. agentExamples. create`
  - `aiplatform. agentExamples. delete`
  - `aiplatform.agentExamples.get`
  - `aiplatform.agentExamples.list`
  - `aiplatform. agentExamples. update`

`aiplatform.agents.*`

  - `aiplatform.agents.create`
  - `aiplatform.agents.delete`
  - `aiplatform.agents.get`
  - `aiplatform.agents.list`
  - `aiplatform.agents.update`

`aiplatform.annotationSpecs.*`

  - `aiplatform. annotationSpecs. create`
  - `aiplatform. annotationSpecs. delete`
  - `aiplatform.annotationSpecs.get`
  - `aiplatform. annotationSpecs. list`
  - `aiplatform. annotationSpecs. update`

`aiplatform.annotations.*`

  - `aiplatform.annotations.create`
  - `aiplatform.annotations.delete`
  - `aiplatform.annotations.get`
  - `aiplatform.annotations.list`
  - `aiplatform.annotations.update`

`aiplatform.apps.*`

  - `aiplatform.apps.create`
  - `aiplatform.apps.delete`
  - `aiplatform.apps.get`
  - `aiplatform.apps.list`
  - `aiplatform.apps.update`

`aiplatform.artifacts.*`

  - `aiplatform.artifacts.create`
  - `aiplatform.artifacts.delete`
  - `aiplatform.artifacts.get`
  - `aiplatform.artifacts.list`
  - `aiplatform.artifacts.update`

`aiplatform. batchPredictionJobs.*`

  - `aiplatform. batchPredictionJobs. cancel`
  - `aiplatform. batchPredictionJobs. create`
  - `aiplatform. batchPredictionJobs. delete`
  - `aiplatform. batchPredictionJobs. get`
  - `aiplatform. batchPredictionJobs. list`

`aiplatform.cacheConfigs.get`

`aiplatform.cachedContents.*`

  - `aiplatform. cachedContents. create`
  - `aiplatform. cachedContents. delete`
  - `aiplatform.cachedContents.get`
  - `aiplatform.cachedContents.list`
  - `aiplatform. cachedContents. update`

`aiplatform.consents.get`

`aiplatform.contexts.*`

  - `aiplatform. contexts. addContextArtifactsAndExecutions`
  - `aiplatform. contexts. addContextChildren`
  - `aiplatform.contexts.create`
  - `aiplatform.contexts.delete`
  - `aiplatform.contexts.get`
  - `aiplatform.contexts.list`
  - `aiplatform. contexts. queryContextLineageSubgraph`
  - `aiplatform.contexts.update`

`aiplatform.customJobs.*`

  - `aiplatform.customJobs.cancel`
  - `aiplatform.customJobs.create`
  - `aiplatform.customJobs.delete`
  - `aiplatform.customJobs.get`
  - `aiplatform.customJobs.list`

`aiplatform.dataItems.*`

  - `aiplatform.dataItems.create`
  - `aiplatform.dataItems.delete`
  - `aiplatform.dataItems.get`
  - `aiplatform.dataItems.list`
  - `aiplatform.dataItems.update`

`aiplatform.dataLabelingJobs.*`

  - `aiplatform. dataLabelingJobs. cancel`
  - `aiplatform. dataLabelingJobs. create`
  - `aiplatform. dataLabelingJobs. delete`
  - `aiplatform. dataLabelingJobs. get`
  - `aiplatform. dataLabelingJobs. list`

`aiplatform.datasetVersions.*`

  - `aiplatform. datasetVersions. create`
  - `aiplatform. datasetVersions. delete`
  - `aiplatform.datasetVersions.get`
  - `aiplatform. datasetVersions. list`
  - `aiplatform. datasetVersions. restore`

`aiplatform.datasets.*`

  - `aiplatform.datasets.create`
  - `aiplatform.datasets.delete`
  - `aiplatform.datasets.export`
  - `aiplatform.datasets.get`
  - `aiplatform.datasets.import`
  - `aiplatform.datasets.list`
  - `aiplatform.datasets.update`

`aiplatform. deploymentResourcePools.*`

  - `aiplatform. deploymentResourcePools. create`
  - `aiplatform. deploymentResourcePools. delete`
  - `aiplatform. deploymentResourcePools. get`
  - `aiplatform. deploymentResourcePools. list`
  - `aiplatform. deploymentResourcePools. queryDeployedModels`
  - `aiplatform. deploymentResourcePools. update`

`aiplatform. edgeDeploymentJobs.*`

  - `aiplatform. edgeDeploymentJobs. create`
  - `aiplatform. edgeDeploymentJobs. delete`
  - `aiplatform. edgeDeploymentJobs. get`
  - `aiplatform. edgeDeploymentJobs. list`

`aiplatform. edgeDeviceDebugInfo. get`

`aiplatform.edgeDevices.*`

  - `aiplatform.edgeDevices.create`
  - `aiplatform.edgeDevices.delete`
  - `aiplatform.edgeDevices.get`
  - `aiplatform.edgeDevices.list`
  - `aiplatform.edgeDevices.update`

`aiplatform.endpoints.create`

`aiplatform.endpoints.delete`

`aiplatform.endpoints.deploy`

`aiplatform.endpoints.explain`

`aiplatform.endpoints.get`

`aiplatform.endpoints.list`

`aiplatform.endpoints.predict`

`aiplatform.endpoints.undeploy`

`aiplatform.endpoints.update`

`aiplatform.entityTypes.create`

`aiplatform.entityTypes.delete`

`aiplatform. entityTypes. deleteFeatureValues`

`aiplatform. entityTypes. exportFeatureValues`

`aiplatform.entityTypes.get`

`aiplatform. entityTypes. importFeatureValues`

`aiplatform.entityTypes.list`

`aiplatform. entityTypes. readFeatureValues`

`aiplatform. entityTypes. streamingReadFeatureValues`

`aiplatform.entityTypes.update`

`aiplatform. entityTypes. writeFeatureValues`

`aiplatform. evaluationExperiments.*`

  - `aiplatform. evaluationExperiments. create`
  - `aiplatform. evaluationExperiments. delete`
  - `aiplatform. evaluationExperiments. get`
  - `aiplatform. evaluationExperiments. list`
  - `aiplatform. evaluationExperiments. update`

`aiplatform.evaluationItems.*`

  - `aiplatform. evaluationItems. create`
  - `aiplatform. evaluationItems. delete`
  - `aiplatform.evaluationItems.get`
  - `aiplatform. evaluationItems. list`
  - `aiplatform. evaluationItems. update`

`aiplatform.evaluationRuns.*`

  - `aiplatform. evaluationRuns. cancel`
  - `aiplatform. evaluationRuns. create`
  - `aiplatform. evaluationRuns. delete`
  - `aiplatform. evaluationRuns. execute`
  - `aiplatform.evaluationRuns.get`
  - `aiplatform.evaluationRuns.list`
  - `aiplatform. evaluationRuns. update`

`aiplatform.evaluationSets.*`

  - `aiplatform. evaluationSets. create`
  - `aiplatform. evaluationSets. delete`
  - `aiplatform.evaluationSets.get`
  - `aiplatform. evaluationSets. import`
  - `aiplatform.evaluationSets.list`
  - `aiplatform. evaluationSets. update`

`aiplatform.exampleStores.*`

  - `aiplatform. exampleStores. create`
  - `aiplatform. exampleStores. delete`
  - `aiplatform.exampleStores.get`
  - `aiplatform.exampleStores.list`
  - `aiplatform. exampleStores. readExample`
  - `aiplatform. exampleStores. update`
  - `aiplatform. exampleStores. writeExample`

`aiplatform.executions.*`

  - `aiplatform. executions. addExecutionEvents`
  - `aiplatform.executions.create`
  - `aiplatform.executions.delete`
  - `aiplatform.executions.get`
  - `aiplatform.executions.list`
  - `aiplatform. executions. queryExecutionInputsAndOutputs`
  - `aiplatform.executions.update`

`aiplatform.extensions.*`

  - `aiplatform.extensions.delete`
  - `aiplatform.extensions.execute`
  - `aiplatform.extensions.get`
  - `aiplatform.extensions.import`
  - `aiplatform.extensions.list`
  - `aiplatform.extensions.update`

`aiplatform. featureGroups. create`

`aiplatform. featureGroups. delete`

`aiplatform.featureGroups.get`

`aiplatform.featureGroups.list`

`aiplatform. featureGroups. update`

`aiplatform. featureMonitorJobs.*`

  - `aiplatform. featureMonitorJobs. create`
  - `aiplatform. featureMonitorJobs. get`
  - `aiplatform. featureMonitorJobs. list`

`aiplatform.featureMonitors.*`

  - `aiplatform. featureMonitors. create`
  - `aiplatform. featureMonitors. delete`
  - `aiplatform.featureMonitors.get`
  - `aiplatform. featureMonitors. list`
  - `aiplatform. featureMonitors. update`

`aiplatform. featureOnlineStores. create`

`aiplatform. featureOnlineStores. delete`

`aiplatform. featureOnlineStores. get`

`aiplatform. featureOnlineStores. list`

`aiplatform. featureOnlineStores. update`

`aiplatform.featureViewSyncs.*`

  - `aiplatform. featureViewSyncs. get`
  - `aiplatform. featureViewSyncs. list`

`aiplatform.featureViews.create`

`aiplatform.featureViews.delete`

`aiplatform. featureViews. directWrite`

`aiplatform. featureViews. fetchFeatureValues`

`aiplatform.featureViews.get`

`aiplatform.featureViews.list`

`aiplatform. featureViews. searchNearestEntities`

`aiplatform.featureViews.sync`

`aiplatform.featureViews.update`

`aiplatform.features.*`

  - `aiplatform.features.create`
  - `aiplatform.features.delete`
  - `aiplatform.features.get`
  - `aiplatform.features.list`
  - `aiplatform.features.update`

`aiplatform. featurestores. batchReadFeatureValues`

`aiplatform. featurestores. create`

`aiplatform. featurestores. delete`

`aiplatform. featurestores. exportFeatures`

`aiplatform.featurestores.get`

`aiplatform. featurestores. importFeatures`

`aiplatform.featurestores.list`

`aiplatform. featurestores. readFeatures`

`aiplatform. featurestores. update`

`aiplatform. featurestores. writeFeatures`

`aiplatform.humanInTheLoops.*`

  - `aiplatform. humanInTheLoops. cancel`
  - `aiplatform. humanInTheLoops. create`
  - `aiplatform. humanInTheLoops. delete`
  - `aiplatform.humanInTheLoops.get`
  - `aiplatform. humanInTheLoops. list`
  - `aiplatform. humanInTheLoops. queryAnnotationStats`
  - `aiplatform. humanInTheLoops. send`
  - `aiplatform. humanInTheLoops. update`

`aiplatform. hyperparameterTuningJobs.*`

  - `aiplatform. hyperparameterTuningJobs. cancel`
  - `aiplatform. hyperparameterTuningJobs. create`
  - `aiplatform. hyperparameterTuningJobs. delete`
  - `aiplatform. hyperparameterTuningJobs. get`
  - `aiplatform. hyperparameterTuningJobs. list`

`aiplatform.indexEndpoints.*`

  - `aiplatform. indexEndpoints. create`
  - `aiplatform. indexEndpoints. delete`
  - `aiplatform. indexEndpoints. deploy`
  - `aiplatform.indexEndpoints.get`
  - `aiplatform.indexEndpoints.list`
  - `aiplatform. indexEndpoints. queryVectors`
  - `aiplatform. indexEndpoints. undeploy`
  - `aiplatform. indexEndpoints. update`

`aiplatform.indexes.*`

  - `aiplatform.indexes.create`
  - `aiplatform.indexes.delete`
  - `aiplatform.indexes.get`
  - `aiplatform.indexes.list`
  - `aiplatform.indexes.update`

`aiplatform.locations.*`

  - `aiplatform. locations. evaluateInstances`
  - `aiplatform.locations.get`
  - `aiplatform.locations.list`

`aiplatform.memories.*`

  - `aiplatform.memories.create`
  - `aiplatform.memories.delete`
  - `aiplatform.memories.generate`
  - `aiplatform.memories.get`
  - `aiplatform.memories.list`
  - `aiplatform.memories.retrieve`
  - `aiplatform.memories.update`

`aiplatform.memoryRevisions.*`

  - `aiplatform.memoryRevisions.get`
  - `aiplatform. memoryRevisions. list`
  - `aiplatform. memoryRevisions. rollback`

`aiplatform.metadataSchemas.*`

  - `aiplatform. metadataSchemas. create`
  - `aiplatform. metadataSchemas. delete`
  - `aiplatform.metadataSchemas.get`
  - `aiplatform. metadataSchemas. list`

`aiplatform.metadataStores.*`

  - `aiplatform. metadataStores. create`
  - `aiplatform. metadataStores. delete`
  - `aiplatform.metadataStores.get`
  - `aiplatform.metadataStores.list`

`aiplatform. modelDeploymentMonitoringJobs.*`

  - `aiplatform. modelDeploymentMonitoringJobs. create`
  - `aiplatform. modelDeploymentMonitoringJobs. delete`
  - `aiplatform. modelDeploymentMonitoringJobs. get`
  - `aiplatform. modelDeploymentMonitoringJobs. list`
  - `aiplatform. modelDeploymentMonitoringJobs. pause`
  - `aiplatform. modelDeploymentMonitoringJobs. resume`
  - `aiplatform. modelDeploymentMonitoringJobs. searchStatsAnomalies`
  - `aiplatform. modelDeploymentMonitoringJobs. update`

`aiplatform. modelEvaluationSlices.*`

  - `aiplatform. modelEvaluationSlices. get`
  - `aiplatform. modelEvaluationSlices. import`
  - `aiplatform. modelEvaluationSlices. list`

`aiplatform.modelEvaluations.*`

  - `aiplatform. modelEvaluations. exportEvaluatedDataItems`
  - `aiplatform. modelEvaluations. get`
  - `aiplatform. modelEvaluations. import`
  - `aiplatform. modelEvaluations. list`

`aiplatform. modelMonitoringJobs.*`

  - `aiplatform. modelMonitoringJobs. create`
  - `aiplatform. modelMonitoringJobs. delete`
  - `aiplatform. modelMonitoringJobs. get`
  - `aiplatform. modelMonitoringJobs. list`

`aiplatform.modelMonitors.*`

  - `aiplatform. modelMonitors. create`
  - `aiplatform. modelMonitors. delete`
  - `aiplatform.modelMonitors.get`
  - `aiplatform.modelMonitors.list`
  - `aiplatform. modelMonitors. searchModelMonitoringAlerts`
  - `aiplatform. modelMonitors. searchModelMonitoringStats`
  - `aiplatform. modelMonitors. update`

`aiplatform.models.*`

  - `aiplatform.models.delete`
  - `aiplatform.models.export`
  - `aiplatform.models.get`
  - `aiplatform.models.list`
  - `aiplatform.models.update`
  - `aiplatform.models.upload`

`aiplatform.nasJobs.*`

  - `aiplatform.nasJobs.cancel`
  - `aiplatform.nasJobs.create`
  - `aiplatform.nasJobs.delete`
  - `aiplatform.nasJobs.get`
  - `aiplatform.nasJobs.list`

`aiplatform.nasTrialDetails.*`

  - `aiplatform.nasTrialDetails.get`
  - `aiplatform. nasTrialDetails. list`

`aiplatform. notebookExecutionJobs.*`

  - `aiplatform. notebookExecutionJobs. create`
  - `aiplatform. notebookExecutionJobs. delete`
  - `aiplatform. notebookExecutionJobs. get`
  - `aiplatform. notebookExecutionJobs. list`

`aiplatform. notebookRuntimeTemplates. apply`

`aiplatform. notebookRuntimeTemplates. create`

`aiplatform. notebookRuntimeTemplates. delete`

`aiplatform. notebookRuntimeTemplates. get`

`aiplatform. notebookRuntimeTemplates. list`

`aiplatform. notebookRuntimeTemplates. update`

`aiplatform.notebookRuntimes.*`

  - `aiplatform. notebookRuntimes. assign`
  - `aiplatform. notebookRuntimes. delete`
  - `aiplatform. notebookRuntimes. get`
  - `aiplatform. notebookRuntimes. list`
  - `aiplatform. notebookRuntimes. start`
  - `aiplatform. notebookRuntimes. update`
  - `aiplatform. notebookRuntimes. upgrade`

`aiplatform.onlineEvaluators.*`

  - `aiplatform. onlineEvaluators. create`
  - `aiplatform. onlineEvaluators. delete`
  - `aiplatform. onlineEvaluators. get`
  - `aiplatform. onlineEvaluators. list`
  - `aiplatform. onlineEvaluators. update`

`aiplatform.operations.list`

`aiplatform. persistentResources. get`

`aiplatform. persistentResources. list`

`aiplatform.pipelineJobs.*`

  - `aiplatform.pipelineJobs.cancel`
  - `aiplatform.pipelineJobs.create`
  - `aiplatform.pipelineJobs.delete`
  - `aiplatform.pipelineJobs.get`
  - `aiplatform.pipelineJobs.list`

`aiplatform. provisionedThroughputRevisions.*`

  - `aiplatform. provisionedThroughputRevisions. get`
  - `aiplatform. provisionedThroughputRevisions. list`

`aiplatform. provisionedThroughputs. get`

`aiplatform. provisionedThroughputs. list`

`aiplatform.ragCorpora.*`

  - `aiplatform.ragCorpora.create`
  - `aiplatform.ragCorpora.delete`
  - `aiplatform.ragCorpora.get`
  - `aiplatform.ragCorpora.list`
  - `aiplatform.ragCorpora.query`
  - `aiplatform.ragCorpora.update`

`aiplatform. ragEngineConfigs. get`

`aiplatform.ragFiles.*`

  - `aiplatform.ragFiles.delete`
  - `aiplatform.ragFiles.get`
  - `aiplatform.ragFiles.import`
  - `aiplatform.ragFiles.list`
  - `aiplatform.ragFiles.upload`

`aiplatform. reasoningEngineRuntimeRevisions.*`

  - `aiplatform. reasoningEngineRuntimeRevisions. delete`
  - `aiplatform. reasoningEngineRuntimeRevisions. get`
  - `aiplatform. reasoningEngineRuntimeRevisions. list`
  - `aiplatform. reasoningEngineRuntimeRevisions. query`

`aiplatform. reasoningEngines. create`

`aiplatform. reasoningEngines. delete`

`aiplatform. reasoningEngines. get`

`aiplatform. reasoningEngines. list`

`aiplatform. reasoningEngines. query`

`aiplatform. reasoningEngines. update`

`aiplatform. sandboxEnvironments.*`

  - `aiplatform. sandboxEnvironments. create`
  - `aiplatform. sandboxEnvironments. delete`
  - `aiplatform. sandboxEnvironments. execute`
  - `aiplatform. sandboxEnvironments. get`
  - `aiplatform. sandboxEnvironments. list`

`aiplatform.schedules.*`

  - `aiplatform.schedules.create`
  - `aiplatform.schedules.delete`
  - `aiplatform.schedules.get`
  - `aiplatform.schedules.list`
  - `aiplatform.schedules.update`

`aiplatform. semanticGovernancePolicies.*`

  - `aiplatform. semanticGovernancePolicies. create`
  - `aiplatform. semanticGovernancePolicies. delete`
  - `aiplatform. semanticGovernancePolicies. get`
  - `aiplatform. semanticGovernancePolicies. list`
  - `aiplatform. semanticGovernancePolicies. update`

`aiplatform. semanticGovernancePolicyEngine.*`

  - `aiplatform. semanticGovernancePolicyEngine. get`
  - `aiplatform. semanticGovernancePolicyEngine. update`

`aiplatform.sessionEvents.*`

  - `aiplatform. sessionEvents. append`
  - `aiplatform.sessionEvents.list`

`aiplatform.sessions.*`

  - `aiplatform.sessions.create`
  - `aiplatform.sessions.delete`
  - `aiplatform.sessions.get`
  - `aiplatform.sessions.list`
  - `aiplatform.sessions.run`
  - `aiplatform.sessions.update`

`aiplatform.specialistPools.*`

  - `aiplatform. specialistPools. create`
  - `aiplatform. specialistPools. delete`
  - `aiplatform.specialistPools.get`
  - `aiplatform. specialistPools. list`
  - `aiplatform. specialistPools. update`

`aiplatform.studies.*`

  - `aiplatform.studies.create`
  - `aiplatform.studies.delete`
  - `aiplatform.studies.get`
  - `aiplatform.studies.list`
  - `aiplatform.studies.update`

`aiplatform. tensorboardExperiments.*`

  - `aiplatform. tensorboardExperiments. create`
  - `aiplatform. tensorboardExperiments. delete`
  - `aiplatform. tensorboardExperiments. get`
  - `aiplatform. tensorboardExperiments. list`
  - `aiplatform. tensorboardExperiments. update`
  - `aiplatform. tensorboardExperiments. write`

`aiplatform.tensorboardRuns.*`

  - `aiplatform. tensorboardRuns. batchCreate`
  - `aiplatform. tensorboardRuns. create`
  - `aiplatform. tensorboardRuns. delete`
  - `aiplatform.tensorboardRuns.get`
  - `aiplatform. tensorboardRuns. list`
  - `aiplatform. tensorboardRuns. update`
  - `aiplatform. tensorboardRuns. write`

`aiplatform. tensorboardTimeSeries.*`

  - `aiplatform. tensorboardTimeSeries. batchCreate`
  - `aiplatform. tensorboardTimeSeries. batchRead`
  - `aiplatform. tensorboardTimeSeries. create`
  - `aiplatform. tensorboardTimeSeries. delete`
  - `aiplatform. tensorboardTimeSeries. get`
  - `aiplatform. tensorboardTimeSeries. list`
  - `aiplatform. tensorboardTimeSeries. read`
  - `aiplatform. tensorboardTimeSeries. update`

`aiplatform.tensorboards.create`

`aiplatform.tensorboards.delete`

`aiplatform.tensorboards.get`

`aiplatform.tensorboards.list`

`aiplatform.tensorboards.update`

`aiplatform.trainingPipelines.*`

  - `aiplatform. trainingPipelines. cancel`
  - `aiplatform. trainingPipelines. create`
  - `aiplatform. trainingPipelines. delete`
  - `aiplatform. trainingPipelines. get`
  - `aiplatform. trainingPipelines. list`

`aiplatform.trials.*`

  - `aiplatform.trials.create`
  - `aiplatform.trials.delete`
  - `aiplatform.trials.get`
  - `aiplatform.trials.list`
  - `aiplatform.trials.update`

`aiplatform.tuningJobs.*`

  - `aiplatform.tuningJobs.cancel`
  - `aiplatform.tuningJobs.create`
  - `aiplatform.tuningJobs.delete`
  - `aiplatform.tuningJobs.get`
  - `aiplatform.tuningJobs.list`
  - `aiplatform. tuningJobs. optimizePrompt`
  - `aiplatform. tuningJobs. validateReinforcementTuningReward`
  - `aiplatform. tuningJobs. vertexTune`

`artifactregistry. repositories. create`

`artifactregistry. repositories. downloadArtifacts`

`artifactregistry. repositories. get`

`artifactregistry. repositories. list`

`artifactregistry. repositories. uploadArtifacts`

`artifactregistry.tags.get`

`artifactregistry.versions.get`

`automl.datasets.export`

`automl.datasets.get`

`automl.datasets.list`

`automl.modelEvaluations.list`

`automl.models.get`

`automl.models.list`

`automl.operations.get`

`automl.tableSpecs.get`

`bigquery.datasets.create`

`bigquery.datasets.get`

`bigquery.jobs.create`

`bigquery.jobs.get`

`bigquery.models.create`

`bigquery.models.export`

`bigquery.models.getData`

`bigquery.objectRefs.read`

`bigquery.readsessions.create`

`bigquery.readsessions.getData`

`bigquery.tables.create`

`bigquery.tables.export`

`bigquery.tables.get`

`bigquery.tables.getData`

`bigquery.tables.list`

`bigquery.tables.update`

`bigquery.tables.updateData`

`bigtable.tables.get`

`bigtable.tables.list`

`bigtable.tables.readRows`

`binaryauthorization. policy. evaluatePolicy`

`cloudtrace.traces.get`

`cloudtrace.traces.list`

`compute.addresses.get`

`compute.addresses.list`

`compute.addresses.use`

`compute.addresses.useInternal`

`compute.disks.create`

`compute.disks.createSnapshot`

`compute.disks.createTagBinding`

`compute.disks.delete`

`compute.disks.get`

`compute.disks.setLabels`

`compute.disks.use`

`compute.disks.useReadOnly`

`compute.globalOperations.get`

`compute.instances.attachDisk`

`compute.instances.create`

`compute. instances. createTagBinding`

`compute.instances.delete`

`compute.instances.detachDisk`

`compute.instances.get`

`compute. instances. getGuestAttributes`

`compute.instances.list`

`compute.instances.setLabels`

`compute.instances.setMetadata`

`compute. instances. setServiceAccount`

`compute.instances.setTags`

`compute.instances.start`

`compute.instances.stop`

`compute.instances.update`

`compute.instances.useReadOnly`

`compute.machineTypes.get`

`compute.networks.get`

`compute.networks.use`

`compute.networks.useExternalIp`

`compute.snapshots.create`

`compute.snapshots.delete`

`compute.snapshots.useReadOnly`

`compute.subnetworks.get`

`compute.subnetworks.list`

`compute.subnetworks.use`

`compute. subnetworks. useExternalIp`

`compute.zoneOperations.get`

`dataflow.jobs.*`

  - `dataflow.jobs.cancel`
  - `dataflow.jobs.create`
  - `dataflow.jobs.get`
  - `dataflow.jobs.list`
  - `dataflow.jobs.snapshot`
  - `dataflow.jobs.updateContents`

`dataflow.messages.list`

`dataflow.metrics.get`

`dataflow.snapshots.*`

  - `dataflow.snapshots.delete`
  - `dataflow.snapshots.get`
  - `dataflow.snapshots.list`

`datalabeling. annotateddatasets. get`

`datalabeling.datasets.export`

`datalabeling.datasets.get`

`datalabeling.datasets.list`

`datalabeling.operations.get`

`hypercomputecluster.clusters.*`

  - `hypercomputecluster. clusters. create`
  - `hypercomputecluster. clusters. delete`
  - `hypercomputecluster. clusters. get`
  - `hypercomputecluster. clusters. list`
  - `hypercomputecluster. clusters. update`

`hypercomputecluster. locations.*`

  - `hypercomputecluster. locations. get`
  - `hypercomputecluster. locations. list`

`hypercomputecluster. operations.*`

  - `hypercomputecluster. operations. cancel`
  - `hypercomputecluster. operations. delete`
  - `hypercomputecluster. operations. get`
  - `hypercomputecluster. operations. list`

`iam.serviceAccounts.actAs`

`iam. serviceAccounts. getAccessToken`

`iam. serviceAccounts. getOpenIdToken`

`logging.links.*`

  - `logging.links.create`
  - `logging.links.delete`
  - `logging.links.get`
  - `logging.links.list`

`logging.logEntries.create`

`logging.logEntries.route`

`logging.views.access`

`logging.views.get`

`ml.models.list`

`ml.operations.get`

`ml.versions.get`

`ml.versions.list`

`monitoring. metricDescriptors. create`

`monitoring. metricDescriptors. get`

`monitoring. metricDescriptors. list`

`monitoring. monitoredResourceDescriptors.*`

  - `monitoring. monitoredResourceDescriptors. get`
  - `monitoring. monitoredResourceDescriptors. list`

`monitoring. notificationChannels. get`

`monitoring.timeSeries.create`

`networkservices. agentGateways. get`

`networkservices. agentGateways. use`

`networkservices.operations.get`

`notebooks.instances.create`

`notebooks.instances.delete`

`notebooks.instances.get`

`observability.links.create`

`observability.links.delete`

`observability.links.get`

`observability.links.list`

`resourcemanager.projects.get`

`resourcemanager.projects.list`

`run.executions.delete`

`run.executions.get`

`run.jobs.create`

`run.jobs.delete`

`run.jobs.get`

`run.jobs.run`

`run.jobs.update`

`run.operations.delete`

`run.operations.get`

`run.routes.invoke`

`run.services.create`

`run.services.delete`

`run.services.get`

`servicemanagement. services. report`

`serviceusage.services.list`

`serviceusage.services.use`

`storage.buckets.create`

`storage.buckets.delete`

`storage.buckets.get`

`storage.buckets.list`

`storage.objects.create`

`storage.objects.delete`

`storage.objects.get`

`storage.objects.list`

`storage.objects.update`

#### Vertex AI RAG Data Service Agent

( `roles/ aiplatform.ragServiceAgent` )

Vertex AI Service Agent used by Vertex RAG to access user imported data, Vertex AI, Document AI processors, and Vector Search in the project

> **Warning:** Do not grant service agent roles to any principals except [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

`aiplatform.endpoints.get`

`aiplatform.endpoints.predict`

`aiplatform.featureViews.get`

`aiplatform.featureViews.list`

`aiplatform.featureViews.sync`

`aiplatform.featureViews.update`

`aiplatform.indexEndpoints.*`

  - `aiplatform. indexEndpoints. create`
  - `aiplatform. indexEndpoints. delete`
  - `aiplatform. indexEndpoints. deploy`
  - `aiplatform.indexEndpoints.get`
  - `aiplatform.indexEndpoints.list`
  - `aiplatform. indexEndpoints. queryVectors`
  - `aiplatform. indexEndpoints. undeploy`
  - `aiplatform. indexEndpoints. update`

`aiplatform.indexes.*`

  - `aiplatform.indexes.create`
  - `aiplatform.indexes.delete`
  - `aiplatform.indexes.get`
  - `aiplatform.indexes.list`
  - `aiplatform.indexes.update`

`aiplatform.models.get`

`aiplatform.ragCorpora.get`

`aiplatform.ragCorpora.list`

`aiplatform.ragCorpora.query`

`aiplatform.ragFiles.get`

`aiplatform.ragFiles.list`

`bigquery.datasets.create`

`bigquery.datasets.get`

`bigquery.jobs.create`

`bigquery.jobs.get`

`bigquery.readsessions.create`

`bigquery.readsessions.getData`

`bigquery.tables.create`

`bigquery.tables.createSnapshot`

`bigquery.tables.deleteSnapshot`

`bigquery.tables.export`

`bigquery.tables.get`

`bigquery.tables.getData`

`bigquery. tables. restoreSnapshot`

`bigquery.tables.update`

`bigquery.tables.updateData`

`documentai. processorVersions. processOnline`

`documentai.processors.get`

`documentai. processors. processOnline`

`logging.logEntries.create`

`logging.logEntries.route`

`storage.buckets.get`

`storage.buckets.list`

`storage.objects.get`

`storage.objects.list`

`vectorsearch.collections.*`

  - `vectorsearch. collections. create`
  - `vectorsearch. collections. delete`
  - `vectorsearch.collections.get`
  - `vectorsearch.collections.list`
  - `vectorsearch. collections. update`

`vectorsearch.dataObjects.*`

  - `vectorsearch. dataObjects. create`
  - `vectorsearch. dataObjects. delete`
  - `vectorsearch.dataObjects.get`
  - `vectorsearch. dataObjects. import`
  - `vectorsearch.dataObjects.query`
  - `vectorsearch. dataObjects. search`
  - `vectorsearch. dataObjects. update`

`vectorsearch.indexes.*`

  - `vectorsearch.indexes.create`
  - `vectorsearch.indexes.delete`
  - `vectorsearch.indexes.get`
  - `vectorsearch.indexes.list`

`vectorsearch.operations.get`

`vectorsearch.operations.list`

#### Vertex AI Custom Code Service Agent

( `roles/ aiplatform.customCodeServiceAgent` )

Gives Vertex AI Custom Code the proper permissions. The aiplatform.customJobs.create IAM permission is highly privileged. Through Vertex AI Custom Training jobs, it effectively grants editor-level access to other services activated for the consumer project, such as GCS and BigQuery.

> **Warning:** Do not grant service agent roles to any principals except [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

`aiplatform.agentExamples.*`

  - `aiplatform. agentExamples. create`
  - `aiplatform. agentExamples. delete`
  - `aiplatform.agentExamples.get`
  - `aiplatform.agentExamples.list`
  - `aiplatform. agentExamples. update`

`aiplatform.agents.*`

  - `aiplatform.agents.create`
  - `aiplatform.agents.delete`
  - `aiplatform.agents.get`
  - `aiplatform.agents.list`
  - `aiplatform.agents.update`

`aiplatform.annotationSpecs.*`

  - `aiplatform. annotationSpecs. create`
  - `aiplatform. annotationSpecs. delete`
  - `aiplatform.annotationSpecs.get`
  - `aiplatform. annotationSpecs. list`
  - `aiplatform. annotationSpecs. update`

`aiplatform.annotations.*`

  - `aiplatform.annotations.create`
  - `aiplatform.annotations.delete`
  - `aiplatform.annotations.get`
  - `aiplatform.annotations.list`
  - `aiplatform.annotations.update`

`aiplatform.apps.*`

  - `aiplatform.apps.create`
  - `aiplatform.apps.delete`
  - `aiplatform.apps.get`
  - `aiplatform.apps.list`
  - `aiplatform.apps.update`

`aiplatform.artifacts.*`

  - `aiplatform.artifacts.create`
  - `aiplatform.artifacts.delete`
  - `aiplatform.artifacts.get`
  - `aiplatform.artifacts.list`
  - `aiplatform.artifacts.update`

`aiplatform. batchPredictionJobs.*`

  - `aiplatform. batchPredictionJobs. cancel`
  - `aiplatform. batchPredictionJobs. create`
  - `aiplatform. batchPredictionJobs. delete`
  - `aiplatform. batchPredictionJobs. get`
  - `aiplatform. batchPredictionJobs. list`

`aiplatform.cacheConfigs.get`

`aiplatform.cachedContents.*`

  - `aiplatform. cachedContents. create`
  - `aiplatform. cachedContents. delete`
  - `aiplatform.cachedContents.get`
  - `aiplatform.cachedContents.list`
  - `aiplatform. cachedContents. update`

`aiplatform.consents.get`

`aiplatform.contexts.*`

  - `aiplatform. contexts. addContextArtifactsAndExecutions`
  - `aiplatform. contexts. addContextChildren`
  - `aiplatform.contexts.create`
  - `aiplatform.contexts.delete`
  - `aiplatform.contexts.get`
  - `aiplatform.contexts.list`
  - `aiplatform. contexts. queryContextLineageSubgraph`
  - `aiplatform.contexts.update`

`aiplatform.customJobs.*`

  - `aiplatform.customJobs.cancel`
  - `aiplatform.customJobs.create`
  - `aiplatform.customJobs.delete`
  - `aiplatform.customJobs.get`
  - `aiplatform.customJobs.list`

`aiplatform.dataItems.*`

  - `aiplatform.dataItems.create`
  - `aiplatform.dataItems.delete`
  - `aiplatform.dataItems.get`
  - `aiplatform.dataItems.list`
  - `aiplatform.dataItems.update`

`aiplatform.dataLabelingJobs.*`

  - `aiplatform. dataLabelingJobs. cancel`
  - `aiplatform. dataLabelingJobs. create`
  - `aiplatform. dataLabelingJobs. delete`
  - `aiplatform. dataLabelingJobs. get`
  - `aiplatform. dataLabelingJobs. list`

`aiplatform.datasetVersions.*`

  - `aiplatform. datasetVersions. create`
  - `aiplatform. datasetVersions. delete`
  - `aiplatform.datasetVersions.get`
  - `aiplatform. datasetVersions. list`
  - `aiplatform. datasetVersions. restore`

`aiplatform.datasets.*`

  - `aiplatform.datasets.create`
  - `aiplatform.datasets.delete`
  - `aiplatform.datasets.export`
  - `aiplatform.datasets.get`
  - `aiplatform.datasets.import`
  - `aiplatform.datasets.list`
  - `aiplatform.datasets.update`

`aiplatform. deploymentResourcePools.*`

  - `aiplatform. deploymentResourcePools. create`
  - `aiplatform. deploymentResourcePools. delete`
  - `aiplatform. deploymentResourcePools. get`
  - `aiplatform. deploymentResourcePools. list`
  - `aiplatform. deploymentResourcePools. queryDeployedModels`
  - `aiplatform. deploymentResourcePools. update`

`aiplatform. edgeDeploymentJobs.*`

  - `aiplatform. edgeDeploymentJobs. create`
  - `aiplatform. edgeDeploymentJobs. delete`
  - `aiplatform. edgeDeploymentJobs. get`
  - `aiplatform. edgeDeploymentJobs. list`

`aiplatform. edgeDeviceDebugInfo. get`

`aiplatform.edgeDevices.*`

  - `aiplatform.edgeDevices.create`
  - `aiplatform.edgeDevices.delete`
  - `aiplatform.edgeDevices.get`
  - `aiplatform.edgeDevices.list`
  - `aiplatform.edgeDevices.update`

`aiplatform.endpoints.create`

`aiplatform.endpoints.delete`

`aiplatform.endpoints.deploy`

`aiplatform.endpoints.explain`

`aiplatform.endpoints.get`

`aiplatform.endpoints.list`

`aiplatform.endpoints.predict`

`aiplatform.endpoints.undeploy`

`aiplatform.endpoints.update`

`aiplatform.entityTypes.create`

`aiplatform.entityTypes.delete`

`aiplatform. entityTypes. deleteFeatureValues`

`aiplatform. entityTypes. exportFeatureValues`

`aiplatform.entityTypes.get`

`aiplatform. entityTypes. importFeatureValues`

`aiplatform.entityTypes.list`

`aiplatform. entityTypes. readFeatureValues`

`aiplatform. entityTypes. streamingReadFeatureValues`

`aiplatform.entityTypes.update`

`aiplatform. entityTypes. writeFeatureValues`

`aiplatform. evaluationExperiments.*`

  - `aiplatform. evaluationExperiments. create`
  - `aiplatform. evaluationExperiments. delete`
  - `aiplatform. evaluationExperiments. get`
  - `aiplatform. evaluationExperiments. list`
  - `aiplatform. evaluationExperiments. update`

`aiplatform.evaluationItems.*`

  - `aiplatform. evaluationItems. create`
  - `aiplatform. evaluationItems. delete`
  - `aiplatform.evaluationItems.get`
  - `aiplatform. evaluationItems. list`
  - `aiplatform. evaluationItems. update`

`aiplatform.evaluationRuns.*`

  - `aiplatform. evaluationRuns. cancel`
  - `aiplatform. evaluationRuns. create`
  - `aiplatform. evaluationRuns. delete`
  - `aiplatform. evaluationRuns. execute`
  - `aiplatform.evaluationRuns.get`
  - `aiplatform.evaluationRuns.list`
  - `aiplatform. evaluationRuns. update`

`aiplatform.evaluationSets.*`

  - `aiplatform. evaluationSets. create`
  - `aiplatform. evaluationSets. delete`
  - `aiplatform.evaluationSets.get`
  - `aiplatform. evaluationSets. import`
  - `aiplatform.evaluationSets.list`
  - `aiplatform. evaluationSets. update`

`aiplatform.exampleStores.*`

  - `aiplatform. exampleStores. create`
  - `aiplatform. exampleStores. delete`
  - `aiplatform.exampleStores.get`
  - `aiplatform.exampleStores.list`
  - `aiplatform. exampleStores. readExample`
  - `aiplatform. exampleStores. update`
  - `aiplatform. exampleStores. writeExample`

`aiplatform.executions.*`

  - `aiplatform. executions. addExecutionEvents`
  - `aiplatform.executions.create`
  - `aiplatform.executions.delete`
  - `aiplatform.executions.get`
  - `aiplatform.executions.list`
  - `aiplatform. executions. queryExecutionInputsAndOutputs`
  - `aiplatform.executions.update`

`aiplatform.extensions.*`

  - `aiplatform.extensions.delete`
  - `aiplatform.extensions.execute`
  - `aiplatform.extensions.get`
  - `aiplatform.extensions.import`
  - `aiplatform.extensions.list`
  - `aiplatform.extensions.update`

`aiplatform. featureGroups. create`

`aiplatform. featureGroups. delete`

`aiplatform.featureGroups.get`

`aiplatform.featureGroups.list`

`aiplatform. featureGroups. update`

`aiplatform. featureMonitorJobs.*`

  - `aiplatform. featureMonitorJobs. create`
  - `aiplatform. featureMonitorJobs. get`
  - `aiplatform. featureMonitorJobs. list`

`aiplatform.featureMonitors.*`

  - `aiplatform. featureMonitors. create`
  - `aiplatform. featureMonitors. delete`
  - `aiplatform.featureMonitors.get`
  - `aiplatform. featureMonitors. list`
  - `aiplatform. featureMonitors. update`

`aiplatform. featureOnlineStores. create`

`aiplatform. featureOnlineStores. delete`

`aiplatform. featureOnlineStores. get`

`aiplatform. featureOnlineStores. list`

`aiplatform. featureOnlineStores. update`

`aiplatform.featureViewSyncs.*`

  - `aiplatform. featureViewSyncs. get`
  - `aiplatform. featureViewSyncs. list`

`aiplatform.featureViews.create`

`aiplatform.featureViews.delete`

`aiplatform. featureViews. directWrite`

`aiplatform. featureViews. fetchFeatureValues`

`aiplatform.featureViews.get`

`aiplatform.featureViews.list`

`aiplatform. featureViews. searchNearestEntities`

`aiplatform.featureViews.sync`

`aiplatform.featureViews.update`

`aiplatform.features.*`

  - `aiplatform.features.create`
  - `aiplatform.features.delete`
  - `aiplatform.features.get`
  - `aiplatform.features.list`
  - `aiplatform.features.update`

`aiplatform. featurestores. batchReadFeatureValues`

`aiplatform. featurestores. create`

`aiplatform. featurestores. delete`

`aiplatform. featurestores. exportFeatures`

`aiplatform.featurestores.get`

`aiplatform. featurestores. importFeatures`

`aiplatform.featurestores.list`

`aiplatform. featurestores. readFeatures`

`aiplatform. featurestores. update`

`aiplatform. featurestores. writeFeatures`

`aiplatform.humanInTheLoops.*`

  - `aiplatform. humanInTheLoops. cancel`
  - `aiplatform. humanInTheLoops. create`
  - `aiplatform. humanInTheLoops. delete`
  - `aiplatform.humanInTheLoops.get`
  - `aiplatform. humanInTheLoops. list`
  - `aiplatform. humanInTheLoops. queryAnnotationStats`
  - `aiplatform. humanInTheLoops. send`
  - `aiplatform. humanInTheLoops. update`

`aiplatform. hyperparameterTuningJobs.*`

  - `aiplatform. hyperparameterTuningJobs. cancel`
  - `aiplatform. hyperparameterTuningJobs. create`
  - `aiplatform. hyperparameterTuningJobs. delete`
  - `aiplatform. hyperparameterTuningJobs. get`
  - `aiplatform. hyperparameterTuningJobs. list`

`aiplatform.indexEndpoints.*`

  - `aiplatform. indexEndpoints. create`
  - `aiplatform. indexEndpoints. delete`
  - `aiplatform. indexEndpoints. deploy`
  - `aiplatform.indexEndpoints.get`
  - `aiplatform.indexEndpoints.list`
  - `aiplatform. indexEndpoints. queryVectors`
  - `aiplatform. indexEndpoints. undeploy`
  - `aiplatform. indexEndpoints. update`

`aiplatform.indexes.*`

  - `aiplatform.indexes.create`
  - `aiplatform.indexes.delete`
  - `aiplatform.indexes.get`
  - `aiplatform.indexes.list`
  - `aiplatform.indexes.update`

`aiplatform.locations.*`

  - `aiplatform. locations. evaluateInstances`
  - `aiplatform.locations.get`
  - `aiplatform.locations.list`

`aiplatform.memories.*`

  - `aiplatform.memories.create`
  - `aiplatform.memories.delete`
  - `aiplatform.memories.generate`
  - `aiplatform.memories.get`
  - `aiplatform.memories.list`
  - `aiplatform.memories.retrieve`
  - `aiplatform.memories.update`

`aiplatform.memoryRevisions.*`

  - `aiplatform.memoryRevisions.get`
  - `aiplatform. memoryRevisions. list`
  - `aiplatform. memoryRevisions. rollback`

`aiplatform.metadataSchemas.*`

  - `aiplatform. metadataSchemas. create`
  - `aiplatform. metadataSchemas. delete`
  - `aiplatform.metadataSchemas.get`
  - `aiplatform. metadataSchemas. list`

`aiplatform.metadataStores.*`

  - `aiplatform. metadataStores. create`
  - `aiplatform. metadataStores. delete`
  - `aiplatform.metadataStores.get`
  - `aiplatform.metadataStores.list`

`aiplatform. modelDeploymentMonitoringJobs.*`

  - `aiplatform. modelDeploymentMonitoringJobs. create`
  - `aiplatform. modelDeploymentMonitoringJobs. delete`
  - `aiplatform. modelDeploymentMonitoringJobs. get`
  - `aiplatform. modelDeploymentMonitoringJobs. list`
  - `aiplatform. modelDeploymentMonitoringJobs. pause`
  - `aiplatform. modelDeploymentMonitoringJobs. resume`
  - `aiplatform. modelDeploymentMonitoringJobs. searchStatsAnomalies`
  - `aiplatform. modelDeploymentMonitoringJobs. update`

`aiplatform. modelEvaluationSlices.*`

  - `aiplatform. modelEvaluationSlices. get`
  - `aiplatform. modelEvaluationSlices. import`
  - `aiplatform. modelEvaluationSlices. list`

`aiplatform.modelEvaluations.*`

  - `aiplatform. modelEvaluations. exportEvaluatedDataItems`
  - `aiplatform. modelEvaluations. get`
  - `aiplatform. modelEvaluations. import`
  - `aiplatform. modelEvaluations. list`

`aiplatform. modelMonitoringJobs.*`

  - `aiplatform. modelMonitoringJobs. create`
  - `aiplatform. modelMonitoringJobs. delete`
  - `aiplatform. modelMonitoringJobs. get`
  - `aiplatform. modelMonitoringJobs. list`

`aiplatform.modelMonitors.*`

  - `aiplatform. modelMonitors. create`
  - `aiplatform. modelMonitors. delete`
  - `aiplatform.modelMonitors.get`
  - `aiplatform.modelMonitors.list`
  - `aiplatform. modelMonitors. searchModelMonitoringAlerts`
  - `aiplatform. modelMonitors. searchModelMonitoringStats`
  - `aiplatform. modelMonitors. update`

`aiplatform.models.*`

  - `aiplatform.models.delete`
  - `aiplatform.models.export`
  - `aiplatform.models.get`
  - `aiplatform.models.list`
  - `aiplatform.models.update`
  - `aiplatform.models.upload`

`aiplatform.nasJobs.*`

  - `aiplatform.nasJobs.cancel`
  - `aiplatform.nasJobs.create`
  - `aiplatform.nasJobs.delete`
  - `aiplatform.nasJobs.get`
  - `aiplatform.nasJobs.list`

`aiplatform.nasTrialDetails.*`

  - `aiplatform.nasTrialDetails.get`
  - `aiplatform. nasTrialDetails. list`

`aiplatform. notebookExecutionJobs.*`

  - `aiplatform. notebookExecutionJobs. create`
  - `aiplatform. notebookExecutionJobs. delete`
  - `aiplatform. notebookExecutionJobs. get`
  - `aiplatform. notebookExecutionJobs. list`

`aiplatform. notebookRuntimeTemplates. apply`

`aiplatform. notebookRuntimeTemplates. create`

`aiplatform. notebookRuntimeTemplates. delete`

`aiplatform. notebookRuntimeTemplates. get`

`aiplatform. notebookRuntimeTemplates. list`

`aiplatform. notebookRuntimeTemplates. update`

`aiplatform.notebookRuntimes.*`

  - `aiplatform. notebookRuntimes. assign`
  - `aiplatform. notebookRuntimes. delete`
  - `aiplatform. notebookRuntimes. get`
  - `aiplatform. notebookRuntimes. list`
  - `aiplatform. notebookRuntimes. start`
  - `aiplatform. notebookRuntimes. update`
  - `aiplatform. notebookRuntimes. upgrade`

`aiplatform.onlineEvaluators.*`

  - `aiplatform. onlineEvaluators. create`
  - `aiplatform. onlineEvaluators. delete`
  - `aiplatform. onlineEvaluators. get`
  - `aiplatform. onlineEvaluators. list`
  - `aiplatform. onlineEvaluators. update`

`aiplatform.operations.list`

`aiplatform. persistentResources. get`

`aiplatform. persistentResources. list`

`aiplatform.pipelineJobs.*`

  - `aiplatform.pipelineJobs.cancel`
  - `aiplatform.pipelineJobs.create`
  - `aiplatform.pipelineJobs.delete`
  - `aiplatform.pipelineJobs.get`
  - `aiplatform.pipelineJobs.list`

`aiplatform. provisionedThroughputRevisions.*`

  - `aiplatform. provisionedThroughputRevisions. get`
  - `aiplatform. provisionedThroughputRevisions. list`

`aiplatform. provisionedThroughputs. get`

`aiplatform. provisionedThroughputs. list`

`aiplatform.ragCorpora.*`

  - `aiplatform.ragCorpora.create`
  - `aiplatform.ragCorpora.delete`
  - `aiplatform.ragCorpora.get`
  - `aiplatform.ragCorpora.list`
  - `aiplatform.ragCorpora.query`
  - `aiplatform.ragCorpora.update`

`aiplatform. ragEngineConfigs. get`

`aiplatform.ragFiles.*`

  - `aiplatform.ragFiles.delete`
  - `aiplatform.ragFiles.get`
  - `aiplatform.ragFiles.import`
  - `aiplatform.ragFiles.list`
  - `aiplatform.ragFiles.upload`

`aiplatform. reasoningEngineRuntimeRevisions.*`

  - `aiplatform. reasoningEngineRuntimeRevisions. delete`
  - `aiplatform. reasoningEngineRuntimeRevisions. get`
  - `aiplatform. reasoningEngineRuntimeRevisions. list`
  - `aiplatform. reasoningEngineRuntimeRevisions. query`

`aiplatform. reasoningEngines. create`

`aiplatform. reasoningEngines. delete`

`aiplatform. reasoningEngines. get`

`aiplatform. reasoningEngines. list`

`aiplatform. reasoningEngines. query`

`aiplatform. reasoningEngines. update`

`aiplatform. sandboxEnvironments.*`

  - `aiplatform. sandboxEnvironments. create`
  - `aiplatform. sandboxEnvironments. delete`
  - `aiplatform. sandboxEnvironments. execute`
  - `aiplatform. sandboxEnvironments. get`
  - `aiplatform. sandboxEnvironments. list`

`aiplatform.schedules.*`

  - `aiplatform.schedules.create`
  - `aiplatform.schedules.delete`
  - `aiplatform.schedules.get`
  - `aiplatform.schedules.list`
  - `aiplatform.schedules.update`

`aiplatform. semanticGovernancePolicies.*`

  - `aiplatform. semanticGovernancePolicies. create`
  - `aiplatform. semanticGovernancePolicies. delete`
  - `aiplatform. semanticGovernancePolicies. get`
  - `aiplatform. semanticGovernancePolicies. list`
  - `aiplatform. semanticGovernancePolicies. update`

`aiplatform. semanticGovernancePolicyEngine.*`

  - `aiplatform. semanticGovernancePolicyEngine. get`
  - `aiplatform. semanticGovernancePolicyEngine. update`

`aiplatform.sessionEvents.*`

  - `aiplatform. sessionEvents. append`
  - `aiplatform.sessionEvents.list`

`aiplatform.sessions.*`

  - `aiplatform.sessions.create`
  - `aiplatform.sessions.delete`
  - `aiplatform.sessions.get`
  - `aiplatform.sessions.list`
  - `aiplatform.sessions.run`
  - `aiplatform.sessions.update`

`aiplatform.specialistPools.*`

  - `aiplatform. specialistPools. create`
  - `aiplatform. specialistPools. delete`
  - `aiplatform.specialistPools.get`
  - `aiplatform. specialistPools. list`
  - `aiplatform. specialistPools. update`

`aiplatform.studies.*`

  - `aiplatform.studies.create`
  - `aiplatform.studies.delete`
  - `aiplatform.studies.get`
  - `aiplatform.studies.list`
  - `aiplatform.studies.update`

`aiplatform. tensorboardExperiments.*`

  - `aiplatform. tensorboardExperiments. create`
  - `aiplatform. tensorboardExperiments. delete`
  - `aiplatform. tensorboardExperiments. get`
  - `aiplatform. tensorboardExperiments. list`
  - `aiplatform. tensorboardExperiments. update`
  - `aiplatform. tensorboardExperiments. write`

`aiplatform.tensorboardRuns.*`

  - `aiplatform. tensorboardRuns. batchCreate`
  - `aiplatform. tensorboardRuns. create`
  - `aiplatform. tensorboardRuns. delete`
  - `aiplatform.tensorboardRuns.get`
  - `aiplatform. tensorboardRuns. list`
  - `aiplatform. tensorboardRuns. update`
  - `aiplatform. tensorboardRuns. write`

`aiplatform. tensorboardTimeSeries.*`

  - `aiplatform. tensorboardTimeSeries. batchCreate`
  - `aiplatform. tensorboardTimeSeries. batchRead`
  - `aiplatform. tensorboardTimeSeries. create`
  - `aiplatform. tensorboardTimeSeries. delete`
  - `aiplatform. tensorboardTimeSeries. get`
  - `aiplatform. tensorboardTimeSeries. list`
  - `aiplatform. tensorboardTimeSeries. read`
  - `aiplatform. tensorboardTimeSeries. update`

`aiplatform.tensorboards.create`

`aiplatform.tensorboards.delete`

`aiplatform.tensorboards.get`

`aiplatform.tensorboards.list`

`aiplatform.tensorboards.update`

`aiplatform.trainingPipelines.*`

  - `aiplatform. trainingPipelines. cancel`
  - `aiplatform. trainingPipelines. create`
  - `aiplatform. trainingPipelines. delete`
  - `aiplatform. trainingPipelines. get`
  - `aiplatform. trainingPipelines. list`

`aiplatform.trials.*`

  - `aiplatform.trials.create`
  - `aiplatform.trials.delete`
  - `aiplatform.trials.get`
  - `aiplatform.trials.list`
  - `aiplatform.trials.update`

`aiplatform.tuningJobs.*`

  - `aiplatform.tuningJobs.cancel`
  - `aiplatform.tuningJobs.create`
  - `aiplatform.tuningJobs.delete`
  - `aiplatform.tuningJobs.get`
  - `aiplatform.tuningJobs.list`
  - `aiplatform. tuningJobs. optimizePrompt`
  - `aiplatform. tuningJobs. validateReinforcementTuningReward`
  - `aiplatform. tuningJobs. vertexTune`

`artifactregistry. repositories. downloadArtifacts`

`artifactregistry. repositories. get`

`artifactregistry. repositories. list`

`artifactregistry.tags.get`

`artifactregistry.versions.get`

`bigquery.datasets.create`

`bigquery.datasets.get`

`bigquery.jobs.create`

`bigquery.jobs.get`

`bigquery.readsessions.create`

`bigquery.readsessions.getData`

`bigquery.tables.create`

`bigquery.tables.export`

`bigquery.tables.get`

`bigquery.tables.getData`

`bigquery.tables.update`

`bigquery.tables.updateData`

`cloudtrace.traces.list`

`iam.serviceAccounts.get`

`iam. serviceAccounts. getAccessToken`

`iam. serviceAccounts. getOpenIdToken`

`iam. serviceAccounts. implicitDelegation`

`iam.serviceAccounts.list`

`iam.serviceAccounts.signBlob`

`iam.serviceAccounts.signJwt`

`logging.logEntries.create`

`logging.logEntries.route`

`logging.views.access`

`logging.views.get`

`monitoring. metricDescriptors. create`

`monitoring. metricDescriptors. get`

`monitoring. metricDescriptors. list`

`monitoring. monitoredResourceDescriptors.*`

  - `monitoring. monitoredResourceDescriptors. get`
  - `monitoring. monitoredResourceDescriptors. list`

`monitoring.timeSeries.create`

`observability.views.access`

`resourcemanager.projects.get`

`resourcemanager.projects.list`

`servicemanagement. services. report`

`serviceusage.services.use`

`storage.buckets.create`

`storage.buckets.delete`

`storage.buckets.get`

`storage.buckets.list`

`storage.objects.create`

`storage.objects.delete`

`storage.objects.get`

`storage.objects.list`

`storage.objects.update`

#### Vertex AI Extension Service Agent

( `roles/ aiplatform.extensionServiceAgent` )

Gives Vertex AI Extension the permissions it needs to function.

> **Warning:** Do not grant service agent roles to any principals except [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

`aiplatform.endpoints.predict`

`aiplatform.locations.get`

`aiplatform.ragCorpora.query`

`discoveryengine. servingConfigs. search`

`iam. serviceAccounts. getAccessToken`

`iam. serviceAccounts. getOpenIdToken`

`logging.logEntries.create`

`logging.logEntries.route`

`serviceusage.services.use`

`storage.objects.get`

#### AI Platform Notebooks Service Agent

( `roles/ notebooks.serviceAgent` )

Provide access for notebooks service agent to manage notebook instances in user projects

> **Warning:** Do not grant service agent roles to any principals except [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

`aiplatform.customJobs.cancel`

`aiplatform.customJobs.create`

`aiplatform.customJobs.get`

`aiplatform.customJobs.list`

`aiplatform. notebookExecutionJobs.*`

  - `aiplatform. notebookExecutionJobs. create`
  - `aiplatform. notebookExecutionJobs. delete`
  - `aiplatform. notebookExecutionJobs. get`
  - `aiplatform. notebookExecutionJobs. list`

`aiplatform. notebookRuntimes. get`

`aiplatform.operations.list`

`aiplatform.pipelineJobs.create`

`aiplatform.schedules.*`

  - `aiplatform.schedules.create`
  - `aiplatform.schedules.delete`
  - `aiplatform.schedules.get`
  - `aiplatform.schedules.list`
  - `aiplatform.schedules.update`

`backupdr. backupPlanAssociations. createForComputeDisk`

`backupdr. backupPlanAssociations. createForComputeInstance`

`backupdr. backupPlanAssociations. deleteForComputeDisk`

`backupdr. backupPlanAssociations. deleteForComputeInstance`

`backupdr. backupPlanAssociations. fetchForComputeDisk`

`backupdr. backupPlanAssociations. getForComputeDisk`

`backupdr. backupPlanAssociations. list`

`backupdr. backupPlanAssociations. triggerBackupForComputeDisk`

`backupdr. backupPlanAssociations. triggerBackupForComputeInstance`

`backupdr. backupPlanAssociations. updateForComputeDisk`

`backupdr. backupPlanAssociations. updateForComputeInstance`

`backupdr.backupPlans.get`

`backupdr.backupPlans.list`

`backupdr. backupPlans. useForComputeDisk`

`backupdr. backupPlans. useForComputeInstance`

`backupdr.backupVaults.get`

`backupdr.backupVaults.list`

`backupdr.locations.list`

`backupdr.operations.get`

`backupdr.operations.list`

`backupdr. serviceConfig. initialize`

`compute.acceleratorTypes.*`

  - `compute.acceleratorTypes.get`
  - `compute.acceleratorTypes.list`

`compute. addresses. createInternal`

`compute. addresses. deleteInternal`

`compute.addresses.get`

`compute.addresses.list`

`compute. addresses. listEffectiveTags`

`compute. addresses. listTagBindings`

`compute.addresses.use`

`compute.addresses.useInternal`

`compute.autoscalers.*`

  - `compute.autoscalers.create`
  - `compute.autoscalers.delete`
  - `compute.autoscalers.get`
  - `compute.autoscalers.list`
  - `compute.autoscalers.update`

`compute.backendBuckets.get`

`compute. backendBuckets. getIamPolicy`

`compute.backendBuckets.list`

`compute. backendBuckets. listEffectiveTags`

`compute. backendBuckets. listTagBindings`

`compute.backendServices.get`

`compute. backendServices. getIamPolicy`

`compute.backendServices.list`

`compute. backendServices. listEffectiveTags`

`compute. backendServices. listTagBindings`

`compute.commitments.get`

`compute.commitments.list`

`compute. commitments. listEffectiveTags`

`compute. commitments. listTagBindings`

`compute.crossSiteNetworks.get`

`compute.crossSiteNetworks.list`

`compute.diskSettings.get`

`compute.diskTypes.*`

  - `compute.diskTypes.get`
  - `compute.diskTypes.list`

`compute.disks.*`

  - `compute. disks. addResourcePolicies`
  - `compute.disks.create`
  - `compute.disks.createSnapshot`
  - `compute.disks.createTagBinding`
  - `compute.disks.delete`
  - `compute.disks.deleteTagBinding`
  - `compute.disks.get`
  - `compute.disks.getIamPolicy`
  - `compute.disks.list`
  - `compute. disks. listEffectiveTags`
  - `compute.disks.listTagBindings`
  - `compute. disks. removeResourcePolicies`
  - `compute.disks.resize`
  - `compute.disks.setIamPolicy`
  - `compute.disks.setLabels`
  - `compute. disks. startAsyncReplication`
  - `compute. disks. stopAsyncReplication`
  - `compute. disks. stopGroupAsyncReplication`
  - `compute.disks.update`
  - `compute.disks.updateKmsKey`
  - `compute.disks.use`
  - `compute.disks.useReadOnly`

`compute. externalVpnGateways. get`

`compute. externalVpnGateways. list`

`compute. externalVpnGateways. listEffectiveTags`

`compute. externalVpnGateways. listTagBindings`

`compute.firewallPolicies.get`

`compute. firewallPolicies. getIamPolicy`

`compute.firewallPolicies.list`

`compute. firewallPolicies. listEffectiveTags`

`compute. firewallPolicies. listTagBindings`

`compute.firewalls.get`

`compute.firewalls.list`

`compute. firewalls. listEffectiveTags`

`compute. firewalls. listTagBindings`

`compute.forwardingRules.get`

`compute.forwardingRules.list`

`compute. forwardingRules. listEffectiveTags`

`compute. forwardingRules. listTagBindings`

`compute.futureReservations.get`

`compute. futureReservations. getIamPolicy`

`compute. futureReservations. list`

`compute. futureReservations. listEffectiveTags`

`compute. futureReservations. listTagBindings`

`compute.globalAddresses.get`

`compute.globalAddresses.list`

`compute. globalAddresses. listEffectiveTags`

`compute. globalAddresses. listTagBindings`

`compute.globalAddresses.use`

`compute. globalForwardingRules. get`

`compute. globalForwardingRules. list`

`compute. globalForwardingRules. listEffectiveTags`

`compute. globalForwardingRules. listTagBindings`

`compute. globalNetworkEndpointGroups.*`

  - `compute. globalNetworkEndpointGroups. attachNetworkEndpoints`
  - `compute. globalNetworkEndpointGroups. create`
  - `compute. globalNetworkEndpointGroups. createTagBinding`
  - `compute. globalNetworkEndpointGroups. delete`
  - `compute. globalNetworkEndpointGroups. deleteTagBinding`
  - `compute. globalNetworkEndpointGroups. detachNetworkEndpoints`
  - `compute. globalNetworkEndpointGroups. get`
  - `compute. globalNetworkEndpointGroups. list`
  - `compute. globalNetworkEndpointGroups. listEffectiveTags`
  - `compute. globalNetworkEndpointGroups. listTagBindings`
  - `compute. globalNetworkEndpointGroups. use`

`compute.globalOperations.get`

`compute. globalOperations. getIamPolicy`

`compute.globalOperations.list`

`compute. globalPublicDelegatedPrefixes. get`

`compute. globalPublicDelegatedPrefixes. list`

`compute.healthChecks.get`

`compute.healthChecks.list`

`compute. healthChecks. listEffectiveTags`

`compute. healthChecks. listTagBindings`

`compute.hosts.*`

  - `compute.hosts.get`
  - `compute.hosts.getVersion`
  - `compute.hosts.list`

`compute.httpHealthChecks.get`

`compute.httpHealthChecks.list`

`compute. httpHealthChecks. listEffectiveTags`

`compute. httpHealthChecks. listTagBindings`

`compute.httpsHealthChecks.get`

`compute.httpsHealthChecks.list`

`compute. httpsHealthChecks. listEffectiveTags`

`compute. httpsHealthChecks. listTagBindings`

`compute.images.*`

  - `compute.images.create`
  - `compute. images. createTagBinding`
  - `compute.images.delete`
  - `compute. images. deleteTagBinding`
  - `compute.images.deprecate`
  - `compute.images.get`
  - `compute.images.getFromFamily`
  - `compute.images.getIamPolicy`
  - `compute.images.list`
  - `compute. images. listEffectiveTags`
  - `compute.images.listTagBindings`
  - `compute.images.setIamPolicy`
  - `compute.images.setLabels`
  - `compute.images.update`
  - `compute.images.useReadOnly`

`compute. instanceGroupManagers.*`

  - `compute. instanceGroupManagers. create`
  - `compute. instanceGroupManagers. createTagBinding`
  - `compute. instanceGroupManagers. delete`
  - `compute. instanceGroupManagers. deleteTagBinding`
  - `compute. instanceGroupManagers. get`
  - `compute. instanceGroupManagers. list`
  - `compute. instanceGroupManagers. listEffectiveTags`
  - `compute. instanceGroupManagers. listTagBindings`
  - `compute. instanceGroupManagers. update`
  - `compute. instanceGroupManagers. use`

`compute.instanceGroups.*`

  - `compute.instanceGroups.create`
  - `compute. instanceGroups. createTagBinding`
  - `compute.instanceGroups.delete`
  - `compute. instanceGroups. deleteTagBinding`
  - `compute.instanceGroups.get`
  - `compute.instanceGroups.list`
  - `compute. instanceGroups. listEffectiveTags`
  - `compute. instanceGroups. listTagBindings`
  - `compute.instanceGroups.update`
  - `compute.instanceGroups.use`

`compute.instanceSettings.*`

  - `compute.instanceSettings.get`
  - `compute. instanceSettings. update`

`compute.instanceTemplates.*`

  - `compute. instanceTemplates. create`
  - `compute. instanceTemplates. delete`
  - `compute.instanceTemplates.get`
  - `compute. instanceTemplates. getIamPolicy`
  - `compute.instanceTemplates.list`
  - `compute. instanceTemplates. setIamPolicy`
  - `compute. instanceTemplates. useReadOnly`

`compute.instances.*`

  - `compute. instances. addAccessConfig`
  - `compute. instances. addNetworkInterface`
  - `compute. instances. addResourcePolicies`
  - `compute.instances.attachDisk`
  - `compute.instances.create`
  - `compute. instances. createTagBinding`
  - `compute.instances.delete`
  - `compute. instances. deleteAccessConfig`
  - `compute. instances. deleteNetworkInterface`
  - `compute. instances. deleteTagBinding`
  - `compute.instances.detachDisk`
  - `compute.instances.get`
  - `compute. instances. getEffectiveFirewalls`
  - `compute. instances. getGuestAttributes`
  - `compute.instances.getIamPolicy`
  - `compute. instances. getScreenshot`
  - `compute. instances. getSerialPortOutput`
  - `compute. instances. getShieldedInstanceIdentity`
  - `compute. instances. getShieldedVmIdentity`
  - `compute.instances.list`
  - `compute. instances. listEffectiveTags`
  - `compute. instances. listReferrers`
  - `compute. instances. listTagBindings`
  - `compute.instances.osAdminLogin`
  - `compute.instances.osLogin`
  - `compute. instances. pscInterfaceCreate`
  - `compute. instances. removeResourcePolicies`
  - `compute.instances.reset`
  - `compute.instances.resume`
  - `compute. instances. sendDiagnosticInterrupt`
  - `compute. instances. setDeletionProtection`
  - `compute. instances. setDiskAutoDelete`
  - `compute.instances.setIamPolicy`
  - `compute.instances.setLabels`
  - `compute. instances. setMachineResources`
  - `compute. instances. setMachineType`
  - `compute.instances.setMetadata`
  - `compute. instances. setMinCpuPlatform`
  - `compute.instances.setName`
  - `compute. instances. setScheduling`
  - `compute. instances. setSecurityPolicy`
  - `compute. instances. setServiceAccount`
  - `compute. instances. setShieldedInstanceIntegrityPolicy`
  - `compute. instances. setShieldedVmIntegrityPolicy`
  - `compute.instances.setTags`
  - `compute. instances. simulateMaintenanceEvent`
  - `compute.instances.start`
  - `compute. instances. startWithEncryptionKey`
  - `compute.instances.stop`
  - `compute.instances.suspend`
  - `compute.instances.update`
  - `compute. instances. updateAccessConfig`
  - `compute. instances. updateDisplayDevice`
  - `compute. instances. updateNetworkInterface`
  - `compute. instances. updateSecurity`
  - `compute. instances. updateShieldedInstanceConfig`
  - `compute. instances. updateShieldedVmConfig`
  - `compute.instances.use`
  - `compute.instances.useReadOnly`

`compute. instantSnapshotGroups.*`

  - `compute. instantSnapshotGroups. create`
  - `compute. instantSnapshotGroups. delete`
  - `compute. instantSnapshotGroups. get`
  - `compute. instantSnapshotGroups. getIamPolicy`
  - `compute. instantSnapshotGroups. list`
  - `compute. instantSnapshotGroups. setIamPolicy`
  - `compute. instantSnapshotGroups. useReadOnly`

`compute. instantSnapshots. create`

`compute. instantSnapshots. delete`

`compute. instantSnapshots. export`

`compute.instantSnapshots.get`

`compute. instantSnapshots. getIamPolicy`

`compute.instantSnapshots.list`

`compute. instantSnapshots. listEffectiveTags`

`compute. instantSnapshots. listTagBindings`

`compute. instantSnapshots. setIamPolicy`

`compute. instantSnapshots. setLabels`

`compute. instantSnapshots. useReadOnly`

`compute. interconnectAttachmentGroups. get`

`compute. interconnectAttachmentGroups. list`

`compute. interconnectAttachments. get`

`compute. interconnectAttachments. list`

`compute. interconnectAttachments. listEffectiveTags`

`compute. interconnectAttachments. listTagBindings`

`compute.interconnectGroups.get`

`compute. interconnectGroups. list`

`compute. interconnectLocations.*`

  - `compute. interconnectLocations. get`
  - `compute. interconnectLocations. list`

`compute. interconnectRemoteLocations.*`

  - `compute. interconnectRemoteLocations. get`
  - `compute. interconnectRemoteLocations. list`

`compute.interconnects.get`

`compute.interconnects.list`

`compute. interconnects. listEffectiveTags`

`compute. interconnects. listTagBindings`

`compute.licenseCodes.*`

  - `compute.licenseCodes.get`
  - `compute. licenseCodes. getIamPolicy`
  - `compute.licenseCodes.list`
  - `compute. licenseCodes. setIamPolicy`

`compute.licenses.create`

`compute.licenses.delete`

`compute.licenses.get`

`compute.licenses.getIamPolicy`

`compute.licenses.list`

`compute. licenses. listEffectiveTags`

`compute. licenses. listTagBindings`

`compute.licenses.setIamPolicy`

`compute.licenses.update`

`compute.machineImages.create`

`compute.machineImages.delete`

`compute.machineImages.get`

`compute. machineImages. getIamPolicy`

`compute.machineImages.list`

`compute. machineImages. listEffectiveTags`

`compute. machineImages. listTagBindings`

`compute. machineImages. setIamPolicy`

`compute. machineImages. setLabels`

`compute. machineImages. useReadOnly`

`compute.machineTypes.*`

  - `compute.machineTypes.get`
  - `compute.machineTypes.list`

`compute.multiMig.*`

  - `compute.multiMig.create`
  - `compute.multiMig.delete`
  - `compute.multiMig.get`
  - `compute.multiMig.list`

`compute.multiMigMembers.*`

  - `compute.multiMigMembers.get`
  - `compute.multiMigMembers.list`

`compute.networkAttachments.get`

`compute. networkAttachments. getIamPolicy`

`compute. networkAttachments. list`

`compute. networkAttachments. listEffectiveTags`

`compute. networkAttachments. listTagBindings`

`compute. networkEdgeSecurityServices. get`

`compute. networkEdgeSecurityServices. list`

`compute. networkEdgeSecurityServices. listEffectiveTags`

`compute. networkEdgeSecurityServices. listTagBindings`

`compute. networkEndpointGroups.*`

  - `compute. networkEndpointGroups. attachNetworkEndpoints`
  - `compute. networkEndpointGroups. create`
  - `compute. networkEndpointGroups. createTagBinding`
  - `compute. networkEndpointGroups. delete`
  - `compute. networkEndpointGroups. deleteTagBinding`
  - `compute. networkEndpointGroups. detachNetworkEndpoints`
  - `compute. networkEndpointGroups. get`
  - `compute. networkEndpointGroups. list`
  - `compute. networkEndpointGroups. listEffectiveTags`
  - `compute. networkEndpointGroups. listTagBindings`
  - `compute. networkEndpointGroups. use`

`compute.networkProfiles.*`

  - `compute.networkProfiles.get`
  - `compute.networkProfiles.list`

`compute.networks.get`

`compute. networks. getEffectiveFirewalls`

`compute. networks. getRegionEffectiveFirewalls`

`compute.networks.list`

`compute. networks. listEffectiveTags`

`compute. networks. listPeeringRoutes`

`compute. networks. listTagBindings`

`compute.networks.use`

`compute.networks.useExternalIp`

`compute.nodeGroups.get`

`compute. nodeGroups. getIamPolicy`

`compute.nodeGroups.list`

`compute.nodeTemplates.get`

`compute. nodeTemplates. getIamPolicy`

`compute.nodeTemplates.list`

`compute.nodeTypes.*`

  - `compute.nodeTypes.get`
  - `compute.nodeTypes.list`

`compute.orgRolloutPlans.get`

`compute.orgRolloutPlans.list`

`compute.orgRollouts.get`

`compute.orgRollouts.list`

`compute. organizations. listAssociations`

`compute.packetMirrorings.get`

`compute.packetMirrorings.list`

`compute. packetMirrorings. listEffectiveTags`

`compute. packetMirrorings. listTagBindings`

`compute.previewFeatures.get`

`compute.previewFeatures.list`

`compute.projects.get`

`compute. projects. setCommonInstanceMetadata`

`compute. publicAdvertisedPrefixes. get`

`compute. publicAdvertisedPrefixes. list`

`compute. publicDelegatedPrefixes. get`

`compute. publicDelegatedPrefixes. list`

`compute. publicDelegatedPrefixes. listEffectiveTags`

`compute. publicDelegatedPrefixes. listTagBindings`

`compute. regionBackendBuckets. get`

`compute. regionBackendBuckets. getIamPolicy`

`compute. regionBackendBuckets. list`

`compute. regionBackendBuckets. listEffectiveTags`

`compute. regionBackendBuckets. listTagBindings`

`compute. regionBackendServices. get`

`compute. regionBackendServices. getIamPolicy`

`compute. regionBackendServices. list`

`compute. regionBackendServices. listEffectiveTags`

`compute. regionBackendServices. listTagBindings`

`compute. regionCompositeHealthChecks. get`

`compute. regionCompositeHealthChecks. list`

`compute. regionFirewallPolicies. get`

`compute. regionFirewallPolicies. getIamPolicy`

`compute. regionFirewallPolicies. list`

`compute. regionFirewallPolicies. listEffectiveTags`

`compute. regionFirewallPolicies. listTagBindings`

`compute. regionHealthAggregationPolicies. get`

`compute. regionHealthAggregationPolicies. list`

`compute. regionHealthCheckServices. get`

`compute. regionHealthCheckServices. list`

`compute.regionHealthChecks.get`

`compute. regionHealthChecks. list`

`compute. regionHealthChecks. listEffectiveTags`

`compute. regionHealthChecks. listTagBindings`

`compute. regionHealthSources. get`

`compute. regionHealthSources. list`

`compute. regionNetworkEndpointGroups.*`

  - `compute. regionNetworkEndpointGroups. attachNetworkEndpoints`
  - `compute. regionNetworkEndpointGroups. create`
  - `compute. regionNetworkEndpointGroups. createTagBinding`
  - `compute. regionNetworkEndpointGroups. delete`
  - `compute. regionNetworkEndpointGroups. deleteTagBinding`
  - `compute. regionNetworkEndpointGroups. detachNetworkEndpoints`
  - `compute. regionNetworkEndpointGroups. get`
  - `compute. regionNetworkEndpointGroups. list`
  - `compute. regionNetworkEndpointGroups. listEffectiveTags`
  - `compute. regionNetworkEndpointGroups. listTagBindings`
  - `compute. regionNetworkEndpointGroups. use`

`compute. regionNetworkPolicies. get`

`compute. regionNetworkPolicies. list`

`compute. regionNotificationEndpoints. get`

`compute. regionNotificationEndpoints. list`

`compute.regionOperations.get`

`compute. regionOperations. getIamPolicy`

`compute.regionOperations.list`

`compute. regionSecurityPolicies. get`

`compute. regionSecurityPolicies. list`

`compute. regionSecurityPolicies. listEffectiveTags`

`compute. regionSecurityPolicies. listTagBindings`

`compute. regionSslCertificates. get`

`compute. regionSslCertificates. list`

`compute. regionSslCertificates. listEffectiveTags`

`compute. regionSslCertificates. listTagBindings`

`compute.regionSslPolicies.get`

`compute.regionSslPolicies.list`

`compute. regionSslPolicies. listAvailableFeatures`

`compute. regionSslPolicies. listEffectiveTags`

`compute. regionSslPolicies. listTagBindings`

`compute. regionTargetHttpProxies. get`

`compute. regionTargetHttpProxies. list`

`compute. regionTargetHttpProxies. listEffectiveTags`

`compute. regionTargetHttpProxies. listTagBindings`

`compute. regionTargetHttpsProxies. get`

`compute. regionTargetHttpsProxies. list`

`compute. regionTargetHttpsProxies. listEffectiveTags`

`compute. regionTargetHttpsProxies. listTagBindings`

`compute. regionTargetTcpProxies. get`

`compute. regionTargetTcpProxies. list`

`compute. regionTargetTcpProxies. listEffectiveTags`

`compute. regionTargetTcpProxies. listTagBindings`

`compute.regionUrlMaps.get`

`compute.regionUrlMaps.list`

`compute. regionUrlMaps. listEffectiveTags`

`compute. regionUrlMaps. listTagBindings`

`compute.regionUrlMaps.validate`

`compute.regions.*`

  - `compute.regions.get`
  - `compute.regions.list`

`compute.reservationBlocks.get`

`compute.reservationBlocks.list`

`compute.reservationSlots.get`

`compute.reservationSlots.list`

`compute. reservationSubBlocks. get`

`compute. reservationSubBlocks. list`

`compute.reservations.get`

`compute.reservations.list`

`compute. reservations. listEffectiveTags`

`compute. reservations. listTagBindings`

`compute.resourcePolicies.*`

  - `compute. resourcePolicies. create`
  - `compute. resourcePolicies. delete`
  - `compute.resourcePolicies.get`
  - `compute. resourcePolicies. getIamPolicy`
  - `compute.resourcePolicies.list`
  - `compute. resourcePolicies. setIamPolicy`
  - `compute. resourcePolicies. update`
  - `compute.resourcePolicies.use`
  - `compute. resourcePolicies. useReadOnly`

`compute.rolloutPlans.get`

`compute.rolloutPlans.list`

`compute.rollouts.get`

`compute.rollouts.list`

`compute.routers.get`

`compute.routers.getRoutePolicy`

`compute.routers.list`

`compute.routers.listBgpRoutes`

`compute. routers. listEffectiveTags`

`compute. routers. listRoutePolicies`

`compute. routers. listTagBindings`

`compute.routes.get`

`compute.routes.list`

`compute. routes. listEffectiveTags`

`compute.routes.listTagBindings`

`compute.securityPolicies.get`

`compute.securityPolicies.list`

`compute. securityPolicies. listEffectiveTags`

`compute. securityPolicies. listTagBindings`

`compute.serviceAttachments.get`

`compute. serviceAttachments. getIamPolicy`

`compute. serviceAttachments. list`

`compute. serviceAttachments. listEffectiveTags`

`compute. serviceAttachments. listTagBindings`

`compute.snapshotGroups.*`

  - `compute.snapshotGroups.create`
  - `compute.snapshotGroups.delete`
  - `compute.snapshotGroups.get`
  - `compute. snapshotGroups. getIamPolicy`
  - `compute.snapshotGroups.list`
  - `compute. snapshotGroups. setIamPolicy`
  - `compute. snapshotGroups. useReadOnly`

`compute.snapshotSettings.get`

`compute.snapshots.*`

  - `compute.snapshots.create`
  - `compute. snapshots. createTagBinding`
  - `compute.snapshots.delete`
  - `compute. snapshots. deleteTagBinding`
  - `compute.snapshots.get`
  - `compute.snapshots.getIamPolicy`
  - `compute.snapshots.list`
  - `compute. snapshots. listEffectiveTags`
  - `compute. snapshots. listTagBindings`
  - `compute.snapshots.setIamPolicy`
  - `compute.snapshots.setLabels`
  - `compute.snapshots.updateKmsKey`
  - `compute.snapshots.useReadOnly`

`compute.spotAssistants.get`

`compute.sslCertificates.get`

`compute.sslCertificates.list`

`compute. sslCertificates. listEffectiveTags`

`compute. sslCertificates. listTagBindings`

`compute.sslPolicies.get`

`compute.sslPolicies.list`

`compute. sslPolicies. listAvailableFeatures`

`compute. sslPolicies. listEffectiveTags`

`compute. sslPolicies. listTagBindings`

`compute.storagePools.get`

`compute. storagePools. getIamPolicy`

`compute.storagePools.list`

`compute. storagePools. listEffectiveTags`

`compute. storagePools. listTagBindings`

`compute.storagePools.use`

`compute.subnetworks.get`

`compute. subnetworks. getIamPolicy`

`compute.subnetworks.list`

`compute. subnetworks. listEffectiveTags`

`compute. subnetworks. listTagBindings`

`compute.subnetworks.use`

`compute. subnetworks. useExternalIp`

`compute.targetGrpcProxies.get`

`compute.targetGrpcProxies.list`

`compute. targetGrpcProxies. listEffectiveTags`

`compute. targetGrpcProxies. listTagBindings`

`compute.targetHttpProxies.get`

`compute.targetHttpProxies.list`

`compute. targetHttpProxies. listEffectiveTags`

`compute. targetHttpProxies. listTagBindings`

`compute.targetHttpsProxies.get`

`compute. targetHttpsProxies. list`

`compute. targetHttpsProxies. listEffectiveTags`

`compute. targetHttpsProxies. listTagBindings`

`compute.targetInstances.get`

`compute.targetInstances.list`

`compute. targetInstances. listEffectiveTags`

`compute. targetInstances. listTagBindings`

`compute.targetPools.get`

`compute.targetPools.list`

`compute. targetPools. listEffectiveTags`

`compute. targetPools. listTagBindings`

`compute.targetSslProxies.get`

`compute.targetSslProxies.list`

`compute. targetSslProxies. listEffectiveTags`

`compute. targetSslProxies. listTagBindings`

`compute.targetTcpProxies.get`

`compute.targetTcpProxies.list`

`compute. targetTcpProxies. listEffectiveTags`

`compute. targetTcpProxies. listTagBindings`

`compute.targetVpnGateways.get`

`compute.targetVpnGateways.list`

`compute. targetVpnGateways. listEffectiveTags`

`compute. targetVpnGateways. listTagBindings`

`compute.urlMaps.get`

`compute.urlMaps.list`

`compute. urlMaps. listEffectiveTags`

`compute. urlMaps. listTagBindings`

`compute.urlMaps.validate`

`compute. vmExtensionPolicies. get`

`compute. vmExtensionPolicies. list`

`compute.vpnGateways.get`

`compute.vpnGateways.list`

`compute. vpnGateways. listEffectiveTags`

`compute. vpnGateways. listTagBindings`

`compute.vpnTunnels.get`

`compute.vpnTunnels.list`

`compute. vpnTunnels. listEffectiveTags`

`compute. vpnTunnels. listTagBindings`

`compute.wireGroups.get`

`compute.wireGroups.list`

`compute.zoneOperations.get`

`compute. zoneOperations. getIamPolicy`

`compute.zoneOperations.list`

`compute.zones.*`

  - `compute.zones.get`
  - `compute.zones.list`

`dataproc.clusters.get`

`dataproc.clusters.use`

`dataproc.jobs.cancel`

`dataproc.jobs.create`

`dataproc.jobs.delete`

`dataproc.jobs.get`

`dataproc.jobs.list`

`dataproc.jobs.update`

`iam.serviceAccounts.actAs`

`iam.serviceAccounts.get`

`iam. serviceAccounts. getAccessToken`

`iam.serviceAccounts.list`

`ml.jobs.create`

`ml.jobs.get`

`ml.jobs.list`

`notebooks.*`

  - `notebooks.environments.create`
  - `notebooks.environments.delete`
  - `notebooks.environments.get`
  - `notebooks. environments. getIamPolicy`
  - `notebooks.environments.list`
  - `notebooks. environments. setIamPolicy`
  - `notebooks.executions.create`
  - `notebooks.executions.delete`
  - `notebooks.executions.get`
  - `notebooks. executions. getIamPolicy`
  - `notebooks.executions.list`
  - `notebooks. executions. setIamPolicy`
  - `notebooks. instances. checkUpgradability`
  - `notebooks.instances.create`
  - `notebooks.instances.delete`
  - `notebooks.instances.diagnose`
  - `notebooks.instances.get`
  - `notebooks.instances.getHealth`
  - `notebooks. instances. getIamPolicy`
  - `notebooks.instances.list`
  - `notebooks.instances.reset`
  - `notebooks. instances. setAccelerator`
  - `notebooks. instances. setIamPolicy`
  - `notebooks.instances.setLabels`
  - `notebooks. instances. setMachineType`
  - `notebooks.instances.start`
  - `notebooks.instances.stop`
  - `notebooks.instances.update`
  - `notebooks. instances. updateConfig`
  - `notebooks. instances. updateShieldInstanceConfig`
  - `notebooks.instances.upgrade`
  - `notebooks.instances.use`
  - `notebooks.locations.get`
  - `notebooks.locations.list`
  - `notebooks.operations.cancel`
  - `notebooks.operations.delete`
  - `notebooks.operations.get`
  - `notebooks.operations.list`
  - `notebooks.runtimes.create`
  - `notebooks.runtimes.delete`
  - `notebooks.runtimes.diagnose`
  - `notebooks.runtimes.get`
  - `notebooks. runtimes. getIamPolicy`
  - `notebooks.runtimes.list`
  - `notebooks.runtimes.reset`
  - `notebooks. runtimes. setIamPolicy`
  - `notebooks.runtimes.start`
  - `notebooks.runtimes.stop`
  - `notebooks.runtimes.switch`
  - `notebooks.runtimes.update`
  - `notebooks.runtimes.upgrade`
  - `notebooks.schedules.create`
  - `notebooks.schedules.delete`
  - `notebooks.schedules.get`
  - `notebooks. schedules. getIamPolicy`
  - `notebooks.schedules.list`
  - `notebooks. schedules. setIamPolicy`

`resourcemanager.projects.get`

`resourcemanager.projects.list`

`serviceusage. consumerpolicy. analyze`

`serviceusage. consumerpolicy. get`

`serviceusage. effectivepolicy. get`

`serviceusage.groups.*`

  - `serviceusage.groups.list`
  - `serviceusage. groups. listExpandedMembers`
  - `serviceusage. groups. listMembers`

`serviceusage.quotas.get`

`serviceusage.services.get`

`serviceusage.services.list`

`serviceusage.values.test`

## Grant Agent Platform service agents access to other resources

Sometimes you need to grant additional roles to an Agent Platform service agent. For example, if you need Agent Platform to access a Cloud Storage bucket in a different project, you'll need to grant one or more additional roles to the service agent.

> **Note:** If you want your custom training code to obtain an OAuth 2.0 access token with the `https://www.googleapis.com/auth/cloud-platform` scope, then you must use a [custom service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account) for training. You can't give this level of access to the Gemini Enterprise Agent Platform Custom Code Service Agent.

### Role addition requirements for BigQuery

The following table describes the required additional roles needed to be added to the Agent Platform Service Agent for BigQuery tables or view in a different project or backed by an external data source.

The term *home project* refers to the project where the Agent Platform dataset or model is located. The term *different project* refers to any other project.

| Table type                                                                                                                  | Table project     | Data source project | Role addition required                                                                                                                                                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Native BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro)                                           | Home project      | N/A                 | None.                                                                                                                                                                                                                                                                                                                                                           |
| [Native BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables-intro)                                           | Different project | N/A                 | `BigQuery Data Viewer` for different project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .                                                                                                                                                                          |
| [BigQuery view](https://docs.cloud.google.com/bigquery/docs/views)                                                          | Home project      | N/A                 | None.                                                                                                                                                                                                                                                                                                                                                           |
| [BigQuery view](https://docs.cloud.google.com/bigquery/docs/views)                                                          | Different project | N/A                 | `BigQuery Data Viewer` for different project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .                                                                                                                                                                          |
| [External BigQuery data source backed by Bigtable](https://docs.cloud.google.com/bigquery/external-data-bigtable)           | Home project      | Home project        | `Bigtable Reader` for home project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#home-project) .                                                                                                                                                                                         |
| [External BigQuery data source backed by Bigtable](https://docs.cloud.google.com/bigquery/external-data-bigtable)           | Home project      | Different project   | `Bigtable Reader` for different project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .                                                                                                                                                                               |
| [External BigQuery data source backed by Bigtable](https://docs.cloud.google.com/bigquery/external-data-bigtable)           | Different project | Different project   | `BigQuery Reader` and `Bigtable Reader` for different project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .                                                                                                                                                         |
| [External BigQuery data source backed by Cloud Storage](https://docs.cloud.google.com/bigquery/external-data-cloud-storage) | Home project      | Home project        | None.                                                                                                                                                                                                                                                                                                                                                           |
| [External BigQuery data source backed by Cloud Storage](https://docs.cloud.google.com/bigquery/external-data-cloud-storage) | Home project      | Different project   | `Storage Object Viewer` for different project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .                                                                                                                                                                         |
| [External BigQuery data source backed by Cloud Storage](https://docs.cloud.google.com/bigquery/external-data-cloud-storage) | Different project | Different project   | `Storage Object Viewer` and `BigQuery Data Viewer` for different project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .                                                                                                                                              |
| [External BigQuery data source backed by Google Sheets](https://docs.cloud.google.com/bigquery/external-data-drive)         | Home project      | N/A                 | Share your Sheets file with the Agent Platform service account. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#share-sheets) .                                                                                                                                                             |
| [External BigQuery data source backed by Google Sheets](https://docs.cloud.google.com/bigquery/external-data-drive)         | Different project | N/A                 | [`BigQuery Reader` for different project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) and [share your Sheets file with the Agent Platform service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#share-sheets) . |

### Role addition requirements for Cloud Storage

If you are accessing data in a Cloud Storage bucket in a different project, you must give the `Storage > Storage Object Viewer` role to Agent Platform in that project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .

If you are using a Cloud Storage bucket to receive data from your local computer for an import operation, and the bucket is in a different project than Google Cloud project, you must give the `Storage > Storage Object Creator` role to Agent Platform in that project. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) .

### Grant access to Agent Platform to resources in your home project

To grant additional roles to a service agent for Agent Platform in your home project:

1.  Go to the **IAM** page of the Google Cloud console for your home project.

2.  Select the **Include Google-provided role grants** checkbox.

3.  Determine the [service agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) you want to grant the permissions to and click the edit pencil icon.
    
    You can filter for **Principal:@gcp-sa-aiplatform-cc.iam.gserviceaccount.com** to find the Agent Platform service agents.

4.  Grant the required roles to the service agent and save your changes.

### Grant access to Agent Platform to resources in a different project

When you use data sources or destinations in a different project, you must give the Agent Platform service agent permissions in that project. The Agent Platform service agent is created after you start the first asynchronous job (for example, creating an endpoint). You can also explicitly create the Agent Platform service agent. For more information, see [gcloud beta services identity create](https://cloud.google.com/sdk/gcloud/reference/beta/services/identity/create) . This Google Cloud CLI command creates the primary service agent and the custom code service agent. However, only the primary service agent is returned in the response.

To add permissions to Agent Platform in a different project:

1.  Go to the **IAM** page of the Google Cloud console for your home project (the project where you are using Agent Platform).

2.  Select the **Include Google-provided role grants** checkbox.

3.  Determine the [service agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) you want to grant the permissions to and copy its email address (listed under **Principal** ).
    
    You can filter for **Principal:@gcp-sa-aiplatform-cc.iam.gserviceaccount.com** to find the Agent Platform service agents.

4.  Change projects to the project where you need to grant the permissions.

5.  Click **Add** , and enter the email address in **New principals** .

6.  Add all required roles and click **Save** .

### Provide access to Google Sheets

If you use an external BigQuery data source backed by Google Sheets, you must share your sheet with the Agent Platform service account. The Agent Platform service account is created after you start the first asynchronous job (for example, creating an endpoint). You can also explicitly create the Agent Platform service account by using gcloud CLI by following [this instruction](https://cloud.google.com/sdk/gcloud/reference/beta/services/identity/create) .

To authorize Agent Platform to access your Sheets file:

1.  Go to the **IAM** page of the Google Cloud console.

2.  Look for the service account with the name `Agent Platform Service Agent` and copy its email address (listed under **Principal** ).

3.  Open your Sheets file and share it with that address.

## What's next

  - [Learn more about IAM](https://docs.cloud.google.com/iam/docs) .
  - [Learn about specific IAM permissions and the operations they support](https://docs.cloud.google.com/vertex-ai/docs/general/iam-permissions) .
  - To learn about recommended ways to set up a project for a team, see [Set up a project for a team](https://docs.cloud.google.com/vertex-ai/docs/general/set-up-project) .
  - [Get an overview of Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/start/introduction-unified-platform) .
