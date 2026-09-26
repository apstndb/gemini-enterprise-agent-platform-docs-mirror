---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents
title: 'REST Resource: projects.locations.agents'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Agent

A Vertex agent contains instructions and configurations for the LLM to execute a certain task.

Fields

`name` `string`

Identifier. The resource name of the agent. Format: `projects/{project}/locations/{location}/agents/{agent}` .

`id` `string`

Immutable. The user-specified id for the agent. This id becomes the final component of the agent resource name. If not provided, Agent Platform will generate a value for this id. The id can be up to 63 characters and must match the regular expression `[a-z]([a-z0-9-]{0,61}[a-z0-9])?` .

`created` ` string ( Timestamp  ` format)

Output only. The time the agent was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updated` ` string ( Timestamp  ` format)

Output only. The time the agent was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`object` `string`

Output only. The object type of the resource. For agents, the value is `agent` .

`base_agent` `string`

Required. Immutable. The base agent for the agent. Supported values: \* `antigravity-preview-05-2026`

Immutable: `agents.patch` rejects a change, including clearing it. The kind of agent this is gets derived from this field when the agent is created and is recorded then; nothing recomputes it afterwards, so a later change would leave the agent described as one kind and behaving as another. Create a new agent instead.

`metadata` `map (key: string, value: string)`

Optional. The metadata for the agent.

`description` `string`

Optional. The description of the agent.

`system_instruction` `string`

Optional. The instructions for the agent to follow. These instructions are passed to the LLM as a system instruction.

`tools[]` ` object ( AgentTool  ` )

Optional. The tools available to the agent.

`environment` `Union type`

The environment configuration for the agent. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`base_environment` ` value ( Value  ` format)

Optional. The base environment configuration for the agent. Valid types:

  - A string value for the environment id, or `remote` for the default.
  - A struct value for the `environment_config` .

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;id&quot;: string,&quot;created&quot;: string,&quot;updated&quot;: string,&quot;object&quot;: string,&quot;base_agent&quot;: string,&quot;metadata&quot;: {string: string,...},&quot;description&quot;: string,&quot;system_instruction&quot;: string,&quot;tools&quot;: [{object (AgentTool)}],// environment&quot;base_environment&quot;: value// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AgentTool

A tool provides a list of actions available to the `  Agent  ` during the process of executing a task.

Example JSON for an MCP server tool: { "type": "mcpServer", "name": "my-mcp-server", "url": "https://api.example.com/mcp", "headers": { "Authorization": "Bearer token123" } }

Fields

`type` `string`

Required. The type of the tool. Supported types:

  - `code_execution`
  - `endpoint`
  - `filesystem`
  - `google_search`
  - `mcp_server`
  - `url_context`

`name` `string`

Optional. The tool's Google Cloud resource name, used to resolve the tool. Applicable when `type` is `mcp_server` or `endpoint` (a tool registered in Agent Registry), for example `projects/{project}/locations/{location}/.../mcpServers/{id}` or `projects/{project}/locations/{location}/.../endpoints/{id}` .

`url` `string`

Optional. Fallback for the tool's runtime reference, consumed by `agents.create` to create the downstream AI App. Applicable when `type` is `mcp_server` or `endpoint` , and optional: the Agent service derives the runtime reference from `name` via Agent Registry ( `GetMcpServer` / `GetEndpoint` ), and reads this only when that lookup yields none.

`headers` `map (key: string, value: string)`

Optional. The headers for the MCP server, such as for authentication. Only applicable when `type` is `mcp_server` .

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
  &quot;type&quot;: string,
  &quot;name&quot;: string,
  &quot;url&quot;: string,
  &quot;headers&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates an agent.

### `            delete           `

Deletes an agent.

### `            get           `

Retrieves an agent.

### `            list           `

Lists the agents in a location that belong to the caller.

### `            patch           `

Updates an agent.
