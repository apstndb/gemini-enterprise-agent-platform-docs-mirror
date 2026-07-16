---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SemanticGovernancePolicyEngine
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SemanticGovernancePolicyEngine
title: SemanticGovernancePolicyEngine
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Define a singleton SemanticGovernancePolicyEngine resource under a project and location.

Fields

`name` `string`

Identifier. The resource name of the SemanticGovernancePolicyEngine. Format: projects/{project}/locations/{location}/semanticGovernancePolicyEngine

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this SemanticGovernancePolicyEngine was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this SemanticGovernancePolicyEngine was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`pscServiceAttachment` `string`

Output only. URI of the PSC attachment resource provided by SGP. Format: projects/{project}/regions/{region}/serviceAttachments/{serviceAttachment}

`ipAddress` `string`

Output only. The private IPv4 address of the PSC endpoint.

`pscForwardingRule` `string`

Output only. The URI of the PSC endpoint resource created in customer project. Format: projects/{project}/regions/{region}/forwardingRules/{forwardingRule}

`state` ` enum ( State  ` )

Output only. The state of the SemanticGovernancePolicyEngine.

`gatewayConfigs` ` map (key: string, value: object ( GatewayConfig  ` ))

Optional. Configurations for gateways. The keys are user-defined names for each gateway. At most 5 gateway configurations are allowed.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;pscServiceAttachment&quot;: string,&quot;ipAddress&quot;: string,&quot;pscForwardingRule&quot;: string,&quot;state&quot;: enum (State),&quot;gatewayConfigs&quot;: {string: {object (GatewayConfig)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## State

state of the SemanticGovernancePolicyEngine.

The lifecycle is: INACTIVE -\> PROVISIONING -\> {ACTIVE, FAILED} and ACTIVE -\> DEPROVISIONING -\> INACTIVE. A FAILED engine may be either re-provisioned or deprovisioned.

Enums

`STATE_UNSPECIFIED`

Default value. This value is unused.

`PROVISIONING`

A provisioning operation is in progress. The engine will transition to ACTIVE on success or FAILED on failure.

`ACTIVE`

The engine and all of its gateway configurations are provisioned and ready to serve traffic.

`DEPROVISIONING`

A deprovisioning operation is in progress. The engine will transition to INACTIVE on success or FAILED on failure.

`INACTIVE`

The engine has no provisioned infrastructure: either never provisioned, or successfully deprovisioned.

`FAILED`

The most recent provisioning or deprovisioning operation failed. The engine may have partial infrastructure that needs explicit deprovision; the engine may be either re-provisioned or deprovisioned to recover.

## GatewayConfig

Configuration for a single gateway.

Fields

`network` `string`

Optional. The URI of the network resource where PSC-E will be provisioned. if not provided `default` network will be used. Format: projects/{project}/global/networks/{network}

`subnetwork` `string`

Optional. The URI of the subnetwork resource where PSC-E will be provisioned. if not provided `default` subnet will be used from the same {location} Format: projects/{project}/regions/{region}/subnetworks/{subnetwork}

`dnsZoneName` `string`

Optional. FQDN of the private DNS zone to create DNS record set for PSC endpoint.

`state` ` enum ( State  ` )

Output only. The state of the Gateway configuration.

`ipAddress` `string`

Output only. The private IP address of the PSC endpoint.

`pscEndpoint` `string`

Output only. The self-link or name of the Private service Connect endpoint forwarding rule.

`dnsRecord` `string`

Output only. The fully qualified record name of the created A-record in Cloud DNS.

`allowedProjects[]` `string`

Optional. Additional consumer projects permitted to attach their own PSC endpoint to this gateway's ServiceAttachment. This is the "decoupled" mode, where the customer creates the PSC endpoint in a project other than this gateway's `network` project. Each listed project is VPC-SC enforced: it must be within the caller's service perimeter. The owning SemanticGovernancePolicyEngine's own project is always permitted implicitly and need not be listed. Format: project id or number.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;network&quot;: string,&quot;subnetwork&quot;: string,&quot;dnsZoneName&quot;: string,&quot;state&quot;: enum (State),&quot;ipAddress&quot;: string,&quot;pscEndpoint&quot;: string,&quot;dnsRecord&quot;: string,&quot;allowedProjects&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## State

state of the Gateway configuration.

Enums

`STATE_UNSPECIFIED`

The default value. This value is used if the state is omitted.

`PROVISIONING`

The Gateway is being provisioned.

`ACTIVE`

The Gateway is active and ready to use.

`DEPROVISIONING`

The Gateway is being de-provisioned.

`INACTIVE`

The Gateway is inactive.

`FAILED`

The Gateway failed to be provisioned.
