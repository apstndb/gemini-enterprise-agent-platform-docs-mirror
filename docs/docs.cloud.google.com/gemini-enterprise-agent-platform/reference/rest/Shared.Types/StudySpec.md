---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/StudySpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/StudySpec
title: StudySpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents specification of a Study.

Fields

`metrics[]` ` object ( MetricSpec  ` )

Required. Metric specs for the Study.

`parameters[]` ` object ( ParameterSpec  ` )

Required. The set of parameters to tune.

`algorithm` ` enum ( Algorithm  ` )

The search algorithm specified for the Study.

`observationNoise` ` enum ( ObservationNoise  ` )

The observation noise level of the study. Currently only supported by the Agent Platform Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline.

`measurementSelectionType` ` enum ( MeasurementSelectionType  ` )

Describe which measurement selection type will be used

`automated_stopping_spec` `Union type`

`automated_stopping_spec` can be only one of the following:

`decayCurveStoppingSpec` ` object ( DecayCurveAutomatedStoppingSpec  ` )

The automated early stopping spec using decay curve rule.

`medianAutomatedStoppingSpec` ` object ( MedianAutomatedStoppingSpec  ` )

The automated early stopping spec using median rule.

`convexAutomatedStoppingSpec` ` object ( ConvexAutomatedStoppingSpec  ` )

The automated early stopping spec using convex stopping rule.

`studyStoppingConfig` ` object ( StudyStoppingConfig  ` )

Conditions for automated stopping of a Study. Enable automated stopping by configuring at least one condition.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metrics&quot;: [{object (MetricSpec)}],&quot;parameters&quot;: [{object (ParameterSpec)}],&quot;algorithm&quot;: enum (Algorithm),&quot;observationNoise&quot;: enum (ObservationNoise),&quot;measurementSelectionType&quot;: enum (MeasurementSelectionType),// automated_stopping_spec&quot;decayCurveStoppingSpec&quot;: {object (DecayCurveAutomatedStoppingSpec)},&quot;medianAutomatedStoppingSpec&quot;: {object (MedianAutomatedStoppingSpec)},&quot;convexAutomatedStoppingSpec&quot;: {object (ConvexAutomatedStoppingSpec)}// Union type&quot;studyStoppingConfig&quot;: {object (StudyStoppingConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## DecayCurveAutomatedStoppingSpec

The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

Fields

`useElapsedDuration` `boolean`

True if `  Measurement.elapsed_duration  ` is used as the x-axis of each Trials Decay Curve. Otherwise, `  Measurement.step_count  ` will be used as the x-axis.

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
  &quot;useElapsedDuration&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## MedianAutomatedStoppingSpec

The median automated stopping rule stops a pending Trial if the Trial's best objectiveValue is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

Fields

`useElapsedDuration` `boolean`

True if median automated stopping rule applies on `  Measurement.elapsed_duration  ` . It means that elapsedDuration field of latest measurement of current Trial is used to compute median objective value for each completed Trials.

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
  &quot;useElapsedDuration&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## ConvexAutomatedStoppingSpec

Configuration for ConvexAutomatedStoppingSpec. When there are enough completed trials (configured by minMeasurementCount), for pending trials with enough measurements and steps, the policy first computes an overestimate of the objective value at maxNumSteps according to the slope of the incomplete objective value curve. No prediction can be made if the curve is completely flat. If the overestimation is worse than the best objective value of the completed trials, this pending trial will be early-stopped, but a last measurement will be added to the pending trial with maxNumSteps and predicted objective value from the autoregression model.

Fields

`maxStepCount` `string ( int64 format)`

Steps used in predicting the final objective for early stopped trials. In general, it's set to be the same as the defined steps in training / tuning. If not defined, it will learn it from the completed trials. When use\_steps is false, this field is set to the maximum elapsed seconds.

`minStepCount` `string ( int64 format)`

Minimum number of steps for a trial to complete. Trials which do not have a measurement with stepCount \> minStepCount won't be considered for early stopping. It's ok to set it to 0, and a trial can be early stopped at any stage. By default, minStepCount is set to be one-tenth of the maxStepCount. When useElapsedDuration is true, this field is set to the minimum elapsed seconds.

`minMeasurementCount` `string ( int64 format)`

The minimal number of measurements in a Trial. Early-stopping checks will not trigger if less than minMeasurementCount+1 completed trials or pending trials with less than minMeasurementCount measurements. If not defined, the default value is 5.

`learningRateParameterName` `string`

The hyper-parameter name used in the tuning job that stands for learning rate. Leave it blank if learning rate is not in a parameter in tuning. The learningRate is used to estimate the objective value of the ongoing trial.

`useElapsedDuration` `boolean`

This bool determines whether or not the rule is applied based on elapsed\_secs or steps. If useElapsedDuration==false, the early stopping decision is made according to the predicted objective values according to the target steps. If useElapsedDuration==true, elapsed\_secs is used instead of steps. Also, in this case, the parameters maxNumSteps and minNumSteps are overloaded to contain max\_elapsed\_seconds and min\_elapsed\_seconds.

`updateAllStoppedTrials` `boolean`

ConvexAutomatedStoppingSpec by default only updates the trials that needs to be early stopped using a newly trained auto-regressive model. When this flag is set to True, all stopped trials from the beginning are potentially updated in terms of their `finalMeasurement` . Also, note that the training logic of autoregressive models is different in this case. Enabling this option has shown better results and this may be the default option in the future.

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
  &quot;maxStepCount&quot;: string,
  &quot;minStepCount&quot;: string,
  &quot;minMeasurementCount&quot;: string,
  &quot;learningRateParameterName&quot;: string,
  &quot;useElapsedDuration&quot;: boolean,
  &quot;updateAllStoppedTrials&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## MetricSpec

Represents a metric to optimize.

Fields

`metricId` `string`

Required. The id of the metric. Must not contain whitespaces and must be unique amongst all MetricSpecs.

`goal` ` enum ( GoalType  ` )

Required. The optimization goal of the metric.

`safetyConfig` ` object ( SafetyMetricConfig  ` )

Used for safe search. In the case, the metric will be a safety metric. You must provide a separate metric for objective metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricId&quot;: string,&quot;goal&quot;: enum (GoalType),&quot;safetyConfig&quot;: {object (SafetyMetricConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## SafetyMetricConfig

Used in safe optimization to specify threshold levels and risk tolerance.

Fields

`safetyThreshold` `number`

Safety threshold (boundary value between safe and unsafe). NOTE that if you leave SafetyMetricConfig unset, a default value of 0 will be used.

`desiredMinSafeTrialsFraction` `number`

Desired minimum fraction of safe trials (over total number of trials) that should be targeted by the algorithm at any time during the study (best effort). This should be between 0.0 and 1.0 and a value of 0.0 means that there is no minimum and an algorithm proceeds without targeting any specific fraction. A value of 1.0 means that the algorithm attempts to only Suggest safe Trials.

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
  &quot;safetyThreshold&quot;: number,
  &quot;desiredMinSafeTrialsFraction&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## ParameterSpec

Represents a single parameter to optimize.

Fields

`parameterId` `string`

Required. The id of the parameter. Must not contain whitespaces and must be unique amongst all ParameterSpecs.

`scaleType` ` enum ( ScaleType  ` )

How the parameter should be scaled. Leave unset for `CATEGORICAL` parameters.

`conditionalParameterSpecs[]` ` object ( ConditionalParameterSpec  ` )

A conditional parameter node is active if the parameter's value matches the conditional node's parent\_value\_condition.

If two items in conditionalParameterSpecs have the same name, they must have disjoint parent\_value\_condition.

`parameter_value_spec` `Union type`

`parameter_value_spec` can be only one of the following:

`doubleValueSpec` ` object ( DoubleValueSpec  ` )

The value spec for a 'DOUBLE' parameter.

`integerValueSpec` ` object ( IntegerValueSpec  ` )

The value spec for an 'INTEGER' parameter.

`categoricalValueSpec` ` object ( CategoricalValueSpec  ` )

The value spec for a 'CATEGORICAL' parameter.

`discreteValueSpec` ` object ( DiscreteValueSpec  ` )

The value spec for a 'DISCRETE' parameter.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameterId&quot;: string,&quot;scaleType&quot;: enum (ScaleType),&quot;conditionalParameterSpecs&quot;: [{object (ConditionalParameterSpec)}],// parameter_value_spec&quot;doubleValueSpec&quot;: {object (DoubleValueSpec)},&quot;integerValueSpec&quot;: {object (IntegerValueSpec)},&quot;categoricalValueSpec&quot;: {object (CategoricalValueSpec)},&quot;discreteValueSpec&quot;: {object (DiscreteValueSpec)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DoubleValueSpec

value specification for a parameter in `DOUBLE` type.

Fields

`minValue` `number`

Required. Inclusive minimum value of the parameter.

`maxValue` `number`

Required. Inclusive maximum value of the parameter.

`defaultValue` `number`

A default value for a `DOUBLE` parameter that is assumed to be a relatively good starting point. Unset value signals that there is no offered starting point.

Currently only supported by the Agent Platform Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline.

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
  &quot;minValue&quot;: number,
  &quot;maxValue&quot;: number,
  &quot;defaultValue&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## IntegerValueSpec

value specification for a parameter in `INTEGER` type.

Fields

`minValue` `string ( int64 format)`

Required. Inclusive minimum value of the parameter.

`maxValue` `string ( int64 format)`

Required. Inclusive maximum value of the parameter.

`defaultValue` `string ( int64 format)`

A default value for an `INTEGER` parameter that is assumed to be a relatively good starting point. Unset value signals that there is no offered starting point.

Currently only supported by the Agent Platform Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline.

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
  &quot;minValue&quot;: string,
  &quot;maxValue&quot;: string,
  &quot;defaultValue&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## CategoricalValueSpec

value specification for a parameter in `CATEGORICAL` type.

Fields

`values[]` `string`

Required. The list of possible categories.

`defaultValue` `string`

A default value for a `CATEGORICAL` parameter that is assumed to be a relatively good starting point. Unset value signals that there is no offered starting point.

Currently only supported by the Agent Platform Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline.

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
  &quot;values&quot;: [
    string
  ],
  &quot;defaultValue&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## DiscreteValueSpec

value specification for a parameter in `DISCRETE` type.

Fields

`values[]` `number`

Required. A list of possible values. The list should be in increasing order and at least 1e-10 apart. For instance, this parameter might have possible settings of 1.5, 2.5, and 4.0. This list should not contain more than 1,000 values.

`defaultValue` `number`

A default value for a `DISCRETE` parameter that is assumed to be a relatively good starting point. Unset value signals that there is no offered starting point. It automatically rounds to the nearest feasible discrete point.

Currently only supported by the Agent Platform Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline.

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
  &quot;values&quot;: [
    number
  ],
  &quot;defaultValue&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## ConditionalParameterSpec

Represents a parameter spec with condition from its parent parameter.

Fields

`parameterSpec` ` object ( ParameterSpec  ` )

Required. The spec for a conditional parameter.

`parent_value_condition` `Union type`

A set of parameter values from the parent ParameterSpec's feasible space. `parent_value_condition` can be only one of the following:

`parentDiscreteValues` ` object ( DiscreteValueCondition  ` )

The spec for matching values from a parent parameter of `DISCRETE` type.

`parentIntValues` ` object ( IntValueCondition  ` )

The spec for matching values from a parent parameter of `INTEGER` type.

`parentCategoricalValues` ` object ( CategoricalValueCondition  ` )

The spec for matching values from a parent parameter of `CATEGORICAL` type.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameterSpec&quot;: {object (ParameterSpec)},// parent_value_condition&quot;parentDiscreteValues&quot;: {object (DiscreteValueCondition)},&quot;parentIntValues&quot;: {object (IntValueCondition)},&quot;parentCategoricalValues&quot;: {object (CategoricalValueCondition)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DiscreteValueCondition

Represents the spec to match discrete values from parent parameter.

Fields

`values[]` `number`

Required. Matches values of the parent parameter of 'DISCRETE' type. All values must exist in `discreteValueSpec` of parent parameter.

The Epsilon of the value matching is 1e-10.

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
  &quot;values&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## IntValueCondition

Represents the spec to match integer values from parent parameter.

Fields

`values[]` `string ( int64 format)`

Required. Matches values of the parent parameter of 'INTEGER' type. All values must lie in `integerValueSpec` of parent parameter.

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
  &quot;values&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## CategoricalValueCondition

Represents the spec to match categorical values from parent parameter.

Fields

`values[]` `string`

Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categoricalValueSpec` of parent parameter.

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
  &quot;values&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## StudyStoppingConfig

The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

Fields

`shouldStopAsap` `boolean`

If true, a Study enters STOPPING\_ASAP whenever it would normally enters STOPPING state.

The bottom line is: set to true if you want to interrupt on-going evaluations of Trials as soon as the study stopping condition is met. (Please see Study.State documentation for the source of truth).

`minimumRuntimeConstraint` ` object ( StudyTimeConstraint  ` )

Each "stopping rule" in this proto specifies an "if" condition. Before Vizier would generate a new suggestion, it first checks each specified stopping rule, from top to bottom in this list. Note that the first few rules (e.g. minimumRuntimeConstraint, minNumTrials) will prevent other stopping rules from being evaluated until they are met. For example, setting `minNumTrials=5` and `always_stop_after= 1 hour` means that the Study will ONLY stop after it has 5 COMPLETED trials, even if more than an hour has passed since its creation. It follows the first applicable rule (whose "if" condition is satisfied) to make a stopping decision. If none of the specified rules are applicable, then Vizier decides that the study should not stop. If Vizier decides that the study should stop, the study enters STOPPING state (or STOPPING\_ASAP if shouldStopAsap = true). IMPORTANT: The automatic study state transition happens precisely as described above; that is, deleting trials or updating StudyConfig NEVER automatically moves the study state back to ACTIVE. If you want to *resume* a Study that was stopped, 1) change the stopping conditions if necessary, 2) activate the study, and then 3) ask for suggestions. If the specified time or duration has not passed, do not stop the study.

`maximumRuntimeConstraint` ` object ( StudyTimeConstraint  ` )

If the specified time or duration has passed, stop the study.

`minNumTrials` `integer`

If there are fewer than this many COMPLETED trials, do not stop the study.

`maxNumTrials` `integer`

If there are more than this many trials, stop the study.

`maxNumTrialsNoProgress` `integer`

If the objective value has not improved for this many consecutive trials, stop the study.

WARNING: Effective only for single-objective studies.

`maxDurationNoProgress` ` string ( Duration  ` format)

If the objective value has not improved for this much time, stop the study.

WARNING: Effective only for single-objective studies.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;shouldStopAsap&quot;: boolean,&quot;minimumRuntimeConstraint&quot;: {object (StudyTimeConstraint)},&quot;maximumRuntimeConstraint&quot;: {object (StudyTimeConstraint)},&quot;minNumTrials&quot;: integer,&quot;maxNumTrials&quot;: integer,&quot;maxNumTrialsNoProgress&quot;: integer,&quot;maxDurationNoProgress&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## StudyTimeConstraint

time-based Constraint for Study

Fields

`constraint` `Union type`

`constraint` can be only one of the following:

`maxDuration` ` string ( Duration  ` format)

Counts the wallclock time passed since the creation of this Study.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endTime` ` string ( Timestamp  ` format)

Compares the wallclock time to this time. Must use UTC timezone.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // constraint
  &quot;maxDuration&quot;: string,
  &quot;endTime&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>
