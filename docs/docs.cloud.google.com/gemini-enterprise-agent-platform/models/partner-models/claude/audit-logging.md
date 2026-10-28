---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/audit-logging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/audit-logging
title: Anthropic managed Claude API audit logging
description: Audited methods and Cloud Audit Logs for the Anthropic managed Claude API (claude.googleapis.com).
data_source: docs.cloud.google.com
---

Cloud Audit Logs for Anthropic managed Claude API let you track administrative and data-access operations on your resources to help you monitor access and configuration changes. You can query these logs in the Logs Explorer and check which Anthropic managed Claude API API methods generate Cloud Audit Logs.

For more information about Cloud Audit Logs, see the following documents:

- [Types of audit logs](https://docs.cloud.google.com/logging/docs/audit#types)
- [Audit log entry structure](https://docs.cloud.google.com/logging/docs/audit#audit_log_entry_structure)
- [Storing and routing audit logs](https://docs.cloud.google.com/logging/docs/audit#storing_and_routing_audit_logs)
- [Cloud Logging pricing summary](https://docs.cloud.google.com/stackdriver/pricing#logs-pricing-summary)
- [Enable Data Access audit logs](https://docs.cloud.google.com/logging/docs/audit/configure-data-access)

## Service name

To view the Anthropic managed Claude API audit logs, do the following:

1.  In the Google Cloud console, go to the Logs Explorer page:

2.  Copy and paste the following query into the **Query** field of the Logs Explorer, and then click **Run query** .

    ```
    protoPayload.serviceName="claude.googleapis.com"
    ```

## Methods by permission type

Each IAM permission has a `type` property, whose value is an enum that can be one of four values: `ADMIN_READ` , `ADMIN_WRITE` , `DATA_READ` , or `DATA_WRITE` . When you call a method, Anthropic managed Claude API generates an audit log whose category is dependent on the `type` property of the permission required to perform the method. Methods that require an IAM permission with the `type` property value of `DATA_READ` , `DATA_WRITE` , or `ADMIN_READ` generate [Data Access](https://docs.cloud.google.com/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `type` property value of `ADMIN_WRITE` generate [Admin Activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity) audit logs.

API methods in the following list that are marked with (LRO) are long-running operations (LROs). These methods usually generate two audit log entries: one when the operation starts and another when it ends. For more information see [Audit logs for long-running operations](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro) .

| Permission type | Methods                                                                                                                                                                                                                                                                                                                                    |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ADMIN_READ`    | `google.cloud.ai.claude.v1.ClaudeManagementService.GetClaudeOrganization` `google.longrunning.Operations.GetOperation` `google.longrunning.Operations.ListOperations`                                                                                                                                                                      |
| `ADMIN_WRITE`   | `google.cloud.ai.claude.v1.ClaudeGatewayService.InvokeClaudeOrganization` `google.cloud.ai.claude.v1.ClaudeManagementService.ActivateClaudeOrganization` (LRO) `google.cloud.ai.claude.v1.ClaudeManagementService.GenerateConsoleAdminUrl` `google.longrunning.Operations.CancelOperation` `google.longrunning.Operations.DeleteOperation` |
| `DATA_WRITE`    | `google.cloud.ai.claude.v1.ClaudeGatewayService.InvokeWorkspace`                                                                                                                                                                                                                                                                           |

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for Anthropic managed Claude API.

### `google.cloud.ai.claude.v1.ClaudeGatewayService`

The following audit logs are associated with methods belonging to `google.cloud.ai.claude.v1.ClaudeGatewayService` .

#### `InvokeClaudeOrganization`

- **Method** : `google.cloud.ai.claude.v1.ClaudeGatewayService.InvokeClaudeOrganization`  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** : See IAM documentation for permissions.
- **Method is a long-running or streaming operation** : [**Streaming RPC**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#streaming)  
- **Filter for this method** : `protoPayload.methodName="google.cloud.ai.claude.v1.ClaudeGatewayService.InvokeClaudeOrganization"`  

#### `InvokeWorkspace`

- **Method** : `google.cloud.ai.claude.v1.ClaudeGatewayService.InvokeWorkspace`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `claude.googleapis.com/messageBatches.get - DATA_READ`
  - `claude.googleapis.com/messages.create - DATA_WRITE`
- **Method is a long-running or streaming operation** : [**Streaming RPC**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#streaming)  
- **Filter for this method** : `protoPayload.methodName="google.cloud.ai.claude.v1.ClaudeGatewayService.InvokeWorkspace"`  

### `google.cloud.ai.claude.v1.ClaudeManagementService`

The following audit logs are associated with methods belonging to `google.cloud.ai.claude.v1.ClaudeManagementService` .

#### `ActivateClaudeOrganization`

- **Method** : `google.cloud.ai.claude.v1.ClaudeManagementService.ActivateClaudeOrganization`  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `claude.claudeOrganizations.activate - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
- **Filter for this method** : `protoPayload.methodName="google.cloud.ai.claude.v1.ClaudeManagementService.ActivateClaudeOrganization"`  

#### `GenerateConsoleAdminUrl`

- **Method** : `google.cloud.ai.claude.v1.ClaudeManagementService.GenerateConsoleAdminUrl`  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `claude.claudeOrganizations.generateConsoleAdminUrl - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.cloud.ai.claude.v1.ClaudeManagementService.GenerateConsoleAdminUrl"`  

#### `GetClaudeOrganization`

- **Method** : `google.cloud.ai.claude.v1.ClaudeManagementService.GetClaudeOrganization`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `claude.claudeOrganizations.get - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.cloud.ai.claude.v1.ClaudeManagementService.GetClaudeOrganization"`  

### `google.longrunning.Operations`

The following audit logs are associated with methods belonging to `google.longrunning.Operations` .

#### `CancelOperation`

- **Method** : `google.longrunning.Operations.CancelOperation`  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `claude.operations.cancel - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.CancelOperation"`  

#### `DeleteOperation`

- **Method** : `google.longrunning.Operations.DeleteOperation`  
- **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
- **Permissions** :
  - `claude.operations.delete - ADMIN_WRITE`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.DeleteOperation"`  

#### `GetOperation`

- **Method** : `google.longrunning.Operations.GetOperation`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `claude.operations.get - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.GetOperation"`  

#### `ListOperations`

- **Method** : `google.longrunning.Operations.ListOperations`  
- **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
- **Permissions** :
  - `claude.operations.list - ADMIN_READ`
- **Method is a long-running or streaming operation** : No.  
- **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.ListOperations"`
