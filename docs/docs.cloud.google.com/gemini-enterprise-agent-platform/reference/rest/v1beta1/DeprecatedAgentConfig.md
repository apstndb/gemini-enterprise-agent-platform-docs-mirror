---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeprecatedAgentConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeprecatedAgentConfig
title: DeprecatedAgentConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> This item is deprecated\!

Deprecated: Use `google.cloud.aiplatform.master.AgentConfig` in `agentEvalData` instead. Configuration for an Agent.

Fields

`agentId` `string`

Optional. Unique identifier of the agent. This id is used to refer to this agent, e.g., in AgentEvent.author, or in the `subAgents` field. It must be unique within the `agents` map.

`agentType` `string`

Optional. The type or class of the agent (e.g., "LlmAgent", "RouterAgent", "ToolUseAgent"). Useful for the autorater to understand the expected behavior of the agent.

`description` `string`

Optional. A high-level description of the agent's role and responsibilities. Critical for evaluating if the agent is routing tasks correctly.

`subAgents[]` `string`

Optional. The list of valid agent IDs (names) that this agent can delegate to. This defines the directed edges in the agent system graph topology.

`developerInstruction` ` object ( InstanceData  ` )

Optional. Contains instructions from the developer for the agent. Can be static or a dynamic prompt template used with the `AgentEvent.state_delta` field.

`tools_data` `Union type`

Data for the tools available to the agent. `tools_data` can be only one of the following:

`toolsText` `string`

A JSON string containing a list of tools available to an agent with info such as name, description, parameters and required parameters.

`tools` ` object ( Tools  ` )

List of tools.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agentId&quot;: string,&quot;agentType&quot;: string,&quot;description&quot;: string,&quot;subAgents&quot;: [string],&quot;developerInstruction&quot;: {object (InstanceData)},// tools_data&quot;toolsText&quot;: string,&quot;tools&quot;: {object (Tools)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Tools

Represents a list of tools for an agent.

Fields

`tool[]` ` object ( Tool  ` )

Optional. List of tools: each tool can have multiple function declarations.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tool&quot;: [{object (Tool)}]}</code></pre></td>
</tr>
</tbody>
</table>
