---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobSpec
title: HyperparameterTuningJobSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`studySpec` ` object ( StudySpec  ` )

Study configuration of the HyperparameterTuningJob.

`trialJobSpec` ` object ( CustomJobSpec  ` )

The spec of a trial job. The same spec applies to the CustomJobs created in all the trials.

`maxTrialCount` `integer`

The desired total number of Trials.

`parallelTrialCount` `integer`

The desired number of Trials to run in parallel.

`maxFailedTrialCount` `integer`

The number of failed Trials that need to be seen before failing the HyperparameterTuningJob.

If set to 0, Agent Platform decides how many Trials must fail before the whole job fails.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;studySpec&quot;: {object (StudySpec)},&quot;trialJobSpec&quot;: {object (CustomJobSpec)},&quot;maxTrialCount&quot;: integer,&quot;parallelTrialCount&quot;: integer,&quot;maxFailedTrialCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>
