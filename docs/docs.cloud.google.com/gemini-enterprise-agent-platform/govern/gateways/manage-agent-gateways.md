---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways
title: Manage Agent Gateway
description: View, update, disassociate, and delete Agent Gateway resources using the {{dynamic_data.site_values.cloud_name_short}} console and the Google Cloud CLI, including mutable and immutable settings.
data_source: docs.cloud.google.com
---

This document describes post-deployment maintenance tasks for Agent Gateway resources. If you haven't created a gateway yet, see [Set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .

## Before you begin

Before you manage Agent Gateway resources, verify the following prerequisites:

- Ensure that you have the required permissions to view, update, and delete gateways, connectivity templates, authorization policies, and authorization extensions. For the full list of permissions, see [Required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) .
- Enable the required services in your project. For details, see [Required APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-apis) .
- If you plan to disassociate workloads from a gateway, ensure that you also have permissions to manage your [Agent Runtime on Gemini Enterprise Agent Platform deployments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents) or [Gemini Enterprise apps](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy#before-you-begin) .

## View and inspect gateways

You can list the Agent Gateway resources in a Google Cloud project and inspect a gateway's configuration, attached extensions, and output-only metadata.

### Console

1.  In the Google Cloud console, go to the **Gateways** page.

2.  View the list of gateways in your selected project.

3.  Click the name of a gateway to open its details page:

    - On the **Details** tab, review the **Overview** , **Access authorization** , **AI Security** , **Service Extensions** , and **VPC configuration** sections.
    - On the **Observability** tab, review gateway traffic and policy metrics. For more information, see [Monitor Agent Gateway traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) .

### gcloud

- List all gateways in a specific region:

  ```
  gcloud network-services agent-gateways list \
    --location=LOCATION \
    --project=PROJECT_ID
  ```

  Replace the following:

  - `LOCATION` : the region where your gateways are deployed, such as `us-central1` .
  - `PROJECT_ID` : the ID of the Google Cloud project that hosts the gateways.

- Inspect the configuration of a specific gateway:

  ```
  gcloud network-services agent-gateways describe AGENT_GATEWAY_NAME \
    --location=LOCATION \
    --project=PROJECT_ID
  ```

  Replace `AGENT_GATEWAY_NAME` with the name of the Agent Gateway resource.

## Immutable settings

Most Agent Gateway configurations such as its associated Agent Registry instances and security and governance policies can be modified in place as described in [Update an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#update-gateway) . However, certain core configurations are immutable and require you to deploy a replacement gateway. Check the following table before modifying gateways:

| Setting                                                                                                 | Mutability                | Requirement or restriction                                                                                                                                                                   |
|---------------------------------------------------------------------------------------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gateway name and region                                                                                 | Immutable                 | To change the name or region, deploy a [replacement gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#replace-gateway) .         |
| Governed access path ( `AGENT_TO_ANYWHERE` or `CLIENT_TO_AGENT` )                                       | Immutable                 | Configured at creation in `googleManaged.governedAccessPath` . Cannot be modified in place.                                                                                                  |
| Private Service Connect network attachment ( `networkAttachment` )                                      | Immutable after being set | Once you associate a network attachment with a gateway, it cannot be changed or removed.                                                                                                     |
| Agent connectivity template and associated Cloud DNS peering, TLS trust config, and VPC egress settings | Conditionally mutable     | You can update the gateway's configuration to reference a different connectivity template with new settings, as long as the new template still references the **same** `networkAttachment` . |

### Replace a gateway to change immutable settings

If you need to change an immutable setting such as the PSC network attachment associated with the gateway, you need to deploy a replacement gateway and migrate your workloads to the new gateway:

1.  Create the replacement Agent Gateway and configure its Identity and Access Management (IAM) and authorization policies. For instructions, see [Set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .

2.  Update your workloads to use the replacement gateway:

    - **Gemini Enterprise apps** : Update the gateway resource name in the app's **Security \> Configuration** settings. See [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy) .
    - **Agent Runtime agents** : Within a single project and region, all Agent Runtime agents must bind to the same gateway. Direct in-place updates from one gateway to another aren't supported. To migrate your agents:
      1.  Ensure every bound agent routes 100% of traffic to its latest revision ( `trafficConfig.trafficSplitAlwaysLatest` ).
      2.  [Disassociate all agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#disassociate-agent-runtime) in the project and region from the previous gateway by setting `spec.deploymentSpec.agentGatewayConfig` to `{}` using [`reasoningEngines.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/patch) , and wait for each update operation to finish.
      3.  Call `reasoningEngines.patch` on each agent to set `spec.deploymentSpec.agentGatewayConfig` to the replacement gateway resource name. For example requests, see [Route Agent Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy#route-traffic) .

3.  After all workloads stop referencing the previous gateway, follow the steps in [Delete an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#delete-gateway) to tear down the previous gateway.

## Update an Agent Gateway

You can update certain Agent Gateway configurations directly in the Google Cloud console or by using the gcloud CLI to export the gateway configuration to a YAML file, make your changes, and re-import the file.

### Update the Agent Registry

You can update the associated Agent Registry in the Google Cloud console or the gcloud CLI. Your gateway should reference the single regional registry corresponding to the gateway's region. If the gateway is linked to a Gemini Enterprise app, the gateway must keep a single registry [matching that app location](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy#plan-ge-agw) .

### Console

1.  In the Google Cloud console, go to the **Gateways** page.

2.  Click the name of the gateway that you want to update.

3.  On the **Details** tab, in the **Overview** section, click **Edit registries** .

4.  Select the regional Agent Registry that matches the region where your gateway is deployed, and then click **Save** .

### gcloud

Export the gateway configuration to `agent-gateway.yaml` using `gcloud network-services agent-gateways export` , edit `registries` , `description` , or `labels` (removing output-only fields such as `createTime` , `updateTime` , `agentGatewayCard` , and `selfLink` ), and re-import the file using `gcloud network-services agent-gateways import` as shown in [Update the gateway's connectivity template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#update-gateway-config) .

### Update the connectivity template

You can update an Agent Gateway resource's connectivity template by using the gcloud CLI.

### gcloud

1.  Create a new `AgentConnectivityTemplate` with your updated connectivity settings, ensuring that it uses the same `networkAttachment` as the existing gateway. For detailed template syntax and configuration instructions, see [Set up Agent Gateway with VPC connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#configure-vpc-connectivity) .

2.  Export the existing gateway configuration to a YAML file:

    ```
    gcloud network-services agent-gateways export AGENT_GATEWAY_NAME \
     --destination="agent-gateway.yaml" \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

    Replace the following:

    - `AGENT_GATEWAY_NAME` : the name of the gateway to update.
    - `LOCATION` : the region where the gateway is deployed.
    - `PROJECT_ID` : the project ID where the gateway is deployed.

3.  In the exported `agent-gateway.yaml` file, keep your existing `protocols` , `registries` , `description` , and `labels` fields intact, remove output-only fields ( `createTime` , `updateTime` , `agentGatewayCard` , `selfLink` ), and update `agentConnectivityTemplate` to reference the new template:

    ```
    name: projects/PROJECT_NUMBER/locations/LOCATION/agentGateways/AGENT_GATEWAY_NAME
    protocols:
      - MCP
    googleManaged:
      governedAccessPath: AGENT_TO_ANYWHERE
    registries:
      - //agentregistry.googleapis.com/projects/PROJECT_NUMBER/locations/LOCATION
    agentConnectivityTemplate: projects/PROJECT_NUMBER/locations/LOCATION/agentConnectivityTemplates/NEW_TEMPLATE_NAME
    ```

    Replace the following:

    - `PROJECT_NUMBER` : the numeric project number where the gateway is deployed ( `agentConnectivityTemplate` requires the project number rather than the project ID).
    - `LOCATION` : the gateway's region.
    - `AGENT_GATEWAY_NAME` : the name of the gateway.
    - `NEW_TEMPLATE_NAME` : the name of the replacement connectivity template.

4.  Re-import the updated YAML file to apply your changes:

    ```
    gcloud network-services agent-gateways import AGENT_GATEWAY_NAME \
     --source="agent-gateway.yaml" \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

5.  Optional: Delete the previous connectivity template after the gateway update finishes:

    ```
    gcloud network-services agent-connectivity-templates delete OLD_TEMPLATE_NAME \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

### Modify IAP settings or Model Armor templates

You can modify IAP enforcement settings and Model Armor templates by updating the authorization extensions attached to your gateway.

### Console

1.  In the Google Cloud console, go to the **Gateways** page.

2.  Click the name of the gateway that you want to update.

3.  On the **Details** tab, update your attached security extensions:

    - **Change IAP enforcement mode** : In the **Access authorization** section, next to **Access authorization** , click **Edit access authorization** . Select **Audit-only** (dry-run mode) or **Enforce policies** , and then click **Save** .

    - **Change Model Armor templates** : In the **AI Security** section, click **Edit request template** next to **Template for requests** or **Edit response template** next to **Template for responses** . Select the replacement template, and then click **Save** .

    > **Note:** The **Access authorization** and **AI Security** sections appear in the Google Cloud console only if you enabled those features when you created the gateway. To attach new IAP, Model Armor, or custom authorization policies to an existing gateway, use the gcloud CLI as described in [Delegate authorization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) .

### gcloud

1.  List the authorization extensions in the gateway's region to identify the extension name:

    ```
    gcloud service-extensions authz-extensions list \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

    Replace `LOCATION` with the gateway's region and `PROJECT_ID` with your project ID.

2.  Inspect the current configuration of the extension:

    ```
    gcloud service-extensions authz-extensions describe AUTHZ_EXTENSION_NAME \
     --location=LOCATION \
     --project=PROJECT_ID \
     --format=yaml
    ```

    Replace `AUTHZ_EXTENSION_NAME` with the name of your IAP or Model Armor `AuthzExtension` resource.

3.  Save the updated extension specification to `authz-extension.yaml` , omitting output-only fields such as `createTime` and `updateTime` :

    - **For an IAP extension** : Include `iamEnforcementMode: "DRY_RUN"` for audit-only mode, or remove `iamEnforcementMode` to enforce policies:

      ```
      name: AUTHZ_EXTENSION_NAME
      service: iap.googleapis.com
      failOpen: false
      timeout: 1s
      metadata:
        iapPolicyVersion: "V2"
        iamEnforcementMode: "DRY_RUN" # Omit this line to enforce policies
      ```

    - **For a Model Armor extension** : Update `request_template_id` and `response_template_id` in `metadata.model_armor_settings` :

      ```
      name: AUTHZ_EXTENSION_NAME
      service: modelarmor.LOCATION.rep.googleapis.com
      failOpen: false
      timeout: 1s
      metadata:
        model_armor_settings: '[
          {
            "request_template_id": "projects/MODEL_ARMOR_PROJECT_ID/locations/LOCATION/templates/REQUEST_TEMPLATE_ID",
            "response_template_id": "projects/MODEL_ARMOR_PROJECT_ID/locations/LOCATION/templates/RESPONSE_TEMPLATE_ID"
          }
        ]'
      ```

      Replace the following:

      - `AUTHZ_EXTENSION_NAME` : the name of your Model Armor `AuthzExtension` resource.
      - `LOCATION` : the gateway's region.
      - `MODEL_ARMOR_PROJECT_ID` : the project ID that hosts your Model Armor templates.
      - `REQUEST_TEMPLATE_ID` and `RESPONSE_TEMPLATE_ID` : the IDs of your request and response templates.

      Ensure that the gateway service account ( `agentGatewayCard.serviceExtensionsServiceAccount` ) has `roles/modelarmor.user` on any newly referenced template project, as well as `roles/modelarmor.calloutUser` and `roles/serviceusage.serviceUsageConsumer` on the gateway project (see [Delegate authorization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) ).

4.  Import the updated extension YAML file:

    ```
    gcloud service-extensions authz-extensions import AUTHZ_EXTENSION_NAME \
     --source="authz-extension.yaml" \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

To attach new authorization policies or modify traffic matching rules on an existing `AuthzPolicy` , see [Delegate authorization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) .

## Disassociate workloads from an Agent Gateway

Before you can delete an Agent Gateway, you must disassociate every Gemini Enterprise app and Agent Runtime agent that references the gateway.

### Disassociate a Gemini Enterprise app

You can unlink an Agent Gateway from a Gemini Enterprise app in the Google Cloud console:

1.  In the Google Cloud console, go to the **Gemini Enterprise** page.

2.  Click the name of the app associated with the gateway.

3.  Click **Security** .

4.  On the **Configuration** tab, under **Agent Gateway configuration** , clear the **Agent Gateway resource name** field.

5.  Click **Save** .

Disassociating an Agent Gateway stops routing the app's outbound traffic through the gateway. Imported agents and Model Context Protocol (MCP) servers remain registered in Agent Registry, but the app can't access them until you link a gateway again. Note that the new gateway must reference the same Agent Registry.

### Disassociate an Agent Runtime agent

The Google Cloud console and the gcloud CLI don't support modifying Agent Runtime gateway bindings. To disassociate an Agent Gateway from a deployed Agent Runtime agent while keeping the agent running, you can call the [`reasoningEngines.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/patch) REST API method to clear `spec.deploymentSpec.agentGatewayConfig` :

1.  Ensure that the agent routes all traffic to the latest revision ( `trafficConfig.trafficSplitAlwaysLatest` set to `true` , or no manual `trafficConfig` split configured). Clearing or changing a gateway binding fails if a manual revision traffic split is active and irreversibly archives all previous revisions. For details, see [Agent Gateway and revisions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-revisions-and-traffic#agent-gateway) .

2.  Send a `PATCH` request to the reasoning engine with `updateMask=spec.deploymentSpec.agentGatewayConfig` and an empty `agentGatewayConfig` object ( `{}` ):

    ```
    curl -X PATCH \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d '{
       "spec": {
         "deploymentSpec": {
           "agentGatewayConfig": {}
         }
       }
     }' \
     "https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/reasoningEngines/RESOURCE_ID?updateMask=spec.deploymentSpec.agentGatewayConfig"
    ```

    Replace the following:

    - `REGION` : the region where the agent is deployed.
    - `PROJECT_ID` : the project ID where the agent is deployed.
    - `RESOURCE_ID` : the [resource ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#resource-identifier) of the agent.

> **Note:** If you no longer need the deployed agent, you can instead delete the agent in the Google Cloud console to release its reference to the gateway. For details, see [Delete a deployed agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#delete) .

## Delete an Agent Gateway

Agent Gateway enforces strict reference tracking to prevent orphaned security policies and broken agent traffic paths. Deleting a gateway fails, and the **Delete** button in the Google Cloud console remains unavailable, if any of the following conditions apply:

- One or more Agent Runtime agents or Gemini Enterprise apps still reference the gateway.
- Any `AuthzPolicy` (for IAP, Model Armor, or a custom provider) or `TelemetryPolicy` still targets the gateway.
- A VPC configuration update operation is still running on the gateway.

Complete the following steps in sequence to delete an Agent Gateway and clean up its associated resources:

### Console

1.  Ensure that no Gemini Enterprise apps or Agent Runtime agents reference the gateway. Follow the instructions in [Disassociate workloads from an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#disassociate-workloads) .

2.  In the Google Cloud console, go to the **Gateways** page.

3.  Click the name of the gateway that you want to delete.

4.  On the **Details** tab, remove all policy associations targeting the gateway:

    - If the **Access authorization** section appears, click **Remove** , and then confirm the deletion. This action deletes both the IAP `AuthzPolicy` and its `AuthzExtension` .
    - If the **AI Security** section appears, click **Remove** , and then confirm the deletion. This action deletes both the Model Armor `AuthzPolicy` and its `AuthzExtension` .
    - Check the **Service Extensions** table. If any custom `AuthzPolicy` resources remain attached, use the **gcloud** tab in this procedure to delete them before continuing.

5.  After all policy associations are removed and no VPC update is in progress, click **Delete** , and then confirm the deletion.

6.  Confirm that the gateway no longer appears in the **Gateways** list for your project.

7.  Optional: Clean up unused connectivity resources if no other gateway uses them. Use the **gcloud** tab to delete the `AgentConnectivityTemplate` , and [delete the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#delete) .

### gcloud

1.  Ensure that no Gemini Enterprise apps or Agent Runtime agents reference the gateway. Follow the instructions in [Disassociate workloads from an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways#disassociate-workloads) .

2.  Remove authorization policies and authorization extensions:

    > **Important:** Always delete each `AuthzPolicy` **before** deleting the `AuthzExtension` that it references. Deleting an `AuthzExtension` first fails because the `AuthzPolicy` holds an active reference to the extension.

    1.  List the authorization policies in the gateway's region to find policies whose `target.resources` field references your gateway, and note any referenced `authzExtensions` :

        ```
        gcloud network-security authz-policies list \
          --location=LOCATION \
          --project=PROJECT_ID \
          --format="yaml(name,target.resources,customProvider.authzExtension.resources)"
        ```

        Replace `LOCATION` with the gateway's region and `PROJECT_ID` with your project ID.

    2.  Delete each `AuthzPolicy` that targets the gateway:

        ```
        gcloud network-security authz-policies delete AUTHZ_POLICY_NAME \
          --location=LOCATION \
          --project=PROJECT_ID
        ```

        Replace `AUTHZ_POLICY_NAME` with the ID of each authorization policy targeting the gateway (for example, `AGENT_GATEWAY_NAME `` -iap-authzpolicy` or `AGENT_GATEWAY_NAME `` -aisecurity-authzpolicy` for console-created policies).

    3.  Optional: After you delete the referencing `AuthzPolicy` resources, delete any `AuthzExtension` resources that no other policies use:

        ```
        gcloud service-extensions authz-extensions delete AUTHZ_EXTENSION_NAME \
          --location=LOCATION \
          --project=PROJECT_ID
        ```

        Replace `AUTHZ_EXTENSION_NAME` with the ID of the unused authorization extension.

3.  Delete the Agent Gateway:

    ```
    gcloud network-services agent-gateways delete AGENT_GATEWAY_NAME \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

    Replace `AGENT_GATEWAY_NAME` with the name of the gateway to delete.

4.  Confirm that the gateway no longer appears in the regional gateway list:

    ```
    gcloud network-services agent-gateways list \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

5.  Optional: You can't delete an `AgentConnectivityTemplate` while an Agent Gateway references it. After you delete the gateway, delete any unused connectivity templates:

    ```
    gcloud network-services agent-connectivity-templates delete CONNECTIVITY_TEMPLATE_NAME \
     --location=LOCATION \
     --project=PROJECT_ID
    ```

    Replace `CONNECTIVITY_TEMPLATE_NAME` with the name of the unused connectivity template. If you no longer need the underlying Private Service Connect network attachment, private Cloud DNS zones, or Certificate Manager `TrustConfig` resources, see [Delete network attachments](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#delete) .

## What's next

Guide

### [Delegate authorization for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)

Learn how to delegate authorization for Agent Gateway to IAP, Model Armor, or your own custom authorization service.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Guide

### [Set up an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway)

Learn how to set up an Agent Gateway.

Troubleshooting

### [Troubleshoot Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway)

Learn how to troubleshoot Agent Gateway connectivity.
