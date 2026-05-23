---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc
title: Notebooks API
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Notebooks API lets you manage Agent Platform Workbench resources in Google Cloud.

## Service: notebooks.googleapis.com

The Service name `notebooks.googleapis.com` is needed to create RPC client stubs.

## `        google.cloud.location.Locations       `

Methods

`  GetLocation  `

Gets information about a location.

`  ListLocations  `

Lists information about the supported locations for this service.

## `        google.cloud.notebooks.v1.ManagedNotebookService       `

Methods

`  CreateRuntime  `

Creates a new Runtime in a given project and location.

`  DeleteRuntime  `

Deletes a single Runtime.

`  GetRuntime  `

Gets details of a single Runtime.

`  ListRuntimes  `

Lists Runtimes in a given project and location.

`  MigrateRuntime  `

Migrate an existing Runtime to a new Workbench Instance.

`  ReportRuntimeEvent  `

Reports and processes a runtime event.

`  ResetRuntime  `

Resets a Managed Notebook Runtime.

`  StartRuntime  `

Starts a Managed Notebook Runtime.

`  StopRuntime  `

Stops a Managed Notebook Runtime.

`  SwitchRuntime  `

Switch a Managed Notebook Runtime.

`  UpdateRuntime  `

Update Notebook Runtime configuration.

## `        google.cloud.notebooks.v1.NotebookService       `

Methods

`  CreateEnvironment  `

Creates a new Environment.

`  CreateExecution  `

Creates a new Execution in a given project and location.

`  CreateInstance  `

Creates a new Instance in a given project and location.

`  CreateSchedule  `

Creates a new Scheduled Notebook in a given project and location.

`  DeleteEnvironment  `

Deletes a single Environment.

`  DeleteExecution  `

Deletes execution

`  DeleteInstance  `

Deletes a single Instance.

`  DeleteSchedule  `

Deletes schedule and all underlying jobs

`  DiagnoseInstance  `

Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

`  GetEnvironment  `

Gets details of a single Environment.

`  GetExecution  `

Gets details of executions

`  GetInstance  `

Gets details of a single Instance.

`  GetInstanceHealth  `

Checks whether a notebook instance is healthy.

`  GetSchedule  `

Gets details of schedule

`  IsInstanceUpgradeable  `

Checks whether a notebook instance is upgradable.

`  ListEnvironments  `

Lists environments in a project.

`  ListExecutions  `

Lists executions in a given project and location

`  ListInstances  `

Lists instances in a given project and location.

`  ListSchedules  `

Lists schedules in a given project and location.

`  MigrateInstance  `

Migrates an existing User-Managed Notebook to Workbench Instances.

`  RegisterInstance  `

Registers an existing legacy notebook instance to the Notebooks API server.

`  ReportInstanceInfo  `

Allows notebook instances to report their latest instance information to the Notebooks API server.

`  ResetInstance  `

Resets a notebook instance.

`  RollbackInstance  `

Rollbacks a notebook instance to the previous version.

`  SetInstanceAccelerator  `

Updates the guest accelerators of a single Instance.

`  SetInstanceLabels  `

Replaces all the labels of an Instance.

`  SetInstanceMachineType  `

Updates the machine type of a single Instance.

`  StartInstance  `

Starts a notebook instance.

`  StopInstance  `

Stops a notebook instance.

`  UpdateInstanceConfig  `

Update Notebook Instance configurations.

`  UpdateInstanceMetadataItems  `

Add/update metadata items for an instance.

`  UpdateShieldedInstanceConfig  `

Updates the Shielded instance configuration of a single Instance.

`  UpgradeInstance  `

Upgrades a notebook instance to the latest version.

## `        google.cloud.notebooks.v2.NotebookService       `

Methods

`  CheckInstanceUpgradability  `

Checks whether a notebook instance is upgradable.

`  CreateInstance  `

Creates a new Instance in a given project and location.

`  DeleteInstance  `

Deletes a single Instance.

`  DiagnoseInstance  `

Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

`  GetConfig  `

Returns various configuration parameters.

`  GetInstance  `

Gets details of a single Instance.

`  ListInstances  `

Lists instances in a given project and location.

`  ResetInstance  `

Resets a notebook instance.

`  ResizeDisk  `

Resize a notebook instance disk to a higher capacity.

`  RestoreInstance  `

RestoreInstance restores an Instance from a BackupSource.

`  RollbackInstance  `

Rollbacks a notebook instance to the previous version.

`  StartInstance  `

Starts a notebook instance.

`  StopInstance  `

Stops a notebook instance.

`  UpdateInstance  `

UpdateInstance updates an Instance.

`  UpgradeInstance  `

Upgrades a notebook instance to the latest version.

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
