---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec
title: ExplanationSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specification of Model explanation.

Fields

`parameters` `object ( `[`ExplanationParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters)` )`

Required. Parameters that configure explaining of the Model's predictions.

`metadata` `object ( `[`ExplanationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationMetadata)` )`

Optional. metadata describing the Model's input and output for explanation.

**JSON representation**

```
{
  "parameters": {
    object (ExplanationParameters)
  },
  "metadata": {
    object (ExplanationMetadata)
  }
}
```

## ExplanationParameters

Parameters to configure explaining for Model's predictions.

Fields

`topK` `integer`

If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs.

`outputIndices` `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)`

If populated, only returns attributions that have [`outputIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_index) contained in outputIndices. It must be an ndarray of integers, with the same shape of the output it's explaining.

If not populated, returns attributions for [`topK`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.top_k) indices of outputs. If neither topK nor outputIndices is populated, returns the argmax index of the outputs.

Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes).

`method` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`sampledShapleyAttribution` `object ( `[`SampledShapleyAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SampledShapleyAttribution)` )`

An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: <https://arxiv.org/abs/1306.4265> .

`integratedGradientsAttribution` `object ( `[`IntegratedGradientsAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#IntegratedGradientsAttribution)` )`

An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>

`xraiAttribution` `object ( `[`XraiAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#XraiAttribution)` )`

An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825>

XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead.

`examples` `object ( `[`Examples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Examples)` )`

Example-based explanations that returns the nearest neighbors from the provided dataset.

End of mutually exclusive fields.

**JSON representation**

```
{
  "topK": integer,
  "outputIndices": array,

  // method
  "sampledShapleyAttribution": {
    object (SampledShapleyAttribution)
  },
  "integratedGradientsAttribution": {
    object (IntegratedGradientsAttribution)
  },
  "xraiAttribution": {
    object (XraiAttribution)
  },
  "examples": {
    object (Examples)
  }
  // Union type
}
```

## SampledShapleyAttribution

An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features.

Fields

`pathCount` `integer`

Required. The number of feature permutations to consider when approximating the Shapley values.

Valid range of its value is \[1, 50\], inclusively.

**JSON representation**

```
{
  "pathCount": integer
}
```

## IntegratedGradientsAttribution

An attribution method that computes the Aumann-Shapley value taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>

Fields

`stepCount` `integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig` `object ( `[`SmoothGradConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SmoothGradConfig)` )`

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig` `object ( `[`BlurBaselineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#BlurBaselineConfig)` )`

Config for IG with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

**JSON representation**

```
{
  "stepCount": integer,
  "smoothGradConfig": {
    object (SmoothGradConfig)
  },
  "blurBaselineConfig": {
    object (BlurBaselineConfig)
  }
}
```

## SmoothGradConfig

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

Fields

`noisySampleCount` `integer`

The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is \[1, 50\]. Defaults to 3.

`GradientNoiseSigma` `Union type`

Represents the standard deviation of the gaussian kernel that will be used to add noise to the interpolated inputs prior to computing gradients. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`noiseSigma` `number`

This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range \[0, 1\], \[-1, 1\] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about [normalization](https://developers.google.com/machine-learning/data-prep/transform/normalization) .

For best results the recommended value is about 10% - 20% of the standard deviation of the input feature. Refer to section 3.2 of the SmoothGrad paper: <https://arxiv.org/pdf/1706.03825.pdf> . Defaults to 0.1.

If the distribution is different per feature, set [`featureNoiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SmoothGradConfig.FIELDS.feature_noise_sigma) instead for each feature.

`featureNoiseSigma` `object ( `[`FeatureNoiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#FeatureNoiseSigma)` )`

This is similar to [`noiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SmoothGradConfig.FIELDS.noise_sigma) , but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, [`noiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SmoothGradConfig.FIELDS.noise_sigma) will be used for all features.

End of mutually exclusive fields.

**JSON representation**

```
{
  "noisySampleCount": integer,

  // GradientNoiseSigma
  "noiseSigma": number,
  "featureNoiseSigma": {
    object (FeatureNoiseSigma)
  }
  // Union type
}
```

## FeatureNoiseSigma

Noise sigma by features. Noise sigma represents the standard deviation of the gaussian kernel that will be used to add noise to interpolated inputs prior to computing gradients.

Fields

`noiseSigma[]` `object ( `[`NoiseSigmaForFeature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#NoiseSigmaForFeature)` )`

Noise sigma per feature. No noise is added to features that are not set.

**JSON representation**

```
{
  "noiseSigma": [
    {
      object (NoiseSigmaForFeature)
    }
  ]
}
```

## NoiseSigmaForFeature

Noise sigma for a single feature.

Fields

`name` `string`

The name of the input feature for which noise sigma is provided. The features are defined in [`explanation metadata inputs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationMetadata.FIELDS.inputs) .

`sigma` `number`

This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to [`noiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SmoothGradConfig.FIELDS.noise_sigma) but represents the noise added to the current feature. Defaults to 0.1.

**JSON representation**

```
{
  "name": string,
  "sigma": number
}
```

## BlurBaselineConfig

Config for blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

Fields

`maxBlurSigma` `number`

The standard deviation of the blur kernel for the blurred baseline. The same blurring parameter is used for both the height and the width dimension. If not set, the method defaults to the zero (i.e. black for images) baseline.

**JSON representation**

```
{
  "maxBlurSigma": number
}
```

## XraiAttribution

An explanation method that redistributes Integrated Gradients attributions to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825>

Supported only by image Models.

Fields

`stepCount` `integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig` `object ( `[`SmoothGradConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#SmoothGradConfig)` )`

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig` `object ( `[`BlurBaselineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#BlurBaselineConfig)` )`

Config for XRAI with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

**JSON representation**

```
{
  "stepCount": integer,
  "smoothGradConfig": {
    object (SmoothGradConfig)
  },
  "blurBaselineConfig": {
    object (BlurBaselineConfig)
  }
}
```

## Examples

Example-based explainability that returns the nearest neighbors from the provided dataset.

Fields

`neighborCount` `integer`

The number of neighbors to return when querying for examples.

`source` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`exampleGcsSource` `object ( `[`ExampleGcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExampleGcsSource)` )`

The Cloud Storage input instances.

End of mutually exclusive fields.

`config` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`nearestNeighborSearchConfig` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

The full configuration for the generated index, the semantics are the same as [`metadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes#Index.FIELDS.metadata) and should match [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-example-based#nearest-neighbor-search-config) .

`presets` `object ( `[`Presets`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Presets)` )`

Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality.

End of mutually exclusive fields.

**JSON representation**

```
{
  "neighborCount": integer,

  // source
  "exampleGcsSource": {
    object (ExampleGcsSource)
  }
  // Union type

  // config
  "nearestNeighborSearchConfig": value,
  "presets": {
    object (Presets)
  }
  // Union type
}
```

## ExampleGcsSource

The Cloud Storage input instances.

Fields

`dataFormat` `enum ( `[`DataFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#DataFormat)` )`

The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported.

`gcsSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GcsSource)` )`

The Cloud Storage location for the input instances.

**JSON representation**

```
{
  "dataFormat": enum (DataFormat),
  "gcsSource": {
    object (GcsSource)
  }
}
```

## DataFormat

The format of the input example instances.

| Enums                     |                                      |
|---------------------------|--------------------------------------|
| `DATA_FORMAT_UNSPECIFIED` | Format unspecified, used when unset. |
| `JSONL`                   | Examples are stored in JSONL files.  |

## Presets

Preset configuration for example-based explanations

Fields

`modality` `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Modality)` )`

The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type.

`query` `enum ( `[`Query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Query)` )`

Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .

**JSON representation**

```
{
  "modality": enum (Modality),
  "query": enum (Query)
}
```

## Query

Preset option controlling parameters for query speed-precision trade-off

| Enums     |                                                                |
|-----------|----------------------------------------------------------------|
| `PRECISE` | More precise neighbors as a trade-off against slower response. |
| `FAST`    | Faster response as a trade-off against less precise neighbors. |

## Modality

Preset option controlling parameters for different modalities

| Enums                  |                                                                   |
|------------------------|-------------------------------------------------------------------|
| `MODALITY_UNSPECIFIED` | Should not be set. Added as a recommended best practice for enums |
| `IMAGE`                | IMAGE modality                                                    |
| `TEXT`                 | TEXT modality                                                     |
| `TABULAR`              | TABULAR modality                                                  |

## ExplanationMetadata

metadata describing the Model's input and output for explanation.

Fields

`inputs` `map (key: string, value: object ( `[`InputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata)` ))`

Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature.

An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in [`ExplanationMetadata.inputs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationMetadata.FIELDS.inputs) . The baseline of the empty feature is chosen by Agent Platform.

For Agent Platform-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, [`featureAttributions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.feature_attributions) are keyed by this key (if not grouped with another feature).

For custom images, the key must match with the key in [`instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#body.request_body.FIELDS.instances) .

`outputs` `map (key: string, value: object ( `[`OutputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#OutputMetadata)` ))`

Required. Map from output names to output metadata.

For Agent Platform-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters.

For custom images, keys are the name of the output field in the prediction to be explained.

Currently only one key is allowed.

`featureAttributionsSchemaUri` `string`

Points to a YAML file stored on Google Cloud Storage describing the format of the [`feature attributions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.feature_attributions) . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML tabular Models always have this field populated by Agent Platform. Note: The URI given on output may be different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`latentSpaceSource` `string`

name of the source to generate embeddings for example based explanations.

**JSON representation**

```
{
  "inputs": {
    string: {
      object (InputMetadata)
    },
    ...
  },
  "outputs": {
    string: {
      object (OutputMetadata)
    },
    ...
  },
  "featureAttributionsSchemaUri": string,
  "latentSpaceSource": string
}
```

## InputMetadata

metadata of the input of a feature.

Fields other than [`InputMetadata.input_baselines`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.input_baselines) are applicable only for Models that are using Agent Platform-provided images for Tensorflow.

Fields

`inputBaselines[]` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

baseline inputs for this feature.

If no baseline is specified, Agent Platform chooses the baseline for this feature. If multiple baselines are specified, Agent Platform returns the average attributions across them in [`Attribution.feature_attributions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.feature_attributions) .

For Agent Platform-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor.

For custom images, the element of the baselines must be in the same format as the feature's input in the [`instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#body.request_body.FIELDS.instances) \[\]. The schema of any single instance may be specified via Endpoint's DeployedModels' [`Model's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.model) [`PredictSchemata's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.predict_schemata) [`instanceSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PredictSchemata#FIELDS.instance_schema_uri) .

`inputTensorName` `string`

name of the input tensor for this feature. Required and is only applicable to Agent Platform-provided images for Tensorflow.

`encoding` `enum ( `[`Encoding`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Encoding)` )`

Defines how the feature is encoded into the input tensor. Defaults to IDENTITY.

`modality` `string`

Modality of the feature. Valid values are: numeric, image. Defaults to numeric.

`featureValueDomain` `object ( `[`FeatureValueDomain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#FeatureValueDomain)` )`

The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized.

`indicesTensorName` `string`

Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`denseShapeTensorName` `string`

Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`indexFeatureMapping[]` `string`

A list of feature names for each index in the input tensor. Required when the input [`InputMetadata.encoding`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.encoding) is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR.

`encodedTensorName` `string`

Encoded tensor is a transformation of the input tensor. Must be provided if choosing [`Integrated Gradients attribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.integrated_gradients_attribution) or [`XRAI attribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.xrai_attribution) and the input tensor is not differentiable.

An encoded tensor is generated if the input tensor is encoded by a lookup table.

`encodedBaselines[]` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

A list of baselines for the encoded tensor.

The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Agent Platform broadcasts to the same shape as the encoded tensor.

`visualization` `object ( `[`Visualization`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Visualization)` )`

Visualization configurations for image explanation.

`groupName` `string`

name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in [`Attribution.feature_attributions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.feature_attributions) , keyed by the group name.

**JSON representation**

```
{
  "inputBaselines": [
    value
  ],
  "inputTensorName": string,
  "encoding": enum (Encoding),
  "modality": string,
  "featureValueDomain": {
    object (FeatureValueDomain)
  },
  "indicesTensorName": string,
  "denseShapeTensorName": string,
  "indexFeatureMapping": [
    string
  ],
  "encodedTensorName": string,
  "encodedBaselines": [
    value
  ],
  "visualization": {
    object (Visualization)
  },
  "groupName": string
}
```

## Encoding

Defines how a feature is encoded. Defaults to IDENTITY.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ENCODING_UNSPECIFIED</code></td>
<td>Default value. This is the same as IDENTITY.</td>
</tr>
<tr class="even">
<td><code>IDENTITY</code></td>
<td>The tensor represents one feature.</td>
</tr>
<tr class="odd">
<td><code>BAG_OF_FEATURES</code></td>
<td><p>The tensor represents a bag of features where each index maps to a feature. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.index_feature_mapping"><code>InputMetadata.index_feature_mapping</code></a> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [27, 6.0, 150]
indexFeatureMapping = [&quot;age&quot;, &quot;height&quot;, &quot;weight&quot;]</code></pre></td>
</tr>
<tr class="even">
<td><code>BAG_OF_FEATURES_SPARSE</code></td>
<td><p>The tensor represents a bag of features where each index maps to a feature. Zero values in the tensor indicates feature being non-existent. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.index_feature_mapping"><code>InputMetadata.index_feature_mapping</code></a> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [2, 0, 5, 0, 1]
indexFeatureMapping = [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;]</code></pre></td>
</tr>
<tr class="odd">
<td><code>INDICATOR</code></td>
<td><p>The tensor is a list of binaries representing whether a feature exists or not (1 indicates existence). <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.index_feature_mapping"><code>InputMetadata.index_feature_mapping</code></a> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [1, 0, 1, 0, 1]
indexFeatureMapping = [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;]</code></pre></td>
</tr>
<tr class="even">
<td><code>COMBINED_EMBEDDING</code></td>
<td><p>The tensor is encoded into a 1-dimensional array represented by an encoded tensor. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.encoded_tensor_name"><code>InputMetadata.encoded_tensor_name</code></a> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;, &quot;.&quot;]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]</code></pre></td>
</tr>
<tr class="odd">
<td><code>CONCAT_EMBEDDING</code></td>
<td><p>Select this encoding when the input tensor is encoded into a 2-dimensional array represented by an encoded tensor. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#InputMetadata.FIELDS.encoded_tensor_name"><code>InputMetadata.encoded_tensor_name</code></a> must be provided for this encoding. The first dimension of the encoded tensor's shape is the same as the input tensor's shape. For example:</p>
<pre data-fenced=""><code>input = [&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;, &quot;.&quot;]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
           [0.2, 0.1, 0.4, 0.3, 0.5],
           [0.5, 0.1, 0.3, 0.5, 0.4],
           [0.5, 0.3, 0.1, 0.2, 0.4],
           [0.4, 0.3, 0.2, 0.5, 0.1]]</code></pre></td>
</tr>
</tbody>
</table>

## FeatureValueDomain

domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then originalMean, and originalStddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

Fields

`minValue` `number`

The minimum permissible value for this feature.

`maxValue` `number`

The maximum permissible value for this feature.

`originalMean` `number`

If this input feature has been normalized to a mean value of 0, the originalMean specifies the mean value of the domain prior to normalization.

`originalStddev` `number`

If this input feature has been normalized to a standard deviation of 1.0, the originalStddev specifies the standard deviation of the domain prior to normalization.

**JSON representation**

```
{
  "minValue": number,
  "maxValue": number,
  "originalMean": number,
  "originalStddev": number
}
```

## Visualization

Visualization configurations for image explanation.

Fields

`type` `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Type)` )`

type of the image visualization. Only applicable to [`Integrated Gradients attribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.integrated_gradients_attribution) . OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES.

`polarity` `enum ( `[`Polarity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#Polarity)` )`

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

`colorMap` `enum ( `[`ColorMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ColorMap)` )`

The color scheme used for the highlighted areas.

Defaults to PINK_GREEN for [`Integrated Gradients attribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.integrated_gradients_attribution) , which shows positive attributions in green and negative in pink.

Defaults to VIRIDIS for [`XRAI attribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.xrai_attribution) , which highlights the most influential regions in yellow and the least influential in blue.

`clipPercentUpperbound` `number`

Excludes attributions above the specified percentile from the highlighted areas. Using the clipPercentUpperbound and clipPercentLowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9.

`clipPercentLowerbound` `number`

Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62.

`overlayType` `enum ( `[`OverlayType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#OverlayType)` )`

How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE.

**JSON representation**

```
{
  "type": enum (Type),
  "polarity": enum (Polarity),
  "colorMap": enum (ColorMap),
  "clipPercentUpperbound": number,
  "clipPercentLowerbound": number,
  "overlayType": enum (OverlayType)
}
```

## Type

type of the image visualization. Only applicable to [`Integrated Gradients attribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec#ExplanationParameters.FIELDS.integrated_gradients_attribution) .

| Enums              |                                                                                 |
|--------------------|---------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Should not be used.                                                             |
| `PIXELS`           | Shows which pixel contributed to the image prediction.                          |
| `OUTLINES`         | Shows which region contributed to the image prediction by outlining the region. |

## Polarity

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

| Enums                  |                                                                                                      |
|------------------------|------------------------------------------------------------------------------------------------------|
| `POLARITY_UNSPECIFIED` | Default value. This is the same as POSITIVE.                                                         |
| `POSITIVE`             | Highlights the pixels/outlines that were most influential to the model's prediction.                 |
| `NEGATIVE`             | Setting polarity to negative highlights areas that does not lead to the models's current prediction. |
| `BOTH`                 | Shows both positive and negative attributions.                                                       |

## ColorMap

The color scheme used for highlighting areas.

| Enums                   |                                                                                                                                                                                            |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `COLOR_MAP_UNSPECIFIED` | Should not be used.                                                                                                                                                                        |
| `PINK_GREEN`            | Positive: green. Negative: pink.                                                                                                                                                           |
| `VIRIDIS`               | Viridis color map: A perceptually uniform color mapping which is easier to see by those with colorblindness and progresses from yellow to green to blue. Positive: yellow. Negative: blue. |
| `RED`                   | Positive: red. Negative: red.                                                                                                                                                              |
| `GREEN`                 | Positive: green. Negative: green.                                                                                                                                                          |
| `RED_GREEN`             | Positive: green. Negative: red.                                                                                                                                                            |
| `PINK_WHITE_GREEN`      | PiYG palette.                                                                                                                                                                              |

## OverlayType

How the original image is displayed in the visualization.

| Enums                      |                                                                                                               |
|----------------------------|---------------------------------------------------------------------------------------------------------------|
| `OVERLAY_TYPE_UNSPECIFIED` | Default value. This is the same as NONE.                                                                      |
| `NONE`                     | No overlay.                                                                                                   |
| `ORIGINAL`                 | The attributions are shown on top of the original image.                                                      |
| `GRAYSCALE`                | The attributions are shown on top of grayscaled version of the original image.                                |
| `MASK_BLACK`               | The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

## OutputMetadata

metadata of the prediction output to be explained.

Fields

`outputTensorName` `string`

name of the output tensor. Required and is only applicable to Agent Platform provided images for Tensorflow.

`display_name_mapping` `Union type`

Defines how to map [`Attribution.output_index`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_index) to [`Attribution.output_display_name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_display_name) .

If neither of the fields are specified, [`Attribution.output_display_name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_display_name) will not be populated. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`indexDisplayNameMapping` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Static mapping between the index and display name.

Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values.

The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The [`Attribution.output_display_name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_display_name) is populated by locating in the mapping with [`Attribution.output_index`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_index) .

`displayNameMappingKey` `string`

Specify a field name in the prediction to look for the display name.

Use this if the prediction contains the display names for the outputs.

The display names in the prediction must have the same shape of the outputs, so that it can be located by [`Attribution.output_index`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation#Attribution.FIELDS.output_index) for a specific output.

End of mutually exclusive fields.

**JSON representation**

```
{
  "outputTensorName": string,

  // display_name_mapping
  "indexDisplayNameMapping": value,
  "displayNameMappingKey": string
  // Union type
}
```
