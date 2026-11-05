---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/dry-run-report
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/dry-run-report
title: Audit dry-run policy violations across controls
description: Query Cloud Logging and BigQuery across Agent Platform governance controls to generate a consolidated dry-run violation report before enabling active enforcement.
data_source: docs.cloud.google.com
---

When you set up an audit-first governed landing zone in Identity-Aware Proxy, you can deploy access, content safety, and perimeter controls in dry-run (audit-only) mode first. In dry-run mode, each control evaluates live agent traffic and writes violation records to Cloud Logging without blocking requests.

This page shows enterprise security and governance administrators how to query dry-run logs across controls and generate a consolidated "would have been blocked" violation report in Observability Analytics or BigQuery before switching policies to active enforcement.

## Dry-run and enforcement modes across controls

An audit-first IAP landing zone typically combines policy controls at the gateway, content, and network perimeter layers. The following table summarizes how dry-run mode and active enforcement are configured and logged for each control:

| Governance control                                                                                                                                                                                                                          | Dry-run (audit-only) configuration                                                                                                                                                                               | Active enforcement configuration                                                                                                                                                                                                                                                                  | Log stream ( `logName` )                                                           |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| [Identity and Access Management (IAM) Unified Access Policies (UAPs)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) on Agent Gateway (evaluated by Identity-Aware Proxy (IAP)) | **Google Cloud console** : Select **Audit-only** under **Access Authorization** . **Google Cloud CLI, API, or Terraform** : Set `iamEnforcementMode: "DRY_RUN"` in the authorization extension `metadata` block. | **Google Cloud console** : Select **Enforce policies** (writes `iamEnforcementMode: "ENFORCED"` when creating a gateway, or removes `iamEnforcementMode` when updating an existing gateway). **gcloud CLI, API, or Terraform** : Remove the `iamEnforcementMode` field from the `metadata` block. | `projects/ `` PROJECT_ID `` /logs/cloudaudit.googleapis.com%2Fdata_access`         |
| [Semantic Governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance) on Agent Gateway                                                                               | Set `sgpEnforcementMode: "DRY_RUN"` in the authorization extension `metadata` block.                                                                                                                             | Remove `sgpEnforcementMode` from `metadata` , or set `sgpEnforcementMode: "ENFORCE"` .                                                                                                                                                                                                            | `projects/ `` PROJECT_ID `` /logs/semantic-governance-policy`                      |
| [Model Armor content security](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) on Agent Gateway                                                                                                | Set `template_metadata.enforcement_type: "INSPECT_ONLY"` and `template_metadata.log_sanitize_operations: true` on your Model Armor template.                                                                     | Set `template_metadata.enforcement_type: "INSPECT_AND_BLOCK"` on your Model Armor template.                                                                                                                                                                                                       | `projects/ `` PROJECT_ID `` /logs/modelarmor.googleapis.com%2Fsanitize_operations` |
| [VPC Service Controls service perimeters](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations)                                                                                                            | Create or update a dry-run service perimeter configuration ( `spec` block with `useExplicitDryRunSpec: true` ).                                                                                                  | Enforce the dry-run perimeter configuration with `gcloud access-context-manager perimeters dry-run enforce` .                                                                                                                                                                                     | `projects/ `` PROJECT_ID `` /logs/cloudaudit.googleapis.com%2Fpolicy`              |
| [Organization Policy Service constraints](https://docs.cloud.google.com/organization-policy/test-policies)                                                                                                                                  | Create or update an organization policy with a dry-run specification ( `dryRunSpec` using the `--dry-run` flag).                                                                                                 | Apply the policy specification as an enforced `spec` .                                                                                                                                                                                                                                            | `projects/ `` PROJECT_ID `` /logs/cloudaudit.googleapis.com%2Fpolicy`              |

### Understand `iamEnforcementMode` values in the UI and API

When you configure IAP authorization extensions for Agent Gateway, you might encounter different behavior depending on whether you manage the extension in the Google Cloud console or through the gcloud CLI, Terraform, and the REST API:

- **Dry-run (audit-only) mode** : Both the Google Cloud console (when you select **Audit-only** ) and the gcloud CLI set `iamEnforcementMode: "DRY_RUN"` in the authorization extension `metadata` map.
- **Active enforcement mode** : When you select **Enforce policies** in the Google Cloud console, the console writes `iamEnforcementMode: "ENFORCED"` to the authorization extension `metadata` map when creating a gateway, or deletes the `iamEnforcementMode` key from `metadata` when updating an existing gateway. However, the IAP first-party API validator rejects any explicit `iamEnforcementMode` value other than `"DRY_RUN"` . At runtime, the data plane enforces policies whenever `iamEnforcementMode` is omitted or does not equal `"DRY_RUN"` .

When you manage authorization extensions with the gcloud CLI, Terraform, or the REST API, always enable active enforcement by removing the `iamEnforcementMode` field from the `metadata` block.

## Before you begin

Before generating a cross-control dry-run violation report, verify the following prerequisites in your Google Cloud project:

1.  **Enable required logging settings** :
    - **IAP on Agent Gateway** : Cloud Audit Logs Data Access logs for `iap.googleapis.com` are generated for gateway authorization evaluations.
    - **Model Armor** : Ensure that `template_metadata.enforcement_type` is set to `"INSPECT_ONLY"` and `template_metadata.log_sanitize_operations` is set to `true` on your Model Armor templates so that inspection results are written to Logging without blocking payloads.
2.  **Prepare your query environment** :
    - To run SQL queries directly in Logging, [upgrade the `_Default` log bucket to use Observability Analytics](https://docs.cloud.google.com/logging/docs/buckets#upgrade-bucket) .
    - To run SQL queries in BigQuery, [configure a log sink](https://docs.cloud.google.com/logging/docs/export/configure_export_v2) that routes logs from your governance project to a BigQuery dataset, or link a dataset to your Observability Analytics-enabled log bucket.
3.  **Verify required IAM roles** :
    - To view Cloud Audit Logs Data Access logs and query `_Default._AllLogs` : Private Logs Viewer ( `roles/logging.privateLogViewer` ) and View Accessor ( `roles/logging.viewAccessor` ).
    - To query exported logs in BigQuery: BigQuery Data Viewer ( `roles/bigquery.dataViewer` ) and BigQuery Job User ( `roles/bigquery.jobUser` ).

## Query dry-run violations per control in Logs Explorer

To inspect individual dry-run violation entries in the **Logs Explorer** , go to the [**Logs Explorer** page](https://console.cloud.google.com/logs) in the Google Cloud console, select your governance project, and run the filter for the control that you want to audit:

- **IAM UAPs ( `iamEnforcementMode: "DRY_RUN"` )** : Finds requests where IAP evaluated a UAP in dry-run mode and determined that access would be denied ( `granted=false` ), while still permitting the request through the gateway:

  ```text
  log_id("cloudaudit.googleapis.com/data_access")
  protoPayload.serviceName="iap.googleapis.com"
  protoPayload.metadata.dryRun=true
  protoPayload.authorizationInfo.granted=false
  ```

  In the matching log entries, inspect `protoPayload.authenticationInfo.principalEmail` for the calling agent identity, `protoPayload.resourceName` for the target destination, and `protoPayload.authorizationInfo` for the evaluated permission ( `iap.resources.egressViaIAP` ).

- **Semantic Governance policies ( `sgpEnforcementMode: "DRY_RUN"` )** : Finds tool calls that violated a natural-language constraint ( `verdict="DENY"` ) while the policy extension was operating in dry-run mode:

  ```text
  log_id("semantic-governance-policy")
  jsonPayload.verdict="DENY"
  ```

  In the matching log entries, inspect `jsonPayload.toolName` for the invoked MCP tool and `jsonPayload.evaluations` for the constraint `id` and `rationale` .

- **Model Armor content security ( `template_metadata.enforcement_type: "INSPECT_ONLY"` )** : Finds prompts or tool responses that matched a configured content safety or sensitive data filter ( `filterMatchState="MATCH_FOUND"` ) during inspect-only evaluation:

  ```text
  log_id("modelarmor.googleapis.com/sanitize_operations")
  jsonPayload.sanitizationResult.filterMatchState="MATCH_FOUND"
  ```

  In the matching log entries, inspect `jsonPayload.sanitizationResult.filterResults` to identify which detector (such as prompt injection, jailbreak, or sensitive data protection) triggered the match.

- **VPC Service Controls dry-run service perimeters** : Finds ingress or egress requests that violated a dry-run service perimeter ( `dryRun="true"` ):

  ```text
  log_id("cloudaudit.googleapis.com/policy")
  protoPayload.metadata.dryRun="true"
  protoPayload.metadata.violationReason!=""
  ```

  In the matching log entries, inspect `protoPayload.metadata.violationReason` , `protoPayload.metadata.ingressViolations` , and `protoPayload.metadata.egressViolations` .

## Generate a consolidated "would have been blocked" report

Before transitioning your controls to active enforcement, run a consolidated SQL query across all governance log streams to produce a single summary of every agent request that would have been blocked during your audit window.

### Observability Analytics

1.  In the Google Cloud console, go to the **Observability Analytics** page.

2.  Paste the following SQL query into the query editor to aggregate dry-run violations across IAM UAPs, Semantic Governance policies, Model Armor, and VPC Service Controls:

    ```sql
    WITH dry_run_violations AS (
    /* 1. IAM UAPs (IAP on Agent Gateway in DRY_RUN mode) */
    SELECT
      timestamp,
      'IAM_UAP_IAP' AS control_layer,
      IFNULL(
        proto_payload.audit_log.authentication_info.principal_email,
        JSON_VALUE(proto_payload.audit_log.authentication_info.third_party_principal, '$.payload.sub')
      ) AS principal_or_agent,
      proto_payload.audit_log.resource_name AS target_or_tool,
      CONCAT(
        'Permission denied in dry-run: ',
        IFNULL(auth.permission, 'iap.resources.egressViaIAP')
      ) AS violation_detail
    FROM
      `PROJECT_ID.global._Default._AllLogs`
    LEFT JOIN
      UNNEST(proto_payload.audit_log.authorization_info) AS auth
    WHERE
      log_id = 'cloudaudit.googleapis.com/data_access'
      AND proto_payload.audit_log.service_name = 'iap.googleapis.com'
      AND JSON_VALUE(proto_payload.audit_log.metadata, '$.dryRun') = 'true'
      AND IFNULL(auth.granted, FALSE) = FALSE

    UNION ALL

    /* 2. Semantic Governance policies (sgpEnforcementMode: DRY_RUN) */
    SELECT
      timestamp,
      'SEMANTIC_GOVERNANCE' AS control_layer,
      IFNULL(
        JSON_VALUE(json_payload, '$.agentId'),
        JSON_VALUE(resource.labels, '$.gateway_name')
      ) AS principal_or_agent,
      IFNULL(JSON_VALUE(json_payload, '$.toolName'), 'mcp_tool_call') AS target_or_tool,
      CONCAT(
        'Verdict DENY: ',
        IFNULL(JSON_VALUE(json_payload, '$.evaluations[0].rationale'), 'Constraint violation')
      ) AS violation_detail
    FROM
      `PROJECT_ID.global._Default._AllLogs`
    WHERE
      log_id = 'semantic-governance-policy'
      AND JSON_VALUE(json_payload, '$.verdict') = 'DENY'

    UNION ALL

    /* 3. Model Armor content security (INSPECT_ONLY template matches) */
    SELECT
      timestamp,
      'MODEL_ARMOR' AS control_layer,
      IFNULL(
        JSON_VALUE(resource.labels, '$.template_id'),
        'model_armor_template'
      ) AS principal_or_agent,
      IFNULL(
        JSON_VALUE(resource.labels, '$.location'),
        'sanitize_operation'
      ) AS target_or_tool,
      CONCAT(
        'Filter match state: ',
        IFNULL(JSON_VALUE(json_payload, '$.sanitizationResult.filterMatchState'), 'MATCH_FOUND')
      ) AS violation_detail
    FROM
      `PROJECT_ID.global._Default._AllLogs`
    WHERE
      log_id = 'modelarmor.googleapis.com/sanitize_operations'
      AND JSON_VALUE(json_payload, '$.sanitizationResult.filterMatchState') = 'MATCH_FOUND'

    UNION ALL

    /* 4. VPC Service Controls dry-run service perimeters */
    SELECT
      timestamp,
      'VPC_SERVICE_CONTROLS' AS control_layer,
      proto_payload.audit_log.authentication_info.principal_email AS principal_or_agent,
      proto_payload.audit_log.resource_name AS target_or_tool,
      CONCAT(
        'Perimeter violation: ',
        IFNULL(JSON_VALUE(proto_payload.audit_log.metadata, '$.violationReason'), 'DRY_RUN_VIOLATION')
      ) AS violation_detail
    FROM
      `PROJECT_ID.global._Default._AllLogs`
    WHERE
      log_id = 'cloudaudit.googleapis.com/policy'
      AND JSON_VALUE(proto_payload.audit_log.metadata, '$.dryRun') = 'true'
      AND JSON_VALUE(proto_payload.audit_log.metadata, '$.violationReason') IS NOT NULL
    )
    SELECT
    control_layer,
    principal_or_agent,
    target_or_tool,
    violation_detail,
    COUNT(*) AS would_have_blocked_count,
    MIN(timestamp) AS first_seen,
    MAX(timestamp) AS last_seen
    FROM
    dry_run_violations
    WHERE
    timestamp >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY)
    GROUP BY
    control_layer,
    principal_or_agent,
    target_or_tool,
    violation_detail
    ORDER BY
    would_have_blocked_count DESC,
    last_seen DESC;
    ```

    Replace `PROJECT_ID` with your Google Cloud project ID.

3.  Click **Run query** .

### BigQuery ( Linked dataset )

If you linked a BigQuery dataset to your Observability Analytics-enabled `_Default` log bucket, you can run the same cross-control query in the **BigQuery Studio** editor by referencing the linked `_AllLogs` table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the query from the **Observability Analytics** tab, replacing `PROJECT_ID `` .global._Default._AllLogs` with your linked dataset table path: `PROJECT_ID `` . `` LINKED_DATASET_ID `` ._AllLogs` .

## Transition controls from dry-run mode to active enforcement

Review the consolidated report and resolve any unintended blocks for legitimate agent workflows (for example, by adding missing target hostnames to Agent Registry, updating UAP CEL conditions, or refining Semantic Governance natural-language rules).

After you confirm that only unauthorized or unsafe requests appear in the dry-run violation report, transition each control to active enforcement:

1.  **IAM UAPs on Agent Gateway** :

    - **Google Cloud console** : Go to the **Agent Gateway** page, edit your gateway, and select **Enforce policies** under **Access Authorization** (which removes `iamEnforcementMode` from the extension `metadata` , enabling active enforcement).

    - **gcloud CLI or Terraform** : In your IAP authorization extension configuration ( `iap-request-authz-extension.yaml` ), remove `iamEnforcementMode: "DRY_RUN"` from the `metadata` block, and re-import the extension:

      ```sh
      gcloud service-extensions authz-extensions import EXTENSION_NAME \
          --source=iap-request-authz-extension.yaml \
          --location=LOCATION
      ```

2.  **Semantic Governance policies** : In your Semantic Governance authorization extension configuration, remove `sgpEnforcementMode: "DRY_RUN"` from the `metadata` block (or set `sgpEnforcementMode: "ENFORCE"` ), and re-import the extension. For instructions, see [Configure Semantic Governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance) .

3.  **Model Armor content security** : On your Model Armor template, update `template_metadata.enforcement_type` from `"INSPECT_ONLY"` to `"INSPECT_AND_BLOCK"` . For instructions, see [Configure Model Armor on a gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) .

4.  **VPC Service Controls service perimeters** : Enforce your dry-run perimeter configuration by following the instructions in [Manage dry-run configurations](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations#enforce) .

## What's next

- [Monitor traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)
- [Create IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
- [Monitor Semantic Governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/monitor-semantic-governance)
- [Monitor content security](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/monitor-content-security)
- [Troubleshoot IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap)
