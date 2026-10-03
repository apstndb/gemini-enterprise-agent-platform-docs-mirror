---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PSCAutomationConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PSCAutomationConfig
title: PSCAutomationConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

PSC config that is used to automatically create PSC endpoints in the user projects.

Fields

`projectId` `string`

Required. Project id used to create forwarding rule.

`network` `string`

Required. The full name of the Google Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/get) : `projects/{project}/global/networks/{network}` .

`ipAddress` `string`

Output only. IP address rule created by the PSC service automation.

`forwardingRule` `string`

Output only. Forwarding rule created by the PSC service automation.

`state` `enum ( `[`PSCAutomationState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PSCAutomationConfig#PSCAutomationState)` )`

Output only. The state of the PSC service automation.

`errorMessage` `string`

Output only. Error message if the PSC service automation failed.

**JSON representation**

```
{
  "projectId": string,
  "network": string,
  "ipAddress": string,
  "forwardingRule": string,
  "state": enum (PSCAutomationState),
  "errorMessage": string
}
```

## PSCAutomationState

The state of the PSC service automation.

| Enums                              |                                           |
|------------------------------------|-------------------------------------------|
| `PSC_AUTOMATION_STATE_UNSPECIFIED` | Should not be used.                       |
| `PSC_AUTOMATION_STATE_SUCCESSFUL`  | The PSC service automation is successful. |
| `PSC_AUTOMATION_STATE_FAILED`      | The PSC service automation has failed.    |
