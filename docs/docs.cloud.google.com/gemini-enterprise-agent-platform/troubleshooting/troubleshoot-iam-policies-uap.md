---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap
title: Troubleshoot IAM Access policies
description: Troubleshoot common IAM access policy enforcement failures, UI errors, gcloud commands, and REST API error messages for Agent Platform.
data_source: docs.cloud.google.com
---

This document helps you diagnose and resolve common issues when configuring and enforcing IAM Unified Access Policies (Access policies) for Agent Gateway egress.

For standard Google Cloud troubleshooting guidance and methodology, see [Troubleshooting documentation guidelines](https://docs.cloud.google.com/guides/docs/troubleshooting) .

## Policy enforcement and access failures

This section describes issues with enforcement.

### Policy isn't being enforced

**Symptom** : An agent can access destination tools, MCP servers, or endpoints even though an IAM deny rule or restrictive allow rule was configured to block the access.

**Cause** : The Agent Gateway authorization extension is running in **dry-run mode** , or the policy binding scope does not match the target resource. In dry-run mode, access decisions are evaluated and logged for auditing, but requests are never blocked.

**Solution** :

1.  **Switch dry-run mode to enforce mode** : First, check your authorization extension configuration file ( `iap-request-authz-extension.yaml` ). If `iamEnforcementMode` is set to `"DRY_RUN"` , update it to `"ENFORCE"` (or remove the `DRY_RUN` setting) and re-import the extension using the gcloud CLI:
    
    ```sh
    gcloud service-extensions authz-extensions import EXTENSION_NAME \
        --source=EXTENSION_FILE.yaml \
        --location=LOCATION
    ```
    
    Replace the following:
    
      - `  EXTENSION_NAME  ` : the name of your authorization extension
      - `  EXTENSION_FILE  ` : the filename of your YAML extension configuration
      - `  LOCATION  ` : the Google Cloud region where your gateway is deployed

2.  **Verify gateway authorization policy delegation** : Verify that your gateway authorization policy ( `policyProfile: REQUEST_AUTHZ` ) is bound to the correct Agent Gateway instance ( `target.resources` ).

3.  **Check policy binding scope** : Verify that the IAM Access policy is bound to the target resource scope where the traffic is arriving.

4.  **Inspect rule precedence** : In a combination policy, deny rules explicitly override allow rules at the same scope. However, check whether an Access policy with a broader allow rule that is bound at the registry or project level is granting access without condition restrictions.

### Enforced policy blocks agent access

**Symptom** : An agent's egress request fails with an HTTP `403 Forbidden` or `PERMISSION_DENIED` error when Agent Gateway policy enforcement is enabled.

**Causes** :

  - The agent's identity is not specified in the Access policy.

  - The agent's identity wasn't granted the `iap.resources.egressViaIAP` permission on the destination resource.

  - The exact destination hostname is not registered in Agent Registry

  - The request attributes don't satisfy the Common Expression Language (CEL) conditions in the Access policy.

**Solution** :

1.  **Switch to dry-run mode for non-disruptive debugging** : While diagnosing the failure, temporarily switch the authorization extension to **dry-run mode** ( `iamEnforcementMode: "DRY_RUN"` ) so active agent traffic is not blocked while you inspect audit logs.

2.  **Query Cloud Audit Logs** : Query Cloud Audit Logs to inspect the exact authorization check and CEL attribute evaluation:
    
    ### gcloud
    
    Run the following `gcloud logging read` command:
    
    ```sh
    gcloud logging read \
        'protoPayload.serviceName="iap.googleapis.com" AND protoPayload.authorizationInfo.permission="iap.resources.egressViaIAP" AND protoPayload.status.code!=0' \
        --project=PROJECT_ID \
        --limit=20
    ```
    
    Replace `  PROJECT_ID  ` with your project ID.
    
    ### Console
    
    1.  In the Google Cloud console, go to the **Logs Explorer** page.
    
    2.  Select your project.
    
    3.  In the query editor, enter the following query:
        
        ```text
            protoPayload.serviceName="iap.googleapis.com"
            protoPayload.authorizationInfo.permission="iap.resources.egressViaIAP"
            protoPayload.status.code!=0
            
        ```
    
    4.  Click **Run query** .
    
    5.  Expand the log entry and inspect `protoPayload.authorizationInfo` to see which target resource URI and permission failed evaluation.

3.  **Verify exact hostname matching** : Agent Gateway matches destination hostnames **exactly** . A Google API or third-party service might resolve through multiple hostname variations depending on the SDK version, regional client configuration, or mTLS usage—for example, `us-central1-aiplatform.googleapis.com` versus `us-central1-aiplatform.mtls.googleapis.com` versus `aiplatform.googleapis.com` .
    
      - If you rely on registered targets, make sure that every exact hostname variation is registered in Agent Registry.
      - If the agent accesses unregistered endpoints, verify that an [unregistered endpoint policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap) grants `iap.resources.egressViaIAP` for that host and path.

4.  **Verify policy binding coverage across scopes** : Check whether a policy binding exists at one of the three supported scopes:
    
      - **Registry-wide** : Grants access across all agents, MCP servers, and endpoints in the registry.
      - **Per-resource** : Grants access to a specific registered MCP server, endpoint, or agent.
      - **Unregistered endpoints** : Grants access to destinations outside Agent Registry.
      - *Note* : When describing policy bindings for a target resource, if the returned output contains an `"etag"` field but no bindings, no IAM policy exists for that target.

## Common UI, gcloud, and REST API error messages

This section describes error messages and how to resolve them.

### Policy not found

**Error message** :

  - **Console UI** : *"The requested policy doesn't exist. Verify that the policy exists for the selected resource."*
  - **API / gcloud** : `POLICY_NOT_FOUND` / `HTTP 404 Not Found`

**Cause** : The Access policy ID specified in your update request or policy binding does not exist in the project or location, or was deleted.

**Solution** : List all available Access policies in your project using `gcloud iam access-policies list --project=<var>PROJECT_ID</var> --location=global` to confirm the exact policy ID and location before binding or updating it.

### Target binding limit exceeded

**Error message** :

  - **Console UI** : *"The selected target has reached its limit for access policy bindings. Delete an existing binding before adding a new one."*
  - **API / gcloud** : `TOO_MANY_ACCESS_POLICY_BINDINGS_PER_TARGET`

**Cause** : You attempted to attach more policy bindings to a target resource (such as an MCP server or registry) than the maximum allowed limit per target.

**Solution** : Instead of creating a separate Access policy and binding for each individual rule, consolidate multiple allow or deny rules into a single Access policy. Remove unused bindings using `gcloud iam policy-bindings delete` .

### Policy binding limit exceeded

**Error message** :

  - **Console UI** : *"The selected policy has reached its limit for bindings. Delete an existing binding before adding a new one."*
  - **API / gcloud** : `TOO_MANY_ACCESS_POLICY_BINDINGS_TO_POLICY`

**Cause** : A single Access policy is attached to too many distinct target resources across your project.

**Solution** : Bind the policy at a broader scope—such as registry-wide scope ( `AgentRegistry` ) or project scope—and use CEL attribute conditions (such as `destination.agent_registry.mcp_server.name` ) to govern access to individual tools within the policy rules.

### Condition limit exceeded

**Error message** :

  - **Console UI** : *"This policy has reached the maximum number of attribute conditions. Remove some conditions to save your changes."*
  - **API / gcloud** : `TOO_MANY_CONDITIONS` / Condition limit exceeded for rule in policy.

**Cause** : A single allow or deny rule contains more Fine-Grained Access Control (FGAC) attribute conditions or complex sub-expressions than supported in a single rule.

**Solution** : Consolidate attribute checks using CEL logical operators ( `&&` , `||` ) or set inclusion lookups ( `in` ), or split your expressions across multiple rules within the same Access policy.

### Outdated rule details

**Error message** :

  - **Console UI** : *"Rule details are outdated. This rule was modified by another user after this page was loaded. Refresh the page to fetch the current details before editing or deleting."*
  - **API / gcloud** : `HTTP 412 Precondition Failed` / `ABORTED` due to `etag` mismatch.

**Cause** : Another administrator or automated process modified the Access policy after you retrieved it, causing your request's `etag` to differ from the active server state.

**Solution** : Refresh the Console page to retrieve the active policy details and `etag` before saving your edits. When using the REST API, perform a `GET` request first to retrieve the active `"etag"` value, and include it in your `PATCH` request payload.

### Cannot delete the last rule in a policy

**Error message** :

  - **Console UI** : *"Cannot delete this rule. The 'Default policy' must contain at least one rule. To remove this rule, delete the policy instead."* or *"This is the last rule in \<policy name\>. Deleting it will also delete the policy and permanently remove all associated bindings, which can affect agent access to resources."*

**Cause** : An IAM Access policy cannot be saved with zero rules.

**Solution** : If you want to remove the only rule in a policy, delete the entire policy. Remember that you must delete all policy bindings that reference the policy before you can delete the policy itself.

### Custom CEL expression preserved in Advanced tab

**Error message** :

  - **Console UI** : *"The custom CEL expression could not be converted into standard UI selections. Your expression is preserved in the Advanced tab."*

**Cause** : You entered a complex CEL condition or function in the **Condition editor** (Advanced tab) that cannot be mapped into the simplified drop-down selectors of the standard condition builder.

**Solution** : This message is an informational notification. Your custom CEL condition is valid and preserved. Continue making any edits directly inside the **Condition editor** tab.

## What's next

  - [CEL attributes for Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap)
  - [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
  - [Manage IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap)
