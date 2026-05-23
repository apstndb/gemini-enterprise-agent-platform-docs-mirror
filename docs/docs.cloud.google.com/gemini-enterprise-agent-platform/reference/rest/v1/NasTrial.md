---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NasTrial
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NasTrial
title: NasTrial
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a uCAIP NasJob trial.

Fields

`id` `string`

Output only. The identifier of the NasTrial assigned by the service.

`state` ` enum ( State  ` )

Output only. The detailed state of the NasTrial.

`finalMeasurement` ` object ( Measurement  ` )

Output only. The final measurement containing the objective value.

`startTime` ` string ( Timestamp  ` format)

Output only. time when the NasTrial was started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Output only. time when the NasTrial's status changed to `SUCCEEDED` or `INFEASIBLE` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;state&quot;: enum (State),&quot;finalMeasurement&quot;: {object (Measurement)},&quot;startTime&quot;: string,&quot;endTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## State

Describes a NasTrial state.

Enums

`STATE_UNSPECIFIED`

The NasTrial state is unspecified.

`REQUESTED`

Indicates that a specific NasTrial has been requested, but it has not yet been suggested by the service.

`ACTIVE`

Indicates that the NasTrial has been suggested.

`STOPPING`

Indicates that the NasTrial should stop according to the service.

`SUCCEEDED`

Indicates that the NasTrial is completed successfully.

`INFEASIBLE`

Indicates that the NasTrial should not be attempted again. The service will set a NasTrial to INFEASIBLE when it's done but missing the finalMeasurement.
