---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest
title: Notebooks API
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Notebooks API lets you manage Agent Platform Workbench resources in Google Cloud.

## Service: notebooks.googleapis.com

To call this service, we recommend that you use the Google-provided [client libraries](https://cloud.google.com/apis/docs/client-libraries-explained) . If your application needs to use your own libraries to call this service, use the following information when you make the API requests.

### Discovery document

A [Discovery Document](https://developers.google.com/discovery/v1/reference/apis) is a machine-readable specification for describing and consuming REST APIs. It is used to build client libraries, IDE plugins, and other tools that interact with Google APIs. One service may provide multiple discovery documents. This service provides the following discovery documents:

  - <https://notebooks.googleapis.com/$discovery/rest?version=v2>
  - <https://notebooks.googleapis.com/$discovery/rest?version=v1>

### Service endpoint

A [service endpoint](https://cloud.google.com/apis/design/glossary#api_service_endpoint) is a base URL that specifies the network address of an API service. One service might have multiple service endpoints. This service has the following service endpoint and all URIs below are relative to this service endpoint:

  - `https://notebooks.googleapis.com`

## REST Resource: [v2.projects.locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations)

Methods

`  get  `

`GET /v2/{name}`  
Gets information about a location.

`  list  `

`GET /v2/{name}/locations`  
Lists information about the supported locations for this service.

## REST Resource: [v2.projects.locations.instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances)

Methods

`  checkUpgradability  `

`GET /v2/{notebookInstance}:checkUpgradability`  
Checks whether a notebook instance is upgradable.

`  create  `

`POST /v2/{parent}/instances`  
Creates a new Instance in a given project and location.

`  delete  `

`DELETE /v2/{name}`  
Deletes a single Instance.

`  diagnose  `

`POST /v2/{name}:diagnose`  
Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

`  get  `

`GET /v2/{name}`  
Gets details of a single Instance.

`  getConfig  `

`GET /v2/{name}/instances:getConfig`  
Returns various configuration parameters.

`  getIamPolicy  `

`GET /v2/{resource}:getIamPolicy`  
Gets the access control policy for a resource.

`  list  `

`GET /v2/{parent}/instances`  
Lists instances in a given project and location.

`  patch  `

`PATCH /v2/{instance.name}`  
UpdateInstance updates an Instance.

`  reset  `

`POST /v2/{name}:reset`  
Resets a notebook instance.

`  resizeDisk  `

`POST /v2/{notebookInstance}:resizeDisk`  
Resize a notebook instance disk to a higher capacity.

`  restore  `

`POST /v2/{name}:restore`  
RestoreInstance restores an Instance from a BackupSource.

`  rollback  `

`POST /v2/{name}:rollback`  
Rollbacks a notebook instance to the previous version.

`  setIamPolicy  `

`POST /v2/{resource}:setIamPolicy`  
Sets the access control policy on the specified resource.

`  start  `

`POST /v2/{name}:start`  
Starts a notebook instance.

`  stop  `

`POST /v2/{name}:stop`  
Stops a notebook instance.

`  testIamPermissions  `

`POST /v2/{resource}:testIamPermissions`  
Returns permissions that a caller has on the specified resource.

`  upgrade  `

`POST /v2/{name}:upgrade`  
Upgrades a notebook instance to the latest version.

## REST Resource: [v2.projects.locations.operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.operations)

Methods

`  cancel  `

`POST /v2/{name}:cancel`  
Starts asynchronous cancellation on a long-running operation.

`  delete  `

`DELETE /v2/{name}`  
Deletes a long-running operation.

`  get  `

`GET /v2/{name}`  
Gets the latest state of a long-running operation.

`  list  `

`GET /v2/{name}/operations`  
Lists operations that match the specified filter in the request.

## REST Resource: [v1.projects.locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations)

Methods

`  get  `

`GET /v1/{name}`  
Gets information about a location.

`  list  `

`GET /v1/{name}/locations`  
Lists information about the supported locations for this service.

## REST Resource: [v1.projects.locations.environments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments)

Methods

`  create  `

`POST /v1/{parent}/environments`  
Creates a new Environment.

`  delete  `

`DELETE /v1/{name}`  
Deletes a single Environment.

`  get  `

`GET /v1/{name}`  
Gets details of a single Environment.

`  list  `

`GET /v1/{parent}/environments`  
Lists environments in a project.

## REST Resource: [v1.projects.locations.executions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.executions)

Methods

`  create  `

`POST /v1/{parent}/executions`  
Creates a new Execution in a given project and location.

`  delete  `

`DELETE /v1/{name}`  
Deletes execution

`  get  `

`GET /v1/{name}`  
Gets details of executions

`  list  `

`GET /v1/{parent}/executions`  
Lists executions in a given project and location

## REST Resource: [v1.projects.locations.instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances)

Methods

`  create  `

`POST /v1/{parent}/instances`  
Creates a new Instance in a given project and location.

`  delete  `

`DELETE /v1/{name}`  
Deletes a single Instance.

`  diagnose  `

`POST /v1/{name}:diagnose`  
Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

`  get  `

`GET /v1/{name}`  
Gets details of a single Instance.

`  getIamPolicy  `

`GET /v1/{resource}:getIamPolicy`  
Gets the access control policy for a resource.

`  getInstanceHealth  `

`GET /v1/{name}:getInstanceHealth`  
Checks whether a notebook instance is healthy.

`  isUpgradeable  `

`GET /v1/{notebookInstance}:isUpgradeable`  
Checks whether a notebook instance is upgradable.

`  list  `

`GET /v1/{parent}/instances`  
Lists instances in a given project and location.

`  migrate  `

`POST /v1/{name}:migrate`  
Migrates an existing User-Managed Notebook to Workbench Instances.

`  register  `

`POST /v1/{parent}/instances:register`  
Registers an existing legacy notebook instance to the Notebooks API server.

`  report  `

`POST /v1/{name}:report`  
Allows notebook instances to report their latest instance information to the Notebooks API server.

`  reset  `

`POST /v1/{name}:reset`  
Resets a notebook instance.

`  rollback  `

`POST /v1/{name}:rollback`  
Rollbacks a notebook instance to the previous version.

`  setAccelerator  `

`PATCH /v1/{name}:setAccelerator`  
Updates the guest accelerators of a single Instance.

`  setIamPolicy  `

`POST /v1/{resource}:setIamPolicy`  
Sets the access control policy on the specified resource.

`  setLabels  `

`PATCH /v1/{name}:setLabels`  
Replaces all the labels of an Instance.

`  setMachineType  `

`PATCH /v1/{name}:setMachineType`  
Updates the machine type of a single Instance.

`  start  `

`POST /v1/{name}:start`  
Starts a notebook instance.

`  stop  `

`POST /v1/{name}:stop`  
Stops a notebook instance.

`  testIamPermissions  `

`POST /v1/{resource}:testIamPermissions`  
Returns permissions that a caller has on the specified resource.

`  updateConfig  `

`PATCH /v1/{name}:updateConfig`  
Update Notebook Instance configurations.

`  updateMetadataItems  `

`PATCH /v1/{name}:updateMetadataItems`  
Add/update metadata items for an instance.

`  updateShieldedInstanceConfig  `

`PATCH /v1/{name}:updateShieldedInstanceConfig`  
Updates the Shielded instance configuration of a single Instance.

`  upgrade  `

`POST /v1/{name}:upgrade`  
Upgrades a notebook instance to the latest version.

## REST Resource: [v1.projects.locations.operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.operations)

Methods

`  cancel  `

`POST /v1/{name}:cancel`  
Starts asynchronous cancellation on a long-running operation.

`  delete  `

`DELETE /v1/{name}`  
Deletes a long-running operation.

`  get  `

`GET /v1/{name}`  
Gets the latest state of a long-running operation.

`  list  `

`GET /v1/{name}/operations`  
Lists operations that match the specified filter in the request.

## REST Resource: [v1.projects.locations.runtimes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes)

Methods

`  create  `

`POST /v1/{parent}/runtimes`  
Creates a new Runtime in a given project and location.

`  delete  `

`DELETE /v1/{name}`  
Deletes a single Runtime.

`  get  `

`GET /v1/{name}`  
Gets details of a single Runtime.

`  getIamPolicy  `

`GET /v1/{resource}:getIamPolicy`  
Gets the access control policy for a resource.

`  list  `

`GET /v1/{parent}/runtimes`  
Lists Runtimes in a given project and location.

`  migrate  `

`POST /v1/{name}:migrate`  
Migrate an existing Runtime to a new Workbench Instance.

`  patch  `

`PATCH /v1/{runtime.name}`  
Update Notebook Runtime configuration.

`  reportEvent  `

`POST /v1/{name}:reportEvent`  
Reports and processes a runtime event.

`  reset  `

`POST /v1/{name}:reset`  
Resets a Managed Notebook Runtime.

`  setIamPolicy  `

`POST /v1/{resource}:setIamPolicy`  
Sets the access control policy on the specified resource.

`  start  `

`POST /v1/{name}:start`  
Starts a Managed Notebook Runtime.

`  stop  `

`POST /v1/{name}:stop`  
Stops a Managed Notebook Runtime.

`  switch  `

`POST /v1/{name}:switch`  
Switch a Managed Notebook Runtime.

`  testIamPermissions  `

`POST /v1/{resource}:testIamPermissions`  
Returns permissions that a caller has on the specified resource.

## REST Resource: [v1.projects.locations.schedules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules)

Methods

`  create  `

`POST /v1/{parent}/schedules`  
Creates a new Scheduled Notebook in a given project and location.

`  delete  `

`DELETE /v1/{name}`  
Deletes schedule and all underlying jobs

`  get  `

`GET /v1/{name}`  
Gets details of schedule

`  list  `

`GET /v1/{parent}/schedules`  
Lists schedules in a given project and location.
