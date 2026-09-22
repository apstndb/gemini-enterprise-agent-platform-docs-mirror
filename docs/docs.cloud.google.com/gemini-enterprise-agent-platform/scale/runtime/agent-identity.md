---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity
title: Use Agent Identity with Agent Runtime
description: Learn how to use Agent Identity on Agent Runtime to provide secure, least-privilege resource access for your agents.
data_source: docs.cloud.google.com
---

Using agent identity on Agent Runtime provides a secure, per-agent identity that enables a least-privilege approach to access management. This document explains how to create agents with agent identities, authorize access to Google Cloud APIs, and manage credentials for third-party services.

## Overview

Agent identity provides a per-agent identity that enables a least-privilege approach and is tied to the lifecycle of the agent, making agent identity a more secure principal than service accounts. Existing access management controls through IAM support agent identity to enable strong governance.

Agent identity credentials are secured by default through a Google-managed Context-Aware Access (CAA) policy. This policy enforces [mTLS binding](https://cloud.google.com/blog/products/identity-security/how-to-prevent-account-takeovers-with-new-certificate-based-access?e=48754805) to ensure that the agent's credentials in the form of [certificate-bound tokens](https://datatracker.ietf.org/doc/html/rfc8705) can only be used from their intended, trusted runtime environment (for example, a Cloud Run container). This security baseline makes stolen credentials un-replayable, protecting against Credential Theft and Account Takeover (ATO).

This page covers the following topics:

  - [**Creating an agent with agent identity**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#create-agent-identity) : Create an agent such that the agent automatically receives a unique identity when you deploy to Agent Runtime.

  - [**Authorize access to Google Cloud APIs using agent identity**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#google-cloud-agent-identity) : Use the provisioned agent identity to grant or deny the agent access to Google Cloud's first party tools, APIs, and resources. This also includes access to other agents hosted on Agent Runtime using [Agent2Agent (A2A) Protocol](https://a2a-protocol.org/latest/) .

  - [**Log agent activity**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#log-agent-activity) : View agent identity in logs across Google Cloud services. For user-delegated flows, logs show both the user identity and the agent identity.

  - [**List agents and agent identity**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#list-agents-identities) : View the list of your agents and their identities in Agent Runtime.

  - [**Opt out of Context-Aware Access**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#opt-out-caa) (not recommended): Opt out of the default Context-Aware Access (CAA) policy.

### Limitations

Agent identities cannot be granted Legacy Bucket roles ( `storage.legacyBucketReader` , `storage.legacyBucketWriter` , or `storage.legacyBucketOwner` ) on Cloud Storage buckets.

## Create an agent with agent identity

You can provision agents you deploy to Agent Runtime with a unique identity upon creating your Agent Runtime instance. The identity is tied to the Agent Runtime's agent resource ID and is independent of the agent framework you used to develop the agent.

You have the following options when creating an agent identity:

  - **Create an Agent Runtime instance without deploying agent code** : If you want to set up IAM policies before deploying the agent, you can create an agent identity without deploying your agent code. To do so, create an Agent Runtime instance with just the `identity_type` field:
    
        import agentplatform
        from agentplatform import types
        
        client = agentplatform.Client(
          project=PROJECT_ID,
          location=LOCATION,
          http_options=dict(api_version="v1beta1")
        )
        remote_app = client.runtimes.create(
          config={
            "display_name": "identity-for-agent",
            "identity_type": types.IdentityType.AGENT_IDENTITY,
          },
        )
    
    Once you create the Agent Runtime instance with the agent identity, you can add agent code using [`client.runtimes.update(...)`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#update) .

  - **Create an Agent Runtime instance while deploying agent code** : If you want to provision the agent identity while deploying your agent code, use the Agent Platform SDK for Python and the `identity_type=AGENT_IDENTITY` flag.
    
    Define the agent in your preferred framework:
    
        from google.adk.agents import Agent
        
        agent = Agent(
            model="gemini-2.5-flash",
            name="minimal_agent",
            instruction="You are a helpful assistant.",
        )
    
    Then, deploy it:
    
        import agentplatform
        from agentplatform import types
        from agentplatform.frameworks import AdkApp
        
        # Initialize the Agent Platform client with v1beta1 API for agent identity support
        client = agentplatform.Client(
          project=PROJECT_ID,
          location=LOCATION,
          http_options=dict(api_version="v1beta1")
        )
        
        # Use the proper wrapper class for your Agent Framework
        app = AdkApp(agent=agent)
        
        # Deploy the agent with Agent Identity
        remote_app = client.runtimes.create(
          agent=app,
          config={
            "display_name": "running-agent-with-identity",
            "identity_type": types.IdentityType.AGENT_IDENTITY,
            "requirements": ["google-cloud-agentplatform[adk,runtimes]"],
            "staging_bucket": f"gs://"BUCKET_NAME",
          },
        )
        
        print(f"Effective Identity: {remote_app.api_resource.spec.effective_identity}")
    
    where BUCKET\_NAME is the name of your Cloud Storage bucket.

  - **Deploy agents by using the Agents CLI** : The [Agents CLI](https://google.github.io/agents-cli/) is ideal for learners, prototyping, and rapid testing, as it offers a quick deployment solution with foundational resources for monitoring. The following command deploys your agent:
    
        agents-cli deploy --agent-identity

  - **Deploy agents with Agent Identity using ADK deploy** : [Setup your agent with ADK](https://adk.dev/deploy/agent-engine/deploy/) . Before you run `adk deploy` , run the following commands in your agent's folder to add a config file with agent identity.
    
        # Create the file
        $ touch .agent_engine_config.json
        
        # Update the file to specify that you're using Agent Identity
        $ echo '{ "identity_type": "AGENT_IDENTITY" }' > .agent_engine_config.json

The Agent Runtime instance is created with a read-only, system attested agent identity (a [principal identifier](https://docs.cloud.google.com/iam/docs/principal-identifiers) ):

    # Agent identity Format
    principal://TRUST_DOMAIN/NAMESPACE/AGENT_NAME
    
    # Example agent identity
    principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID

The following parts are auto-provisioned to you as part of agent identity:

  - TRUST\_DOMAIN : A trust domain is provisioned for you when you enable the Agent Platform API:
    
      - If you have an organization, the trust domain is created at the organization level with the format `agents.global.org- ORGANIZATION_ID .system.id.goog` .
    
      - If your project doesn't have an organization, a trust domain is created at the project level with the format `agents.global.proj- PROJECT_NUMBER .system.id.goog` .

  - NAMESPACE : The agent's immutable resource path.

  - AGENT\_NAME : The immutable `agent-reasoning-engine-id` .

Agent identity is based on [SPIFFE](https://spiffe.io/docs/latest/spiffe-about/spiffe-concepts/) . We also auto-provision and manage an x509 certificate on the agent with the same identity for secure authentication. By default, the agent gets access to its own logging, metrics, model access, sessions, memories, and sandboxes ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

Agent identities come with a default `roles/aiplatform.agentContextEditor` and `roles/aiplatform.agentDefaultAccess` roles so that agents have basic permissions to operate.

You can [view the identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#list-agents-identities) through the Agent Runtime Google Cloud console and API.

> **Note:** If the identity flag isn't configured, the Agent Runtime instance continues to use service accounts. This ensures backward compatibility if you already implemented Infrastructure-as-Code-based deployments on your agents.

## Access Google Cloud APIs and services using agent identity

Once you create an agent with agent identity, you can grant or deny the agent access to Google Cloud APIs and services using the following IAM policies:

  - **Allow policies** : Grant an agent access to a Google Cloud resource.

  - **Deny policies** : Deny an agent access to a Google Cloud resource.

### Grant access to an agent

Grant IAM permissions to the agent identity. We recommend the following roles:

  - `roles/aiplatform.expressUser` : Grant access to running inference, sessions, and memory.

  - `roles/serviceusage.serviceUsageConsumer` : Grant the agent permission to use the project's quota and the Agent Platform SDK.

  - `roles/browser` : Grant access to basic Google Cloud functionalities.

Additional permissions might be needed if you use logging, metrics, and Cloud API registry, and for any other resource you want to expose to your agent. See later for more examples.

Create an [IAM allow policy](https://docs.cloud.google.com/iam/docs/allow-policies) to grant an agent an IAM role:

``` 
  # Example: Grant the agent access to vision API.
  gcloud RESOURCE_TYPE add-iam-policy-binding RESOURCE_ID \
  --member="principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID" \
  --role="ROLE_NAME" \
```

Replace the following:

  - RESOURCE\_TYPE : The type of resource (for example, `projects` or `organizations` ).

  - RESOURCE\_ID : The ID of the resource to which you want to grant access.

  - ORGANIZATION\_ID : The ID for your organization.

  - PROJECT\_NUMBER : Your project number.

  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations#supported-regions-agent-engine) for Runtime.

  - AGENT\_ENGINE\_ID : The resource ID of your Agent Runtime instance.

  - ROLE\_NAME is the name of the role that you want to grant. For example, `roles/vision.user` . For a list of predefined roles, see [Understanding roles](https://docs.cloud.google.com/iam/docs/understanding-roles) .

Once IAM is configured, the Agent Platform SDK's [Application Default Credentials](https://docs.cloud.google.com/docs/authentication/application-default-credentials) automatically uses the agent identity to perform authentication to Google Cloud resources.

### Grant access for Agent-to-Agent (A2A) delegation

When you design a multi-agent system where a parent agent invokes a remote subagent registered in [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) , the parent agent's identity must have permissions to discover the subagent in Agent Registry and to invoke its endpoint.

To ensure that the parent agent's identity has the necessary permissions to discover and invoke a remote subagent, ask your administrator to grant the following IAM roles to the parent agent's identity:

> **Important:** You must grant these roles to the parent agent's identity, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

  - Let the parent agent look up the subagent's endpoint at runtime: [Agent Registry API Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/agentregistry#agentregistry.viewer) ( `roles/agentregistry.viewer` ) on the parent project or registry resource
  - Let the parent agent send messages to the subagent: [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) on the target subagent's reasoning engine resource

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give the parent agent's identity the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For example, to grant the `roles/agentregistry.viewer` role on the project, you can use the following Google Cloud CLI command:

    gcloud projects add-iam-policy-binding PROJECT_NUMBER \
        --member="principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/PARENT_AGENT_ENGINE_ID" \
        --role="roles/agentregistry.viewer"

Replace the following:

  - `  ORGANIZATION_ID  ` : The ID for your organization.
  - `  PROJECT_NUMBER  ` : Your project number.
  - `  LOCATION  ` : The region where your parent agent is deployed.
  - `  PARENT_AGENT_ENGINE_ID  ` : The resource ID of your parent agent's Agent Runtime instance.

### Grant access to multiple agents

You can grant an IAM role to all Agent Runtime agents in a particular project or across an entire organization.

To grant a role to all Agent Runtime agents in a project, use one of the following commands.

If your project belongs to an organization:

    # Grant all agents in a project the following role
    gcloud RESOURCE_TYPE add-iam-policy-binding RESOURCE_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role="ROLE_NAME"

If your project does not belong to an organization:

    # Grant all agents in an orgless project the following role
    gcloud RESOURCE_TYPE add-iam-policy-binding RESOURCE_ID \
    --member="principalSet://agents.global.proj-PROJECT_NUMBER.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role="ROLE_NAME"

It can be easier to grant common permissions such as quota, logging, or access to models to all agents in the project to simplify deployments. Then grant specific narrow permissions to individual agents for more sensitive permissions such as access to data. Granting such permissions is possible at any time after the first usage of the agent identity feature within an organization or project, so it can be performed before the deployment of the agent.

For example, the following commands grant basic roles to all agents in a project:

    gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role=roles/serviceusage.serviceUsageConsumer
    
    gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role=roles/browser
    
    gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role=roles/aiplatform.expressUser
    
    gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role=roles/cloudapiregistry.viewer
    
    gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role=roles/logging.logWriter
    
    gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platformContainer/aiplatform/projects/PROJECT_NUMBER" \
    --role=roles/monitoring.metricWriter

To grant a role to all Agent Runtime agents across an organization:

    # Grant all agents in an organization the following role
    gcloud RESOURCE_TYPE add-iam-policy-binding RESOURCE_ID \
    --member="principalSet://agents.global.org-ORGANIZATION_ID.system.id.goog/attribute.platform/aiplatform" \
    --role="ROLE_NAME"

### Deny access to an agent

To deny an agent access to resources, you can use the [IAM deny policy](https://docs.cloud.google.com/iam/docs/deny-overview) or set up a [principal access boundary policy](https://docs.cloud.google.com/iam/docs/principal-access-boundary-policies) .

  - Deny the agent access to certain resources using the IAM deny policy.
    
        // Deny policy (deny all agents across the org from ability to create or delete buckets)
        
        {
        "displayName": "Deny access to bucket for all agent identities in the org",
        "rules": [
          {
            "denyRule": {
              "deniedPrincipals": [
                "principalSet://<org.id>.global.agent.id.goog/*"
              ],
              "deniedPermissions": [
                "iam.googleapis.com/roles.create",
                "storage.googleapis.com/buckets.delete"
              ]
            }
          }
        ]
        }

  - Set up Principal Access Boundary to limit the resources that the agent may access, despite other permissions that the agent might have:
    
        // PAB Policy (Only allow agents to operate within resource boundary)
        
        {
            "name":"organizations/ORGANIZATION_ID/locations/global/principalAccessBoundaryPolicies/example-policy",
            "details": {
            "rules": [
              {
                "description": "Restrict agent identity inside a folder",
                "resources": [
                  "//cloudresourcemanager.googleapis.com/folder/0123456789012"
                ],
                "effect": "ALLOW"
              }
            ],
          }
        }
        
        // Bind PAB policy to all identities in the organization (incl agent id)
        
        gcloud iam principal-access-boundary-policies bindings create example-pab-binding \
              --organization=organizations/ORGANIZATION_ID \
              --policy=example-policy \ --target-principal-set=cloudresourcemanager.googleapis.com/organizations/ORGANIZATION_ID

## CI/CD and automation guidance

Automated deployment pipelines that delete and re-create agents (such as blue-green deployments, ephemeral testing environments, or Terraform workflows) can experience silent runtime access loss. Because each redeployment creates a new `reasoningEngines` resource with a unique ID, the agent receives a new principal identifier. Any prior IAM permissions granted to the previous principal are not inherited by the new principal.

To manage permissions in automated pipelines, use the following strategies:

  - **Retrieve the new principal ID dynamically:** Capture the `spec.effectiveIdentity` value from the deployment response, or query the REST API after deployment to obtain the active identity of the agent. Apply the required IAM bindings to this new principal as a post-deployment step.
    
    For example, you can query the active identity with `gcloud` by using the following command:
    
        gcloud ai reasoning-engines describe RESOURCE_ID \
          --project=PROJECT_ID \
          --location=LOCATION \
          --format="value(spec.effectiveIdentity)"
    
    In Terraform, you can dynamically construct the agent identity principal from the deployed `google_vertex_ai_reasoning_engine` resource ID and reference it in IAM bindings:
    
        resource "google_vertex_ai_reasoning_engine" "reasoning_engine" {
          provider = google-beta
        
          project      = var.project_id
          region       = var.region
          display_name = var.display_name
          description  = var.agent_description
        
          spec {
            agent_framework = "google-adk"
            identity_type   = "AGENT_IDENTITY"
        
            source_code_spec {
              inline_source {
                source_archive = filebase64(data.archive_file.agent_tarball.output_path)
              }
        
              python_spec {
                entrypoint_module = var.agent_python_spec.entrypoint_module
                entrypoint_object = var.agent_python_spec.entrypoint_object
                requirements_file = var.agent_python_spec.requirements_path
                version           = var.agent_python_spec.version
              }
            }
        
            deployment_spec {
              env {
                name  = "GOOGLE_CLOUD_AGENT_ENGINE_ENABLE_TELEMETRY"
                value = "true"
              }
        
              env {
                name  = "OTEL_INSTRUMENTATION_GENAI_CAPTURE_MESSAGE_CONTENT"
                value = "true"
              }
            }
          }
        }
        
        locals {
          agent_resource_id        = element(split("/", google_vertex_ai_reasoning_engine.reasoning_engine.id), -1)
          agent_identity_principal = "principal://agents.global.org-${data.google_organization.org.org_id}.system.id.goog/resources/aiplatform/projects/${data.google_project.project.number}/locations/${var.region}/reasoningEngines/${local.agent_resource_id}"
        }

  - **Use project-scoped `principalSets` for baseline permissions:** Because `principalSet` bindings target all agents in a project, they survive agent deletion and re-creation. Grant common, non-sensitive roles (such as service usage, logging, and general model inference) to the project-wide `principalSet` instead of individual agent principals. Limit individual `principal://` bindings to highly sensitive data sources.

## Log agent activity

If you enable Cloud Logging, you can [view logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/logging#query-logs) of which agent and users have accessed a Google Cloud resource.

  - When the agent acts on a user's behalf, the logs show both the agent's and user's identities.

  - When the agent is acting on its own authority, the logs only show the agent's identity.

## List agents and their identities

You can see the list of your agent identities in Agent Runtime using the Google Cloud console and command line.

### Console

1.  In the Google Cloud console, go to the Agent Platform **Deployments** page.  
    
    Deployed agents that are part of the selected project appear in the list. You can use the **Filter** field to filter the list by your specified column.

2.  For each agent, agent identity is listed under the **Identity** column.

### REST API

You can retrieve the agent identity when [getting an Agent Runtime instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#get) using the REST API.

The response includes the agent identity in the following format:

    {
      ...
      spec: {
        "effectiveIdentity": "agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID"
      }
      ...
    }

For Agent Runtime instances not using agent identity, the `effectiveIdentity` field contains the service agent or service account name associated with the Agent Runtime instance.

## Opt out of Context-Aware Access (CAA)

By default, attempting to use an access token outside of its intended Agent Runtime runtime results in the following error:

    Error Code: "401"
    Error Details: "Context-Aware Access requirements are not met"

For corner cases, such as specific token sharing requirements among agents, you can opt out of the default CAA policy. This action is strongly discouraged, as it leaves an agent vulnerable to credential theft.

Opt out of the default Context-Aware Access (CAA) policy by setting the following [environment variable](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#environment-variables) when you [create your Agent Runtime instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#create-agent-identity) :

    config={
      "env_vars": {
        "GOOGLE_API_PREVENT_AGENT_TOKEN_SHARING_FOR_GCP_SERVICES": False,
      }
    }

## What's next

Guide

### [Manage deployed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents)

Learn how to manage agents that have been deployed to the Agent Platform managed runtime.

Guide

### [Use an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent)

Use an agent with Agent Platform Runtime.
