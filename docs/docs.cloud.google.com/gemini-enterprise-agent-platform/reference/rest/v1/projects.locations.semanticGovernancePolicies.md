---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies
title: 'REST Resource: projects.locations.semanticGovernancePolicies'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SemanticGovernancePolicy

Represents a governance policy applied to a specific Agent and optionally a specific Tool within that Agent.

Fields

`name` `string`

Identifier. Resource name of the SemanticGovernancePolicy.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this SemanticGovernancePolicy was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this SemanticGovernancePolicy was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write transactions. If provided, the request will only succeed if the etag matches the current value. Otherwise, an ABORTED error will be returned.

`displayName` `string`

Optional. The user-defined name of the SemanticGovernancePolicy.

`description` `string`

Optional. The description of the SemanticGovernancePolicy.

`naturalLanguageConstraint` `string`

Required. The natural language constraint of the SemanticGovernancePolicy.

`agent` `string`

Required. The name of the agent in Agent Registry that is affected by this policy. Format: `projects/{project}/locations/{location}/agents/{agent}`

`mcpTools[]` `object ( `[`McpTool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies#McpTool)` )`

Optional. The McpTools that are affected by this policy.

`agentIdentity` `string`

Output only. Represents the principal of the agent, used by the Policy Decision Point (PDP) for governance checks. For more information, see <https://docs.cloud.google.com/agent-builder/agent-engine/agent-identity>

Format: `principal://TRUST_DOMAIN/NAMESPACE/AGENT_NAME`

Example: `principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID`

`agentResponseCustomization` `object ( `[`AgentResponseCustomization`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies#AgentResponseCustomization)` )`

Optional. Settings for customizing the agent's response to end users when this policy is evaluated, such as messages displayed when the policy denies a request.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "displayName": string,
  "description": string,
  "naturalLanguageConstraint": string,
  "agent": string,
  "mcpTools": [
    {
      object (McpTool)
    }
  ],
  "agentIdentity": string,
  "agentResponseCustomization": {
    object (AgentResponseCustomization)
  }
}
```

## McpTool

Represents a governance policy applied to MCP tools used by an Agent.

Fields

`mcpServer` `string`

Required. The resource name of the McpServer in Agent Registry that is affected by this policy. Format: `projects/{project}/locations/{location}/mcpServers/{mcpServer}`

`tools[]` `string`

Required. The resource names of the tools used by the Agent that is affected by this policy. Currently, exactly one tool must be specified.

**JSON representation**

```
{
  "mcpServer": string,
  "tools": [
    string
  ]
}
```

## AgentResponseCustomization

Customizes the agent's response to the end user when a `SemanticGovernancePolicy` is evaluated (for example, with a custom message shown on denial).

Fields

`denialMessage` `string`

Optional. Custom message shown to the end user when the policy check results in a denial. Use this to explain the rationale to the user. Max 1000 characters.

**JSON representation**

```
{
  "denialMessage": string
}
```

| Methods                                                                                                                                           |                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/create) | Creates a SemanticGovernancePolicy.                   |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/delete) | Deletes a SemanticGovernancePolicy.                   |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/get)       | Gets a SemanticGovernancePolicy.                      |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/list)     | Lists SemanticGovernancePolicies in a given location. |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/patch)   | Updates a SemanticGovernancePolicy.                   |
