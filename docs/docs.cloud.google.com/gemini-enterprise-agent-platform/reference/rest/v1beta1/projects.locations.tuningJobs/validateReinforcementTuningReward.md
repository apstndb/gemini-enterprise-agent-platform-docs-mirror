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

`sampleResponse` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Required. The sample response for validating the reward configuration.

`example` `object ( `[`ReinforcementTuningExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample)` )`

Required. The example to validate the reward configuration.

`reward_config` `Union type`

The reward configuration to validate. This can be a single or a composite reward configuration. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`singleRewardConfig` `object ( `[`SingleReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SingleReinforcementTuningRewardConfig)` )`

Optional. Single Reward function configuration for reinforcement tuning.

`compositeRewardConfig` `object ( `[`CompositeReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CompositeReinforcementTuningRewardConfig)` )`

Optional. Composite reward function configuration for reinforcement tuning.

End of mutually exclusive fields.

### Response body

Response message for [`GenAiTuningService.ValidateReinforcementTuningReward`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward#google.cloud.aiplatform.v1beta1.GenAiTuningService.ValidateReinforcementTuningReward) .

If successful, the response body contains data with the following structure:

Fields

`rewardDetails `**`(deprecated)`** `map (key: string, value: number)`

> This item is deprecated!

Output only. Deprecated: Use [`rewardInfoDetails`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward#body.ValidateReinforcementTuningRewardResponse.FIELDS.reward_info_details) instead. A map from reward name to the calculated reward for the reward function. This field will only be populated when a [`CompositeReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CompositeReinforcementTuningRewardConfig) is provided in the request. It will not be set for a [`SingleReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SingleReinforcementTuningRewardConfig) .

`errorStatus` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. In case of an error, this field will be populated with a detailed error message for overall rewards to help with debugging.

`rewardInfoDetails` `map (key: string, value: object ( `[`ReinforcementTuningRewardInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward#ReinforcementTuningRewardInfo)` ))`

A map from reward name to reward info.

`overallReward` `number`

Output only. The overall weighted reward. For a [`CompositeReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CompositeReinforcementTuningRewardConfig) , this is the weighted average of all rewards. For a [`SingleReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SingleReinforcementTuningRewardConfig) , this will be the value of the single reward.

`error `**`(deprecated)`** `string`

> This item is deprecated!

Output only. Deprecated: Use [`errorStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward#body.ValidateReinforcementTuningRewardResponse.FIELDS.error_status) instead. In case of an error, this field will be populated with a detailed error message to help with debugging.

**JSON representation**

```
{
  "rewardDetails": {
    string: number,
    ...
  },
  "errorStatus": {
    object (Status)
  },
  "rewardInfoDetails": {
    string: {
      object (ReinforcementTuningRewardInfo)
    },
    ...
  },
  "overallReward": number,
  "error": string
}
```

## ReinforcementTuningRewardInfo

The reward info for a reward function.

Fields

`userRequestedAuxInfo` `string`

Output only. The user-requested auxiliary info for the reward function. This field is set only if the Cloud Run reward function configured by user returns a "user_requested_aux_info". Refer to [`ReinforcementTuningCloudRunRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCloudRunRewardScorer) for more details.

`errorStatus` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. In case of an error for this reward, this field will be populated with a detailed error status.

`reward` `number`

Output only. The calculated reward for the reward function.

**JSON representation**

```
{
  "userRequestedAuxInfo": string,
  "errorStatus": {
    object (Status)
  },
  "reward": number
}
```
