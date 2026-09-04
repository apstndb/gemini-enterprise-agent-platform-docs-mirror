---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap
title: Manage IAM Access policies
description: Learn how to create, list, view, update, and delete Identity and Access Management access policies and policy bindings for Agent Platform.
data_source: docs.cloud.google.com
---

You can create, list, view, update, and delete IAM Unified Access Policies (Access policies) and policy bindings using the Google Cloud console, the gcloud CLI, or the REST API.

Agent Gateway uses Identity-Aware Proxy (IAP) to enforce these egress policies across your agents, MCP servers, and endpoints. For an overview of how policies work, see [IAM Access policies overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap) . For detailed rule examples and CEL attributes, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

## Required roles

To get the permissions that you need to manage Access policies and policy bindings, ask your administrator to grant you the following IAM roles on your project:

  - View Access policies and bindings: [Access Policy Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.accessPolicyViewer) ( `roles/iam.accessPolicyViewer` )
  - Create, update, and delete Access policies and bindings: [Access Policy Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.accessPolicyAdmin) ( `roles/iam.accessPolicyAdmin` )
  - Bind policies to a project: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an Access policy

An Access policy contains one or more allow or deny rules. Before a policy takes effect, you must [bind it to a target resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap#bind-policy) .

For more information about creating Access policies, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

### Console

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  To add an IAM Access policy for Agent Gateway egress, click add **Create** .

4.  In the **Policy details** pane, do the following:
    
    1.  Click the **Policy** field.
    2.  In the drop-down list, select **Create new policy** .
    3.  In the **Policy name** field, enter a descriptive name for the policy.
    4.  In **Add Rules** , configure your allow or deny rules and CEL conditions. For Access policy configuration steps and examples, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .
    5.  To save the rule, click **Create** .

### gcloud

To create an Access policy using the gcloud CLI, define your policy rules in a JSON file and run the `create` command:

```sh
gcloud iam access-policies create POLICY_NAME \
    --details-rules=POLICY_FILE \
    --project=PROJECT_ID \
    --location=global
```

Replace the following:

  - `  POLICY_NAME  ` : the name of the policy
  - `  POLICY_FILE  ` : the path to the policy file—for example: `my-policy.json`
  - `  PROJECT_ID  ` : the project ID that contains the policy

### API

To create an Access policy using the REST API, make a `POST` request to the `accessPolicies` endpoint:

```sh
curl -X POST \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
-d '{
  "details": {
    "rules": [
      {
        "description": "RULE_DESCRIPTION",
        "effect": "ALLOW",
        "principals": [
          "principal://agents.global.proj-PROJECT_NUMBER.system.id.goog/resources/aiplatform/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_NAME"
        ],
        "operation": {
          "permissions": [
            "iap.resources.egressViaIAP"
          ]
        },
        "conditions": {
          "iap.googleapis.com": {
            "expression": "CEL_EXPRESSION"
          }
        }
      }
    ]
  }
}'
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID
  - `  POLICY_NAME  ` : the ID for the new policy
  - `  PROJECT_NUMBER  ` : the project number
  - `  LOCATION  ` : the agent location
  - `  AGENT_NAME  ` : the source agent ID
  - `  CEL_EXPRESSION  ` : your CEL condition expression

## Bind a policy to a target resource

To enforce an Access policy, bind it to a target resource scope, such as a project or an Agent Gateway instance.

### Console

When you save a policy, it is automatically bound to the project.

### gcloud

To bind an Access policy to a target resource using the gcloud CLI, run the following command:

```sh
gcloud iam policy-bindings create BINDING_NAME \
    --policy="projects/PROJECT_ID/locations/global/accessPolicies/POLICY_NAME" \
    --target-resource="TARGET_RESOURCE" \
    --project=PROJECT_ID \
    --location=global
```

Replace the following:

  - `  BINDING_NAME  ` : the name for your policy binding

  - `  PROJECT_ID  ` : your Google Cloud project ID

  - `  POLICY_NAME  ` : the name of your access policy

  - `  TARGET_RESOURCE  ` : the full resource URI for the project, formatted as follows:
    
    ```html
        //cloudresourcemanager.googleapis.com/projects/PROJECT_ID
        
    ```

### API

To bind an Access policy to a target resource using the REST API, make a `POST` request to the `policyBindings` endpoint:

```sh
curl -X POST \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/policyBindings?policyBindingId=BINDING_NAME" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
-d '{
  "policy": "projects/PROJECT_ID/locations/global/accessPolicies/POLICY_NAME",
  "target": {
    "resource": "TARGET_RESOURCE"
  }
}'
```

Replace the following:

  - `  PROJECT_ID  ` : your project ID
  - `  BINDING_NAME  ` : a name for your policy binding
  - `  POLICY_NAME  ` : the name of the Access policy
  - `  TARGET_RESOURCE  ` : the full resource URI for the binding target—for example:
  - Project: ` //cloudresourcemanager.googleapis.com/projects/ PROJECT_ID  `
  - Agent Gateway: ` //networkservices.googleapis.com/projects/ PROJECT_ID /locations/ LOCATION /agentGateways/ GATEWAY_NAME  `

## List policies and policy bindings

You can list all Access policies in your project or list all policy bindings attached to a target resource.

### List Access policies

### Console

1.  In the Google Cloud console, go to the **Policies** page.
2.  All Access policies created in your project appear in the list in the **Unified Access Policies** tab.

### gcloud

To list Access policies in your project, run the following command:

```sh
gcloud iam access-policies list \
  --project=PROJECT_ID \
  --location=global
```

### API

To list Access policies using the REST API, make a `GET` request to the `accessPolicies` endpoint:

```sh
curl -X GET \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies" \
-H "Authorization: Bearer $(gcloud auth print-access-token)"
```

### List policy bindings

### Console

Because policies that are managed through the console are automatically bound to the project, you must use the gcloud CLI or the REST API to view policy bindings.

### gcloud

To list policy bindings in your project, run the following command:

```sh
gcloud iam policy-bindings list \
  --project=PROJECT_ID \
  --location=global
```

To filter policy bindings by a specific target resource, specify the `--target-resource` flag:

```sh
gcloud iam policy-bindings list \
  --target-resource="TARGET_RESOURCE" \
  --project=PROJECT_ID \
  --location=global
```

### API

To list policy bindings using the REST API, make a `GET` request to the `policyBindings` endpoint:

```sh
curl -X GET \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/policyBindings" \
-H "Authorization: Bearer $(gcloud auth print-access-token)"
```

## Describe a policy or policy binding

You can retrieve the detailed configuration and rules of a specific Access policy or policy binding.

### Describe an Access policy

### Console

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In the **Agent policies** table in the Access policies tab, locate the policy that you want to describe.

4.  In the row for the policy, click more\_vert **More actions** , and then click **View rule** .

### gcloud

To describe a specific Access policy, run the following command:

```sh
gcloud iam access-policies describe POLICY_NAME \
  --project=PROJECT_ID \
  --location=global
```

### API

To retrieve a specific Access policy using the REST API, make a `GET` request:

```sh
curl -X GET \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies/POLICY_NAME" \
-H "Authorization: Bearer $(gcloud auth print-access-token)"
```

### Describe a policy binding

### Console

Because policies that are managed through the console are automatically bound to the project, you must use the gcloud CLI or the REST API to view policy bindings.

### gcloud

To describe a specific policy binding, run the following command:

```sh
gcloud iam policy-bindings describe BINDING_NAME \
  --project=PROJECT_ID \
  --location=global
```

### API

To retrieve a specific policy binding using the REST API, make a `GET` request:

```sh
curl -X GET \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/policyBindings/BINDING_NAME" \
-H "Authorization: Bearer $(gcloud auth print-access-token)"
```

## Update policies and policy bindings

You can update the rules inside an existing Access policy or update the target or policy referenced by a policy binding.

### Update an Access policy

### Console

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In the **Agent policies** table in the Access policies tab, locate the policy row that you want to edit.

4.  Click more\_vert **More actions** , and then click **Edit rule** .

5.  Modify the rules, effect, principals, or CEL conditions.

6.  Click **Save** .

### gcloud

To update an existing Access policy using the gcloud CLI, save your modified rules to a JSON file and run the following command:

```sh
gcloud iam access-policies update POLICY_NAME \
  --details-rules=POLICY_FILE.json \
  --project=PROJECT_ID \
  --location=global
```

### API

To update an Access policy using the REST API, make a `PATCH` request to the Access policy endpoint:

```sh
curl -X PATCH \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies/POLICY_NAME?updateMask=details" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
-d '{
  "details": {
    "rules": [
      {
        "description": "RULE_DESCRIPTION",
        "effect": "ALLOW",
        "principals": [
          "principal://agents.global.proj-PROJECT_NUMBER.system.id.goog/resources/aiplatform/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_NAME"
        ],
        "operation": {
          "permissions": [
            "iap.resources.egressViaIAP"
          ]
        }
      }
    ]
  }
}'
```

### Update a policy binding

### Console

To update a policy binding, you must use the gcloud CLI or the REST API.

### gcloud

To update a policy binding to reference a different policy or target, run the following command:

```sh
gcloud iam policy-bindings update BINDING_NAME \
  --policy="projects/PROJECT_ID/locations/global/accessPolicies/NEW_POLICY_NAME" \
  --project=PROJECT_ID \
  --location=global
```

### API

To update a policy binding using the REST API, make a `PATCH` request:

```sh
curl -X PATCH \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/policyBindings/BINDING_NAME?updateMask=policy" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
-d '{
  "policy": "projects/PROJECT_ID/locations/global/accessPolicies/NEW_POLICY_NAME"
}'
```

## Delete policies and policy bindings

> **Caution:** Before you can delete an Access policy, you must first delete all policy bindings that reference it.

### Delete a policy binding

### Console

To delete a policy binding, you must use the gcloud CLI or the REST API.

### gcloud

To delete a policy binding, run the following command:

```sh
gcloud iam policy-bindings delete BINDING_NAME \
  --project=PROJECT_ID \
  --location=global
```

### API

To delete a policy binding using the REST API, make a `DELETE` request:

```sh
curl -X DELETE \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/policyBindings/BINDING_NAME" \
-H "Authorization: Bearer $(gcloud auth print-access-token)"
```

### Delete an Access policy

### Console

To delete an Access policy, you must delete all of the rules in the policy.

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In the **Agent Policies** table of the **Unified Access Policies** tab, filter filter\_list **Filter** or locate the policy that you want to delete.

4.  Click more\_vert **More actions** , and then click **Delete rule** .

### gcloud

To delete an Access policy after deleting its bindings, run the following command:

```sh
gcloud iam access-policies delete POLICY_NAME \
  --project=PROJECT_ID \
  --location=global
```

### API

To delete an Access policy using the REST API, make a `DELETE` request:

```sh
curl -X DELETE \
"https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies/POLICY_NAME" \
-H "Authorization: Bearer $(gcloud auth print-access-token)"
```

## What's next

  - [CEL attributes for Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap)
  - [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
  - [Troubleshoot IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap)

Overview

### [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview)

Get an overview of Agent Gateway.

Guide

### [Configure content and business policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance)

Learn how to configure content and business policies.

Guide

### [Test policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/test-policies)

Learn how to test policies.
