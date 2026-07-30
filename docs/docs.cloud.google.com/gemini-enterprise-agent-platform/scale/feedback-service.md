---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service
title: Feedback service overview
description: Collect, manage, and trace user qualitative feedback alongside system events and telemetry.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The Agent Platform Feedback service enables you to collect and analyze user feedback from interactions with your agents. It provides the necessary infrastructure, eliminating the need to maintain your own feedback database. The service stores user reactions and links them to the corresponding conversation event timelines.

You can start collecting feedback for your agent from your end users by integrating directly with the Feedback service API or using the SDK. The API and SDK let you manage feedback entries using standard CRUDL (create, retrieve, update, delete, and list) operations and attach additional conversation details to feedback entries through the `FeedbackContext` resource.

For more information, see [Manage feedback with Python SDK or REST API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/manage-with-sdk-or-api) or [View feedback in the console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/view-with-ui) .

## Core concepts

  - **Feedback entry:** Tracks a discrete qualitative data provided by an end user. Each entry captures binary sentiment, specific feedback labels, and optional free-form text.
  - **Feedback type:** The binary sentiment from the end user, represented by `thumbs_up` and `thumbs_down` .
  - **Session ID ( `session_id` ) and Event ID ( `event_id` ):** Required fields connecting feedback to a specific conversation turn or event.
  - **Feedback context:** An optional resource attached to a feedback entry that stores transcripts or conversation logs, preserving context even if the original session is deleted. This resource can store the whole conversation or the messages selected by the user, depending on what you choose to include.
  - **Feedback label:** A classification that specifies the nature of an operational issue or a successful outcome.
      - Positive feedback labels (typically used with `thumbs_up` ) include:
          - `accurate`
          - `complete`
          - `helpful`
          - `on_topic`
          - `fast`
          - `safe`
          - `factual`
          - `tool_success`
      - Negative feedback labels (typically used with `thumbs_down` ) include:
          - `inaccurate`
          - `incomplete`
          - `unhelpful`
          - `off_topic`
          - `too_slow`
          - `unsafe`
          - `hallucination`
          - `tool_error`

## Before you begin

To use the Feedback service, make sure you have the following:

  - An existing Agent Runtime instance. For more information, see [Develop an Agent Development Kit agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-adk-agent) .
  - Optional: To view feedback entries next to trace events in the console, make sure your Agent Runtime instance has [tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing) enabled.

### Get the required roles

To get the permissions that you need to use the Feedback service, ask your administrator to grant you the following IAM roles on your project:

  - All: [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

If you're making requests to the Feedback service from Google Cloud, make sure that your service account has the necessary permissions. User-managed service accounts must have the [Agent Platform User (aiplatform.user)](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) permission to interact with the Feedback service.

The [Reasoning Engine Service Agent](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.reasoningEngineServiceAgent) already has the necessary permissions to manage feedback, so outbound requests from Agent Runtime should already have permission to access the Feedback service.

## What's next

  - [Manage feedback using Python SDK or REST API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/manage-with-sdk-or-api)
  - [View feedback in the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/view-with-ui)
