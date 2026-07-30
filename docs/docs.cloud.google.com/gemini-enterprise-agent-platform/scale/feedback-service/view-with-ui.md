---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/view-with-ui
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/view-with-ui
title: View feedback in the Google Cloud console
description: View user feedback for your agent in the {{dynamic_data.site_values.cloud_name_short}} console.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to view received end-user feedback in the Google Cloud console.

## Before you begin

To view feedback entries in the Google Cloud console, make sure of the following:

  - Your Agent Runtime instance has [tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing) enabled.
  - Your agent is configured to use OpenTelemetry (OTel) to generate trace spans and handle trace context propagation. The console UI maps feedback entries to traces using the OpenTelemetry-generated span attribute `gcp.vertex.agent.event_id` .

## View feedback

The Feedback service is integrated with the **Traces** tab in the Google Cloud console. In the **Traces** tab, you can view and filter traces that have feedback attached in both the **Sessions view** and **Traces view** tabs.

To view feedback entries for your agent:

1.  In the Google Cloud console, navigate to the **Agent Platform \> Agents** page.

2.  In the left navigation menu, select **Deployments** .

3.  Select your agent.
    
    Agent Engine instances that are part of the selected project appear in the list. You can use the **Filter** field to filter the list by your specified column.

4.  Click the name of your Agent Engine instance.

5.  Click the **Traces** tab. Use the **Sessions view** or **Traces view** to find traces with feedback:
    
      - **Sessions view** :
        1.  Filter the sessions list by the **Feedback** column.
        2.  Click the session you want to view to display its list of traces.
        3.  Select a trace ID that displays a feedback icon badge.
      - **Traces view** :
        1.  Click the **Traces view** tab.
        2.  Filter the traces list by the **Feedback** column.
        3.  Select a trace ID that displays a feedback icon badge.

6.  In the trace details pane, click the **Feedback** tab to view the feedback details, such as the feedback type, comments, labels, ID, and creation time.

### UI limitations

  - **Event ID requirements** : The UI only supports tracking and mapping feedback entries that use the OpenTelemetry-generated UUID ( `gcp.vertex.agent.event_id` ) fetched from the trace spans.
  - **Duplicate submissions** : If multiple feedback entries are submitted with the same `session_id` and `event_id` combination, the console UI only displays the last received feedback entry.

## Cloud Trace integration

When a user submits feedback, the Feedback service exports telemetry spans to Cloud Trace. To locate user feedback alongside reasoning engine execution events, search and filter these exported spans by their attributes. For details on how to find and view these traces, see the [Set up tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing#view-traces) guide.

Because traces are immutable, deleting or updating a feedback entry does not affect previously exported traces.

Each feedback telemetry trace contains a span named `gcp.vertex.agent.feedback` with the following resource and span attributes:

| Attribute                              | Attribute type | Description                                                                     |
| -------------------------------------- | -------------- | ------------------------------------------------------------------------------- |
| `gcp.project_id`                       | Resource       | Project ID of a Google Cloud console project.                                   |
| `cloud.resource.id`                    | Resource       | ID of the reasoning engine instance.                                            |
| `gcp.vertex.agent.feedback.type`       | Span           | Feedback type ( `THUMBS_UP` , `THUMBS_DOWN` , or `FEEDBACK_TYPE_UNSPECIFIED` ). |
| `gen_ai.conversation_id`               | Span           | Session ID associated with the interaction.                                     |
| `gcp.vertex.agent.event_id`            | Span           | Event ID associated with the specific conversation turn.                        |
| `gcp.vertex.agent.feedback.entry.name` | Span           | Resource path of the created feedback entry.                                    |
| `gcp.vertex.agent.feedback.labels`     | Span           | Optional. List of feedback labels.                                              |

## What's next

  - [Manage feedback with Python SDK or REST API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/feedback-service/manage-with-sdk-or-api)
  - [Set up tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing)
