---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward
title: 'Method: tuningJobs.validateReinforcementTuningReward'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tuningJobs.validateReinforcementTuningReward

Validates a reward on a given example.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /tuningJobs:validateReinforcementTuningReward`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to validate the reward in Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`sampleResponse` ` object ( Content  ` )

Required. The sample response for validating the reward configuration.

`example` ` object ( ReinforcementTuningExample  ` )

Required. The example to validate the reward configuration.

`reward_config` `Union type`

The reward configuration to validate. This can be a single or a composite reward configuration. `reward_config` can be only one of the following:

`singleRewardConfig` ` object ( SingleReinforcementTuningRewardConfig  ` )

Optional. Single Reward function configuration for reinforcement tuning.

`compositeRewardConfig` ` object ( CompositeReinforcementTuningRewardConfig  ` )

Optional. Composite reward function configuration for reinforcement tuning.

### Response body

Response message for `  GenAiTuningService.ValidateReinforcementTuningReward  ` .

If successful, the response body contains data with the following structure:

Fields

` rewardDetails (deprecated)  ` `map (key: string, value: number)`

> This item is deprecated\!

Output only. Deprecated: Use `  rewardInfoDetails  ` instead. A map from reward name to the calculated reward for the reward function. This field will only be populated when a `  CompositeReinforcementTuningRewardConfig  ` is provided in the request. It will not be set for a `  SingleReinforcementTuningRewardConfig  ` .

`rewardInfoDetails` ` map (key: string, value: object ( ReinforcementTuningRewardInfo  ` ))

A map from reward name to reward info.

`overallReward` `number`

Output only. The overall weighted reward. For a `  CompositeReinforcementTuningRewardConfig  ` , this is the weighted average of all rewards. For a `  SingleReinforcementTuningRewardConfig  ` , this will be the value of the single reward.

`error` `string`

Output only. In case of an error, this field will be populated with a detailed error message to help with debugging.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rewardDetails&quot;: {string: number,...},&quot;rewardInfoDetails&quot;: {string: {object (ReinforcementTuningRewardInfo)},...},&quot;overallReward&quot;: number,&quot;error&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ReinforcementTuningRewardInfo

The reward info for a reward function.

Fields

`userRequestedAuxInfo` `string`

Output only. The user-requested auxiliary info for the reward function. This field is set only if the Cloud Run reward function configured by user returns a "user\_requested\_aux\_info". Refer to `  ReinforcementTuningCloudRunRewardScorer  ` for more details.

`reward` `number`

Output only. The calculated reward for the reward function.

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
  &quot;userRequestedAuxInfo&quot;: string,
  &quot;reward&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
