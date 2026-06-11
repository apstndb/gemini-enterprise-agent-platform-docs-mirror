---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/iam-permissions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/iam-permissions
title: Gemini Enterprise Agent Platform IAM permissions
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The following table lists common Agent Platform operations and the permissions that they require.

To determine if one or more **permissions** are included in a [Gemini Enterprise Agent Platform IAM role](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) , you can use one of the following methods:

  - The [`gcloud iam roles describe`](https://docs.cloud.google.com/sdk/gcloud/reference/iam/roles/describe) command
  - The [`roles.get()`](https://docs.cloud.google.com/iam/reference/rest/v1/roles/get) method in the IAM API

  

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Resource</th>
<th>Operation</th>
<th>Permissions needed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>batchPredictionJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/cancel">Cancel a batchPredictionJob</a></td>
<td><ul>
<li>aiplatform.batchPredictionJobs.cancel (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>batchPredictionJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/create">Create a batchPredictionJob</a></td>
<td><ul>
<li>aiplatform.batchPredictionJobs.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>batchPredictionJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/delete">Delete a batchPredictionJob</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.batchPredictionJobs.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.batchPredictionJobs.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.batchPredictionJobs.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.batchPredictionJobs.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.batchPredictionJobs.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>batchPredictionJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/get">Get a batchPredictionJob</a></td>
<td><ul>
<li>aiplatform.batchPredictionJobs.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>batchPredictionJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/list">List a batchPredictionJob</a></td>
<td><ul>
<li>aiplatform.batchPredictionJobs.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>customJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/cancel">Cancel a customJob</a></td>
<td><ul>
<li>aiplatform.customJobs.cancel (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>customJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/create">Create a customJob</a></td>
<td><ul>
<li>aiplatform.customJobs.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>customJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/delete">Delete a customJob</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.customJobs.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.customJobs.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.customJobs.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.customJobs.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.customJobs.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>customJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/get">Get a customJob</a></td>
<td><ul>
<li>aiplatform.customJobs.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>customJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/list">List a customJob</a></td>
<td><ul>
<li>aiplatform.customJobs.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/create">Create a dataset</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.datasets.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/delete">Delete a dataset</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.datasets.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export">Export a dataset</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.datasets.export (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.export (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/get">Get a dataset</a></td>
<td><ul>
<li>aiplatform.datasets.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/import">Import a dataset</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.datasets.import (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.import (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/list">List a dataset</a></td>
<td><ul>
<li>aiplatform.datasets.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/patch">Update a dataset</a></td>
<td><ul>
<li>aiplatform.datasets.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets.annotationSpecs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.annotationSpecs/get">Get a dataset's annotationSpecs</a></td>
<td><ul>
<li>aiplatform.annotationSpecs.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets.dataItems</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.dataItems/list">List a dataset's dataItems</a></td>
<td><ul>
<li>aiplatform.dataItems.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets.dataItems.annotations</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.dataItems.annotations/list">List a dataset.dataItems.annotations</a></td>
<td><ul>
<li>aiplatform.annotations.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets.savedQueries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.savedQueries/list">Lists SavedQueries in a Dataset.</a></td>
<td><ul>
<li>aiplatform.datasets.get (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/create">Create an endpoint</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.endpoints.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.endpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.endpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.endpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.endpoints.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/delete">Delete an endpoint</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.endpoints.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.endpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.endpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.endpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.endpoints.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel">Deploy model to an endpoint</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.endpoints.deploy (permission needed on the <code dir="ltr" translate="no">endpoint</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.endpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.endpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.endpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.endpoints.deploy (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain">Explain an endpoint</a></td>
<td><ul>
<li>aiplatform.endpoints.explain (permission needed on the <code dir="ltr" translate="no">endpoint</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/get">Get an endpoint</a></td>
<td><ul>
<li>aiplatform.endpoints.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/list">List an endpoint</a></td>
<td><ul>
<li>aiplatform.endpoints.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/patch">Update an endpoint</a></td>
<td><ul>
<li>aiplatform.endpoints.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict">Predict an endpoint</a></td>
<td><ul>
<li>aiplatform.endpoints.predict (permission needed on the <code dir="ltr" translate="no">endpoint</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>endpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict">Perform an online prediction with an arbitrary HTTP payload.</a></td>
<td><ul>
<li>aiplatform.endpoints.predict (permission needed on the <code dir="ltr" translate="no">endpoint</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>endpoints</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/undeployModel">Undeploy a model to an endpoint</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.endpoints.undeploy (permission needed on the <code dir="ltr" translate="no">endpoint</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.endpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.endpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.endpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.endpoints.undeploy (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/batchReadFeatureValues">Batch reads Feature values from a Featurestore.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.featurestores.batchReadFeatureValues (permission needed on the <code dir="ltr" translate="no">featurestore</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.batchReadFeatureValues (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/create">Creates a new Featurestore in a given project and location.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.featurestores.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/delete">Deletes a single Featurestore.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.featurestores.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/get">Gets details of a single Featurestore.</a></td>
<td><ul>
<li>aiplatform.featurestores.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/list">Lists Featurestores in a given project and location.</a></td>
<td><ul>
<li>aiplatform.featurestores.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/patch">Updates the parameters of a single Featurestore.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.featurestores.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/searchFeatures">Searches Features matching a query in a given project.</a></td>
<td><ul>
<li>aiplatform.features.list (permission needed on the <code dir="ltr" translate="no">location</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/create">Creates a new EntityType in a given Featurestore.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.entityTypes.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/delete">Deletes a single EntityType.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.entityTypes.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/exportFeatureValues">Exports Feature values from all the entities of a target EntityType.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.entityTypes.exportFeatureValues (permission needed on the <code dir="ltr" translate="no">entityType</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.entityTypes.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.entityTypes.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.entityTypes.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.entityTypes.exportFeatureValues (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/get">Gets details of a single EntityType.</a></td>
<td><ul>
<li>aiplatform.entityTypes.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/importFeatureValues">Imports Feature values into the Featurestore from a source storage.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.entityTypes.importFeatureValues (permission needed on the <code dir="ltr" translate="no">entityType</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.entityTypes.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.entityTypes.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.entityTypes.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.entityTypes.importFeatureValues (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/list">Lists EntityTypes in a given Featurestore.</a></td>
<td><ul>
<li>aiplatform.entityTypes.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/patch">Updates the parameters of a single EntityType.</a></td>
<td><ul>
<li>aiplatform.entityTypes.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/readFeatureValues">Reads Feature values of a specific entity of an EntityType.</a></td>
<td><ul>
<li>aiplatform.entityTypes.readFeatureValues (permission needed on the <code dir="ltr" translate="no">entityType</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/streamingReadFeatureValues">Reads Feature values for multiple entities.</a></td>
<td><ul>
<li>aiplatform.entityTypes.streamingReadFeatureValues (permission needed on the <code dir="ltr" translate="no">entityType</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes.features</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/batchCreate">Creates a batch of Features in a given EntityType.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.features.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes.features</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/create">Creates a new Feature in a given EntityType.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.features.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes.features</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/delete">Deletes a single Feature.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.features.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes.features</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/get">Gets details of a single Feature.</a></td>
<td><ul>
<li>aiplatform.features.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>featurestores.entityTypes.features</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/list">Lists Features in a given EntityType.</a></td>
<td><ul>
<li>aiplatform.features.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores.entityTypes.features</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/patch">Updates the paramters of a single Feature</a></td>
<td><ul>
<li>aiplatform.features.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>hyperparameterTuningJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/cancel">Cancel a hyperparameterTuningJob</a></td>
<td><ul>
<li>aiplatform.hyperparameterTuningJobs.cancel (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>hyperparameterTuningJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/create">Create a hyperparameterTuningJob</a></td>
<td><ul>
<li>aiplatform.hyperparameterTuningJobs.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>hyperparameterTuningJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/delete">Delete a hyperparameterTuningJob</a></td>
<td><ul>
<li>aiplatform.hyperparameterTuningJobs.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>hyperparameterTuningJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/get">Get a hyperparameterTuningJob</a></td>
<td><ul>
<li>aiplatform.hyperparameterTuningJobs.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>hyperparameterTuningJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/list">List a hyperparameterTuningJob</a></td>
<td><ul>
<li>aiplatform.hyperparameterTuningJobs.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/create">Creates an IndexEndpoint.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexEndpoints.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexEndpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/delete">Deletes an IndexEndpoint.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexEndpoints.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexEndpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/deployIndex">Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexEndpoints.deploy (permission needed on the <code dir="ltr" translate="no">indexEndpoint</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexEndpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/get">Gets an IndexEndpoint.</a></td>
<td><ul>
<li>aiplatform.indexEndpoints.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/list">Lists IndexEndpoints in a Location.</a></td>
<td><ul>
<li>aiplatform.indexEndpoints.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/mutateDeployedIndex">Update an existing DeployedIndex under an IndexEndpoint.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexEndpoints.deploy (permission needed on the <code dir="ltr" translate="no">indexEndpoint</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexEndpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/patch">Updates an IndexEndpoint.</a></td>
<td><ul>
<li>aiplatform.indexEndpoints.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>indexEndpoints</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/undeployIndex">Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexEndpoints.undeploy (permission needed on the <code dir="ltr" translate="no">indexEndpoint</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexEndpoints.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexEndpoints.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/create">Creates an Index.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexes.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexes.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexes.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>indexes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/delete">Deletes an Index.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexes.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexes.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexes.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/get">Gets an Index.</a></td>
<td><ul>
<li>aiplatform.indexes.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>indexes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/list">Lists Indexes in a Location.</a></td>
<td><ul>
<li>aiplatform.indexes.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>indexes</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/patch">Updates an Index.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.indexes.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexes.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexes.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/create">Initializes a MetadataStore, including allocation of resources.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.metadataStores.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/delete">Deletes a single MetadataStore and all its child resources (Artifacts, Executions, and Contexts).</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.metadataStores.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/get">Retrieves a specific MetadataStore.</a></td>
<td><ul>
<li>aiplatform.metadataStores.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list">Lists MetadataStores for a Location.</a></td>
<td><ul>
<li>aiplatform.metadataStores.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/create">Creates an Artifact associated with a MetadataStore.</a></td>
<td><ul>
<li>aiplatform.artifacts.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/delete">Deletes an Artifact.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.artifacts.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.artifacts.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.artifacts.delete (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.artifacts.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.artifacts.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/get">Retrieves a specific Artifact.</a></td>
<td><ul>
<li>aiplatform.artifacts.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/list">Lists Artifacts in the MetadataStore.</a></td>
<td><ul>
<li>aiplatform.artifacts.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/patch">Updates a stored Artifact.</a></td>
<td><ul>
<li>aiplatform.artifacts.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/purge">Purges Artifacts.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.artifacts.delete (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.artifacts.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.artifacts.delete (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.artifacts.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.artifacts.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.artifacts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/queryArtifactLineageSubgraph">Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.</a></td>
<td><ul>
<li>aiplatform.artifacts.get (permission needed on the <code dir="ltr" translate="no">artifact</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/addContextArtifactsAndExecutions">Adds a set of Artifacts and Executions to a Context.</a></td>
<td><ul>
<li>aiplatform.contexts.addContextArtifactsAndExecutions (permission needed on the <code dir="ltr" translate="no">context</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/addContextChildren">Adds a set of Contexts as children to a parent Context.</a></td>
<td><ul>
<li>aiplatform.contexts.addContextChildren (permission needed on the <code dir="ltr" translate="no">context</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/create">Creates a Context associated with a MetadataStore.</a></td>
<td><ul>
<li>aiplatform.contexts.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/delete">Deletes a stored Context.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.contexts.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.contexts.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.contexts.delete (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.contexts.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.contexts.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/get">Retrieves a specific Context.</a></td>
<td><ul>
<li>aiplatform.contexts.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/list">Lists Contexts on the MetadataStore.</a></td>
<td><ul>
<li>aiplatform.contexts.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/patch">Updates a stored Context.</a></td>
<td><ul>
<li>aiplatform.contexts.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/purge">Purges Contexts.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.contexts.delete (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.contexts.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.contexts.delete (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.contexts.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.contexts.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.contexts</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/queryContextLineageSubgraph">Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.</a></td>
<td><ul>
<li>aiplatform.contexts.queryContextLineageSubgraph (permission needed on the <code dir="ltr" translate="no">context</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/addExecutionEvents">Adds Events to the specified Execution.</a></td>
<td><ul>
<li>aiplatform.executions.addExecutionEvents (permission needed on the <code dir="ltr" translate="no">execution</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/create">Creates an Execution associated with a MetadataStore.</a></td>
<td><ul>
<li>aiplatform.executions.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/delete">Deletes an Execution.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.executions.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.executions.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.executions.delete (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.executions.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.executions.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/get">Retrieves a specific Execution.</a></td>
<td><ul>
<li>aiplatform.executions.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/list">Lists Executions in the MetadataStore.</a></td>
<td><ul>
<li>aiplatform.executions.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/patch">Updates a stored Execution.</a></td>
<td><ul>
<li>aiplatform.executions.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/purge">Purges Executions.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.executions.delete (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.executions.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.executions.delete (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.executions.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.executions.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.executions</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/queryExecutionInputsAndOutputs">Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting Events.</a></td>
<td><ul>
<li>aiplatform.executions.queryExecutionInputsAndOutputs (permission needed on the <code dir="ltr" translate="no">execution</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.metadataSchemas</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/create">Creates a MetadataSchema.</a></td>
<td><ul>
<li>aiplatform.metadataSchemas.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>metadataStores.metadataSchemas</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/get">Retrieves a specific MetadataSchema.</a></td>
<td><ul>
<li>aiplatform.metadataSchemas.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>metadataStores.metadataSchemas</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/list">Lists MetadataSchemas.</a></td>
<td><ul>
<li>aiplatform.metadataSchemas.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>migratableResources</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/batchMigrate">Batchmigrate a migratableResource</a></td>
<td><ul>
<li>aiplatform.migratableResources.migrate (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>migratableResources</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.migratableResources/search">Search a migratableResource</a></td>
<td><ul>
<li>aiplatform.migratableResources.search (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/create">Creates a ModelDeploymentMonitoringJob.</a></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/delete">Deletes a ModelDeploymentMonitoringJob.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.indexes.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.indexes.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.indexes.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/get">Gets a ModelDeploymentMonitoringJob.</a></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/list">Lists ModelDeploymentMonitoringJobs in a Location.</a></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/patch">Updates a ModelDeploymentMonitoringJob.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.modelDeploymentMonitoringJobs.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.modelDeploymentMonitoringJobs.update (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/pause">Pauses a ModelDeploymentMonitoringJob.</a></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.pause (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/resume">Resumes a paused ModelDeploymentMonitoringJob.</a></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.resume (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>modelDeploymentMonitoringJobs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies">Searches Model Monitoring Statistics generated within a given time window.</a></td>
<td><ul>
<li>aiplatform.modelDeploymentMonitoringJobs.searchStatsAnomalies (permission needed on the <code dir="ltr" translate="no">modelDeploymentMonitoringJob</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>models</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/delete">Delete a model</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.models.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.models.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.models.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.models.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.models.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>models</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export">Export a model</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.models.export (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.models.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.models.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.models.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.models.export (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>models</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/get">Get a model</a></td>
<td><ul>
<li>aiplatform.models.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>models</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/list">List a model</a></td>
<td><ul>
<li>aiplatform.models.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>models</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/patch">Update a model</a></td>
<td><ul>
<li>aiplatform.models.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>models</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/upload">Upload a model</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.models.upload (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.models.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.models.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.models.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.models.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>models.evaluations</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/get">Get a model evaluation</a></td>
<td><ul>
<li>aiplatform.modelEvaluations.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>models.evaluations</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/list">List a model evaluation</a></td>
<td><ul>
<li>aiplatform.modelEvaluations.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>models.evaluations.slices</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/get">Get a model evaluations slice</a></td>
<td><ul>
<li>aiplatform.modelEvaluationSlices.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>models.evaluations.slices</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list">List a model evaluations slice</a></td>
<td><ul>
<li>aiplatform.modelEvaluationSlices.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>pipelineJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/cancel">Cancel a pipelineJob</a></td>
<td><ul>
<li>aiplatform.pipelineJobs.cancel (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>pipelineJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/create">Create a pipelineJob</a></td>
<td><ul>
<li>aiplatform.pipelineJobs.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>pipelineJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/delete">Delete a pipelineJob</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.pipelineJobs.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.pipelinejobs.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.pipelinejobs.get (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>pipelineJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/get">Get a pipelineJob</a></td>
<td><ul>
<li>aiplatform.pipelineJobs.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>pipelineJobs</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/list">List a pipelineJob</a></td>
<td><ul>
<li>aiplatform.pipelineJobs.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>specialistPools</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/create">Create a specialistPool</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.specialistPools.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.specialistPools.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.specialistPools.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.specialistPools.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.specialistPools.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>specialistPools</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/delete">Delete a specialistPool</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.specialistPools.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.specialistPools.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.specialistPools.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.specialistPools.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.specialistPools.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>specialistPools</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/get">Get a specialistPool</a></td>
<td><ul>
<li>aiplatform.specialistPools.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>specialistPools</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/list">List a specialistPool</a></td>
<td><ul>
<li>aiplatform.specialistPools.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>specialistPools</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/patch">Update a specialistPool</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.specialistPools.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.specialistPools.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.specialistPools.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.specialistPools.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.specialistPools.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/create">Creates a Study.</a></td>
<td><ul>
<li>aiplatform.studies.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/delete">Deletes a Study.</a></td>
<td><ul>
<li>aiplatform.studies.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/get">Gets a Study by name.</a></td>
<td><ul>
<li>aiplatform.studies.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list">Lists all the studies in a region for an associated project.</a></td>
<td><ul>
<li>aiplatform.studies.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/lookup">Looks a study up using the user-defined displayName field instead of the fully qualified resource name.</a></td>
<td><ul>
<li>aiplatform.studies.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/addTrialMeasurement">Adds a measurement of the objective metrics to a Trial.</a></td>
<td><ul>
<li>aiplatform.trials.update (permission needed on the <code dir="ltr" translate="no">trialName</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/checkTrialEarlyStoppingState">Checks whether a Trial should stop or not.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.trials.get (permission needed on the <code dir="ltr" translate="no">trialName</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.trials.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.trials.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.trials.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.trials.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/complete">Marks a Trial as complete.</a></td>
<td><ul>
<li>aiplatform.trials.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/create">Adds a user provided Trial to a Study.</a></td>
<td><ul>
<li>aiplatform.trials.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/delete">Deletes a Trial.</a></td>
<td><ul>
<li>aiplatform.trials.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/get">Gets a Trial.</a></td>
<td><ul>
<li>aiplatform.trials.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/list">Lists the Trials associated with a Study.</a></td>
<td><ul>
<li>aiplatform.trials.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/listOptimalTrials">Lists the pareto-optimal Trials for multi-objective Study or the optimal Trials for single-objective Study.</a></td>
<td><ul>
<li>aiplatform.trials.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/stop">Stops a Trial.</a></td>
<td><ul>
<li>aiplatform.trials.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>studies.trials</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/suggest">Adds one or more Trials to a Study, with parameter values suggested by Vertex AI Vizier.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.trials.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.studies.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.studies.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.studies.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.studies.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/create">Creates a Tensorboard.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.tensorboards.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/delete">Deletes a Tensorboard.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.tensorboards.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.tensorboardRuns.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/get">Gets a Tensorboard.</a></td>
<td><ul>
<li>aiplatform.tensorboards.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/list">Lists Tensorboards in a Location.</a></td>
<td><ul>
<li>aiplatform.tensorboards.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/patch">Updates a Tensorboard.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.tensorboards.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.tensorboards.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.tensorboards.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.tensorboards.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.tensorboards.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/create">Creates a TensorboardExperiment.</a></td>
<td><ul>
<li>aiplatform.tensorboardExperiments.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/delete">Deletes a TensorboardExperiment.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.tensorboardExperiments.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.tensorboardExperiments.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.tensorboardExperiments.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.tensorboardExperiments.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.tensorboardExperiments.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/get">Gets a TensorboardExperiment.</a></td>
<td><ul>
<li>aiplatform.tensorboardExperiments.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/list">Lists TensorboardExperiments in a Location</a></td>
<td><ul>
<li>aiplatform.tensorboardExperiments.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/patch">Updates a TensorboardExperiment.</a></td>
<td><ul>
<li>aiplatform.tensorboardExperiments.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/write">Write time series data points of multiple TensorboardTimeSeries in multiple TensorboardRun's.</a></td>
<td><ul>
<li>aiplatform.tensorboardExperiments.write (permission needed on the <code dir="ltr" translate="no">tensorboardExperiment</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate">Batch create TensorboardRuns.</a></td>
<td><ul>
<li>aiplatform.tensorboardRuns.batchCreate (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/create">Creates a TensorboardRun.</a></td>
<td><ul>
<li>aiplatform.tensorboardRuns.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/delete">Deletes a TensorboardRun.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.tensorboardRuns.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.tensorboardRuns.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/get">Gets a TensorboardRun.</a></td>
<td><ul>
<li>aiplatform.tensorboardRuns.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/list">Lists TensorboardRuns in a Location.</a></td>
<td><ul>
<li>aiplatform.tensorboardRuns.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/patch">Updates a TensorboardRun.</a></td>
<td><ul>
<li>aiplatform.tensorboardRuns.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/write">Write time series data points into multiple TensorboardTimeSeries under a TensorboardRun.</a></td>
<td><ul>
<li>aiplatform.tensorboardRuns.write (permission needed on the <code dir="ltr" translate="no">tensorboardRun</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate">Batch create TensorboardTimeSeries that belong to a TensorboardExperiment.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.batchCreate (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/batchRead">Reads multiple TensorboardTimeSeries' data.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.batchRead (permission needed on the <code dir="ltr" translate="no">tensorboard</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/create">Creates a TensorboardTimeSeries.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/delete">Deletes a TensorboardTimeSeries.</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.tensorboardRuns.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.tensorboardRuns.update (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/exportTensorboardTimeSeries">Exports a TensorboardTimeSeries' data.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.read (permission needed on the <code dir="ltr" translate="no">tensorboardTimeSeries</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/get">Gets a TensorboardTimeSeries.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/list">Lists TensorboardTimeSeries in a Location.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/patch">Updates a TensorboardTimeSeries.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.update (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/read">Reads a TensorboardTimeSeries' data.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.read (permission needed on the <code dir="ltr" translate="no">tensorboardTimeSeries</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>tensorboards.experiments.runs.timeSeries</td>
<td><a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries/readBlobData">Gets bytes of TensorboardBlobs.</a></td>
<td><ul>
<li>aiplatform.tensorboardTimeSeries.read (permission needed on the <code dir="ltr" translate="no">timeSeries</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>trainingPipelines</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/cancel">Cancel a trainingPipeline</a></td>
<td><ul>
<li>aiplatform.trainingPipelines.cancel (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>trainingPipelines</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create">Create a trainingPipeline</a></td>
<td><ul>
<li>aiplatform.trainingPipelines.create (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>trainingPipelines</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/delete">Delete a trainingPipeline</a> <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><ul>
<li>aiplatform.trainingPipelines.delete (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul>
<br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.trainingPipelines.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.trainingPipelines.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.trainingPipelines.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.trainingPipelines.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>trainingPipelines</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/get">Get a trainingPipeline</a></td>
<td><ul>
<li>aiplatform.trainingPipelines.get (permission needed on the <code dir="ltr" translate="no">name</code> resource)</li>
</ul></td>
</tr>
<tr class="even">
<td>trainingPipelines</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/list">List a trainingPipeline</a></td>
<td><ul>
<li>aiplatform.trainingPipelines.list (permission needed on the <code dir="ltr" translate="no">parent</code> resource)</li>
</ul></td>
</tr>
<tr class="odd">
<td>N/A</td>
<td>Generic delete operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td>Delete data item operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores</td>
<td>Import features operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.featurestores.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.featurestores.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.featurestores.importFeatures (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td>Delete annotation operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets</td>
<td>Batch delete DataItems operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td>Generate stats operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>datasets</td>
<td>Delete AnnotationSpec operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>hyperparameterTuningJobs</td>
<td>Delete HP tuning job <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.hyperparameterTuningJobs.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.hyperparameterTuningJobs.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.hyperparameterTuningJobs.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.hyperparameterTuningJobs.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>nasJobs</td>
<td>Delete NAS job <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.nasJobs.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.nasJobs.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.nasJobs.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.nasJobs.delete (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>N/A</td>
<td>Create HumanInTheLoop operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>featurestores</td>
<td>Export features operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.featurestores.get (to call GET on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>N/A</td>
<td>Delete HumanInTheLoop operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>N/A</td>
<td>Send HumanInTheLoop entry operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.humanInTheLoops.send (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td>Calculate data item label stats <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>N/A</td>
<td>Migrate resources operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.locations.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.locations.get (to call DELETE on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="even">
<td>datasets</td>
<td>Create DataItem operation <sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td><br />
<strong>Other permissions:</strong>
<ul>
<li>aiplatform.datasets.get (to call GET on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call DELETE on the long-running operation returned)</li>
<li>aiplatform.datasets.get (to call WAIT on the long-running operation returned)</li>
<li>aiplatform.datasets.update (to call CANCEL on the long-running operation returned)</li>
</ul></td>
</tr>
<tr class="odd">
<td>N/A</td>
<td><sup>†</sup><br />
<br />
<br />

<p><sup>†</sup> Starts a long-running operation</p></td>
<td></td>
</tr>
</tbody>
</table>

## What's next

  - For information about Agent Platform predefined, basic and custom roles, as well as general information about service accounts and agents, see [Access control](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .
  - For detailed information about controlling permissions with a custom service account, see [Using a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .
  - Learn more about using IAM to access resources in the [Granting, changing, and revoking access to resources](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) topic of the IAM documentation.
