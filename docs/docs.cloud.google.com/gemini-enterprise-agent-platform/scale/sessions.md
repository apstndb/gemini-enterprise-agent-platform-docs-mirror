---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions
title: Agent Platform Sessions overview
description: Manage agent interaction history, conversation context, and long-term memory with Agent Platform Sessions via Agent Development Kit (ADK) or API.
data_source: docs.cloud.google.com
---

Agent Platform Sessions maintains the history of interactions between a user and agents. Sessions provides definitive sources for long-term memory and conversation context.

You have several options to use Agent Platform Sessions:

- [Agent Development Kit (ADK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-adk) : Once you deploy your ADK agent to Gemini Enterprise Agent Platform, session management is handled automatically.

- [API calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-api) : You can make direct API calls to Agent Platform Sessions if you don't want to manage sessions using an ADK agent.

## Core concepts

- **Session** : A session represents the chronological sequence of messages and actions (events) for a single, ongoing interaction between a user and your agent system.

- **Event** : An event stores the content of the conversation, as well as the actions taken by the agents such as function calls. Events support a flexible schema to accommodate custom data and different frameworks.

- **State** : A state holds temporary data relevant only during the current conversation.

- **Memory** : Memory is personalized information that can be accessed across multiple sessions for a particular user. The agent can use memories to personalize responses to the user and ensure cross-session continuity.

## Core functionalities

The core functionalities of Agent Platform Sessions include the following:

- **Starting new conversations** : Create new sessions when a user begins an interaction with an agent.

- **Resuming existing conversations** : Retrieving a specific session so the agent can resume a conversation that has been paused.

- **Saving progress** : Append new interactions (events) to a session's history to update the session.

- **Listing conversations** : Find the active session threads for a particular user and application.

- **Cleaning up** : Delete session objects and their associated data when conversations are finished or no longer needed.

## Enterprise security and governance

Agent Platform Sessions supports enterprise security controls to help you protect conversation history, session state, and events from unauthorized access or data exfiltration.

### VPC Service Controls (VPC Service Controls)

Agent Platform Sessions supports [VPC Service Controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) to mitigate the risk of data exfiltration for your session data and conversation events. Because `sessions` and `events` are child resources of an Agent Runtime ( `reasoningEngines` ) instance served through the Agent Platform API ( `aiplatform.googleapis.com` ), adding Agent Platform API to a VPC Service Controls service perimeter protects all session operations ( `CreateSession` , `GetSession` , `ListSessions` , `UpdateSession` , `DeleteSession` , `AppendEvent` , and `ListEvents` ).

When configuring VPC Service Controls for Sessions, follow these guidelines:

- **Perimeter configuration** : Add the Agent Platform API ( `aiplatform.googleapis.com` ) to your VPC Service Controls service perimeter. Ensure that your project is added to the service perimeter before you create the parent Agent Runtime instance that hosts your sessions.
- **Private endpoint connectivity** : Route requests to `LOCATION `` -aiplatform.googleapis.com` (or `aiplatform.googleapis.com` for global endpoints) from your VPC network through `restricted.googleapis.com` ( `199.36.153.4/30` ) or an internal Private Service Connect endpoint for Google APIs.
- **Using Sessions with Agent Gateway in a service perimeter** : When an agent deployed on Agent Runtime is bound to an enforcing Agent Gateway in Agent-to-Anywhere (egress) mode, outbound API calls from your agent to Sessions traverse the gateway. To avoid perimeter or gateway blocks:
  - Configure the gateway using an agent connectivity template ( `AgentConnectivityTemplate` ) with `vpcEgress` set to `ALL_TRAFFIC` and private Cloud DNS peering for `googleapis.com.` . For details, see [VPC Service Controls compliance for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#vpc-sc-compliance) .
  - Register and allowlist the regional and mTLS `Agent Platform API` endpoints in Agent Registry so your agent can call the Sessions endpoint ( `https:// `` LOCATION `` -aiplatform.googleapis.com/ `` API_VERSION `` /projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /reasoningEngines/ `` RESOURCE_ID `` /sessions` ), and grant your agent identity the IAP Egressor ( `roles/iap.egressor` ) role. For step-by-step instructions, see [Route Agent Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy#allowlist-essential-apis) .

### Customer-managed encryption keys (CMEK)

By default, Google Cloud encrypts session state and conversation events at rest using Google-owned and Google-managed encryption keys. To protect your session data using keys that you manage in Cloud Key Management Service (Cloud KMS), specify the `encryption_spec` ( `kms_key_name` ) when you create the parent Agent Runtime instance. All sessions and events stored under that instance inherit its CMEK configuration. For general project and key setup steps, see [CMEK for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) .

The following limitations apply when using CMEK with Sessions:

- **Global endpoint and deployed runtime restrictions** : You can't use CMEK when Sessions is configured to use the `global` endpoint ( `location="global"` ), because Cloud Key Management Service requires encryption keys to reside within a geographic data residency boundary. To use CMEK, create a standalone parent instance (without deploying agent runtime code) in a [supported regional or multi-regional location](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) with a matching Cloud KMS key (for multi-regional instances, use a `us` key for `us` or a `europe` key for `eu` ). If the parent instance also deploys an agent on Agent Runtime, you must use a single-region location, because deployed runtimes don't support CMEK on multi-regional endpoints ( `us` or `eu` ).
- **Encryption key can't be updated** : Once an instance is created with a Cloud KMS key, you can't change the key for that instance. To use a different key, you must create a new instance.

## What's next

- [Manage sessions using ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-adk) .
- [Manage sessions using API calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-api) .
- [Control access to Agent Platform Sessions with IAM Conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/iam-conditions) .
