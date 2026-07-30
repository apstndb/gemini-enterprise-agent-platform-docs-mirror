---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/manage-with-sdk-or-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/manage-with-sdk-or-api
title: Manage feedback using Python SDK or REST API
description: Manage feedback entries and feedback context using direct API calls or the SDK.
data_source: docs.cloud.google.com
---

This page describes how to use the Feedback service API and SDK to manage feedback entries and context. You can implement custom feedback controls (such as thumbs-up or thumbs-down buttons) in a user interface like chat widgets or mobile apps and use the Feedback service to track feedback.

## Before you begin

Make sure you have the following:

  - The Agent Platform User ( `roles/aiplatform.user` ) role.
  - Set up authentication by following the [Authentication](https://docs.cloud.google.com/docs/authentication/client-libraries) steps.
  - A deployed Agent Runtime instance. If you don't have a deployed instance, see [Deploy an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) or initialize and create one by following the steps in the next section.
  - Optional: To view feedback entries next to trace events in the console, make sure your Agent Runtime instance has [tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing) enabled.

## Create an Agent Runtime instance

If you don't have an existing Agent Runtime instance, you can initialize the client and create one:

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    # If you don't have an Agent Engine instance already, create an instance.
    agent_engine = client.agent_engines.create()
    
    # Optionally, print out the Agent Engine resource name. You will need the
    # resource name to interact with the Feedback service later on.
    print(agent_engine.api_resource.name)

### REST API

An Agent Runtime resource name uses the following format: `projects/` PROJECT\_ID `/locations/` LOCATION `/reasoningEngines/` AGENT\_ENGINE\_ID

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Runtime.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Runtime instance.

## Create a feedback entry

Before submitting feedback, you must have an existing session with few messages exchanged between the user and the agent. Identify the response you want to send feedback on, and obtain its event ID and session ID.

To do this:

1.  [Create an interaction session](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-api) with an agent.

2.  Send a query to the agent and identify the response that you want to send feedback on.

3.  Grab the session ID and the response event's ID (which acts as the event ID for the feedback entry). If you're using the managed Session Service with ADK, you can get the event ID from the `raw_event.id` field of the list events response (see [List events in a session](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-api#list-events) ).

> **Note:** While the API and SDK accept any arbitrary session ID and event ID, the feedback won't associate correctly or be visible in the console UI unless the IDs match a session and response event associated with an existing interaction session.
> 
> If you're using the Feedback service with an ADK agent, the `event_id` must be the same as the **`gcp.vertex.agent.event_id`** on a span emitted by the ADK (such as a `generate_content` or `execute_tool` span), for example, `c9ba0d5e-9ba2-41cb-abf4-49680e9d8ce4` . Otherwise, you won't be able to see traces in the console, but the Feedback service API will still work.

Programmatically log a feedback entry bound directly to a target `session_id` and `event_id` defining a user-agent conversation event.

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    operation = client.feedback_entries.create(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID",
        session_id="SESSION_ID",
        event_id="EVENT_ID",
        feedback_type="THUMBS_UP",
        config={
            "feedback_text": "The response was helpful and accurate.",
            "feedback_labels": ["accurate"],
            "user_id": "user-123",
            "source": "Chat UI",
            "custom_metadata": {"model_temperature": "0.7"},
        }
    )
    
    # Retrieve the created feedback entry details
    feedback_entry = operation.response
    print(f"Created feedback entry: {feedback_entry.name}")

Supported values for `feedback_type` are:

  - `"THUMBS_UP"`
  - `"THUMBS_DOWN"`
  - `"FEEDBACK_TYPE_UNSPECIFIED"`

### REST API

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.
  - SESSION\_ID : The session ID defining the conversation associated with the feedback.
  - EVENT\_ID : The event ID identifying the specific message or node targeted by the feedback.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries

Request JSON body:

    {
      "sessionId": "SESSION_ID",
      "eventId": "EVENT_ID",
      "feedbackType": "THUMBS_DOWN",
      "feedbackLabels": ["inaccurate"],
      "feedbackText": "The answer was incorrect.",
      "userId": "user-123",
      "source": "Chat UI",
      "customMetadata": {
        "temperature": "0.7"
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries" | Select-Object -Expand Content

You receive a long-running operation indicating the status of the feedback entry creation.

## Retrieve a feedback entry

Fetch the full, structured payload of an isolated feedback record using its unique resource address.

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    feedback_entry = client.feedback_entries.get(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID"
    )
    
    print(f"Feedback Type: {feedback_entry.feedback_type}")
    print(f"Feedback Text: {feedback_entry.feedback_text}")

### REST API

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.
  - FEEDBACK\_ENTRY\_ID : The resource ID of the feedback entry.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID" | Select-Object -Expand Content

The response includes the feedback entry details such as the session ID, type, labels, and text.

## List feedback entries

List feedback entries in your Agent Runtime instance. You can apply filters and ordering properties.

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    response = client.feedback_entries.list(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID",
        config={
            "filter": 'session_id="SESSION_ID"',
            "order_by": "create_time desc"
        }
    )
    
    for entry in response:
        print(f"Entry name: {entry.name}, Type: {entry.feedback_type}")

### REST API

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries" | Select-Object -Expand Content

The response includes a list of feedback entries matching any applied filters, along with a pagination token if there are additional entries.

You can use the `filter` query parameter to query by specific attributes. To sort, use the `order_by` query parameter.

Supported fields for filtering:

  - `session_id` , such as `session_id="SESSION_ID"`
  - `user_id` , such as `user_id="YOUR_USER_ID"`
  - `feedback_type` , such as `feedback_type="THUMBS_DOWN"`
  - `feedback_labels` , such as `feedback_labels: "inaccurate"`
  - `create_time`
  - `update_time`

Supported fields for sorting:

  - `create_time`
  - `update_time`

## Update a feedback entry

Update details on an existing feedback entry such as modifying labels, comments, or custom metadata.

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    operation = client.feedback_entries.update(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID",
        feedback_type="THUMBS_DOWN",
        config={
            "feedback_text": "Actually, this response was not accurate.",
            "feedback_labels": ["inaccurate"],
        }
    )
    
    updated_entry = operation.response
    print(f"Updated entry: {updated_entry.name}")

### REST API

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.
  - FEEDBACK\_ENTRY\_ID : The resource ID of the feedback entry to update.

HTTP method and URL:

    PATCH https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID?updateMask=feedbackType,feedbackLabels,feedbackText

Request JSON body:

    {
      "feedbackType": "THUMBS_DOWN",
      "feedbackLabels": ["inaccurate", "incomplete"],
      "feedbackText": "The response was details-lacking and inaccurate."
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID?updateMask=feedbackType,feedbackLabels,feedbackText"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID?updateMask=feedbackType,feedbackLabels,feedbackText" | Select-Object -Expand Content

You receive a long-running operation indicating the progress of the update operation.

## Delete a feedback entry

Permanently delete a feedback entry from your project.

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    client.feedback_entries.delete(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID"
    )
    
    print("Feedback entry deleted.")

### REST API

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.
  - FEEDBACK\_ENTRY\_ID : The resource ID of the feedback entry to delete.

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID" | Select-Object -Expand Content

You receive a long-running operation showing the deletion status.

## Feedback context

The feedback context ( `FeedbackContext` ) is a child resource of a feedback entry ( `FeedbackEntry` ) that is automatically created and deleted together with its parent feedback entry. By default, the feedback context contains an empty list of events.

The feedback context stores transcripts or event states associated with the feedback entry. This resource separation:

  - **Preserves conversation history:** Even if the original session is deleted, the transcripts or logs stored in the feedback context are retained.
  - **Reduces response size:** When retrieving feedback entries, you don't need to fetch the detailed context details.

The `FeedbackContext` resource has the following structure:

    projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext

### Retrieve feedback context

Get the details and conversation events stored in the feedback context:

### Python SDK

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    feedback_context = client.feedback_entries.feedback_contexts.get(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext"
    )
    
    # Point to event list
    for event in feedback_context.context_events:
        print(f"Author: {event.author}")
        if event.content and event.content.parts:
            print(f"Content: {event.content.parts[0].text}")

### REST API

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.
  - FEEDBACK\_ENTRY\_ID : The resource ID of the feedback entry.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext" | Select-Object -Expand Content

The response includes details for the requested feedback context, including the list of conversation events associated with the parent feedback entry.

### Create and update feedback context

### Python SDK

To populate or modify the conversation history associated with a feedback entry, update the feedback context using the following two-step flow:

1.  **Create the feedback entry** : Call standard methods to create the primary feedback record.
2.  **Update the feedback context** : After obtaining the feedback entry ID, send a request to populate the context events.

<!-- end list -->

    import os
    import vertexai
    
    # Set this environment variable to enable the Enterprise features.
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    
    client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
    )
    
    # Construct conversation events
    session_event = {
        "author": "user",
        "content": {
            "role": "user",
            "parts": [{"text": "Hello Agent"}]
        }
    }
    
    operation = client.feedback_entries.feedback_contexts.update(
        name="projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID",
        context_events=[session_event]
    )
    
    updated_context = operation.response
    print("Feedback context updated successfully.")

### REST API

To populate or modify the conversation history associated with a feedback entry, update the feedback context using the following two-step flow:

1.  **Create the feedback entry** : Call `CreateFeedbackEntry` to create the primary feedback record.
2.  **Update the feedback context** : Once you obtain the feedback entry ID, send a `PATCH` request to the context child resource ( `UpdateFeedbackContext` ) to populate `contextEvents` .

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where your Agent Engine instance is located.
  - AGENT\_ENGINE\_ID : The resource ID of your Agent Engine instance.
  - FEEDBACK\_ENTRY\_ID : The resource ID of the feedback entry.

HTTP method and URL:

    PATCH https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext?updateMask=contextEvents

Request JSON body:

    {
      "contextEvents": [
        {
          "author": "user",
          "content": {
            "role": "user",
            "parts": [
              {
                "text": "What is the capital of France?"
              }
            ]
          }
        },
        {
          "author": "agent",
          "content": {
            "role": "model",
            "parts": [
              {
                "text": "Paris is the capital of France."
              }
            ]
          }
        }
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext?updateMask=contextEvents"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID/feedbackEntries/FEEDBACK_ENTRY_ID/feedbackContext?updateMask=contextEvents" | Select-Object -Expand Content

You receive a long-running operation showing the update progress of the feedback context.

To remove the feedback context, send an empty update (for example, with `context_events` set to an empty list).
