---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies
title: 'REST Resource: projects.locations.semanticGovernancePolicies'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SemanticGovernancePolicy

Represents a governance policy applied to a specific Agent and optionally a specific Tool within that Agent.

Fields

`name` `string`

Identifier. Resource name of the SemanticGovernancePolicy.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this SemanticGovernancePolicy was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

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

Required. The name of the agent in Agent Registry that is affected by this policy.

`mcpTools[]` ` object ( McpTool  ` )

Optional. The McpTools that are affected by this policy.

`agentIdentity` `string`

Output only. Represents the principal of the agent, used by the Policy Decision Point (PDP) for governance checks. For more information, see <https://docs.cloud.google.com/agent-builder/agent-engine/agent-identity>

Format: `principal://TRUST_DOMAIN/NAMESPACE/AGENT_NAME`

Example: `principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/aiplatform/projects/PROJECT_NUMBER/locations/LOCATION/reasoningEngines/AGENT_ENGINE_ID`

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;naturalLanguageConstraint&quot;: string,&quot;agent&quot;: string,&quot;mcpTools&quot;: [{object (McpTool)}],&quot;agentIdentity&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## McpTool

Represents a governance policy applied to MCP tools used by an Agent.

Fields

`mcpServer` `string`

Required. The resource name of the McpServer in Agent Registry that is affected by this policy. Format: `projects/{project}/locations/{location}/mcpServers/{mcpServer}`

`tools[]` `string`

Optional. The resource names of the McpTools used by the Agent that is affected by this policy. If not specified, the policy applies to all McpTools in the McpServer.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mcpServer&quot;: string,
  &quot;tools&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a SemanticGovernancePolicy.

### `            delete           `

Deletes a SemanticGovernancePolicy.

### `            get           `

Gets a SemanticGovernancePolicy.

### `            list           `

Lists SemanticGovernancePolicies in a given location.

### `            patch           `

Updates a SemanticGovernancePolicy.
