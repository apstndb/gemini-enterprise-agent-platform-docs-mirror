---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/audit-logging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/audit-logging
title: Agent Platform audit logging information
description: Learn about the audit logs created by Agent Platform as part of Cloud Audit Logs.
data_source: docs.cloud.google.com
---

This document describes the audit logs created by Gemini Enterprise Agent Platform as part of [Cloud Audit Logs](https://docs.cloud.google.com/logging/docs/audit) .

## Overview

Google Cloud services write audit logs to help you answer the questions, "Who did what, where, and when?" within your Google Cloud resources.

Your Google Cloud projects contain only the audit logs for resources that are directly within the Google Cloud project. Other Google Cloud resources, such as folders, organizations, and billing accounts, contain the audit logs for the entity itself.

For a general overview of Cloud Audit Logs, see [Cloud Audit Logs overview](https://docs.cloud.google.com/logging/docs/audit) . For a deeper understanding of the audit log format, see [Understand audit logs](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs) .

## Available audit logs

The following types of audit logs are available for Agent Platform:

- Admin Activity audit logs

  Includes "admin write" operations that write metadata or configuration information.

  You can't disable Admin Activity audit logs.

- Data Access audit logs

  Includes "admin read" operations that read metadata or configuration information. Also includes "data read" and "data write" operations that read or write user-provided data.

  To receive Data Access audit logs, you must [explicitly enable](https://docs.cloud.google.com/logging/docs/audit/configure-data-access#config-console-enable) them.

- System Event audit logs

  Identifies automated Google Cloud actions that modify the configuration of resources.

  You can't disable System Event audit logs.

For fuller descriptions of the audit log types, see [Types of audit logs](https://docs.cloud.google.com/logging/docs/audit#types) .

## Audited operations

The following table summarizes which API operations correspond to each audit log type in Agent Platform:

| Audit logs category                 | Agent Platform operations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Admin Activity audit logs           | batchPredictionJobs.cancel batchPredictionJobs.create batchPredictionJobs.delete customJobs.cancel customJobs.create customJobs.delete dataLabelingJobs.cancel dataLabelingJobs.create dataLabelingJobs.delete datasets.create datasets.delete datasets.export datasets.import datasets.patch endpoints.create endpoints.delete endpoints.deployModel endpoints.patch endpoints.undeployModel featurestores.create featurestores.delete featurestores.patch featurestores.setIamPolicy featurestores.entityTypes.create featurestores.entityTypes.delete featurestores.entityTypes.patch featurestores.entityTypes.setIamPolicy featurestores.entityTypes.features.batchCreate featurestores.entityTypes.features.create featurestores.entityTypes.features.delete featurestores.entityTypes.features.patch hyperparameterTuningJobs.cancel hyperparameterTuningJobs.create hyperparameterTuningJobs.delete indexEndpoints.create indexEndpoints.delete indexEndpoints.deployIndex indexEndpoints.mutateDeployedIndex indexEndpoints.patch indexEndpoints.undeployIndex memories.create memories.delete memories.generate memories.purge memories.update memoryRevisions.rollback metadataStores.create metadataStores.delete metadataStores.artifacts.create metadataStores.artifacts.delete metadataStores.artifacts.patch metadataStores.artifacts.purge metadataStores.contexts.addContextArtifactsAndExecutions metadataStores.contexts.addContextChildren metadataStores.contexts.create metadataStores.contexts.delete metadataStores.contexts.patch metadataStores.contexts.purge metadataStores.executions.addExecutionEvents metadataStores.executions.create metadataStores.executions.delete metadataStores.executions.patch metadataStores.executions.purge metadataStores.metadataSchemas.create migratableResources.batchMigrate modelDeploymentMonitoringJobs.create modelDeploymentMonitoringJobs.delete modelDeploymentMonitoringJobs.patch modelDeploymentMonitoringJobs.pause modelDeploymentMonitoringJobs.resume modelDevelopmentClusters.create modelDevelopmentClusters.delete modelDevelopmentClusters.get modelDevelopmentClusters.list modelDevelopmentClusters.update models.delete models.deleteVersion models.export models.mergeVersionAliases models.patch models.upload models.evaluations.import models.evaluations.slices.batchImport modelMonitors.create modelMonitors.delete modelMonitors.update modelMonitoringJobs.create modelMonitoringJobs.delete operations.cancel pipelineJobs.cancel pipelineJobs.create pipelineJobs.delete ragCorpora.create ragCorpora.delete ragEngineConfigs.update sandboxEnvironments.create sandboxEnvironments.delete sandboxEnvironments.snapshot sandboxEnvironmentSnapshots.delete sandboxEnvironmentTemplates.create sandboxEnvironmentTemplates.delete schedules.create schedules.delete schedules.update specialistPools.create specialistPools.delete specialistPools.patch studies.create studies.delete studies.trials.addTrialMeasurement studies.trials.complete studies.trials.create studies.trials.delete studies.trials.stop studies.trials.suggest tensorboards.create tensorboards.delete tensorboards.patch tensorboards.experiments.create tensorboards.experiments.delete tensorboards.experiments.patch tensorboards.experiments.write tensorboards.experiments.runs.batchCreate tensorboards.experiments.runs.create tensorboards.experiments.runs.delete tensorboards.experiments.runs.patch tensorboards.experiments.runs.write tensorboards.experiments.runs.timeSeries.batchCreate tensorboards.experiments.runs.timeSeries.create tensorboards.experiments.runs.timeSeries.delete tensorboards.experiments.runs.timeSeries.patch trainingPipelines.cancel trainingPipelines.create trainingPipelines.delete tuningJobs.cancel tuningJobs.create deploymentResourcePool.create deploymentResourcePool.delete semanticGovernancePolicies.create semanticGovernancePolicies.update semanticGovernancePolicies.delete |
| Data Access (ADMIN_READ) audit logs | batchPredictionJobs.get batchPredictionJobs.list customJobs.get customJobs.list dataLabelingJobs.get dataLabelingJobs.list datasets.get datasets.list datasets.annotationSpecs.get datasets.annotations.list datasets.savedQueries.list endpoints.get endpoints.list featurestores.get featurestores.getIamPolicy featurestores.list featurestores.searchFeatures featurestores.entityTypes.get featurestores.entityTypes.getIamPolicy featurestores.entityTypes.list featurestores.entityTypes.features.get featurestores.entityTypes.features.list hyperparameterTuningJobs.get hyperparameterTuningJobs.list indexEndpoints.get indexEndpoints.list indexes.get indexes.delete memories.get memories.list memoryRevisions.get memoryRevisions.list metadataStores.get metadataStores.list metadataStores.artifacts.get metadataStores.artifacts.list metadataStores.artifacts.queryArtifactLineageSubgraph metadataStores.contexts.get metadataStores.contexts.list metadataStores.contexts.queryContextLineageSubgraph metadataStores.executions.get metadataStores.executions.list metadataStores.executions.queryExecutionInputsAndOutputs metadataStores.metadataSchemas.get metadataStores.metadataSchemas.list migratableResources.search modelDeploymentMonitoringJobs.get modelDeploymentMonitoringJobs.list models.get models.list models.listVersions models.evaluations.get models.evaluations.list models.evaluations.slices.get models.evaluations.slices.list modelMonitors.get modelMonitors.list modelMonitoringJobs.get modelMonitoringJobs.list pipelineJobs.get pipelineJobs.list ragCorpora.get ragCorpora.list ragEngineConfigs.get sandboxEnvironments.get sandboxEnvironments.list sandboxEnvironmentSnapshots.get sandboxEnvironmentSnapshots.list sandboxEnvironmentTemplates.get sandboxEnvironmentTemplates.list schedules.get schedules.list specialistPools.get specialistPools.list studies.get studies.list studies.lookup studies.trials.checkTrialEarlyStoppingState studies.trials.get studies.trials.list studies.trials.listOptimalTrials tensorboards.get tensorboards.list tensorboards.experiments.get tensorboards.experiments.list tensorboards.experiments.runs.get tensorboards.experiments.runs.list tensorboards.experiments.runs.timeSeries.batchRead tensorboards.experiments.runs.timeSeries.exportTensorboardTimeSeries tensorboards.experiments.runs.timeSeries.get tensorboards.experiments.runs.timeSeries.list tensorboards.experiments.runs.timeSeries.read tensorboards.experiments.runs.timeSeries.readBlobData trainingPipelines.get trainingPipelines.list tuningJobs.get tuningJobs.list deploymentResourcePool.get deploymentResourcePool.list deploymentResourcePool.queryDeployedModels semanticGovernancePolicies.list semanticGovernancePolicies.get                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Data Access (DATA_READ) audit logs  | datasets.dataItems.list endpoints.explain endpoints.predict endpoints.predictLongRunning endpoints.rawPredict featurestores.batchReadFeatureValues featurestores.entityTypes.exportFeatureValues featurestores.entityTypes.readFeatureValues featurestores.entityTypes.streamingReadFeatureValues indexEndpoints.findNeighbors memories.retrieve modelDeploymentMonitoringJobs.searchModelDeploymentMonitoringStatsAnomalies modelMonitors.searchModelMonitoringAlerts modelMonitors.searchModelMonitoringStats onlineEvaluators.get onlineEvaluators.list ragFiles.get ragFiles.list sessions.get sessions.list sessionEvents.list                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Data Access (DATA_WRITE) audit logs | featurestores.entityTypes.importFeatureValues indexes.create indexes.patch indexes.removeDatapoints indexes.upsertDatapoints onlineEvaluators.create onlineEvaluators.update onlineEvaluators.delete ragFiles.delete ragFiles.import ragFiles.upload sandboxEnvironments.execute sessions.create sessions.update sessions.delete sessionEvents.append                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| System Event audit logs             | InstanceVerification.LogEvidence                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## Audit log format

Audit log entries include the following objects:

- The log entry itself, which is an object of type [`LogEntry`](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry) . Useful fields include the following:

  - The `logName` contains the resource ID and audit log type. The resource is a project, folder, organization, or billing account.
  - The `resource` contains the target of the audited operation.
  - The `timeStamp` contains the time of the audited operation.
  - The `protoPayload` contains the audited information.

- The audit logging data, which is an [`AuditLog`](https://docs.cloud.google.com/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog) object held in the `protoPayload` field of the log entry.

  - The `@type` field is set to `"type.googleapis.com/google.cloud.audit.AuditLog"` .
  - The `serviceName` field identifies the service that wrote the audit log. The format of this field is service specific.

- Optional service-specific audit information, which is a service-specific object. For earlier integrations, this object is held in the `serviceData` field of the `AuditLog` object; later integrations use the `metadata` field.

For other fields in these objects, and how to interpret them, review [Understand audit logs](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs) .

### Log name

Cloud Audit Logs log names include resource identifiers indicating the Google Cloud project or other Google Cloud entity that owns the audit logs, and whether the log contains Admin Activity, Data Access, Policy Denied, or System Event audit logging data.

The following are the audit log names, including variables for the resource identifiers:

```
   projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Factivity
   projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Fdata_access
   projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Fsystem_event
   projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Fpolicy

   folders/FOLDER_ID/logs/cloudaudit.googleapis.com%2Factivity
   folders/FOLDER_ID/logs/cloudaudit.googleapis.com%2Fdata_access
   folders/FOLDER_ID/logs/cloudaudit.googleapis.com%2Fsystem_event
   folders/FOLDER_ID/logs/cloudaudit.googleapis.com%2Fpolicy

   billingAccounts/BILLING_ACCOUNT_ID/logs/cloudaudit.googleapis.com%2Factivity
   billingAccounts/BILLING_ACCOUNT_ID/logs/cloudaudit.googleapis.com%2Fdata_access
   billingAccounts/BILLING_ACCOUNT_ID/logs/cloudaudit.googleapis.com%2Fsystem_event
   billingAccounts/BILLING_ACCOUNT_ID/logs/cloudaudit.googleapis.com%2Fpolicy

   organizations/ORGANIZATION_ID/logs/cloudaudit.googleapis.com%2Factivity
   organizations/ORGANIZATION_ID/logs/cloudaudit.googleapis.com%2Fdata_access
   organizations/ORGANIZATION_ID/logs/cloudaudit.googleapis.com%2Fsystem_event
   organizations/ORGANIZATION_ID/logs/cloudaudit.googleapis.com%2Fpolicy
```

> **Note:** The part of the log name following `/logs/` must be URL-encoded. The forward-slash character, `/` , must be written as `%2F` .

### Service name

Agent Platform audit logs use the service name `aiplatform.googleapis.com` .

For a list of all the Cloud Logging API service names and their corresponding monitored resource type, see [Map services to resources](https://docs.cloud.google.com/logging/docs/api/v2/resource-list#service-names) .

### Resource types

Agent Platform audit logs use the resource type `audited_resource` for all audit logs.

For a list of all the Cloud Logging monitored resource types and descriptive information, see [Monitored resource types](https://docs.cloud.google.com/logging/docs/api/v2/resource-list#resource-types) .

### Caller identities

The IP address of the caller is held in the `RequestMetadata.caller_ip` field of the [`AuditLog`](https://docs.cloud.google.com/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog) object. Logging might redact certain caller identities and IP addresses.

For information about what information is redacted in audit logs, see [Caller identities in audit logs](https://docs.cloud.google.com/logging/docs/audit#user-id) .

## Enable audit logging

System Event audit logs are always enabled; you can't disable them.

Admin Activity audit logs are always enabled; you can't disable them.

Data Access audit logs are disabled by default and aren't written unless explicitly enabled (the exception is Data Access audit logs for BigQuery, which can't be disabled).

For information about enabling some or all of your Data Access audit logs, see [Enable Data Access audit logs](https://docs.cloud.google.com/logging/docs/audit/configure-data-access) .

## Permissions and roles

[IAM](https://docs.cloud.google.com/iam/docs) permissions and roles determine your ability to access audit logs data in Google Cloud resources.

When deciding which [Logging-specific permissions and roles](https://docs.cloud.google.com/logging/docs/access-control#permissions_and_roles) apply to your use case, consider the following:

- The Logs Viewer role ( `roles/logging.viewer` ) gives you read-only access to Admin Activity, Policy Denied, and System Event audit logs. If you have just this role, you cannot view Data Access audit logs that are in the `_Default` bucket.

- The Private Logs Viewer role `(roles/logging.privateLogViewer` ) includes the permissions contained in `roles/logging.viewer` , plus the ability to read Data Access audit logs in the `_Default` bucket.

  Note that if these private logs are stored in user-defined buckets, then any user who has permissions to read logs in those buckets can read the private logs. For more information about log buckets, see [Routing and storage overview](https://docs.cloud.google.com/logging/docs/routing/overview) .

For more information about the IAM permissions and roles that apply to audit logs data, see [Access control with IAM](https://docs.cloud.google.com/logging/docs/access-control) .

## View logs

You can query for all audit logs or you can query for logs by their audit log name. The audit log name includes the [resource identifier](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) of the Google Cloud project, folder, billing account, or organization for which you want to view audit logging information. Your queries can specify indexed [`LogEntry`](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry) fields. For more information about querying your logs, see [Build queries in the Logs Explorer](https://docs.cloud.google.com/logging/docs/view/building-queries)

The Logs Explorer lets you view filter individual log entries. If you want to use SQL to analyze groups of log entries, then use the **Log Analytics** page. For more information, see:

- [Query and view logs in Observability Analytics](https://docs.cloud.google.com/logging/docs/analyze/query-and-view) .
- [Sample queries for security insights](https://docs.cloud.google.com/logging/docs/analyze/analyze-audit-logs) .
- [Chart query results](https://docs.cloud.google.com/logging/docs/analyze/charts) .

Most audit logs can be viewed in Cloud Logging by using the Google Cloud console, the Google Cloud CLI, or the Logging API. However, for audit logs related to billing, you can only use the Google Cloud CLI or the Logging API.

### Console

In the Google Cloud console, you can use the Logs Explorer to retrieve your audit log entries for your Google Cloud project, folder, or organization:

1.  In the Google Cloud console, go to the segment **Logs Explorer** page:

    If you use the search bar to find this page, then select the result whose subheading is **Logging** .

2.  Select an existing Google Cloud project, folder, or organization.

3.  To display all audit logs, enter either of the following queries into the query-editor field, and then click **Run query** :

    ```
    logName:"cloudaudit.googleapis.com"
    ```

    ```
    protoPayload."@type"="type.googleapis.com/google.cloud.audit.AuditLog"
    ```

4.  To display the audit logs for a specific resource and audit log type, in the **Query builder** pane, do the following:

    - In **Resource type** , select the Google Cloud resource whose audit logs you want to see.

    - In **Log name** , select the audit log type that you want to see:

      - For Admin Activity audit logs, select **activity** .
      - For Data Access audit logs, select **data_access** .
      - For System Event audit logs, select **system_event** .
      - For Policy Denied audit logs, select **policy** .

    - Click **Run query** .

    If you don't see these options, then there aren't any audit logs of that type available in the Google Cloud project, folder, or organization.

    If you're experiencing issues when trying to view logs in the Logs Explorer, see the [troubleshooting](https://docs.cloud.google.com/logging/docs/view/logs-explorer-interface#troubleshooting) information.

    For more information about querying by using the Logs Explorer, see [Build queries in the Logs Explorer](https://docs.cloud.google.com/logging/docs/view/building-queries) .

### gcloud

The Google Cloud CLI provides a command-line interface to the Logging API. Supply a valid resource identifier in each of the log names. For example, if your query includes a ` PROJECT_ID ` , then the project identifier you supply must refer to the currently selected Google Cloud project.

To read your Google Cloud project-level audit log entries, run the following command:

```
gcloud logging read "logName : projects/PROJECT_ID/logs/cloudaudit.googleapis.com" \
    --project=PROJECT_ID
```

To read your folder-level audit log entries, run the following command:

```
gcloud logging read "logName : folders/FOLDER_ID/logs/cloudaudit.googleapis.com" \
    --folder=FOLDER_ID
```

To read your organization-level audit log entries, run the following command:

```
gcloud logging read "logName : organizations/ORGANIZATION_ID/logs/cloudaudit.googleapis.com" \
    --organization=ORGANIZATION_ID
```

To read your Cloud Billing account-level audit log entries, run the following command:

```
gcloud logging read "logName : billingAccounts/BILLING_ACCOUNT_ID/logs/cloudaudit.googleapis.com" \
    --billing-account=BILLING_ACCOUNT_ID
```

Add the [`--freshness` flag](https://docs.cloud.google.com/sdk/gcloud/reference/logging/read#--freshness) to your command to read logs that are more than 1 day old.

For more information about using the gcloud CLI, see [`gcloud logging read`](https://docs.cloud.google.com/sdk/gcloud/reference/logging/read) .

### REST

When building your queries, supply a valid resource identifier in each of the log names. For example, if your query includes a ` PROJECT_ID ` , then the project identifier you supply must refer to the currently selected Google Cloud project.

For example, to use the Logging API to view your project-level audit log entries, do the following:

1.  Go to the **Try this API** section in the documentation for the [`entries.list`](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/entries/list) method.

2.  Put the following into the **Request body** part of the **Try this API** form. Clicking this [prepopulated form](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/entries/list?apix_params=%7B%22resource%22%3A%7B%22resourceNames%22%3A%5B%22projects%2F%5BPROJECT_ID%5D%22%5D%2C%22pageSize%22%3A5%2C%22filter%22%3A%22logName%3D(projects%2F%5BPROJECT_ID%5D%2Flogs%2Fcloudaudit.googleapis.com%252Factivity%20OR%20projects%2F%5BPROJECT_ID%5D%2Flogs%2Fcloudaudit.googleapis.com%252Fsystem_events%20OR%20projects%2F%5BPROJECT_ID%5D%2Flogs%2Fcloudaudit.googleapis.com%252Fdata_access)%22%7D%7D) automatically fills the request body, but you need to supply a valid ` PROJECT_ID ` in each of the log names.

    ```
    {
      "resourceNames": [
        "projects/PROJECT_ID"
      ],
      "pageSize": 5,
      "filter": "logName : projects/PROJECT_ID/logs/cloudaudit.googleapis.com"
    }
    ```

3.  Click **Execute** .

## Route audit logs

You can [route audit logs](https://docs.cloud.google.com/logging/docs/routing/overview) to supported destinations in the same way that you can route other kinds of logs. Here are some reasons you might want to route your audit logs:

- To keep audit logs for a longer period of time or to use more powerful search capabilities, you can route copies of your audit logs to Cloud Storage, BigQuery, or Pub/Sub. Using Pub/Sub, you can route to other applications, other repositories, and to third parties.

- To manage your audit logs across an entire organization, you can create [aggregated sinks](https://docs.cloud.google.com/logging/docs/export/aggregated_sinks) that can route logs from any or all Google Cloud projects in the organization.

<!-- -->

- If your enabled Data Access audit logs are pushing your Google Cloud projects over your log allotments, you can create sinks that exclude the Data Access audit logs from Logging.

For instructions about routing logs, see [Route logs to supported destinations](https://docs.cloud.google.com/logging/docs/export/configure_export_v2) .

## Pricing

For more information about pricing, see the Cloud Logging sections in the [Google Cloud Observability pricing](https://cloud.google.com/products/observability/pricing) page.
