---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1
title: Package google.cloud.notebooks.v1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

- [`ManagedNotebookService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ManagedNotebookService) (interface)
- [`NotebookService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.NotebookService) (interface)
- [`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ContainerImage) (message)
- [`CreateEnvironmentRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateEnvironmentRequest) (message)
- [`CreateExecutionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateExecutionRequest) (message)
- [`CreateInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateInstanceRequest) (message)
- [`CreateRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateRuntimeRequest) (message)
- [`CreateScheduleRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateScheduleRequest) (message)
- [`DeleteEnvironmentRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteEnvironmentRequest) (message)
- [`DeleteExecutionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteExecutionRequest) (message)
- [`DeleteInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteInstanceRequest) (message)
- [`DeleteRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteRuntimeRequest) (message)
- [`DeleteScheduleRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteScheduleRequest) (message)
- [`DiagnoseInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DiagnoseInstanceRequest) (message)
- [`DiagnosticConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DiagnosticConfig) (message)
- [`EncryptionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.EncryptionConfig) (message)
- [`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Environment) (message)
- [`Event`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Event) (message)
- [`Event.EventType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Event.EventType) (enum)
- [`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution) (message)
- [`Execution.State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution.State) (enum)
- [`ExecutionTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate) (message)
- [`ExecutionTemplate.DataprocParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.DataprocParameters) (message)
- [`ExecutionTemplate.JobType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.JobType) (enum)
- [`ExecutionTemplate.ScaleTier`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.ScaleTier) (enum)
- [`ExecutionTemplate.SchedulerAcceleratorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.SchedulerAcceleratorConfig) (message)
- [`ExecutionTemplate.SchedulerAcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.SchedulerAcceleratorType) (enum)
- [`ExecutionTemplate.VertexAIParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.VertexAIParameters) (message)
- [`GetEnvironmentRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetEnvironmentRequest) (message)
- [`GetExecutionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetExecutionRequest) (message)
- [`GetInstanceHealthRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceHealthRequest) (message)
- [`GetInstanceHealthResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceHealthResponse) (message)
- [`GetInstanceHealthResponse.HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceHealthResponse.HealthState) (enum)
- [`GetInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceRequest) (message)
- [`GetRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetRuntimeRequest) (message)
- [`GetScheduleRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetScheduleRequest) (message)
- [`Instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance) (message)
- [`Instance.AcceleratorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.AcceleratorConfig) (message)
- [`Instance.AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.AcceleratorType) (enum)
- [`Instance.Disk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.Disk) (message)
- [`Instance.Disk.GuestOsFeature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.Disk.GuestOsFeature) (message)
- [`Instance.DiskEncryption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.DiskEncryption) (enum)
- [`Instance.DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.DiskType) (enum)
- [`Instance.NicType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.NicType) (enum)
- [`Instance.ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.ShieldedInstanceConfig) (message)
- [`Instance.State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.State) (enum)
- [`Instance.UpgradeHistoryEntry`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.UpgradeHistoryEntry) (message)
- [`Instance.UpgradeHistoryEntry.Action`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.UpgradeHistoryEntry.Action) (enum)
- [`Instance.UpgradeHistoryEntry.State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.UpgradeHistoryEntry.State) (enum)
- [`InstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceConfig) (message)
- [`InstanceMigrationEligibility`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceMigrationEligibility) (message)
- [`InstanceMigrationEligibility.Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceMigrationEligibility.Error) (enum)
- [`InstanceMigrationEligibility.Warning`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceMigrationEligibility.Warning) (enum)
- [`IsInstanceUpgradeableRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.IsInstanceUpgradeableRequest) (message)
- [`IsInstanceUpgradeableResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.IsInstanceUpgradeableResponse) (message)
- [`ListEnvironmentsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListEnvironmentsRequest) (message)
- [`ListEnvironmentsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListEnvironmentsResponse) (message)
- [`ListExecutionsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListExecutionsRequest) (message)
- [`ListExecutionsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListExecutionsResponse) (message)
- [`ListInstancesRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListInstancesRequest) (message)
- [`ListInstancesResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListInstancesResponse) (message)
- [`ListRuntimesRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListRuntimesRequest) (message)
- [`ListRuntimesResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListRuntimesResponse) (message)
- [`ListSchedulesRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListSchedulesRequest) (message)
- [`ListSchedulesResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListSchedulesResponse) (message)
- [`LocalDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDisk) (message)
- [`LocalDisk.RuntimeGuestOsFeature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDisk.RuntimeGuestOsFeature) (message)
- [`LocalDiskInitializeParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDiskInitializeParams) (message)
- [`LocalDiskInitializeParams.DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDiskInitializeParams.DiskType) (enum)
- [`MigrateInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateInstanceRequest) (message)
- [`MigrateInstanceRequest.PostStartupScriptOption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateInstanceRequest.PostStartupScriptOption) (enum)
- [`MigrateInstanceResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateInstanceResponse) (message)
- [`MigrateRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateRuntimeRequest) (message)
- [`MigrateRuntimeRequest.PostStartupScriptOption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateRuntimeRequest.PostStartupScriptOption) (enum)
- [`OperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.OperationMetadata) (message)
- [`RegisterInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RegisterInstanceRequest) (message)
- [`ReportInstanceInfoRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReportInstanceInfoRequest) (message)
- [`ReportRuntimeEventRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReportRuntimeEventRequest) (message)
- [`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReservationAffinity) (message)
- [`ReservationAffinity.Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReservationAffinity.Type) (enum)
- [`ResetInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ResetInstanceRequest) (message)
- [`ResetRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ResetRuntimeRequest) (message)
- [`RollbackInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RollbackInstanceRequest) (message)
- [`Runtime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime) (message)
- [`Runtime.HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime.HealthState) (enum)
- [`Runtime.State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime.State) (enum)
- [`RuntimeAcceleratorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAcceleratorConfig) (message)
- [`RuntimeAcceleratorConfig.AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAcceleratorConfig.AcceleratorType) (enum)
- [`RuntimeAccessConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAccessConfig) (message)
- [`RuntimeAccessConfig.RuntimeAccessType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAccessConfig.RuntimeAccessType) (enum)
- [`RuntimeMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMetrics) (message)
- [`RuntimeMigrationEligibility`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMigrationEligibility) (message)
- [`RuntimeMigrationEligibility.Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMigrationEligibility.Error) (enum)
- [`RuntimeMigrationEligibility.Warning`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMigrationEligibility.Warning) (enum)
- [`RuntimeShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeShieldedInstanceConfig) (message)
- [`RuntimeSoftwareConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeSoftwareConfig) (message)
- [`RuntimeSoftwareConfig.PostStartupScriptBehavior`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeSoftwareConfig.PostStartupScriptBehavior) (enum)
- [`Schedule`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Schedule) (message)
- [`Schedule.State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Schedule.State) (enum)
- [`SetInstanceAcceleratorRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SetInstanceAcceleratorRequest) (message)
- [`SetInstanceLabelsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SetInstanceLabelsRequest) (message)
- [`SetInstanceMachineTypeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SetInstanceMachineTypeRequest) (message)
- [`StartInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StartInstanceRequest) (message)
- [`StartRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StartRuntimeRequest) (message)
- [`StopInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StopInstanceRequest) (message)
- [`StopRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StopRuntimeRequest) (message)
- [`SwitchRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SwitchRuntimeRequest) (message)
- [`UpdateInstanceConfigRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateInstanceConfigRequest) (message)
- [`UpdateInstanceMetadataItemsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateInstanceMetadataItemsRequest) (message)
- [`UpdateInstanceMetadataItemsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateInstanceMetadataItemsResponse) (message)
- [`UpdateRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateRuntimeRequest) (message)
- [`UpdateShieldedInstanceConfigRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateShieldedInstanceConfigRequest) (message)
- [`UpgradeInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpgradeInstanceRequest) (message)
- [`UpgradeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpgradeType) (enum)
- [`VirtualMachine`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachine) (message)
- [`VirtualMachineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachineConfig) (message)
- [`VirtualMachineConfig.BootImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachineConfig.BootImage) (message)
- [`VirtualMachineConfig.NicType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachineConfig.NicType) (enum)
- [`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VmImage) (message)

## ManagedNotebookService

API v1 service for Managed Notebooks.

**CreateRuntime**

`rpc CreateRuntime( `[`CreateRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new Runtime in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteRuntime**

`rpc DeleteRuntime( `[`DeleteRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Deletes a single Runtime.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetRuntime**

`rpc GetRuntime( `[`GetRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetRuntimeRequest)` ) returns ( `[`Runtime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime)` )`

Gets details of a single Runtime. The location must be a regional endpoint rather than zonal.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListRuntimes**

`rpc ListRuntimes( `[`ListRuntimesRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListRuntimesRequest)` ) returns ( `[`ListRuntimesResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListRuntimesResponse)` )`

Lists Runtimes in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**MigrateRuntime**

`rpc MigrateRuntime( `[`MigrateRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Migrate an existing Runtime to a new Workbench Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ReportRuntimeEvent**

`rpc ReportRuntimeEvent( `[`ReportRuntimeEventRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReportRuntimeEventRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Reports and processes a runtime event.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ResetRuntime**

`rpc ResetRuntime( `[`ResetRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ResetRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Resets a Managed Notebook Runtime.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**StartRuntime**

`rpc StartRuntime( `[`StartRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StartRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Starts a Managed Notebook Runtime. Perform "Start" on GPU instances; "Resume" on CPU instances See: <https://cloud.google.com/compute/docs/instances/stop-start-instance> <https://cloud.google.com/compute/docs/instances/suspend-resume-instance>

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**StopRuntime**

`rpc StopRuntime( `[`StopRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StopRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Stops a Managed Notebook Runtime. Perform "Stop" on GPU instances; "Suspend" on CPU instances See: <https://cloud.google.com/compute/docs/instances/stop-start-instance> <https://cloud.google.com/compute/docs/instances/suspend-resume-instance>

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SwitchRuntime**

`rpc SwitchRuntime( `[`SwitchRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SwitchRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Switch a Managed Notebook Runtime.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateRuntime**

`rpc UpdateRuntime( `[`UpdateRuntimeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateRuntimeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Update Notebook Runtime configuration.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## NotebookService

API v1 service for Cloud AI Platform Notebooks.

**CreateEnvironment**

`rpc CreateEnvironment( `[`CreateEnvironmentRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateEnvironmentRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new Environment.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateExecution**

`rpc CreateExecution( `[`CreateExecutionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateExecutionRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new Execution in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateInstance**

`rpc CreateInstance( `[`CreateInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new Instance in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**CreateSchedule**

`rpc CreateSchedule( `[`CreateScheduleRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.CreateScheduleRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a new Scheduled Notebook in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteEnvironment**

`rpc DeleteEnvironment( `[`DeleteEnvironmentRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteEnvironmentRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Deletes a single Environment.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteExecution**

`rpc DeleteExecution( `[`DeleteExecutionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteExecutionRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Deletes execution

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteInstance**

`rpc DeleteInstance( `[`DeleteInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Deletes a single Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteSchedule**

`rpc DeleteSchedule( `[`DeleteScheduleRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DeleteScheduleRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Deletes schedule and all underlying jobs

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DiagnoseInstance**

`rpc DiagnoseInstance( `[`DiagnoseInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DiagnoseInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetEnvironment**

`rpc GetEnvironment( `[`GetEnvironmentRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetEnvironmentRequest)` ) returns ( `[`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Environment)` )`

Gets details of a single Environment.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetExecution**

`rpc GetExecution( `[`GetExecutionRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetExecutionRequest)` ) returns ( `[`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution)` )`

Gets details of executions

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetInstance**

`rpc GetInstance( `[`GetInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceRequest)` ) returns ( `[`Instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance)` )`

Gets details of a single Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetInstanceHealth**

`rpc GetInstanceHealth( `[`GetInstanceHealthRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceHealthRequest)` ) returns ( `[`GetInstanceHealthResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceHealthResponse)` )`

Checks whether a notebook instance is healthy.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetSchedule**

`rpc GetSchedule( `[`GetScheduleRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetScheduleRequest)` ) returns ( `[`Schedule`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Schedule)` )`

Gets details of schedule

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**IsInstanceUpgradeable**

`rpc IsInstanceUpgradeable( `[`IsInstanceUpgradeableRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.IsInstanceUpgradeableRequest)` ) returns ( `[`IsInstanceUpgradeableResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.IsInstanceUpgradeableResponse)` )`

Checks whether a notebook instance is upgradable.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListEnvironments**

`rpc ListEnvironments( `[`ListEnvironmentsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListEnvironmentsRequest)` ) returns ( `[`ListEnvironmentsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListEnvironmentsResponse)` )`

Lists environments in a project.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListExecutions**

`rpc ListExecutions( `[`ListExecutionsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListExecutionsRequest)` ) returns ( `[`ListExecutionsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListExecutionsResponse)` )`

Lists executions in a given project and location

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListInstances**

`rpc ListInstances( `[`ListInstancesRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListInstancesRequest)` ) returns ( `[`ListInstancesResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListInstancesResponse)` )`

Lists instances in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListSchedules**

`rpc ListSchedules( `[`ListSchedulesRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListSchedulesRequest)` ) returns ( `[`ListSchedulesResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ListSchedulesResponse)` )`

Lists schedules in a given project and location.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**MigrateInstance**

`rpc MigrateInstance( `[`MigrateInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Migrates an existing User-Managed Notebook to Workbench Instances.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RegisterInstance**

`rpc RegisterInstance( `[`RegisterInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RegisterInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Registers an existing legacy notebook instance to the Notebooks API server. Legacy instances are instances created with the legacy Compute Engine calls. They are not manageable by the Notebooks API out of the box. This call makes these instances manageable by the Notebooks API.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ReportInstanceInfo**

`rpc ReportInstanceInfo( `[`ReportInstanceInfoRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReportInstanceInfoRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Allows notebook instances to report their latest instance information to the Notebooks API server. The server will merge the reported information to the instance metadata store. Do not use this method directly.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ResetInstance**

`rpc ResetInstance( `[`ResetInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ResetInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Resets a notebook instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**RollbackInstance**

`rpc RollbackInstance( `[`RollbackInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RollbackInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Rollbacks a notebook instance to the previous version.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SetInstanceAccelerator**

`rpc SetInstanceAccelerator( `[`SetInstanceAcceleratorRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SetInstanceAcceleratorRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Updates the guest accelerators of a single Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SetInstanceLabels**

`rpc SetInstanceLabels( `[`SetInstanceLabelsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SetInstanceLabelsRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Replaces all the labels of an Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SetInstanceMachineType**

`rpc SetInstanceMachineType( `[`SetInstanceMachineTypeRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.SetInstanceMachineTypeRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Updates the machine type of a single Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**StartInstance**

`rpc StartInstance( `[`StartInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StartInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Starts a notebook instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**StopInstance**

`rpc StopInstance( `[`StopInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.StopInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Stops a notebook instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateInstanceConfig**

`rpc UpdateInstanceConfig( `[`UpdateInstanceConfigRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateInstanceConfigRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Update Notebook Instance configurations.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateInstanceMetadataItems**

`rpc UpdateInstanceMetadataItems( `[`UpdateInstanceMetadataItemsRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateInstanceMetadataItemsRequest)` ) returns ( `[`UpdateInstanceMetadataItemsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateInstanceMetadataItemsResponse)` )`

Add/update metadata items for an instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateShieldedInstanceConfig**

`rpc UpdateShieldedInstanceConfig( `[`UpdateShieldedInstanceConfigRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpdateShieldedInstanceConfigRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Updates the Shielded instance configuration of a single Instance.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpgradeInstance**

`rpc UpgradeInstance( `[`UpgradeInstanceRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpgradeInstanceRequest)` ) returns ( `[`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation)` )`

Upgrades a notebook instance to the latest version.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## ContainerImage

Definition of a container image for starting a notebook instance with the environment installed in a container.

| Fields       |                                                                                                                |
|--------------|----------------------------------------------------------------------------------------------------------------|
| `repository` | `string` Required. The path to the container image repository. For example: `gcr.io/{project_id}/{image_name}` |
| `tag`        | `string` The tag of the container image. If not specified, this defaults to the latest tag.                    |

## CreateEnvironmentRequest

Request for creating a notebook environment.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.environments.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>environment_id</code></td>
<td><p><code>string</code></p>
<p>Required. User-defined unique ID of this environment. The <code>environment_id</code> must be 1 to 63 characters long and contain only lowercase letters, numeric characters, and dashes. The first character must be a lowercase letter and the last character cannot be a dash.</p></td>
</tr>
<tr class="odd">
<td><code>environment</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Environment"><code>Environment</code></a></p>
<p>Required. The environment to be created.</p></td>
</tr>
</tbody>
</table>

## CreateExecutionRequest

Request to create notebook execution

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.executions.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>execution_id</code></td>
<td><p><code>string</code></p>
<p>Required. User-defined unique ID of this execution.</p></td>
</tr>
<tr class="odd">
<td><code>execution</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution"><code>Execution</code></a></p>
<p>Required. The execution to be created.</p></td>
</tr>
</tbody>
</table>

## CreateInstanceRequest

Request for creating a notebook instance.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.instances.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>instance_id</code></td>
<td><p><code>string</code></p>
<p>Required. User-defined unique ID of this instance.</p></td>
</tr>
<tr class="odd">
<td><code>instance</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance"><code>Instance</code></a></p>
<p>Required. The instance to be created.</p></td>
</tr>
</tbody>
</table>

## CreateRuntimeRequest

Request for creating a Managed Notebook Runtime.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.runtimes.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>runtime_id</code></td>
<td><p><code>string</code></p>
<p>Required. User-defined unique ID of this Runtime.</p></td>
</tr>
<tr class="odd">
<td><code>runtime</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime"><code>Runtime</code></a></p>
<p>Required. The Runtime to be created.</p></td>
</tr>
<tr class="even">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## CreateScheduleRequest

Request for created scheduled notebooks

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.schedules.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>schedule_id</code></td>
<td><p><code>string</code></p>
<p>Required. User-defined unique ID of this schedule.</p></td>
</tr>
<tr class="odd">
<td><code>schedule</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Schedule"><code>Schedule</code></a></p>
<p>Required. The schedule to be created.</p></td>
</tr>
</tbody>
</table>

## DeleteEnvironmentRequest

Request for deleting a notebook environment.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/environments/{environment_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.environments.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DeleteExecutionRequest

Request for deleting a scheduled notebook execution

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/executions/{execution_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.executions.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DeleteInstanceRequest

Request for deleting a notebook instance.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DeleteRuntimeRequest

Request for deleting a Managed Notebook Runtime.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.delete</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## DeleteScheduleRequest

Request for deleting an Schedule

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/schedules/{schedule_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.schedules.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DiagnoseInstanceRequest

Request for creating a notebook instance diagnostic file.

| Fields              |                                                                                                                                                                                                                                                              |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`              | `string` Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`                                                                                                                                                              |
| `diagnostic_config` | [`DiagnosticConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.DiagnosticConfig) Required. Defines flags that are used to run the diagnostic tool |
| `timeout_minutes`   | `int32` Optional. Maximum amount of time in minutes before the operation times out.                                                                                                                                                                          |

## DiagnosticConfig

Defines flags that are used to run the diagnostic tool

| Fields                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gcs_bucket`                   | `string` Required. User Cloud Storage bucket location (REQUIRED). Must be formatted with path prefix ( `gs://$GCS_BUCKET` ). Permissions: User Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account attached to VM. Google Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account or user credentials attached to VM depending on authentication mode. Cloud Storage bucket Log file will be written to `gs://$GCS_BUCKET/$RELATIVE_PATH/$VM_DATE_$TIME.tar.gz` |
| `relative_path`                | `string` Optional. Defines the relative storage path in the Cloud Storage bucket where the diagnostic logs will be written: Default path will be the root directory of the Cloud Storage bucket ( `gs://$GCS_BUCKET/$DATE_$TIME.tar.gz` ) Example of full path where Log file will be written: `gs://$GCS_BUCKET/$RELATIVE_PATH/`                                                                                                                                                                                                           |
| `repair_flag_enabled`          | `bool` Optional. Enables flag to repair service for instance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `packet_capture_flag_enabled`  | `bool` Optional. Enables flag to capture packets from the instance for 30 seconds                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `copy_home_files_flag_enabled` | `bool` Optional. Enables flag to copy all `/home/jupyter` folder contents                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

## EncryptionConfig

Represents a custom encryption key configuration that can be applied to a resource. This will encrypt all disks in Virtual Machine.

| Fields    |                                                                                                                                                                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kms_key` | `string` The Cloud KMS resource identifier of the customer-managed encryption key used to protect a resource, such as a disks. It has the following format: `projects/{PROJECT_ID}/locations/{REGION}/keyRings/{KEY_RING_NAME}/cryptoKeys/{KEY_NAME}` |

## Environment

Definition of a software environment that is used to start a notebook instance.

| Fields                                                                                                                                         |                                                                                                                                                                                                                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                         | `string` Output only. Name of this environment. Format: `projects/{project_id}/locations/{location}/environments/{environment_id}`                                                                                                            |
| `display_name`                                                                                                                                 | `string` Display name of this environment for the UI.                                                                                                                                                                                         |
| `description`                                                                                                                                  | `string` A brief description of this environment.                                                                                                                                                                                             |
| `post_startup_script`                                                                                                                          | `string` Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path. Example: `"gs://path-to-file/file-name"`                                                       |
| `create_time`                                                                                                                                  | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. The time at which this environment was created.                                                                                                |
| Union field `image_type` . Type of the environment; can be one of VM image, or container image. `image_type` can be only one of the following: |                                                                                                                                                                                                                                               |
| `vm_image`                                                                                                                                     | [`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VmImage) Use a Compute Engine VM image to start the notebook instance.       |
| `container_image`                                                                                                                              | [`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ContainerImage) Use a container image to start the notebook instance. |

## Event

The definition of an Event for a managed / semi-managed notebook instance.

| Fields        |                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `report_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Event report time.                                                                                            |
| `type`        | [`EventType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Event.EventType) Event type. |
| `details`     | `map<string, string>` Optional. Event details. This field is used to pass event information.                                                                                                    |

## EventType

The definition of the event types.

| Enums                    |                                                                                                                                                                                                    |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `EVENT_TYPE_UNSPECIFIED` | Event is not specified.                                                                                                                                                                            |
| `IDLE`                   | The instance / runtime is idle                                                                                                                                                                     |
| `HEARTBEAT`              | The instance / runtime is available. This event indicates that instance / runtime underlying compute is operational.                                                                               |
| `HEALTH`                 | The instance / runtime health is available. This event indicates that instance / runtime health information.                                                                                       |
| `MAINTENANCE`            | The instance / runtime is available. This event allows instance / runtime to send Host maintenance information to Control Plane. <https://cloud.google.com/compute/docs/gpus/gpu-host-maintenance> |

## Execution

The definition of a single executed notebook.

| Fields                 |                                                                                                                                                                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `execution_template`   | [`ExecutionTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate) execute metadata including name, hardware spec, region, labels, etc. |
| `name`                 | `string` Output only. The resource name of the execute. Format: `projects/{project_id}/locations/{location}/executions/{execution_id}`                                                                                                                             |
| `display_name`         | `string` Output only. Name used for UI purposes. Name can only contain alphanumeric characters and underscores '\_'.                                                                                                                                               |
| `description`          | `string` A brief description of this execution.                                                                                                                                                                                                                    |
| `create_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time the Execution was instantiated.                                                                                                                                |
| `update_time`          | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time the Execution was last updated.                                                                                                                                |
| `state`                | [`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution.State) Output only. State of the underlying AI Platform job.                              |
| `output_notebook_file` | `string` Output notebook file generated by this execution                                                                                                                                                                                                          |
| `job_uri`              | `string` Output only. The URI of the external job used to execute the notebook.                                                                                                                                                                                    |

## State

Enum description of the state of the underlying AIP job.

| Enums               |                                                                                              |
|---------------------|----------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The job state is unspecified.                                                                |
| `QUEUED`            | The job has been just created and processing has not yet begun.                              |
| `PREPARING`         | The service is preparing to execution the job.                                               |
| `RUNNING`           | The job is in progress.                                                                      |
| `SUCCEEDED`         | The job completed successfully.                                                              |
| `FAILED`            | The job failed. `error_message` should contain the details of the failure.                   |
| `CANCELLING`        | The job is being cancelled. `error_message` should describe the reason for the cancellation. |
| `CANCELLED`         | The job has been cancelled. `error_message` should describe the reason for the cancellation. |
| `EXPIRED`           | The job has become expired (relevant to Vertex AI jobs)                                      |
| `INITIALIZING`      | The Execution is being created.                                                              |

## ExecutionTemplate

The description a notebook execution workload.

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
<td><code>scale_tier </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.ScaleTier"><code>ScaleTier</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Required. Scale tier of the hardware used for notebook execution. DEPRECATED Will be discontinued. As right now only CUSTOM is supported.</p></td>
</tr>
<tr class="even">
<td><code>master_type</code></td>
<td><p><code>string</code></p>
<p>Specifies the type of virtual machine to use for your training job's master worker. You must specify this field when <code>scaleTier</code> is set to <code>CUSTOM</code> .</p>
<p>You can use certain Compute Engine machine types directly in this field. The following types are supported:</p>
<ul>
<li><code>n1-standard-4</code></li>
<li><code>n1-standard-8</code></li>
<li><code>n1-standard-16</code></li>
<li><code>n1-standard-32</code></li>
<li><code>n1-standard-64</code></li>
<li><code>n1-standard-96</code></li>
<li><code>n1-highmem-2</code></li>
<li><code>n1-highmem-4</code></li>
<li><code>n1-highmem-8</code></li>
<li><code>n1-highmem-16</code></li>
<li><code>n1-highmem-32</code></li>
<li><code>n1-highmem-64</code></li>
<li><code>n1-highmem-96</code></li>
<li><code>n1-highcpu-16</code></li>
<li><code>n1-highcpu-32</code></li>
<li><code>n1-highcpu-64</code></li>
<li><code>n1-highcpu-96</code></li>
</ul>
<p>Alternatively, you can use the following legacy machine types:</p>
<ul>
<li><code>standard</code></li>
<li><code>large_model</code></li>
<li><code>complex_model_s</code></li>
<li><code>complex_model_m</code></li>
<li><code>complex_model_l</code></li>
<li><code>standard_gpu</code></li>
<li><code>complex_model_m_gpu</code></li>
<li><code>complex_model_l_gpu</code></li>
<li><code>standard_p100</code></li>
<li><code>complex_model_m_p100</code></li>
<li><code>standard_v100</code></li>
<li><code>large_model_v100</code></li>
<li><code>complex_model_m_v100</code></li>
<li><code>complex_model_l_v100</code></li>
</ul>
<p>Finally, if you want to use a TPU for training, specify <code>cloud_tpu</code> in this field. Learn more about the <a href="https://cloud.google.com/ai-platform/training/docs/using-tpus#configuring_a_custom_tpu_machine">special configuration options for training with TPU</a> .</p></td>
</tr>
<tr class="odd">
<td><code>accelerator_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.SchedulerAcceleratorConfig"><code>SchedulerAcceleratorConfig</code></a></p>
<p>Configuration (count and accelerator type) for hardware running notebook execution.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Labels for execution. If execution is scheduled, a field included will be 'nbs-scheduled'. Otherwise, it is an immediate execution, and an included field will be 'nbs-immediate'. Use fields to efficiently index between various types of executions.</p></td>
</tr>
<tr class="odd">
<td><code>input_notebook_file</code></td>
<td><p><code>string</code></p>
<p>Path to the notebook file to execute. Must be in a Google Cloud Storage bucket. Format: <code>gs://{bucket_name}/{folder}/{notebook_file_name}</code> Ex: <code>gs://notebook_user/scheduled_notebooks/sentiment_notebook.ipynb</code></p></td>
</tr>
<tr class="even">
<td><code>container_image_uri</code></td>
<td><p><code>string</code></p>
<p>Container Image URI to a DLVM Example: 'gcr.io/deeplearning-platform-release/base-cu100' More examples can be found at: <a href="https://cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container">https://cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container</a></p></td>
</tr>
<tr class="odd">
<td><code>output_notebook_folder</code></td>
<td><p><code>string</code></p>
<p>Path to the notebook folder to write to. Must be in a Google Cloud Storage bucket path. Format: <code>gs://{bucket_name}/{folder}</code> Ex: <code>gs://notebook_user/scheduled_notebooks</code></p></td>
</tr>
<tr class="even">
<td><code>params_yaml_file</code></td>
<td><p><code>string</code></p>
<p>Parameters to be overridden in the notebook during execution. Ref <a href="https://papermill.readthedocs.io/en/latest/usage-parameterize.html">https://papermill.readthedocs.io/en/latest/usage-parameterize.html</a> on how to specifying parameters in the input notebook and pass them here in an YAML file. Ex: <code>gs://notebook_user/scheduled_notebooks/sentiment_notebook_params.yaml</code></p></td>
</tr>
<tr class="odd">
<td><code>parameters</code></td>
<td><p><code>string</code></p>
<p>Parameters used within the 'input_notebook_file' notebook.</p></td>
</tr>
<tr class="even">
<td><code>service_account</code></td>
<td><p><code>string</code></p>
<p>The email address of a service account to use when running the execution. You must have the <code>iam.serviceAccounts.actAs</code> permission for the specified service account.</p></td>
</tr>
<tr class="odd">
<td><code>job_type</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.JobType"><code>JobType</code></a></p>
<p>The type of Job to be used on this execution.</p></td>
</tr>
<tr class="even">
<td><code>kernel_spec</code></td>
<td><p><code>string</code></p>
<p>Name of the kernel spec to use. This must be specified if the kernel spec name on the execution target does not match the name in the input notebook file.</p></td>
</tr>
<tr class="odd">
<td><code>tensorboard</code></td>
<td><p><code>string</code></p>
<p>The name of a Vertex AI [Tensorboard] resource to which this execution will upload Tensorboard logs. Format: <code>projects/{project}/locations/{location}/tensorboards/{tensorboard}</code></p></td>
</tr>
<tr class="even">
<td>Union field <code>job_parameters</code> . Parameters for an execution type. NOTE: There are currently no extra parameters for VertexAI jobs. <code>job_parameters</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>dataproc_parameters</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.DataprocParameters"><code>DataprocParameters</code></a></p>
<p>Parameters used in Dataproc JobType executions.</p></td>
</tr>
<tr class="even">
<td><code>vertex_ai_parameters</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.VertexAIParameters"><code>VertexAIParameters</code></a></p>
<p>Parameters used in Vertex AI JobType executions.</p></td>
</tr>
</tbody>
</table>

## DataprocParameters

Parameters used in Dataproc JobType executions.

| Fields    |                                                                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| `cluster` | `string` URI for cluster used to run Dataproc execution. Format: `projects/{PROJECT_ID}/regions/{REGION}/clusters/{CLUSTER_NAME}` |

## JobType

The backend used for this execution.

| Enums                  |                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_TYPE_UNSPECIFIED` | No type specified.                                                                                                                  |
| `VERTEX_AI`            | Custom Job in `aiplatform.googleapis.com` . Default value for an execution.                                                         |
| `DATAPROC`             | Run execution on a cluster with Dataproc as a job. <https://cloud.google.com/dataproc/docs/reference/rest/v1/projects.regions.jobs> |

## ScaleTier

Required. Specifies the machine types, the number of replicas for workers and parameter servers.

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
<td><code>SCALE_TIER_UNSPECIFIED</code></td>
<td>Unspecified Scale Tier.</td>
</tr>
<tr class="even">
<td><code>BASIC</code></td>
<td>A single worker instance. This tier is suitable for learning how to use Cloud ML, and for experimenting with new models using small datasets.</td>
</tr>
<tr class="odd">
<td><code>STANDARD_1</code></td>
<td>Many workers and a few parameter servers.</td>
</tr>
<tr class="even">
<td><code>PREMIUM_1</code></td>
<td>A large number of workers with many parameter servers.</td>
</tr>
<tr class="odd">
<td><code>BASIC_GPU</code></td>
<td>A single worker instance with a K80 GPU.</td>
</tr>
<tr class="even">
<td><code>BASIC_TPU</code></td>
<td>A single worker instance with a Cloud TPU.</td>
</tr>
<tr class="odd">
<td><code>CUSTOM</code></td>
<td><p>The CUSTOM tier is not a set tier, but rather enables you to use your own cluster specification. When you use this tier, set values to configure your processing cluster according to these guidelines:</p>
<ul>
<li>You <em>must</em> set <code>ExecutionTemplate.masterType</code> to specify the type of machine to use for your master node. This is the only required setting.</li>
</ul></td>
</tr>
</tbody>
</table>

## SchedulerAcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `core_count` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus) to find a valid combination. TPUs are not supported.

| Fields       |                                                                                                                                                                                                                                                         |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`       | [`SchedulerAcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate.SchedulerAcceleratorType) Type of this accelerator. |
| `core_count` | `int64` Count of cores of this accelerator.                                                                                                                                                                                                             |

## SchedulerAcceleratorType

Hardware accelerator types for AI Platform Training jobs.

| Enums                                    |                                                  |
|------------------------------------------|--------------------------------------------------|
| `SCHEDULER_ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type. Default to no GPU. |
| `NVIDIA_TESLA_K80`                       | Nvidia Tesla K80 GPU.                            |
| `NVIDIA_TESLA_P100`                      | Nvidia Tesla P100 GPU.                           |
| `NVIDIA_TESLA_V100`                      | Nvidia Tesla V100 GPU.                           |
| `NVIDIA_TESLA_P4`                        | Nvidia Tesla P4 GPU.                             |
| `NVIDIA_TESLA_T4`                        | Nvidia Tesla T4 GPU.                             |
| `NVIDIA_TESLA_A100`                      | Nvidia Tesla A100 GPU.                           |
| `TPU_V2`                                 | TPU v2.                                          |
| `TPU_V3`                                 | TPU v3.                                          |

## VertexAIParameters

Parameters used in Vertex AI JobType executions.

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `network` | `string` The full name of the Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Job should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is a network name. Private services access must already be configured for the network. If left unspecified, the job is not peered with any network. |
| `env`     | `map<string, string>` Environment variables. At most 100 environment variables can be specified and unique. Example: `GCP_BUCKET=gs://my-bucket/samples/`                                                                                                                                                                                                                                                                                                                                                                                                                                           |

## GetEnvironmentRequest

Request for getting a notebook environment.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/environments/{environment_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.environments.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetExecutionRequest

Request for getting scheduled notebook execution

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/executions/{execution_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.executions.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetInstanceHealthRequest

Request for checking if a notebook instance is healthy.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.getHealth</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetInstanceHealthResponse

Response for checking if a notebook instance is healthy.

| Fields         |                                                                                                                                                                                                                                                                      |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `health_state` | [`HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.GetInstanceHealthResponse.HealthState) Output only. Runtime health_state.                       |
| `health_info`  | `map<string, string>` Output only. Additional information about instance health. Example: healthInfo": { "docker_proxy_agent_status": "1", "docker_status": "1", "jupyterlab_api_status": "-1", "jupyterlab_status": "-1", "updated": "2020-10-18 09:40:03.573409" } |

## HealthState

If an instance is healthy or not.

| Enums                      |                                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | The instance substate is unknown.                                                                                          |
| `HEALTHY`                  | The instance is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.       |
| `UNHEALTHY`                | The instance is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state. |
| `AGENT_NOT_INSTALLED`      | The instance has not installed health monitoring agent. Applies to ACTIVE state.                                           |
| `AGENT_NOT_RUNNING`        | The instance health monitoring agent is not running. Applies to ACTIVE state.                                              |

## GetInstanceRequest

Request for getting a notebook instance.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetRuntimeRequest

Request for getting a Managed Notebook Runtime.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetScheduleRequest

Request for getting scheduled notebook.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/schedules/{schedule_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.schedules.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## Instance

The definition of a notebook instance.

| Fields                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                           | `string` Output only. The name of this notebook instance. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`                                                                                                                                                                                                                                                                                                                   |
| `post_startup_script`                                                                                                                            | `string` Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).                                                                                                                                                                                                                                                                         |
| `proxy_uri`                                                                                                                                      | `string` Output only. The proxy endpoint that is used to access the Jupyter notebook.                                                                                                                                                                                                                                                                                                                                                                    |
| `instance_owners[]`                                                                                                                              | `string` Input only. The owner of this instance after creation. Format: `alias@example.com` Currently supports one owner only. If not specified, all of the service account users of your VM instance's service account can use the instance.                                                                                                                                                                                                            |
| `service_account`                                                                                                                                | `string` The service account on this instance, giving access to other Google Cloud services. You can use any service account within the same project, but you must have the service account user permission to use the instance. If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.                                                          |
| `service_account_scopes[]`                                                                                                                       | `string` Optional. The URIs of service account scopes to be included in Compute Engine instances. If not specified, the following [scopes](https://cloud.google.com/compute/docs/access/service-accounts#accesscopesiam) are defined: - <https://www.googleapis.com/auth/cloud-platform> - <https://www.googleapis.com/auth/userinfo.email> If not using default scopes, you need at least: <https://www.googleapis.com/auth/compute>                    |
| `machine_type`                                                                                                                                   | `string` Required. The [Compute Engine machine type](https://cloud.google.com/compute/docs/machine-resource) of this instance.                                                                                                                                                                                                                                                                                                                           |
| `accelerator_config`                                                                                                                             | [`AcceleratorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.AcceleratorConfig) The hardware accelerator used on this instance. If you use accelerators, make sure that your configuration has [enough vCPUs and memory to support the `machine_type` you have selected](https://cloud.google.com/compute/docs/gpus/#gpus-list) . |
| `state`                                                                                                                                          | [`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.State) Output only. The state of this instance.                                                                                                                                                                                                                                  |
| `install_gpu_driver`                                                                                                                             | `bool` Whether the end user authorizes Google Cloud to install GPU driver on this instance. If this field is empty or set to false, the GPU driver won't be installed. Only applicable to instances with GPUs.                                                                                                                                                                                                                                           |
| `custom_gpu_driver_path`                                                                                                                         | `string` Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.                                                                                                                                                                                                                                                                                                     |
| `boot_disk_type`                                                                                                                                 | [`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.DiskType) Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).                                                                                                                                            |
| `boot_disk_size_gb`                                                                                                                              | `int64` Input only. The size of the boot disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). The minimum recommended value is 100 GB. If not specified, this defaults to 100.                                                                                                                                                                                                                                                     |
| `data_disk_type`                                                                                                                                 | [`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.DiskType) Input only. The type of the data disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).                                                                                                                                            |
| `data_disk_size_gb`                                                                                                                              | `int64` Input only. The size of the data disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). You can choose the size of the data disk based on how big your notebooks and data are. If not specified, this defaults to 100.                                                                                                                                                                                                       |
| `no_remove_data_disk`                                                                                                                            | `bool` Input only. If true, the data disk will not be auto deleted when deleting the instance.                                                                                                                                                                                                                                                                                                                                                           |
| `disk_encryption`                                                                                                                                | [`DiskEncryption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.DiskEncryption) Input only. Disk encryption method used on the boot and data disks, defaults to GMEK.                                                                                                                                                                   |
| `kms_key`                                                                                                                                        | `string` Input only. The KMS key used to encrypt the disks, only applicable if disk_encryption is CMEK. Format: `projects/{project_id}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}` Learn more about [using your own encryption keys](https://docs.cloud.google.com/kms/docs/quickstart) .                                                                                                                                           |
| `disks[]`                                                                                                                                        | [`Disk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.Disk) Output only. Attached disks to notebook instance.                                                                                                                                                                                                                           |
| `shielded_instance_config`                                                                                                                       | [`ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.ShieldedInstanceConfig) Optional. Shielded VM configuration. [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .                                                                             |
| `no_public_ip`                                                                                                                                   | `bool` If true, no external IP will be assigned to this instance.                                                                                                                                                                                                                                                                                                                                                                                        |
| `no_proxy_access`                                                                                                                                | `bool` If true, the notebook instance will not register with the proxy.                                                                                                                                                                                                                                                                                                                                                                                  |
| `network`                                                                                                                                        | `string` The name of the VPC that this instance is in. Format: `projects/{project_id}/global/networks/{network_id}`                                                                                                                                                                                                                                                                                                                                      |
| `subnet`                                                                                                                                         | `string` The name of the subnet that this instance is in. Format: `projects/{project_id}/regions/{region}/subnetworks/{subnetwork_id}`                                                                                                                                                                                                                                                                                                                   |
| `labels`                                                                                                                                         | `map<string, string>` Labels to apply to this instance. These can be later modified by the setLabels method.                                                                                                                                                                                                                                                                                                                                             |
| `metadata`                                                                                                                                       | `map<string, string>` Custom metadata to apply to this instance. For example, to specify a Cloud Storage bucket for automatic backup, you can use the `gcs-data-bucket` metadata tag. Format: `"--metadata=gcs-data-bucket=BUCKET"` .                                                                                                                                                                                                                    |
| `tags[]`                                                                                                                                         | `string` Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).                                                                                                                                                                                                                                                                                               |
| `upgrade_history[]`                                                                                                                              | [`UpgradeHistoryEntry`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.UpgradeHistoryEntry) The upgrade history of this instance.                                                                                                                                                                                                         |
| `nic_type`                                                                                                                                       | [`NicType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.NicType) Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.                                                                                                                                                                              |
| `reservation_affinity`                                                                                                                           | [`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReservationAffinity) Optional. The optional reservation affinity. Setting this field will apply the specified [Zonal Compute Reservation](https://cloud.google.com/compute/docs/instances/reserving-zonal-resources) to this notebook instance.                             |
| `creator`                                                                                                                                        | `string` Output only. Email address of entity that sent original CreateInstance request.                                                                                                                                                                                                                                                                                                                                                                 |
| `can_ip_forward`                                                                                                                                 | `bool` Optional. Flag to enable ip forwarding or not, default false/off. <https://cloud.google.com/vpc/docs/using-routes#canipforward>                                                                                                                                                                                                                                                                                                                   |
| `create_time`                                                                                                                                    | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Instance creation time.                                                                                                                                                                                                                                                                                                                                   |
| `update_time`                                                                                                                                    | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Instance update time.                                                                                                                                                                                                                                                                                                                                     |
| `instance_migration_eligibility`                                                                                                                 | [`InstanceMigrationEligibility`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceMigrationEligibility) Output only. Checks how feasible a migration from UmN to WbI is.                                                                                                                                                                     |
| Union field `environment` . Type of the environment; can be one of VM image, or container image. `environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `vm_image`                                                                                                                                       | [`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VmImage) Use a Compute Engine VM image to start the notebook instance.                                                                                                                                                                                                                  |
| `container_image`                                                                                                                                | [`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ContainerImage) Use a container image to start the notebook instance.                                                                                                                                                                                                            |
| `migrated`                                                                                                                                       | `bool` Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance                                                                                                                                                                                                                                                                                                                                                      |

## AcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `core_count` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination. TPUs are not supported.

| Fields       |                                                                                                                                                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`       | [`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.AcceleratorType) Type of this accelerator. |
| `core_count` | `int64` Count of cores of this accelerator.                                                                                                                                                                                  |

## AcceleratorType

Definition of the types of hardware accelerators that can be used on this instance.

| Enums                          |                                                             |
|--------------------------------|-------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Accelerator type is not specified.                          |
| `NVIDIA_TESLA_K80`             | Accelerator type is Nvidia Tesla K80.                       |
| `NVIDIA_TESLA_P100`            | Accelerator type is Nvidia Tesla P100.                      |
| `NVIDIA_TESLA_V100`            | Accelerator type is Nvidia Tesla V100.                      |
| `NVIDIA_TESLA_P4`              | Accelerator type is Nvidia Tesla P4.                        |
| `NVIDIA_TESLA_T4`              | Accelerator type is Nvidia Tesla T4.                        |
| `NVIDIA_TESLA_A100`            | Accelerator type is Nvidia Tesla A100.                      |
| `NVIDIA_L4`                    | Accelerator type is Nvidia Tesla L4.                        |
| `NVIDIA_A100_80GB`             | Accelerator type is Nvidia Tesla A100 80GB.                 |
| `NVIDIA_TESLA_T4_VWS`          | Accelerator type is NVIDIA Tesla T4 Virtual Workstations.   |
| `NVIDIA_TESLA_P100_VWS`        | Accelerator type is NVIDIA Tesla P100 Virtual Workstations. |
| `NVIDIA_TESLA_P4_VWS`          | Accelerator type is NVIDIA Tesla P4 Virtual Workstations.   |
| `NVIDIA_H100_80GB`             | Accelerator type is NVIDIA H100 80GB.                       |
| `NVIDIA_H100_MEGA_80GB`        | Accelerator type is NVIDIA H100 Mega 80GB.                  |
| `TPU_V2`                       | (Coming soon) Accelerator type is TPU V2.                   |
| `TPU_V3`                       | (Coming soon) Accelerator type is TPU V3.                   |

## Disk

An instance-attached disk resource.

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
<td><code>auto_delete</code></td>
<td><p><code>bool</code></p>
<p>Indicates whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).</p></td>
</tr>
<tr class="even">
<td><code>boot</code></td>
<td><p><code>bool</code></p>
<p>Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.</p></td>
</tr>
<tr class="odd">
<td><code>device_name</code></td>
<td><p><code>string</code></p>
<p>Indicates a unique device name of your choice that is reflected into the <code>/dev/disk/by-id/google-*</code> tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.</p>
<p>If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine.This field is only applicable for persistent disks.</p></td>
</tr>
<tr class="even">
<td><code>disk_size_gb</code></td>
<td><p><code>int64</code></p>
<p>Indicates the size of the disk in base-2 GB.</p></td>
</tr>
<tr class="odd">
<td><code>guest_os_features[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.Disk.GuestOsFeature"><code>GuestOsFeature</code></a></p>
<p>Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.</p></td>
</tr>
<tr class="even">
<td><code>index</code></td>
<td><p><code>int64</code></p>
<p>A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.</p></td>
</tr>
<tr class="odd">
<td><code>interface</code></td>
<td><p><code>string</code></p>
<p>Indicates the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:</p>
<ul>
<li><code>NVME</code></li>
<li><code>SCSI</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>Type of the resource. Always compute#attachedDisk for attached disks.</p></td>
</tr>
<tr class="odd">
<td><code>licenses[]</code></td>
<td><p><code>string</code></p>
<p>A list of publicly visible licenses. Reserved for Google's use. A License represents billing and aggregate usage data for public and marketplace images.</p></td>
</tr>
<tr class="even">
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>The mode in which to attach this disk, either <code>READ_WRITE</code> or <code>READ_ONLY</code> . If not specified, the default is to attach the disk in <code>READ_WRITE</code> mode. Valid values:</p>
<ul>
<li><code>READ_ONLY</code></li>
<li><code>READ_WRITE</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>source</code></td>
<td><p><code>string</code></p>
<p>Indicates a valid partial or full URL to an existing Persistent Disk resource.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Indicates the type of the disk, either <code>SCRATCH</code> or <code>PERSISTENT</code> . Valid values:</p>
<ul>
<li><code>PERSISTENT</code></li>
<li><code>SCRATCH</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GuestOsFeature

Guest OS features for boot disk.

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
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>The ID of a supported feature. Read Enabling guest operating system features to see a list of available options. Valid values:</p>
<ul>
<li><code>FEATURE_TYPE_UNSPECIFIED</code></li>
<li><code>MULTI_IP_SUBNET</code></li>
<li><code>SECURE_BOOT</code></li>
<li><code>UEFI_COMPATIBLE</code></li>
<li><code>VIRTIO_SCSI_MULTIQUEUE</code></li>
<li><code>WINDOWS</code></li>
</ul></td>
</tr>
</tbody>
</table>

## DiskEncryption

Definition of the disk encryption options.

| Enums                         |                                                                |
|-------------------------------|----------------------------------------------------------------|
| `DISK_ENCRYPTION_UNSPECIFIED` | Disk encryption is not specified.                              |
| `GMEK`                        | Use Google managed encryption keys to encrypt the boot disk.   |
| `CMEK`                        | Use customer managed encryption keys to encrypt the boot disk. |

## DiskType

Possible disk types for notebook instances.

| Enums                   |                                |
|-------------------------|--------------------------------|
| `DISK_TYPE_UNSPECIFIED` | Disk type not set.             |
| `PD_STANDARD`           | Standard persistent disk type. |
| `PD_SSD`                | SSD persistent disk type.      |
| `PD_BALANCED`           | Balanced persistent disk type. |
| `PD_EXTREME`            | Extreme persistent disk type.  |

## NicType

The type of vNIC driver. Default should be UNSPECIFIED_NIC_TYPE.

| Enums                  |                    |
|------------------------|--------------------|
| `UNSPECIFIED_NIC_TYPE` | No type specified. |
| `VIRTIO_NET`           | VIRTIO             |
| `GVNIC`                | GVNIC              |

## ShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

| Fields                        |                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enable_secure_boot`          | `bool` Defines whether the instance has Secure Boot enabled. Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.                                                                |
| `enable_vtpm`                 | `bool` Defines whether the instance has the vTPM enabled. Enabled by default.                                                                                                                                                                                                                                                                   |
| `enable_integrity_monitoring` | `bool` Defines whether the instance has integrity monitoring enabled. Enables monitoring and attestation of the boot integrity of the instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the instance is created. Enabled by default. |

## State

The definition of the states of this instance.

| Enums               |                                                                                                      |
|---------------------|------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | State is not specified.                                                                              |
| `STARTING`          | The control logic is starting the instance.                                                          |
| `PROVISIONING`      | The control logic is installing required frameworks and registering the instance with notebook proxy |
| `ACTIVE`            | The instance is running.                                                                             |
| `STOPPING`          | The control logic is stopping the instance.                                                          |
| `STOPPED`           | The instance is stopped.                                                                             |
| `DELETED`           | The instance is deleted.                                                                             |
| `UPGRADING`         | The instance is upgrading.                                                                           |
| `INITIALIZING`      | The instance is being created.                                                                       |
| `REGISTERING`       | The instance is getting registered.                                                                  |
| `SUSPENDING`        | The instance is suspending.                                                                          |
| `SUSPENDED`         | The instance is suspended.                                                                           |

## UpgradeHistoryEntry

The entry of VM image upgrade history.

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
<td><code>snapshot</code></td>
<td><p><code>string</code></p>
<p>The snapshot of the boot disk of this notebook instance before upgrade.</p></td>
</tr>
<tr class="even">
<td><code>vm_image</code></td>
<td><p><code>string</code></p>
<p>The VM image before this instance upgrade.</p></td>
</tr>
<tr class="odd">
<td><code>container_image</code></td>
<td><p><code>string</code></p>
<p>The container image before this instance upgrade.</p></td>
</tr>
<tr class="even">
<td><code>framework</code></td>
<td><p><code>string</code></p>
<p>The framework of this notebook instance.</p></td>
</tr>
<tr class="odd">
<td><code>version</code></td>
<td><p><code>string</code></p>
<p>The version of the notebook instance before this upgrade.</p></td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.UpgradeHistoryEntry.State"><code>State</code></a></p>
<p>The state of this instance upgrade history entry.</p></td>
</tr>
<tr class="odd">
<td><code>create_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>The time that this instance upgrade history entry is created.</p></td>
</tr>
<tr class="even">
<td><code>target_image </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Target VM Image. Format: <code>ainotebooks-vm/project/image-name/name</code> .</p></td>
</tr>
<tr class="odd">
<td><code>action</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.UpgradeHistoryEntry.Action"><code>Action</code></a></p>
<p>Action. Rolloback or Upgrade.</p></td>
</tr>
<tr class="even">
<td><code>target_version</code></td>
<td><p><code>string</code></p>
<p>Target VM Version, like m63.</p></td>
</tr>
</tbody>
</table>

## Action

The definition of operations of this upgrade history entry.

| Enums                |                             |
|----------------------|-----------------------------|
| `ACTION_UNSPECIFIED` | Operation is not specified. |
| `UPGRADE`            | Upgrade.                    |
| `ROLLBACK`           | Rollback.                   |

## State

The definition of the states of this upgrade history entry.

| Enums               |                                    |
|---------------------|------------------------------------|
| `STATE_UNSPECIFIED` | State is not specified.            |
| `STARTED`           | The instance upgrade is started.   |
| `SUCCEEDED`         | The instance upgrade is succeeded. |
| `FAILED`            | The instance upgrade is failed.    |

## InstanceConfig

Notebook instance configurations that can be updated.

| Fields                      |                                                                                                                                                         |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `notebook_upgrade_schedule` | `string` Cron expression in UTC timezone, used to schedule instance auto upgrade. Please follow the [cron format](https://en.wikipedia.org/wiki/Cron) . |
| `enable_health_monitoring`  | `bool` Verifies core internal services are running.                                                                                                     |

## InstanceMigrationEligibility

InstanceMigrationEligibility represents the feasibility information of a migration from UmN to WbI.

| Fields       |                                                                                                                                                                                                                                                                                                                            |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `warnings[]` | [`Warning`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceMigrationEligibility.Warning) Output only. Certain configurations will be defaulted during the migration.                                         |
| `errors[]`   | [`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceMigrationEligibility.Error) Output only. Certain configurations make the UmN ineligible for an automatic migration. A manual migration is required. |

## Error

A migration error message means certain configurations make the UmN ineligible for an automatic migration. A manual migration is required.

| Enums               |                                                   |
|---------------------|---------------------------------------------------|
| `ERROR_UNSPECIFIED` | Default type.                                     |
| `DATAPROC_HUB`      | The UmN uses Dataproc Hub and cannot be migrated. |

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

| Enums                          |                                                                                                                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `WARNING_UNSPECIFIED`          | Default type.                                                                                                                                                                   |
| `UNSUPPORTED_MACHINE_TYPE`     | The UmN uses an machine type that's unsupported in WbI. It will be migrated with the default machine type e2-standard-4. Users can change the machine type after the migration. |
| `UNSUPPORTED_ACCELERATOR_TYPE` | The UmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. User can attach an accelerator after the migration.                     |
| `UNSUPPORTED_OS`               | The UmN uses an operating system that's unsupported in WbI (e.g. Debian 10, Ubuntu). It will be replaced with Debian 11 in WbI.                                                 |
| `NO_REMOVE_DATA_DISK`          | This UmN is configured with no_remove_data_disk, which is no longer available in WbI.                                                                                           |
| `GCS_BACKUP`                   | This UmN is configured with the Cloud Storage backup feature, which is no longer available in WbI.                                                                              |
| `POST_STARTUP_SCRIPT`          | This UmN is configured with a post startup script. Please optionally provide the `post_startup_script_option` for the migration.                                                |

## IsInstanceUpgradeableRequest

Request for checking if a notebook instance is upgradeable.

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
<td><code>notebook_instance</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>notebookInstance</code> :</p>
<ul>
<li><code>notebooks.instances.checkUpgradability</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpgradeType"><code>UpgradeType</code></a></p>
<p>Optional. The optional UpgradeType. Setting this field will search for additional compute images to upgrade this instance.</p></td>
</tr>
</tbody>
</table>

## IsInstanceUpgradeableResponse

Response for checking if a notebook instance is upgradeable.

| Fields            |                                                                                                                                                                     |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `upgradeable`     | `bool` If an instance is upgradeable.                                                                                                                               |
| `upgrade_version` | `string` The version this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.             |
| `upgrade_info`    | `string` Additional information about upgrade.                                                                                                                      |
| `upgrade_image`   | `string` The new image self link this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true. |

## ListEnvironmentsRequest

Request for listing environments.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.environments.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Maximum return size of the list call.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>A previous returned page token that can be used to continue listing from the last result.</p></td>
</tr>
</tbody>
</table>

## ListEnvironmentsResponse

Response for listing environments.

| Fields            |                                                                                                                                                                                                                    |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `environments[]`  | [`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Environment) A list of returned environments. |
| `next_page_token` | `string` A page token that can be used to continue listing from the last result in the next list call.                                                                                                             |
| `unreachable[]`   | `string` Locations that could not be reached.                                                                                                                                                                      |

## ListExecutionsRequest

Request for listing scheduled notebook executions.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.executions.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Maximum return size of the list call.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>A previous returned page token that can be used to continue listing from the last result.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Filter applied to resulting executions. Currently only supports filtering executions by a specified <code>schedule_id</code> . Format: <code>schedule_id=&lt;Schedule_ID&gt;</code></p></td>
</tr>
<tr class="odd">
<td><code>order_by</code></td>
<td><p><code>string</code></p>
<p>Sort by field.</p></td>
</tr>
</tbody>
</table>

## ListExecutionsResponse

Response for listing scheduled notebook executions

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
<td><code>executions[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution"><code>Execution</code></a></p>
<p>A list of returned instances.</p></td>
</tr>
<tr class="even">
<td><code>next_page_token</code></td>
<td><p><code>string</code></p>
<p>Page token that can be used to continue listing from the last result in the next list call.</p></td>
</tr>
<tr class="odd">
<td><code>unreachable[]</code></td>
<td><p><code>string</code></p>
<p>Executions IDs that could not be reached. For example:</p>
<pre data-fenced=""><code>[&#39;projects/{project_id}/location/{location}/executions/imagenet_test1&#39;,
 &#39;projects/{project_id}/location/{location}/executions/classifier_train1&#39;]</code></pre></td>
</tr>
</tbody>
</table>

## ListInstancesRequest

Request for listing notebook instances.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.instances.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Maximum return size of the list call.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>A previous returned page token that can be used to continue listing from the last result.</p></td>
</tr>
<tr class="even">
<td><code>order_by</code></td>
<td><p><code>string</code></p>
<p>Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).</p></td>
</tr>
<tr class="odd">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. List filter.</p></td>
</tr>
</tbody>
</table>

## ListInstancesResponse

Response for listing notebook instances.

| Fields            |                                                                                                                                                                                                           |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `instances[]`     | [`Instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance) A list of returned instances. |
| `next_page_token` | `string` Page token that can be used to continue listing from the last result in the next list call.                                                                                                      |
| `unreachable[]`   | `string` Locations that could not be reached. For example, `['us-west1-a', 'us-central1-b']` . A ListInstancesResponse will only contain either instances or unreachables,                                |

## ListRuntimesRequest

Request for listing Managed Notebook Runtimes.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.runtimes.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Maximum return size of the list call.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>A previous returned page token that can be used to continue listing from the last result.</p></td>
</tr>
<tr class="even">
<td><code>order_by</code></td>
<td><p><code>string</code></p>
<p>Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).</p></td>
</tr>
<tr class="odd">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Optional. List filter.</p></td>
</tr>
</tbody>
</table>

## ListRuntimesResponse

Response for listing Managed Notebook Runtimes.

| Fields            |                                                                                                                                                                                                        |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `runtimes[]`      | [`Runtime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime) A list of returned Runtimes. |
| `next_page_token` | `string` Page token that can be used to continue listing from the last result in the next list call.                                                                                                   |
| `unreachable[]`   | `string` Locations that could not be reached. For example, `['us-west1', 'us-central1']` . A ListRuntimesResponse will only contain either runtimes or unreachables,                                   |

## ListSchedulesRequest

Request for listing scheduled notebook job.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.schedules.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Maximum return size of the list call.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>A previous returned page token that can be used to continue listing from the last result.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>Filter applied to resulting schedules.</p></td>
</tr>
<tr class="odd">
<td><code>order_by</code></td>
<td><p><code>string</code></p>
<p>Field to order results by.</p></td>
</tr>
</tbody>
</table>

## ListSchedulesResponse

Response for listing scheduled notebook job.

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
<td><code>schedules[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Schedule"><code>Schedule</code></a></p>
<p>A list of returned instances.</p></td>
</tr>
<tr class="even">
<td><code>next_page_token</code></td>
<td><p><code>string</code></p>
<p>Page token that can be used to continue listing from the last result in the next list call.</p></td>
</tr>
<tr class="odd">
<td><code>unreachable[]</code></td>
<td><p><code>string</code></p>
<p>Schedules that could not be reached. For example:</p>
<pre data-fenced=""><code>[&#39;projects/{project_id}/location/{location}/schedules/monthly_digest&#39;,
 &#39;projects/{project_id}/location/{location}/schedules/weekly_sentiment&#39;]</code></pre></td>
</tr>
</tbody>
</table>

## LocalDisk

A Local attached disk resource.

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
<td><code>auto_delete</code></td>
<td><p><code>bool</code></p>
<p>Optional. Output only. Specifies whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).</p></td>
</tr>
<tr class="even">
<td><code>boot</code></td>
<td><p><code>bool</code></p>
<p>Optional. Output only. Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.</p></td>
</tr>
<tr class="odd">
<td><code>device_name</code></td>
<td><p><code>string</code></p>
<p>Optional. Output only. Specifies a unique device name of your choice that is reflected into the <code>/dev/disk/by-id/google-*</code> tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.</p>
<p>If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine. This field is only applicable for persistent disks.</p></td>
</tr>
<tr class="even">
<td><code>guest_os_features[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDisk.RuntimeGuestOsFeature"><code>RuntimeGuestOsFeature</code></a></p>
<p>Output only. Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.</p></td>
</tr>
<tr class="odd">
<td><code>index</code></td>
<td><p><code>int32</code></p>
<p>Output only. A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.</p></td>
</tr>
<tr class="even">
<td><code>initialize_params</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDiskInitializeParams"><code>LocalDiskInitializeParams</code></a></p>
<p>Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new instance.</p>
<p>This property is mutually exclusive with the source property; you can only define one or the other, but not both.</p></td>
</tr>
<tr class="odd">
<td><code>interface</code></td>
<td><p><code>string</code></p>
<p>Specifies the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:</p>
<ul>
<li><code>NVME</code></li>
<li><code>SCSI</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>Output only. Type of the resource. Always compute#attachedDisk for attached disks.</p></td>
</tr>
<tr class="odd">
<td><code>licenses[]</code></td>
<td><p><code>string</code></p>
<p>Output only. Any valid publicly visible licenses.</p></td>
</tr>
<tr class="even">
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>The mode in which to attach this disk, either <code>READ_WRITE</code> or <code>READ_ONLY</code> . If not specified, the default is to attach the disk in <code>READ_WRITE</code> mode. Valid values:</p>
<ul>
<li><code>READ_ONLY</code></li>
<li><code>READ_WRITE</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>source</code></td>
<td><p><code>string</code></p>
<p>Specifies a valid partial or full URL to an existing Persistent Disk resource.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Specifies the type of the disk, either <code>SCRATCH</code> or <code>PERSISTENT</code> . If not specified, the default is <code>PERSISTENT</code> . Valid values:</p>
<ul>
<li><code>PERSISTENT</code></li>
<li><code>SCRATCH</code></li>
</ul></td>
</tr>
</tbody>
</table>

## RuntimeGuestOsFeature

Optional. A list of features to enable on the guest operating system. Applicable only for bootable images. Read [Enabling guest operating system features](https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features) to see a list of available options. Guest OS features for boot disk.

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
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>The ID of a supported feature. Read <a href="https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features">Enabling guest operating system features</a> to see a list of available options.</p>
<p>Valid values:</p>
<ul>
<li><code>FEATURE_TYPE_UNSPECIFIED</code></li>
<li><code>MULTI_IP_SUBNET</code></li>
<li><code>SECURE_BOOT</code></li>
<li><code>UEFI_COMPATIBLE</code></li>
<li><code>VIRTIO_SCSI_MULTIQUEUE</code></li>
<li><code>WINDOWS</code></li>
</ul></td>
</tr>
</tbody>
</table>

## LocalDiskInitializeParams

Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new runtime. This property is mutually exclusive with the source property; you can only define one or the other, but not both.

| Fields         |                                                                                                                                                                                                                                                                                                                                |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `description`  | `string` Optional. Provide this property when creating the disk.                                                                                                                                                                                                                                                               |
| `disk_name`    | `string` Optional. Specifies the disk name. If not specified, the default is to use the name of the instance. If the disk with the instance name exists already in the given zone/region, a new name will be automatically generated.                                                                                          |
| `disk_size_gb` | `int64` Optional. Specifies the size of the disk in base-2 GB. If not specified, the disk will be the same size as the image (usually 10GB). If specified, the size must be equal to or larger than 10GB. Default 100 GB.                                                                                                      |
| `disk_type`    | [`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDiskInitializeParams.DiskType) Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ). |
| `labels`       | `map<string, string>` Optional. Labels to apply to this disk. These can be later modified by the disks.setLabels method. This field is only applicable for persistent disks.                                                                                                                                                   |

## DiskType

Possible disk types.

| Enums                   |                                |
|-------------------------|--------------------------------|
| `DISK_TYPE_UNSPECIFIED` | Disk type not set.             |
| `PD_STANDARD`           | Standard persistent disk type. |
| `PD_SSD`                | SSD persistent disk type.      |
| `PD_BALANCED`           | Balanced persistent disk type. |
| `PD_EXTREME`            | Extreme persistent disk type.  |

## MigrateInstanceRequest

Request for migrating a User-Managed Notebook to Workbench Instances.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires one or more of the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permissions on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.get</code></li>
<li><code>notebooks.instances.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>post_startup_script_option</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateInstanceRequest.PostStartupScriptOption"><code>PostStartupScriptOption</code></a></p>
<p>Optional. Specifies the behavior of post startup script during migration.</p></td>
</tr>
</tbody>
</table>

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

| Enums                                    |                                                                                          |
|------------------------------------------|------------------------------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED` | Post startup script option is not specified. Default is POST_STARTUP_SCRIPT_OPTION_SKIP. |
| `POST_STARTUP_SCRIPT_OPTION_SKIP`        | Not migrate the post startup script to the new Workbench Instance.                       |
| `POST_STARTUP_SCRIPT_OPTION_RERUN`       | Redownload and rerun the same post startup script as the User-Managed Notebook.          |

## MigrateInstanceResponse

This type has no fields.

Blank message response type for MigrateInstance.

## MigrateRuntimeRequest

Request for migrating a Runtime to a Workbench Instance.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires one or more of the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permissions on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.get</code></li>
<li><code>notebooks.instances.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>network</code></td>
<td><p><code>string</code></p>
<p>Optional. Name of the VPC that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same VPC, and this field must be empty. Format: <code>projects/{project_id}/global/networks/{network_id}</code></p></td>
</tr>
<tr class="odd">
<td><code>subnet</code></td>
<td><p><code>string</code></p>
<p>Optional. Name of the subnet that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same subnet, and this field must be empty. Format: <code>projects/{project_id}/regions/{region}/subnetworks/{subnetwork_id}</code></p></td>
</tr>
<tr class="even">
<td><code>service_account</code></td>
<td><p><code>string</code></p>
<p>Optional. The service account to be included in the Compute Engine instance of the new Workbench Instance when the Runtime uses "single user only" mode for permission. If not specified, the <a href="https://cloud.google.com/compute/docs/access/service-accounts#default_service_account">Compute Engine default service account</a> is used. When the Runtime uses service account mode for permission, it will reuse the same service account, and this field must be empty.</p></td>
</tr>
<tr class="odd">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Optional. Idempotent request UUID.</p></td>
</tr>
<tr class="even">
<td><code>post_startup_script_option</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.MigrateRuntimeRequest.PostStartupScriptOption"><code>PostStartupScriptOption</code></a></p>
<p>Optional. Specifies the behavior of post startup script during migration.</p></td>
</tr>
</tbody>
</table>

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

| Enums                                    |                                                                                          |
|------------------------------------------|------------------------------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED` | Post startup script option is not specified. Default is POST_STARTUP_SCRIPT_OPTION_SKIP. |
| `POST_STARTUP_SCRIPT_OPTION_SKIP`        | Not migrate the post startup script to the new Workbench Instance.                       |
| `POST_STARTUP_SCRIPT_OPTION_RERUN`       | Redownload and rerun the same post startup script as the Google-Managed Notebook.        |

## OperationMetadata

Represents the metadata of the long-running operation.

| Fields                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `create_time`            | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the operation was created.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `end_time`               | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) The time the operation finished running.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `target`                 | `string` Server-defined resource path for the target of the operation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `verb`                   | `string` Name of the verb executed by the operation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `status_message`         | `string` Human-readable status of the operation, if any.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `requested_cancellation` | `bool` Identifies whether the user has requested cancellation of the operation. Operations that have successfully been cancelled have [`google.longrunning.Operation.error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.longrunning#google.longrunning.Operation.FIELDS.google.rpc.Status.google.longrunning.Operation.error) value with a [`google.rpc.Status.code`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.rpc#google.rpc.Status.FIELDS.int32.google.rpc.Status.code) of `1` , corresponding to `Code.CANCELLED` . |
| `api_version`            | `string` API version used to start the operation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `endpoint`               | `string` API endpoint name of this operation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## RegisterInstanceRequest

Request for registering a notebook instance.

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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{project_id}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.instances.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>instance_id</code></td>
<td><p><code>string</code></p>
<p>Required. User defined unique ID of this instance. The <code>instance_id</code> must be 1 to 63 characters long and contain only lowercase letters, numeric characters, and dashes. The first character must be a lowercase letter and the last character cannot be a dash.</p></td>
</tr>
</tbody>
</table>

## ReportInstanceInfoRequest

Request for notebook instances to report information to Notebooks API.

| Fields     |                                                                                                                                                   |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`                                                   |
| `vm_id`    | `string` Required. The VM hardware token for authenticating the VM. <https://cloud.google.com/compute/docs/instances/verifying-instance-identity> |
| `metadata` | `map<string, string>` The metadata reported to Notebooks API. This will be merged to the instance metadata store                                  |

## ReportRuntimeEventRequest

Request for reporting a Managed Notebook Event.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>iam.permissions.none</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>vm_id</code></td>
<td><p><code>string</code></p>
<p>Required. The VM hardware token for authenticating the VM. <a href="https://cloud.google.com/compute/docs/instances/verifying-instance-identity">https://cloud.google.com/compute/docs/instances/verifying-instance-identity</a></p></td>
</tr>
<tr class="odd">
<td><code>event</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Event"><code>Event</code></a></p>
<p>Required. The Event to be reported.</p></td>
</tr>
</tbody>
</table>

## ReservationAffinity

Reservation Affinity for consuming Zonal reservation.

| Fields                     |                                                                                                                                                                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consume_reservation_type` | [`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ReservationAffinity.Type) Optional. Type of reservation to consume |
| `key`                      | `string` Optional. Corresponds to the label key of reservation resource.                                                                                                                                                         |
| `values[]`                 | `string` Optional. Corresponds to the label values of reservation resource.                                                                                                                                                      |

## Type

Indicates whether to consume capacity from an reservation or not.

| Enums                  |                                                                                                          |
|------------------------|----------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default type.                                                                                            |
| `NO_RESERVATION`       | Do not consume from any allocated capacity.                                                              |
| `ANY_RESERVATION`      | Consume any reservation available.                                                                       |
| `SPECIFIC_RESERVATION` | Must consume from a specific reservation. Must specify key value fields for specifying the reservations. |

## ResetInstanceRequest

Request for resetting a notebook instance

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.reset</code></li>
</ul></td>
</tr>
</tbody>
</table>

## ResetRuntimeRequest

Request for resetting a Managed Notebook Runtime.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.reset</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## RollbackInstanceRequest

Request for rollbacking a notebook instance

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>iam.permissions.none</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>target_snapshot</code></td>
<td><p><code>string</code></p>
<p>Required. The snapshot for rollback. Example: <code>projects/test-project/global/snapshots/krwlzipynril</code> .</p></td>
</tr>
</tbody>
</table>

## Runtime

The definition of a Runtime for a managed notebook instance.

| Fields                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                        | `string` Output only. The resource name of the runtime. Format: `projects/{project}/locations/{location}/runtimes/{runtimeId}`                                                                                                                                                                                                                                                                                                         |
| `state`                                                                                                                                       | [`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime.State) Output only. Runtime state.                                                                                                                                                                                                                              |
| `health_state`                                                                                                                                | [`HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime.HealthState) Output only. Runtime health_state.                                                                                                                                                                                                           |
| `access_config`                                                                                                                               | [`RuntimeAccessConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAccessConfig) The config settings for accessing runtime.                                                                                                                                                                                           |
| `software_config`                                                                                                                             | [`RuntimeSoftwareConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeSoftwareConfig) The config settings for software inside the runtime.                                                                                                                                                                             |
| `metrics`                                                                                                                                     | [`RuntimeMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMetrics) Output only. Contains Runtime daemon metrics such as Service status and JupyterLab stats.                                                                                                                                                      |
| `create_time`                                                                                                                                 | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Runtime creation time.                                                                                                                                                                                                                                                                                                                  |
| `update_time`                                                                                                                                 | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Runtime update time.                                                                                                                                                                                                                                                                                                                    |
| `labels`                                                                                                                                      | `map<string, string>` Optional. The labels to associate with this Managed Notebook or Runtime. Label **keys** must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . Label **values** may be empty, but, if present, must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . No more than 32 labels can be associated with a cluster. |
| `runtime_migration_eligibility`                                                                                                               | [`RuntimeMigrationEligibility`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMigrationEligibility) Output only. Checks how feasible a migration from GmN to WbI is.                                                                                                                                                     |
| Union field `runtime_type` . Type of the runtime; currently only supports Compute Engine VM. `runtime_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `virtual_machine`                                                                                                                             | [`VirtualMachine`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachine) Use a Compute Engine VM image to start the managed notebook instance.                                                                                                                                                                          |
| `migrated`                                                                                                                                    | `bool` Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance                                                                                                                                                                                                                                                                                                                                    |

## HealthState

The runtime substate.

| Enums                      |                                                                                                                           |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | The runtime substate is unknown.                                                                                          |
| `HEALTHY`                  | The runtime is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.       |
| `UNHEALTHY`                | The runtime is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state. |
| `AGENT_NOT_INSTALLED`      | The runtime has not installed health monitoring agent. Applies to ACTIVE state.                                           |
| `AGENT_NOT_RUNNING`        | The runtime health monitoring agent is not running. Applies to ACTIVE state.                                              |

## State

The definition of the states of this runtime.

| Enums               |                                                                                                                         |
|---------------------|-------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | State is not specified.                                                                                                 |
| `STARTING`          | The compute layer is starting the runtime. It is not ready for use.                                                     |
| `PROVISIONING`      | The compute layer is installing required frameworks and registering the runtime with notebook proxy. It cannot be used. |
| `ACTIVE`            | The runtime is currently running. It is ready for use.                                                                  |
| `STOPPING`          | The control logic is stopping the runtime. It cannot be used.                                                           |
| `STOPPED`           | The runtime is stopped. It cannot be used.                                                                              |
| `DELETING`          | The runtime is being deleted. It cannot be used.                                                                        |
| `UPGRADING`         | The runtime is upgrading. It cannot be used.                                                                            |
| `INITIALIZING`      | The runtime is being created and set up. It is not ready for use.                                                       |

## RuntimeAcceleratorConfig

Definition of the types of hardware accelerators that can be used. See [Compute Engine AcceleratorTypes](https://cloud.google.com/compute/docs/reference/beta/acceleratorTypes) . Examples:

- `nvidia-tesla-k80`
- `nvidia-tesla-p100`
- `nvidia-tesla-v100`
- `nvidia-tesla-p4`
- `nvidia-tesla-t4`
- `nvidia-tesla-a100`

| Fields       |                                                                                                                                                                                                                                       |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`       | [`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAcceleratorConfig.AcceleratorType) Accelerator model. |
| `core_count` | `int64` Count of cores of this accelerator.                                                                                                                                                                                           |

## AcceleratorType

Type of this accelerator.

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
<td><code>ACCELERATOR_TYPE_UNSPECIFIED</code></td>
<td>Accelerator type is not specified.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_K80</code></td>
<td><p>Accelerator type is Nvidia Tesla K80.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_P100</code></td>
<td>Accelerator type is Nvidia Tesla P100.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_V100</code></td>
<td>Accelerator type is Nvidia Tesla V100.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_P4</code></td>
<td>Accelerator type is Nvidia Tesla P4.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_T4</code></td>
<td>Accelerator type is Nvidia Tesla T4.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_A100</code></td>
<td>Accelerator type is Nvidia Tesla A100 - 40GB.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_L4</code></td>
<td>Accelerator type is Nvidia L4.</td>
</tr>
<tr class="odd">
<td><code>TPU_V2</code></td>
<td>(Coming soon) Accelerator type is TPU V2.</td>
</tr>
<tr class="even">
<td><code>TPU_V3</code></td>
<td>(Coming soon) Accelerator type is TPU V3.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_T4_VWS</code></td>
<td>Accelerator type is NVIDIA Tesla T4 Virtual Workstations.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_P100_VWS</code></td>
<td>Accelerator type is NVIDIA Tesla P100 Virtual Workstations.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_P4_VWS</code></td>
<td>Accelerator type is NVIDIA Tesla P4 Virtual Workstations.</td>
</tr>
</tbody>
</table>

## RuntimeAccessConfig

Specifies the login configuration for Runtime

| Fields          |                                                                                                                                                                                                                                                          |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `access_type`   | [`RuntimeAccessType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAccessConfig.RuntimeAccessType) The type of access mode this instance. |
| `runtime_owner` | `string` The owner of this runtime after creation. Format: `alias@example.com` Currently supports one owner only.                                                                                                                                        |
| `proxy_uri`     | `string` Output only. The proxy endpoint that is used to access the runtime.                                                                                                                                                                             |

## RuntimeAccessType

Possible ways to access runtime. Authentication mode. Currently supports: Single User only.

| Enums                             |                                                                                                                                                                                                                                      |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `RUNTIME_ACCESS_TYPE_UNSPECIFIED` | Unspecified access.                                                                                                                                                                                                                  |
| `SINGLE_USER`                     | Single user login.                                                                                                                                                                                                                   |
| `SERVICE_ACCOUNT`                 | Service Account mode. In Service Account mode, Runtime creator will specify a SA that exists in the consumer project. Using Runtime Service Account field. Users accessing the Runtime need ActAs (Service Account User) permission. |

## RuntimeMetrics

Contains runtime daemon metrics, such as OS and kernels and sessions stats.

| Fields           |                                                        |
|------------------|--------------------------------------------------------|
| `system_metrics` | `map<string, string>` Output only. The system metrics. |

## RuntimeMigrationEligibility

RuntimeMigrationEligibility represents the feasibility information of a migration from GmN to WbI.

| Fields       |                                                                                                                                                                                                                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `warnings[]` | [`Warning`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMigrationEligibility.Warning) Output only. Certain configurations will be defaulted during the migration.                                         |
| `errors[]`   | [`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeMigrationEligibility.Error) Output only. Certain configurations make the GmN ineligible for an automatic migration. A manual migration is required. |

## Error

A migration error message means certain configurations make the GmN ineligible for an automatic migration. A manual migration is required.

| Enums               |                                                                        |
|---------------------|------------------------------------------------------------------------|
| `ERROR_UNSPECIFIED` | Default type.                                                          |
| `CUSTOM_CONTAINER`  | The GmN is configured with custom container(s) and cannot be migrated. |

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

| Enums                          |                                                                                                                                                              |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `WARNING_UNSPECIFIED`          | Default type.                                                                                                                                                |
| `UNSUPPORTED_ACCELERATOR_TYPE` | The GmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. Users can attach an accelerator after the migration. |
| `UNSUPPORTED_OS`               | The GmN uses an operating system that's unsupported in WbI (e.g. Debian 10). It will be replaced with Debian 11 in WbI.                                      |
| `RESERVED_IP_RANGE`            | This GmN is configured with reserved IP range, which is no longer applicable in WbI.                                                                         |
| `GOOGLE_MANAGED_NETWORK`       | This GmN is configured with a Google managed network. Please provide the `network` and `subnet` options for the migration.                                   |
| `POST_STARTUP_SCRIPT`          | This GmN is configured with a post startup script. Please optionally provide the `post_startup_script_option` for the migration.                             |
| `SINGLE_USER`                  | This GmN is configured with single user mode. Please optionally provide the `service_account` option for the migration.                                      |

## RuntimeShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

| Fields                        |                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enable_secure_boot`          | `bool` Defines whether the instance has Secure Boot enabled. Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.                                                                |
| `enable_vtpm`                 | `bool` Defines whether the instance has the vTPM enabled. Enabled by default.                                                                                                                                                                                                                                                                   |
| `enable_integrity_monitoring` | `bool` Defines whether the instance has integrity monitoring enabled. Enables monitoring and attestation of the boot integrity of the instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the instance is created. Enabled by default. |

## RuntimeSoftwareConfig

Specifies the selection and configuration of software inside the runtime. The properties to set on runtime. Properties keys are specified in `key:value` format, for example:

- `idle_shutdown: true`
- `idle_shutdown_timeout: 180`
- `enable_health_monitoring: true`

| Fields                         |                                                                                                                                                                                                                                                                              |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `notebook_upgrade_schedule`    | `string` Cron expression in UTC timezone, used to schedule instance auto upgrade. Please follow the [cron format](https://en.wikipedia.org/wiki/Cron) .                                                                                                                      |
| `idle_shutdown_timeout`        | `int32` Time in minutes to wait before shutting down runtime. Default: 180 minutes                                                                                                                                                                                           |
| `install_gpu_driver`           | `bool` Install Nvidia Driver automatically. Default: True                                                                                                                                                                                                                    |
| `custom_gpu_driver_path`       | `string` Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.                                                                                                                         |
| `post_startup_script`          | `string` Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).                                                                                             |
| `kernels[]`                    | [`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ContainerImage) Optional. Use a list of container images to use as Kernels in the notebook instance. |
| `post_startup_script_behavior` | [`PostStartupScriptBehavior`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeSoftwareConfig.PostStartupScriptBehavior) Behavior for the post startup script.    |
| `enable_health_monitoring`     | `bool` Verifies core internal services are running. Default: True                                                                                                                                                                                                            |
| `idle_shutdown`                | `bool` Runtime will automatically shutdown after idle_shutdown_time. Default: True                                                                                                                                                                                           |
| `upgradeable`                  | `bool` Output only. Bool indicating whether an newer image is available in an image family.                                                                                                                                                                                  |
| `disable_terminal`             | `bool` Bool indicating whether JupyterLab terminal will be available or not. Default: False                                                                                                                                                                                  |
| `version`                      | `string` Output only. version of boot image such as M100, from release label of the image.                                                                                                                                                                                   |
| `mixer_disabled`               | `bool` Bool indicating whether mixer client should be disabled. Default: False                                                                                                                                                                                               |

## PostStartupScriptBehavior

Behavior for the post startup script.

| Enums                                      |                                                                           |
|--------------------------------------------|---------------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` | Unspecified post startup script behavior. Will run only once at creation. |
| `RUN_EVERY_START`                          | Runs the post startup script provided during creation at every start.     |
| `DOWNLOAD_AND_RUN_EVERY_START`             | Downloads and runs the provided post startup script at every start.       |

## Schedule

The definition of a schedule.

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                | `string` Output only. The name of this schedule. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`                                                                                                                                                                                                                                                                                                                                |
| `display_name`        | `string` Output only. Display name used for UI purposes. Name can only contain alphanumeric characters, hyphens `-` , and underscores `_` .                                                                                                                                                                                                                                                                                                                  |
| `description`         | `string` A brief description of this environment.                                                                                                                                                                                                                                                                                                                                                                                                            |
| `state`               | [`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Schedule.State)                                                                                                                                                                                                                                                                               |
| `cron_schedule`       | `string` Cron-tab formatted schedule by which the job will execute. Format: minute, hour, day of month, month, day of week, e.g. `0 0 * * WED` = every Wednesday More examples: <https://crontab.guru/examples.html>                                                                                                                                                                                                                                         |
| `time_zone`           | `string` Timezone on which the cron_schedule. The value of this field must be a time zone name from the tz database. TZ Database: <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones> Note that some time zones include a provision for daylight savings time. The rules for daylight saving time are determined by the chosen tz. For UTC use the string "utc". If a time zone is not specified, the default will be in UTC (also known as GMT). |
| `create_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time the schedule was created.                                                                                                                                                                                                                                                                                                                                |
| `update_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time the schedule was last updated.                                                                                                                                                                                                                                                                                                                           |
| `execution_template`  | [`ExecutionTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ExecutionTemplate) Notebook Execution Template corresponding to this schedule.                                                                                                                                                                                                    |
| `recent_executions[]` | [`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Execution) Output only. The most recent execution names triggered from this schedule and their corresponding states.                                                                                                                                                                      |

## State

State of the job.

| Enums               |                                                                                                                                                                                                                                                                                                       |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified state.                                                                                                                                                                                                                                                                                    |
| `ENABLED`           | The job is executing normally.                                                                                                                                                                                                                                                                        |
| `PAUSED`            | The job is paused by the user. It will not execute. A user can intentionally pause the job using [Cloud Scheduler](https://cloud.google.com/scheduler/docs/creating#pause) .                                                                                                                          |
| `DISABLED`          | The job is disabled by the system due to error. The user cannot directly set a job to be disabled.                                                                                                                                                                                                    |
| `UPDATE_FAILED`     | The job state resulting from a failed [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) operation. To recover a job from this state, retry [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) until a successful response is received. |
| `INITIALIZING`      | The schedule resource is being created.                                                                                                                                                                                                                                                               |
| `DELETING`          | The schedule resource is being deleted.                                                                                                                                                                                                                                                               |

## SetInstanceAcceleratorRequest

Request for setting instance accelerator.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.setAccelerator</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.AcceleratorType"><code>AcceleratorType</code></a></p>
<p>Required. Type of this accelerator.</p></td>
</tr>
<tr class="odd">
<td><code>core_count</code></td>
<td><p><code>int64</code></p>
<p>Required. Count of cores of this accelerator. Note that not all combinations of <code>type</code> and <code>core_count</code> are valid. See <a href="https://cloud.google.com/compute/docs/gpus/#gpus-list">GPUs on Compute Engine</a> to find a valid combination. TPUs are not supported.</p></td>
</tr>
</tbody>
</table>

## SetInstanceLabelsRequest

Request for setting instance labels.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.setLabels</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Labels to apply to this instance. These can be later modified by the setLabels method</p></td>
</tr>
</tbody>
</table>

## SetInstanceMachineTypeRequest

Request for setting instance machine type.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.setMachineType</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>machine_type</code></td>
<td><p><code>string</code></p>
<p>Required. The <a href="https://cloud.google.com/compute/docs/machine-resource">Compute Engine machine type</a> .</p></td>
</tr>
</tbody>
</table>

## StartInstanceRequest

Request for starting a notebook instance

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.start</code></li>
</ul></td>
</tr>
</tbody>
</table>

## StartRuntimeRequest

Request for starting a Managed Notebook Runtime.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.start</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## StopInstanceRequest

Request for stopping a notebook instance

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.stop</code></li>
</ul></td>
</tr>
</tbody>
</table>

## StopRuntimeRequest

Request for stopping a Managed Notebook Runtime.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.stop</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## SwitchRuntimeRequest

Request for switching a Managed Notebook Runtime.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/runtimes/{runtime_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.runtimes.switch</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>machine_type</code></td>
<td><p><code>string</code></p>
<p>machine type.</p></td>
</tr>
<tr class="odd">
<td><code>accelerator_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAcceleratorConfig"><code>RuntimeAcceleratorConfig</code></a></p>
<p>accelerator config.</p></td>
</tr>
<tr class="even">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## UpdateInstanceConfigRequest

Request for updating instance configurations.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.updateConfig</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.InstanceConfig"><code>InstanceConfig</code></a></p>
<p>The instance configurations to be updated.</p></td>
</tr>
</tbody>
</table>

## UpdateInstanceMetadataItemsRequest

Request for adding/changing metadata items for an instance.

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.updateConfig</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>items</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Metadata items to add/update for the instance.</p></td>
</tr>
</tbody>
</table>

## UpdateInstanceMetadataItemsResponse

Response for adding/changing metadata items for an instance.

| Fields  |                                                                                |
|---------|--------------------------------------------------------------------------------|
| `items` | `map<string, string>` Map of items that were added/updated to/in the metadata. |

## UpdateRuntimeRequest

Request for updating a Managed Notebook configuration.

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
<td><code>runtime</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Runtime"><code>Runtime</code></a></p>
<p>Required. The Runtime to be updated.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>runtime</code> :</p>
<ul>
<li><code>notebooks.runtimes.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Required. Specifies the path, relative to <code>Runtime</code> , of the field to update. For example, to change the software configuration kernels, the <code>update_mask</code> parameter would be specified as <code>software_config.kernels</code> , and the <code>PATCH</code> request body would specify the new value, as follows:</p>
<pre data-fenced=""><code>{
  &quot;software_config&quot;:{
    &quot;kernels&quot;: [{
       &#39;repository&#39;:
       &#39;gcr.io/deeplearning-platform-release/pytorch-gpu&#39;, &#39;tag&#39;:
       &#39;latest&#39; }],
    }
}</code></pre>
<p>Currently, only the following fields can be updated:</p>
<ul>
<li><code>software_config.kernels</code></li>
<li><code>software_config.post_startup_script</code></li>
<li><code>software_config.custom_gpu_driver_path</code></li>
<li><code>software_config.idle_shutdown</code></li>
<li><code>software_config.idle_shutdown_timeout</code></li>
<li><code>software_config.disable_terminal</code></li>
<li><code>labels</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>request_id</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

## UpdateShieldedInstanceConfigRequest

Request for updating the Shielded Instance config for a notebook instance. You can only use this method on a stopped instance

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.updateShieldInstanceConfig</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>shielded_instance_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.Instance.ShieldedInstanceConfig"><code>ShieldedInstanceConfig</code></a></p>
<p>ShieldedInstance configuration to be updated.</p></td>
</tr>
</tbody>
</table>

## UpgradeInstanceRequest

Request for upgrading a notebook instance

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{project_id}/locations/{location}/instances/{instance_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.upgrade</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.UpgradeType"><code>UpgradeType</code></a></p>
<p>Optional. The optional UpgradeType. Setting this field will search for additional compute images to upgrade this instance.</p></td>
</tr>
</tbody>
</table>

## UpgradeType

Definition of the types of upgrade that can be used on this instance.

| Enums                      |                                       |
|----------------------------|---------------------------------------|
| `UPGRADE_TYPE_UNSPECIFIED` | Upgrade type is not specified.        |
| `UPGRADE_FRAMEWORK`        | Upgrade ML framework.                 |
| `UPGRADE_OS`               | Upgrade Operating System.             |
| `UPGRADE_CUDA`             | Upgrade CUDA.                         |
| `UPGRADE_ALL`              | Upgrade All (OS, Framework and CUDA). |

## VirtualMachine

Runtime using Virtual Machine for computing.

| Fields                   |                                                                                                                                                                                                                                             |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `instance_name`          | `string` Output only. The user-friendly name of the Managed Compute Engine instance.                                                                                                                                                        |
| `instance_id`            | `string` Output only. The unique identifier of the Managed Compute Engine instance.                                                                                                                                                         |
| `virtual_machine_config` | [`VirtualMachineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachineConfig) Virtual Machine configuration settings. |

## VirtualMachineConfig

The config settings for virtual machine.

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
<td><code>zone</code></td>
<td><p><code>string</code></p>
<p>Output only. The zone where the virtual machine is located. If using regional request, the notebooks service will pick a location in the corresponding runtime region. On a get request, zone will always be present. Example: * <code>us-central1-b</code></p></td>
</tr>
<tr class="even">
<td><code>machine_type</code></td>
<td><p><code>string</code></p>
<p>Required. The Compute Engine machine type used for runtimes. Short name is valid. Examples: * <code>n1-standard-2</code> * <code>e2-standard-8</code></p></td>
</tr>
<tr class="odd">
<td><code>container_images[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.ContainerImage"><code>ContainerImage</code></a></p>
<p>Optional. Use a list of container images to use as Kernels in the notebook instance.</p></td>
</tr>
<tr class="even">
<td><code>data_disk</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.LocalDisk"><code>LocalDisk</code></a></p>
<p>Required. Data disk option configuration settings.</p></td>
</tr>
<tr class="odd">
<td><code>encryption_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.EncryptionConfig"><code>EncryptionConfig</code></a></p>
<p>Optional. Encryption settings for virtual machine data disk.</p></td>
</tr>
<tr class="even">
<td><code>shielded_instance_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeShieldedInstanceConfig"><code>RuntimeShieldedInstanceConfig</code></a></p>
<p>Optional. Shielded VM Instance configuration settings.</p></td>
</tr>
<tr class="odd">
<td><code>accelerator_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.RuntimeAcceleratorConfig"><code>RuntimeAcceleratorConfig</code></a></p>
<p>Optional. The Compute Engine accelerator configuration for this runtime.</p></td>
</tr>
<tr class="even">
<td><code>network</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine network to be used for machine communications. Cannot be specified with subnetwork. If neither <code>network</code> nor <code>subnet</code> is specified, the "default" network of the project is used, if it exists.</p>
<p>A full URL or partial URI. Examples:</p>
<ul>
<li><code>https://www.googleapis.com/compute/v1/projects/[project_id]/global/networks/default</code></li>
<li><code>projects/[project_id]/global/networks/default</code></li>
</ul>
<p>Runtimes are managed resources inside Google Infrastructure. Runtimes support the following network configurations:</p>
<ul>
<li>Google Managed Network (Network &amp; subnet are empty)</li>
<li>Consumer Project VPC (network &amp; subnet are required). Requires configuring Private Service Access.</li>
<li>Shared VPC (network &amp; subnet are required). Requires configuring Private Service Access.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>subnet</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine subnetwork to be used for machine communications. Cannot be specified with network.</p>
<p>A full URL or partial URI are valid. Examples:</p>
<ul>
<li><code>https://www.googleapis.com/compute/v1/projects/[project_id]/regions/us-east1/subnetworks/sub0</code></li>
<li><code>projects/[project_id]/regions/us-east1/subnetworks/sub0</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>internal_ip_only</code></td>
<td><p><code>bool</code></p>
<p>Optional. If true, runtime will only have internal IP addresses. By default, runtimes are not restricted to internal IP addresses, and will have ephemeral external IP addresses assigned to each vm. This <code>internal_ip_only</code> restriction can only be enabled for subnetwork enabled networks, and all dependencies must be configured to be accessible without external IP addresses.</p></td>
</tr>
<tr class="odd">
<td><code>tags[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine network tags to add to runtime (see <a href="https://cloud.google.com/vpc/docs/add-remove-network-tags">Add network tags</a> ).</p></td>
</tr>
<tr class="even">
<td><code>guest_attributes</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Output only. The Compute Engine guest attributes. (see <a href="https://cloud.google.com/compute/docs/storing-retrieving-metadata#guest_attributes">Project and instance guest attributes</a> ).</p></td>
</tr>
<tr class="odd">
<td><code>metadata</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Optional. The Compute Engine metadata entries to add to virtual machine. (see <a href="https://cloud.google.com/compute/docs/storing-retrieving-metadata#project_and_instance_metadata">Project and instance metadata</a> ).</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Optional. The labels to associate with this runtime. Label <strong>keys</strong> must contain 1 to 63 characters, and must conform to <a href="https://www.ietf.org/rfc/rfc1035.txt">RFC 1035</a> . Label <strong>values</strong> may be empty, but, if present, must contain 1 to 63 characters, and must conform to <a href="https://www.ietf.org/rfc/rfc1035.txt">RFC 1035</a> . No more than 32 labels can be associated with a cluster.</p></td>
</tr>
<tr class="odd">
<td><code>nic_type</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachineConfig.NicType"><code>NicType</code></a></p>
<p>Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.</p></td>
</tr>
<tr class="even">
<td><code>reserved_ip_range</code></td>
<td><p><code>string</code></p>
<p>Optional. Reserved IP Range name is used for VPC Peering. The subnetwork allocation will use the range <em>name</em> if it's assigned.</p>
<p>Example: managed-notebooks-range-c</p>
<pre data-fenced=""><code>PEERING_RANGE_NAME_3=managed-notebooks-range-c
gcloud compute addresses create $PEERING_RANGE_NAME_3 \
  --global \
  --prefix-length=24 \
  --description=&quot;Google Cloud Managed Notebooks Range 24 c&quot; \
  --network=$NETWORK \
  --addresses=192.168.0.0 \
  --purpose=VPC_PEERING</code></pre>
<p>Field value will be: <code>managed-notebooks-range-c</code></p></td>
</tr>
<tr class="odd">
<td><code>boot_image</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1#google.cloud.notebooks.v1.VirtualMachineConfig.BootImage"><code>BootImage</code></a></p>
<p>Optional. Boot image metadata used for runtime upgradeability.</p></td>
</tr>
</tbody>
</table>

## BootImage

This type has no fields.

Definition of the boot image used by the Runtime. Used to facilitate runtime upgradeability.

## NicType

The type of vNIC driver. Default should be UNSPECIFIED_NIC_TYPE.

| Enums                  |                    |
|------------------------|--------------------|
| `UNSPECIFIED_NIC_TYPE` | No type specified. |
| `VIRTIO_NET`           | VIRTIO             |
| `GVNIC`                | GVNIC              |

## VmImage

Definition of a custom Compute Engine virtual machine image for starting a notebook instance with the environment installed directly on the VM.

| Fields                                                                                                                |                                                                                                               |
|-----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `project`                                                                                                             | `string` Required. The name of the Google Cloud project that this VM image belongs to. Format: `{project_id}` |
| Union field `image` . The reference to an external Compute Engine VM image. `image` can be only one of the following: |                                                                                                               |
| `image_name`                                                                                                          | `string` Use VM image name to find the image.                                                                 |
| `image_family`                                                                                                        | `string` Use this VM image family to find the image; the newest image in this family will be used.            |
