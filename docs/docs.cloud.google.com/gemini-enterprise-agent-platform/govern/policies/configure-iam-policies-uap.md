---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap
title: Create IAM Access policies
description: Learn how to create Identity and Access Management policies to govern agentic communication in Agent Platform.
data_source: docs.cloud.google.com
---

You can create [Identity and Access Management (IAM) Unified Access Policies (Access policies)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#access-policies) that govern agentic communication between agents and destination resources, such as [agent registries](https://docs.cloud.google.com/agent-registry/overview) , MCP servers, agents, and registered and unregistered endpoints.

[Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) uses Identity-Aware Proxy (IAP) to evaluate and enforce Access policies.

In the Google Cloud console, you can use the **Policies** page to create Agent Gateway IAM Unified Access Policies (Access policies). Access policies can contain allow rules, deny rules, or both.

You can use the Google Cloud CLI and the REST API to create IAM Access policies by first creating JSON-formatted policy files, creating the policies, and binding them with projects that contain your Agent Gateway instances.

To learn how to update and delete Access policies, see [Manage IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap) .

## Before you begin

Before you create an IAM Access policy, do the following:

1.  You must turn the enforcement off for the **Disable binding access policy to resource** ( `constraints/iam.managed.disableAccessPolicyBindings` ) managed constraint. By default, this boolean constraint is enabled for new organizations, and prevents you from binding an IAM v3 API access policy to a resource. For more information, see [Updating policies with boolean rules](https://docs.cloud.google.com/organization-policy/apply-policies#boolean_constraints) .

2.  Set up a Google Cloud billing project.

3.  Enable the required APIs:
    
    ```sh
    gcloud services enable \
        agentregistry.googleapis.com \
        aiplatform.googleapis.com \
        iam.googleapis.com \
        networkservices.googleapis.com
    ```

4.  Make sure that you have [set up an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) and IAP using an IAP v2 policy. We recommend that you initially configure Agent Gateway in dry-run mode. For more information about Agent Gateway, see [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) .

5.  Populate your Agent Registry with target destination resources, such as agents, MCP servers, and endpoints.

6.  Determine the [agent identities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) of the source agents that you want to manage access from. To manage access from an entire registry using the Google Cloud console, select the project that contains the registry.

7.  Review [IAP and Access policy best practices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#best-practices) .

### Required roles

To get the permissions that you need to configure Agent Platform for AI agents, ask your administrator to grant you the following IAM roles on your project:

  - Create Agent Gateway instances: IAP Policy Admin ( `roles/iap.admin` ) or Network Security Admin ( `roles/networksecurity.admin` )
  - Create and bind Access policies: [Access Policy Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.accessPolicyAdmin) ( `roles/iam.accessPolicyAdmin` )
  - Bind policy to a project: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create IAM Access policies

Access policies let you configure multiple rules. Each rule can have an allow effect or a deny effect.

> **Note:** Deny rules are evaluated first. If a deny rule condition evaluates to `true` , access is immediately blocked, even if a parallel allow rule also evaluates to `true` .

### Create an Access policy with an allow rule

You can create an Access policy with an allow rule using the Google Cloud console, the gcloud CLI, or the REST API.

### Console

To create an Access policy in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  To add an IAM Access policy for Agent Gateway egress, click add **Create** .

4.  In **Policy details** , do the following:
    
    1.  Click the **Policy** field.
    2.  In the drop-down list, select **Create new policy** .
    3.  In the **Policy name** field, enter the name of the policy. The policy ID is automatically generated based on the policy name.
    4.  Optional: Click **Edit** to edit the policy ID. In the **Policy ID** field, you can change the name of the policy ID.
    5.  In **Add Rules** , expand the default rule, **Rule 1** or click **Add a rule** .

5.  Create one or more [rules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#rules) for your [Access policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#create-ag-iam-policy) . View [examples of different policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#example-policies) .

6.  To create your policy, click **Create** .

After you save your policy, the following happens:

  - The IAM `iap.resources.egressViaIAP` permission is granted to the principals in your policy.

  - The policy is automatically bound to the selected project.

  - All Agent Gateway instances in this project can enforce any policy associated with the project.

### gcloud

To create an Access policy in the gcloud CLI, do the following:

1.  Create a JSON-formatted policy file. Access policies can contain one or more [rules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#rules) . Each rule controls access from one or more agent principals to one or more target resources.
    
    ```json
    [
      {
        "description": "RULE_DESCRIPTION",
        "effect": "RULE_EFFECT",
        "principals": [
          AGENT_PRINCIPALS
        ],
        "operation": {
          "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
        },
        
        "conditions": {
          "iap.googleapis.com": {
            "expression": "CEL_EXPRESSION"
          }
        }
        
      }
    ]
    ```
    
    Replace the following:
    
      - `  RULE_DESCRIPTION  ` : the description of the rule
    
      - `  RULE_EFFECT  ` : the effect of the rule, which is either `ALLOW` or `DENY`
    
      - `  AGENT_PRINCIPALS  ` : the principals for the source agent identity. Agent principals can be an array of one or more individual principals or principal sets:
        
          - **Built-in agent identities:** ` principal:// TRUST_DOMAIN / AGENT_UNIQUE_IDENTIFIER  `
            
            The structure of `  AGENT_UNIQUE_IDENTIFIER  ` depends on the Google Cloud service hosting the agent:
            
              - **Agent Runtime (Reasoning Engine):** `principal://agents.global.org-123456789012.system.id.goog/resources/aiplatform/projects/9876543210/locations/us-central1/reasoningEngines/my-agent`
              - **Gemini Enterprise (Discovery Engine):** `principal://agents.global.org-123456789012.system.id.goog/resources/discoveryengine/projects/9876543210/locations/global/engines/my-engine/assistants/default_assistant/agents/default/core_assistant`
              - **Cloud Run (Agent Identity):** `principal://agents.global.org-123456789012.system.id.goog/resources/run/projects/9876543210/locations/us-central1/services/my-cloud-run-agent`
            
            Replace the following:
            
              - `  TRUST_DOMAIN  ` : the trust domain of the project or organization that contains the agent principal (for example, `agents.global.org- ORGANIZATION_ID .system.id.goog` or `agents.global.proj- PROJECT_NUMBER .system.id.goog` )
              - `  AGENT_UNIQUE_IDENTIFIER  ` : the resource URI path of the agent instance
        
          - **Workload Identity Federation (custom or external agents):** ` principal://iam.googleapis.com/projects/ PROJECT_NUMBER /locations/global/workloadIdentityPools/ POOL_ID /subject/ SUBJECT  ` —for example, `principal://iam.googleapis.com/projects/1234567890/locations/global/workloadIdentityPools/my-agent-identity/subject/ns/default/sa/my-agent`
            
            Replace the following:
            
              - `  PROJECT_NUMBER  ` : the project number of the project that contains the workload identity pool
              - `  POOL_ID  ` : the ID of the workload identity pool
              - `  SUBJECT  ` : the subject identifier of the agent principal
    
      - `  CONDITION  ` : the condition parameter, formatted as follows:
        
        ```json
        "conditions": {
          "iap.googleapis.com": {
            "expression": "CEL_EXPRESSION"
          }
        }
        ```
        
        Replace `  CEL_EXPRESSION  ` with a conditional expression—for example:
        
            "destination.agent_registry.mcp_server.name == '/projects/corp-apim-prod/locations/us-east1/mcpServers/finance-data-service' && destination.agent_registry.mcp_server.tool.name == 'updateRecord'"
        
        This expression must be a valid CEL expression. It must evaluate to `true` for access to be allowed.
    
    In all agent egress policies, you must set the permission to `iap.resources.egressViaIAP` .
    
    For more information, see [Access policy rules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#rules) and [Example policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#example-policies) .

2.  To create the Access policy, run the following command:
    
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

### REST API

To create and bind a policy using the REST API, do the following:

1.  Save the JSON-formatted policy details to a file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          RULES
        ]
      }
    }
    ```
    
    Replace `  RULES  ` with one or more [rules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#rules) .

2.  To create the Access policy, make a `POST` request to the `accessPolicies` endpoint:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

### Create a combination allow and deny Access policy

You can configure an Access policy containing both allow and deny rules by using the Google Cloud console, the gcloud CLI, and the REST API.

> **Note:** Deny rules are evaluated before and override allow rules. This means that deny rules can disallow access even if an allow rule would otherwise permit access.

### Console

To create an Access policy with both allow and deny rules in the Google Cloud console, do the following:

1.  In **Add Rules** , configure the allow rule:
    1.  In **Rule description** , enter the description for the allow rule.
    2.  In **Rule effect** , select **Allow** .
    3.  Select the agent principals and target resources, and add the allow [CEL conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#conditions) .
    4.  To save the allow rule, click **Save** .
2.  To add the deny rule, click **Add a rule** :
    1.  In **Rule description** , enter the description for the deny rule.
    2.  In **Rule effect** , select **Deny** .
    3.  Select the agent principals and target resources, and add the deny [CEL conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#conditions) .
    4.  To save the deny rule, click **Save** .
3.  To create the policy, click **Create** .

### gcloud

To create an Access policy file containing both allow and deny rules, do the following:

1.  Save the following to your JSON-formatted policy file:
    
    ```json
    [
      {
        "description": "ALLOW_RULE_DESCRIPTION",
        "effect": "ALLOW",
        "principals": [
          "AGENT_PRINCIPALS_ALLOW"
        ],
        "operation": {
          "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
        },
        "conditions": {
          "iap.googleapis.com": {
            "expression": "CEL_EXPRESSION_ALLOW"
          }
        }
      },
      {
        "description": "DENY_RULE_DESCRIPTION",
        "effect": "DENY",
        "principals": [
          "AGENT_PRINCIPALS_DENY"
        ],
        "operation": {
          "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
        },
        "conditions": {
          "iap.googleapis.com": {
            "expression": "CEL_EXPRESSION_DENY"
          }
        }
      }
    ]
    ```
    
    Replace the following:
    
      - `  ALLOW_RULE_DESCRIPTION  ` : the description of the allow rule
      - `  DENY_RULE_DESCRIPTION  ` : the description of the deny rule
      - `  AGENT_PRINCIPALS_ALLOW  ` : the agent principals that you want to allow—for example, ` principal://agents.global.proj- PROJECT_NUMBER .system.id.goog/resources/aiplatform/projects/ PROJECT_ID /locations/ LOCATION /reasoningEngines/ AGENT_NAME  `
      - `  AGENT_PRINCIPALS_DENY  ` : the agent principals that you want to deny—for example, ` principal://agents.global.proj- PROJECT_NUMBER .system.id.goog/resources/aiplatform/projects/ PROJECT_ID /locations/ LOCATION /reasoningEngines/ AGENT_NAME  `
      - `  CEL_EXPRESSION_ALLOW  ` : the CEL expression for the allow rule—for example, `destination.agent_registry.mcp_server.name == "/projects/my-project/locations/us-east1/mcpServers/finance-data-service" && destination.agent_registry.mcp_server.tool.name == "getStatements"`
      - `  CEL_EXPRESSION_DENY  ` : the CEL expression for the deny rule—for example, `destination.agent_registry.mcp_server.name == "/projects/my-project/locations/us-east1/mcpServers/finance-data-service" && destination.agent_registry.mcp_server.tool.name == "updateRecord"`

2.  To create the Access policy, run the following command:
    
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

3.  To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### REST API

To create an Access policy containing both allow and deny rules using the REST API, do the following:

1.  Save the following to a JSON-formatted policy file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "ALLOW_RULE_DESCRIPTION",
            "effect": "ALLOW",
            "principals": [
              "AGENT_PRINCIPALS_ALLOW"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "CEL_EXPRESSION_ALLOW"
              }
            }
          },
          {
            "description": "DENY_RULE_DESCRIPTION",
            "effect": "DENY",
            "principals": [
              "AGENT_PRINCIPALS_DENY"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "CEL_EXPRESSION_DENY"
              }
            }
          }
        ]
      }
    }
    ```
    
    Replace the following:
    
      - `  ALLOW_RULE_DESCRIPTION  ` : the description of the allow rule
      - `  DENY_RULE_DESCRIPTION  ` : the description of the deny rule
      - `  AGENT_PRINCIPALS_ALLOW  ` : the agent principals that you want to allow
      - `  AGENT_PRINCIPALS_DENY  ` : the agent principals that you want to deny
      - `  CEL_EXPRESSION_ALLOW  ` : the CEL expression for the allow rule
      - `  CEL_EXPRESSION_DENY  ` : the CEL expression for the deny rule

2.  To create the policy, run the following `curl` command:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

3.  To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### Bind an Access policy to a project

### Console

After you save your policy, the following happens:

  - The IAM `iap.resources.egressViaIAP` permission is granted to the principals in your policy.

  - The policy is automatically bound to the selected project.

  - All Agent Gateway instances in this project can enforce any policy associated with the project.

### gcloud

To bind the policy to the target resource, run the following command:

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

### REST API

To bind the policy to the target resource, make a `POST` request to the `policyBindings` endpoint:

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

  - `  PROJECT_ID  ` : the project ID
  - `  BINDING_NAME  ` : a name for the binding
  - `  POLICY_NAME  ` : the name of the policy that you created earlier in this document
  - `  TARGET_RESOURCE  ` : the full resource URI for the binding target, which can be one of the following:
      - Project: ` //cloudresourcemanager.googleapis.com/projects/ PROJECT_ID  `
      - Agent Gateway: ` //networkservices.googleapis.com/projects/ PROJECT_ID /locations/ LOCATION /agentGateways/ GATEWAY_NAME  `

### Create rules

Access policies can contain one or more rules. Each rule controls access from one or more agent principals to one or more target resources.

### Console

In the Google Cloud console, edit your Access policy and do the following:

1.  Edit your existing rule. To add a rule, click **Add a rule** .
2.  **Rule description** : a human-readable description for this rule
3.  **Select principals** : The source agent principals that the rule manages access from. Principals can be one of the following:
      - **All agents in this project** : All agents that exist in the current project.
      - **Individual agents** : One or more specific principals that you can select. Agents are defined by their agent identities.
      - **Custom principal set** : One or more principal sets that you can specify by entering a [principal identifier](https://docs.cloud.google.com/iam/docs/principal-identifiers) . Principal identifiers must start with `principalSet://` and refer to agent identities.
4.  **Effect** : the rule's effect, which can be one of the following:
      - **Allow** : allows the principals to access the resources
      - **Deny** : disallows the principals from accessing the resources
5.  **Select resources** : One or more types of destination resources that you can select. Resource types include the following:
      - **Registry** : All resources that are registered in an Agent Registry location
    
      - **Agent** : A destination agent that is registered in Agent Registry
    
      - **MCP server** : A destination MCP server that is registered in Agent Registry. You can use [conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#conditions) to further control MCP server access.
        
        > **Important:** The condition builder and condition editor support a subset of CEL attributes. To create a condition with full attribute support, use the **Custom** tab in **Select resources** , or use the gcloud CLI or the IAP REST API.
    
      - **Endpoint** : A destination endpoint that is registered in Agent Registry
    
      - **Unregistered endpoint** : A destination endpoint that is not registered in Agent Registry and is accessed through an external URL. You can use [conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#conditions) to further control unregistered endpoint access.
        
        > **Important:** The condition builder and condition editor support a subset of CEL attributes. To create a condition with full attribute support, use the **Custom** tab in **Select resources** , or use the gcloud CLI or the IAP REST API.

### gcloud

Rules in a JSON-formatted file have the following general format:

```json
{
  "description": "RULE_DESCRIPTION",
  "effect": "EFFECT",
  "principals": [
    "AGENT_PRINCIPALS"
  ],
  "operation": {
    "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
  },
  "conditions": {
    "iap.googleapis.com": {
      "expression": "CONDITION"
    }
  }
}
```

The policy file contains the following:

  - `  RULE_DESCRIPTION  ` : a human-readable description for this rule

  - `  EFFECT  ` : the rule's effect, which can be one of the following:

  - `ALLOW` allows the principal to access the resources

  - `DENY` disallows the principal from accessing the resources

  - `  CONDITION  ` : a CEL expression that conditionally evaluates to true or false. If the expression evaluates to true, then the rule goes into effect. Conditions can also contain references to specific resources that principals can access:

  - `destination.agent_registry` : the destination resource is registered in Agent Registry.

  - `destination.unregistered` : the destination resource is unregistered. It is accessed through a URL. Access can be controlled in the condition.

To learn more about conditions, see [Conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#conditions) . Learn more about conditions attributes in [CEL attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap) .

### REST API

To create and bind a policy using the REST API, do the following:

1.  Save the JSON-formatted policy details to a file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "RULE_DESCRIPTION",
            "effect": "EFFECT",
            "principals": [
              "AGENT_PRINCIPALS"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "CONDITION"
              }
            }
          }
        ]
      }
    }
    ```
    
    Add one or more rules to the `details` field. In each rule, replace the following:
    
      - `  RULE_DESCRIPTION  ` : one or more [rules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#rules)
    
      - `  EFFECT  ` : the rule's effect, which can be one of the following:
        
          - `ALLOW` allows the principal to access the resources
        
          - `DENY` disallows the principal from accessing the resources
    
      - `  AGENT_PRINCIPALS  ` : the agent principals that you want to grant access to.
    
      - `  CONDITION  ` : a CEL expression that conditionally evaluates to true or false. If the expression evaluates to true, then the rule goes into effect. Conditions can also contain references to specific resources that principals can access:
        
          - `destination.agent_registry` : the destination resource is registered in Agent Registry.
          - `destination.unregistered` : the destination resource is unregistered. It is accessed through a URL. Access can be controlled in the condition.
    
    To learn more about conditions, see [Conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#conditions) . Learn more about conditions attributes in [CEL attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap) .

2.  To create the Access policy, make a `POST` request to the `accessPolicies` endpoint:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

3.  To bind the policy to the target resource, make a `POST` request to the `policyBindings` endpoint:
    
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
    
      - `  PROJECT_ID  ` : the project ID
      - `  BINDING_NAME  ` : a name for the binding
      - `  POLICY_NAME  ` : the name of the policy that you created earlier in this document
      - `  TARGET_RESOURCE  ` : the full resource URI for the project formatted as follows: ` //cloudresourcemanager.googleapis.com/projects/ PROJECT_ID  `

### Create conditions

Conditions are Boolean CEL expressions that determine access from agent principals to certain resources.

### Console

In the Google Cloud console you can create conditions by doing the following:

1.  In the **Select resource(s)** section of your rule, select one of the following tabs:
    
      - **Standard** : In the **Standard** tab, select one or more resource types and then use the condition builder or the condition editor to create a condition.
        
        > **Important:** The condition builder and condition editor support a subset of CEL attributes. To create a condition with full attribute support, use the **Custom** tab in **Select resources** , or use the gcloud CLI or the IAP REST API.
    
      - **Custom** : In the **Custom** tab, you can use the condition editor to create a custom condition in which you can use CEL attributes to specify your destination resources and other conditions.

2.  To save the condition along with your rule, click **Save** .

### gcloud

In the policy file, conditions determine which destination resources your agent principals can access and under what conditions they are accessed.

Conditions are defined in the `conditions` field of a rule. For example:

```json
"conditions": {
  "iap.googleapis.com": {
    "expression": "destination.agent_registry.mcp_server.name == '/projects/my-project/locations/us-east1/mcpServers/finance-data-service' && destination.agent_registry.mcp_server.tool.name == 'getStatements'"
  }
}
```

For more information, see [Example policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#example-policies) .

### REST API

In the policy file, conditions determine which destination resources your agent principals can access and under what conditions they are accessed.

Conditions are defined in the `conditions` field of a rule. For example:

```json
"conditions": {
  "iap.googleapis.com": {
    "expression": "destination.agent_registry.mcp_server.name == '/projects/my-project/locations/us-east1/mcpServers/finance-data-service' && destination.agent_registry.mcp_server.tool.name == 'getStatements'"
  }
}
```

For more information, see [Example policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#example-policies) .

## Test and verify Access policies

After you create and bind your policies, verify that your agent can access the resources by doing the following:

1.  Trigger actions from your agents to test the rules in your Access policy. Make sure that you test that allow effect rules and deny effect rules perform as you expect.

2.  Inspect Cloud Audit Logs for IAP entries by filtering logs with the following query:
    
    ```text
    protoPayload.metadata.iapPolicyVersion="v2"
    protoPayload.serviceName="iap.googleapis.com"
    resource.labels.project_id="PROJECT_ID"
    ```
    
    Replace `  PROJECT_ID  ` with your project ID.
    
    The log entries display the access decision, principal, target, and CEL expression evaluation details. We recommend that, during testing, you use `DRY_RUN` mode so that policy violations don't block access.

3.  Adjust policy rules based on evaluation results in the audit logs.

4.  After you confirm that your rules operate as expected, update your gateway service extension metadata, and set `iamEnforcementMode` to `"ENFORCE"` .

## Example policies

The following are examples of egress policies for agent principal interactions:

  - [Agent to registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#agent-to-registry)
  - [Agent to agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#agent-to-agent)
  - [Agent to MCP server](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#agent-to-mcp-server)
  - [Agent to endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#agent-to-endpoint)
  - [Agent to unregistered endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#example-unregistered-endpoints)

For instructions on creating and binding policies, see [Create Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#create-ag-iam-policy) .

### Create an agent-to-registry Access policy

An agent-to-registry policy lets your agent access all of the agents, MCP servers, and endpoints in a specific Agent Registry location in a project.

### Console

To create an agent-to-registry policy in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In **Policy details** , select a policy or create a new one. If you're creating a new policy, enter a policy name—for example, `allow-registry-access` .

4.  In **Add Rules** , configure the rule:
    
      - **Rule description** : `Allow all agents in project to access us-central1 registry`
      - **Rule effect** : **Allow**
      - **Select principals** : In **Principal sets** , select **All agents in this project** .
      - **Select resource(s)** : Select **Standard** \> **Registry** , and select `us-central1` .

5.  To save the rule, click **Save** .

6.  To create the policy, click **Create** .

To learn how to create and bind policies, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#create-ag-iam-policy) .

### gcloud

The following example policy shows an Access policy rule that allows all agents in a project access to all destination resources in a specific registry:

```json
{
  [
    {
      "description": "Allow all agents in project 9876543210 to access all destination resources in the us-central1 registry",
      "effect": "ALLOW",
      "principals": [
        "principalSet://agents.global.org-123456789012.system.id.goog/attribute.platformContainer/aiplatform/projects/9876543210"
      ],
      "operation": {
        "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
      },
      "conditions": {
        "iap.googleapis.com": {
          "expression": "destination.is_registered == true && destination.agent_registry.location == 'us-central1'"
        }
      }
    }
  ]
}
```

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### REST API

To create an Access policy that allows all agents in a project access to all destination resources in a specific registry, do the following:

1.  Save the following to a JSON-formatted policy file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "Allow all agents in project 9876543210 to access all destination resources in the us-central1 registry",
            "effect": "ALLOW",
            "principals": [
              "principalSet://agents.global.org-123456789012.system.id.goog/attribute.platformContainer/aiplatform/projects/9876543210"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "destination.is_registered == true && destination.agent_registry.location == 'us-central1'"
              }
            }
          }
        ]
      }
    }
    ```

2.  To create the policy, run the following `curl` command:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

#### Agent-to-registry CEL attributes

The following table describes the CEL attributes that you can use in an agent-to-registry rule condition:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.is_registered</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code dir="ltr" translate="no">true</code> , <code dir="ltr" translate="no">false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.agent_registry.resource_type</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code dir="ltr" translate="no">'AGENT'</code> , <code dir="ltr" translate="no">'ENDPOINT'</code> , <code dir="ltr" translate="no">'MCP_SERVER'</code> , <code dir="ltr" translate="no">'SKILL'</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.location</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Google Cloud location ID (for example, <code dir="ltr" translate="no">'global'</code> , <code dir="ltr" translate="no">'us-central1'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.agent_registry.project_id</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Google Cloud project ID</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### Create an agent-to-agent egress Access policy

An agent-to-agent policy allows a source agent to invoke a target agent registered in Agent Registry.

### Console

To create an agent-to-agent policy in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In **Policy details** , select a policy or create a new one. If you're creating a new policy, enter a policy name—for example, `allow-orchestrator-to-support-agent` .

4.  In **Add Rules** , configure the rule:
    
      - **Rule description** : `Allow orchestrator agent to invoke customer-support agent`
      - **Rule effect** : **Allow**
      - **Select principals** : Select **Specific agents** , and select `orchestrator-agent` .
      - **Select resource(s)** : Select **Standard** \> **Agent** , and select `customer-support-agent` .

5.  To save the rule, click **Save** .

6.  To create the policy, click **Create** .

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### gcloud

The following example policy shows an IAM allow rule that allows an orchestrator agent to invoke a specific subagent registered in the Agent Registry:

```json
{
  [
    {
      "description": "Allow orchestrator agent to invoke customer-support agent",
      "effect": "ALLOW",
      "principals": [
        "principal://agents.global.org-123456789012.system.id.goog/resources/aiplatform/projects/9876543210/locations/us-central1/reasoningEngines/orchestrator-agent"
      ],
      "operation": {
        "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
      },
      "conditions": {
        "iap.googleapis.com": {
          "expression": "destination.agent_registry.agent.name == '/projects/9876543210/locations/us-central1/agents/customer-support-agent'"
        }
      }
    }
  ]
}
```

To create and bind the policy by using the gcloud CLI, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#create-ag-iam-policy) .

### REST API

To create an IAM policy with an allow rule that allows an orchestrator agent to invoke a specific subagent registered in the Agent Registry, do the following:

1.  Save the following to a JSON-formatted policy file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "Allow orchestrator agent to invoke customer-support agent",
            "effect": "ALLOW",
            "principals": [
              "principal://agents.global.org-123456789012.system.id.goog/resources/aiplatform/projects/9876543210/locations/us-central1/reasoningEngines/orchestrator-agent"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "destination.agent_registry.agent.name == '/projects/9876543210/locations/us-central1/agents/customer-support-agent'"
              }
            }
          }
        ]
      }
    }
    ```

2.  To create the policy, run the following `curl` command:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

#### Agent-to-agent CEL attributes

The following table describes the CEL attributes that you can use in an agent-to-agent policy condition:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.agent.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Agent resource name ( <code dir="ltr" translate="no">projects/             PROJECT_ID            /locations/             LOCATION            /agents/             AGENT_NAME           </code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### Create an agent-to-MCP server egress Access policy

An agent-to-MCP server egress policy controls access from an agent to specific tools or annotations on a Model Context Protocol (MCP) server.

### Console

To create an agent-to-MCP server policy in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In **Policy details** , select a policy or create a new one. If you're creating a new policy, enter a policy name—for example, `allow-github-read-only` .

4.  In **Add Rules** , configure the rule:
    
      - **Rule description** : `Allow read-only access to GitHubTool on MCP server`
    
      - **Rule effect** : **Allow**
    
      - **Select principals** : Select the agent principal—for example, `my-ae-agent` .
    
      - **Select resource(s)** : Select the **Custom** tab.
    
      - **Conditions** : In the condition editor, enter:
        
        ```text
        destination.agent_registry.mcp_server.tool.name == 'GitHubTool' && destination.agent_registry.mcp_server.tool.annotations.read_only_hint == true
        ```

5.  To save the rule, click **Save** .

6.  To create the policy, click **Create** .

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### gcloud

The following example policy shows an IAM allow rule that allows a Workload Identity Federation-formatted agent principal read-only access to a tool called `GitHubTool` :

```json
{
  [
    {
      "description": "Allow read-only access to GitHubTool on MCP server",
      "effect": "ALLOW",
      "principals": [
        "principal://iam.googleapis.com/projects/9876543210/locations/global/workloadIdentityPools/POOL_ID/subject/ns/default/sa/my-ae-agent"
      ],
      "operation": {
        "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
      },
      "conditions": {
        "iap.googleapis.com": {
          "expression": "destination.agent_registry.mcp_server.tool.name == 'GitHubTool' && destination.agent_registry.mcp_server.tool.annotations.read_only_hint == true"
        }
      }
    }
  ]
}
```

Replace the following:

  - `  POOL_ID  ` : the workload identity pool ID. Depending on your pool type, format the ID as follows:
  - **Google-managed pool:** `  PROJECT_ID .svc.id.goog `
  - **Self-managed pool:** `  POOL_NAME .global. POOL_HOST_PROJECT_NUMBER .workload.id.goog `

To create and bind the policy by using the gcloud CLI, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#create-ag-iam-policy) .

### REST API

To create an IAM Access policy that allows an agent using Workload Identity Federation read-only access to a tool called `GitHubTool` , do the following:

1.  Save the following to a JSON-formatted policy file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "Allow read-only access to GitHubTool on MCP server",
            "effect": "ALLOW",
            "principals": [
              "principal://iam.googleapis.com/projects/9876543210/locations/global/workloadIdentityPools/POOL_ID/subject/ns/default/sa/my-ae-agent"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "destination.agent_registry.mcp_server.tool.name == 'GitHubTool' && destination.agent_registry.mcp_server.tool.annotations.read_only_hint == true"
              }
            }
          }
        ]
      }
    }
    ```

2.  To create the policy, run the following `curl` command:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  POOL_ID  ` : the workload identity pool ID. Depending on your pool type, format the ID as follows:
      - **Google-managed pool:** `  PROJECT_ID .svc.id.goog `
      - **Self-managed pool:** `  POOL_NAME .global. POOL_HOST_PROJECT_NUMBER .workload.id.goog `
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

To create and bind the policy by using the REST API, see [Create Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#create-ag-iam-policy) .

#### Agent-to-MCP CEL attributes

The following table describes the CEL attributes that you can use in an agent-to-MCP server policy condition:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>MCP server resource name ( <code dir="ltr" translate="no">projects/             PROJECT_ID            /locations/             LOCATION            /mcpServers/             MCP_SERVER_NAME           </code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.method</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>MCP method name (for example, <code dir="ltr" translate="no">'tools'</code> , <code dir="ltr" translate="no">'prompts'</code> , <code dir="ltr" translate="no">'resources'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.tool.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Tool name (for example, <code dir="ltr" translate="no">'search_code'</code> , <code dir="ltr" translate="no">'execute'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.tool.annotations.read_only_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code dir="ltr" translate="no">true</code> , <code dir="ltr" translate="no">false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.tool.annotations.destructive_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code dir="ltr" translate="no">true</code> , <code dir="ltr" translate="no">false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.tool.annotations.idempotent_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code dir="ltr" translate="no">true</code> , <code dir="ltr" translate="no">false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.tool.annotations.open_world_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code dir="ltr" translate="no">true</code> , <code dir="ltr" translate="no">false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.prompt.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Prompt name</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.mcp_server.resource.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Resource name</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### Create an agent-to-endpoint egress Access policy

An agent-to-endpoint egress policy allows an agent to access a registered service endpoint in Agent Registry.

### Console

To create an agent-to-endpoint policy in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In **Policy details** , select a policy or create a new one. If you're creating a new policy, enter a policy name—for example, `allow-translator-to-endpoint` .

4.  In **Add Rules** , configure the rule:
    
      - **Rule description** : `Allow translator agent to access translation endpoint`
    
      - **Rule effect** : **Allow**
    
      - **Select principals** : Select **Specific agents** , and select `translator-agent` .
    
      - **Select resource(s)** : Select the **Custom** tab.
    
      - **Conditions** : In the condition editor, enter:
        
        ```text
        destination.agent_registry.endpoint.name == '/projects/9876543210/locations/us-central1/endpoints/translation-service'
        ```

5.  To save the rule, click **Save** .

6.  To create the policy, click **Create** .

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### gcloud

The following example shows an IAM allow policy that allows an agent to access a registered service endpoint:

```json
[
  {
    "description": "Allow translator agent access to registered translation endpoint",
    "effect": "ALLOW",
    "principals": [
      "principal://agents.global.org-123456789012.system.id.goog/resources/aiplatform/projects/9876543210/locations/us-central1/reasoningEngines/translator-agent"
    ],
    "operation": {
      "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
    },
    "conditions": {
      "iap.googleapis.com": {
        "expression": "destination.agent_registry.endpoint.name == '/projects/9876543210/locations/us-central1/endpoints/translation-service'"
      }
    }
  }
]
```

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### REST API

To create an IAM allow policy that allows an agent to access a registered service endpoint, do the following:

1.  Save the following to a JSON-formatted policy file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "Allow translator agent access to registered translation endpoint",
            "effect": "ALLOW",
            "principals": [
              "principal://agents.global.org-123456789012.system.id.goog/resources/aiplatform/projects/9876543210/locations/us-central1/reasoningEngines/translator-agent"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "destination.agent_registry.endpoint.name == '/projects/9876543210/locations/us-central1/endpoints/translation-service'"
              }
            }
          }
        ]
      }
    }
    ```

2.  To create the policy, run the following `curl` command:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

#### Agent-to-endpoint CEL attributes

The following table describes the CEL attributes that you can use in an agent-to-endpoint policy condition:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.agent_registry.endpoint.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Endpoint resource name ( <code dir="ltr" translate="no">projects/             PROJECT_ID            /locations/             LOCATION            /endpoints/             ENDPOINT_NAME           </code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

### Create an agent-to-unregistered endpoint Access policy

An agent-to-unregistered endpoint policy allows an agent to access external, third-party APIs and endpoints that aren't registered in Agent Registry.

### Console

To create an agent-to-unregistered endpoint policy in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Policies** page:

2.  In the project selector, select the project that contains the agent gateways that will use the Access policy.

3.  In **Policy details** , select a policy or create a new one. If you're creating a new policy, enter a policy name—for example, `allow-ocr-api-access` .

4.  In **Add Rules** , configure the rule:
    
      - **Rule description** : `Allow POST access to external OCR service`
    
      - **Rule effect** : **Allow**
    
      - **Select principals** : Select the agent principal (for example, `my-ae-agent` ).
    
      - **Select resource(s)** : Select **Standard** \> **Unregistered endpoint** .
    
      - **Conditions** : Click the **Custom** tab.
    
      - In the condition editor, enter:
        
        ```text
        destination.unregistered.host.endsWith('example-ocr.com') && destination.unregistered.path.startsWith('/v2/process') && destination.unregistered.method == 'POST'
        ```

5.  To save the rule, click **Save** .

6.  To create the policy, click **Create** .

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### gcloud

The following example shows an Access policy that allows an agent to access an unregistered endpoint with a path that starts with `/v2/process` and ends with `example-ocr.com` :

```json
[
  {
    "description": "Allow POST access to unregistered OCR endpoint",
    "effect": "ALLOW",
    "principals": [
      "principal://iam.googleapis.com/projects/9876543210/locations/global/workloadIdentityPools/POOL_ID/subject/ns/default/sa/my-ae-agent"
    ],
    "operation": {
      "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
    },
    "conditions": {
      "iap.googleapis.com": {
        "expression": "destination.unregistered.host.endsWith('example-ocr.com') && destination.unregistered.path.startsWith('/v2/process') && destination.unregistered.method == 'POST'"
      }
    }
  }
]
```

Replace the following:

  - `  POOL_ID  ` : the workload identity pool ID. Depending on your pool type, format the ID as follows:
  - **Google-managed pool:** `  PROJECT_ID .svc.id.goog `
  - **Self-managed pool:** `  POOL_NAME .global. POOL_HOST_PROJECT_NUMBER .workload.id.goog `

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

### REST API

To create an Access policy that allows an agent to access an unregistered endpoint with a path that starts with `/v2/process` and ends with `example-ocr.com` , do the following:

1.  Save the following to a JSON-formatted policy file named `agent-access-policy.json` :
    
    ```json
    {
      "details": {
        "rules": [
          {
            "description": "Allow POST access to unregistered OCR endpoint",
            "effect": "ALLOW",
            "principals": [
              "principal://iam.googleapis.com/projects/9876543210/locations/global/workloadIdentityPools/POOL_ID/subject/ns/default/sa/my-ae-agent"
            ],
            "operation": {
              "permissions": ["iap.googleapis.com/resources.egressViaIAP"]
            },
            "conditions": {
              "iap.googleapis.com": {
                "expression": "destination.unregistered.host.endsWith('example-ocr.com') && destination.unregistered.path.startsWith('/v2/process') && destination.unregistered.method == 'POST'"
              }
            }
          }
        ]
      }
    }
    ```

2.  To create the policy, run the following `curl` command:
    
    ```sh
    curl -X POST \
    "https://iam.googleapis.com/v3beta/projects/PROJECT_ID/locations/global/accessPolicies?accessPolicyId=POLICY_NAME" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d @agent-access-policy.json
    ```
    
    Replace the following:
    
      - `  POOL_ID  ` : the workload identity pool ID. Depending on your pool type, format the ID as follows:
      - **Google-managed pool:** `  PROJECT_ID .svc.id.goog `
      - **Self-managed pool:** `  POOL_NAME .global. POOL_HOST_PROJECT_NUMBER .workload.id.goog `
      - `  PROJECT_ID  ` : the project ID
      - `  POLICY_NAME  ` : the policy name

To activate the policy, [bind the Access policy to your project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap#bind-uap) .

#### Agent-to-unregistered endpoint CEL attributes

The following table describes the CEL attributes that you can use in an agent-to-unregistered endpoint policy condition:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.unregistered.host</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Hostname (for example, <code dir="ltr" translate="no">'google.com'</code> , <code dir="ltr" translate="no">'example.com'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code> , <code dir="ltr" translate="no">.startsWith()</code> , <code dir="ltr" translate="no">.endsWith()</code> , <code dir="ltr" translate="no">.contains()</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">destination.unregistered.path</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Request path (for example, <code dir="ltr" translate="no">'/admin'</code> , <code dir="ltr" translate="no">'/api/v1'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code> , <code dir="ltr" translate="no">.startsWith()</code> , <code dir="ltr" translate="no">.endsWith()</code> , <code dir="ltr" translate="no">.contains()</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">destination.unregistered.method</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>HTTP method (for example, <code dir="ltr" translate="no">'get'</code> , <code dir="ltr" translate="no">'post'</code> , <code dir="ltr" translate="no">'put'</code> , <code dir="ltr" translate="no">'delete'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code dir="ltr" translate="no">==</code> , <code dir="ltr" translate="no">!=</code> , <code dir="ltr" translate="no">in</code></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

> **Note:** The `startsWith()` , `endsWith()` , and `contains()` functions (or `STARTS_WITH` , `ENDS_WITH` , and `CONTAINS` ) are supported only for the `destination.unregistered.host` and `destination.unregistered.path` attributes. Other attributes don't support these string functions.

## What's next

  - [CEL attributes for Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap)
  - [Manage IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap)
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
