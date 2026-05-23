---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/suggest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/suggest
title: 'Method: trials.suggest'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.suggest

Adds one or more Trials to a Study, with parameter values suggested by Agent Platform Vizier. Returns a long-running operation associated with the generation of Trial suggestions. When this long-running operation succeeds, it will contain a `  SuggestTrialsResponse  ` .

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /trials:suggest`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The project and location that the Study belongs to. Format: `projects/{project}/locations/{location}/studies/{study}`

### Request body

The request body contains data with the following structure:

Fields

`suggestionCount` `integer`

Required. The number of suggestions requested. It must be positive.

`clientId` `string`

Required. The identifier of the client that is requesting the suggestion.

If multiple SuggestTrialsRequests have the same `clientId` , the service will return the identical suggested Trial if the Trial is pending, and provide a new Trial if the last suggested Trial was completed.

`contexts[]` ` object ( TrialContext  ` )

Optional. This allows you to specify the "context" for a Trial; a context is a slice (a subspace) of the search space.

Typical uses for contexts: 1) You are using Vizier to tune a server for best performance, but there's a strong weekly cycle. The context specifies the day-of-week. This allows Tuesday to generalize from Wednesday without assuming that everything is identical. 2) Imagine you're optimizing some medical treatment for people. As they walk in the door, you know certain facts about them (e.g. sex, weight, height, blood-pressure). Put that information in the context, and Vizier will adapt its suggestions to the patient. 3) You want to do a fair A/B test efficiently. Specify the "A" and "B" conditions as contexts, and Vizier will generalize between "A" and "B" conditions. If they are similar, this will allow Vizier to converge to the optimum faster than if "A" and "B" were separate Studies. NOTE: You can also enter contexts as REQUESTED Trials, e.g. via the trials.create() RPC; that's the asynchronous option where you don't need a close association between contexts and suggestions.

NOTE: All the Parameters you set in a context MUST be defined in the Study. NOTE: You must supply 0 or $suggestionCount contexts. If you don't supply any contexts, Vizier will make suggestions from the full search space specified in the StudySpec; if you supply a full set of context, each suggestion will match the corresponding context. NOTE: A Context with no features set matches anything, and allows suggestions from the full search space. NOTE: Contexts MUST lie within the search space specified in the StudySpec. It's an error if they don't. NOTE: Contexts preferentially match ACTIVE then REQUESTED trials before new suggestions are generated. NOTE: Generation of suggestions involves a match between a Context and (optionally) a REQUESTED trial; if that match is not fully specified, a suggestion will be geneated in the merged subspace.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## TrialContext

Fields

`description` `string`

A human-readable field which can store a description of this context. This will become part of the resulting Trial's description field.

`parameters[]` ` object ( Parameter  ` )

If/when a Trial is generated or selected from this Context, its Parameters will match any parameters specified here. (I.e. if this context specifies parameter name:'a' intValue:3, then a resulting Trial will have intValue:3 for its parameter named 'a'.) Note that we first attempt to match existing REQUESTED Trials with contexts, and if there are no matches, we generate suggestions in the subspace defined by the parameters specified here. NOTE: a Context without any Parameters matches the entire feasible search space.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;description&quot;: string,&quot;parameters&quot;: [{object (Parameter)}]}</code></pre></td>
</tr>
</tbody>
</table>
