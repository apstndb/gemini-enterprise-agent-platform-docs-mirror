---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Date
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Date
title: Date
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a whole or partial calendar date, such as a birthday. The time of day and time zone are either specified elsewhere or are insignificant. The date is relative to the Gregorian Calendar. This can represent one of the following:

  - A full date, with non-zero year, month, and day values.
  - A month and day, with a zero year (for example, an anniversary).
  - A year on its own, with a zero month and a zero day.
  - A year and month, with a zero day (for example, a credit card expiration date).

Related types:

  - `google.type.TimeOfDay`
  - `google.type.DateTime`
  - `  google.protobuf.Timestamp  `

Fields

`year` `integer`

year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.

`month` `integer`

Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.

`day` `integer`

Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant.

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
  &quot;year&quot;: integer,
  &quot;month&quot;: integer,
  &quot;day&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
