---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.feedbackEntries/updateFeedbackContext
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.feedbackEntries/updateFeedbackContext
title: 'Method: feedbackEntries.updateFeedbackContext'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.feedbackEntries.updateFeedbackContext

Updates the FeedbackContext associated with a FeedbackEntry.

Only the fields specified in updateMask are modified. If the mask is empty, all mutable fields are replaced with the values supplied in the request.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{feedbackContext.name}`  

`PATCH https://{service-endpoint}/v1beta1/{feedbackContext.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`feedbackContext.name` `string`

Identifier. The resource name. Assigned by the server on create.

Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/feedbackEntries/{feedbackEntry}/feedbackContext`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. The field mask that controls which fields are updated. If unset or empty, all mutable fields of the FeedbackContext are replaced with the values from feedbackContext.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  FeedbackContext  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
