---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport
title: 'Method: slices.batchImport'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.evaluations.slices.batchImport

Imports a list of externally generated EvaluatedAnnotations.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent}:batchImport`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the parent ModelEvaluationSlice resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}/slices/{slice}`

### Request body

The request body contains data with the following structure:

Fields

`evaluatedAnnotations[]` `object ( `[`EvaluatedAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation)` )`

Required. Evaluated annotations resource to be imported.

### Response body

Response message for [`ModelService.BatchImportEvaluatedAnnotations`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#google.cloud.aiplatform.v1beta1.ModelService.BatchImportEvaluatedAnnotations)

If successful, the response body contains data with the following structure:

Fields

`importedEvaluatedAnnotationsCount` `integer`

Output only. Number of EvaluatedAnnotations imported.

**JSON representation**

```
{
  "importedEvaluatedAnnotationsCount": integer
}
```

## EvaluatedAnnotation

True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice with slice of `annotationSpec` dimension.

Fields

`type` `enum ( `[`EvaluatedAnnotationType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotationType)` )`

Output only. type of the EvaluatedAnnotation.

`predictions[]` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Output only. The model predicted annotations.

For true positive, there is one and only one prediction, which matches the only one ground truth annotation in [`groundTruths`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.ground_truths) .

For false positive, there is one and only one prediction, which doesn't match any ground truth annotation of the corresponding [`data_item_view_id`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.evaluated_data_item_view_id) .

For false negative, there are zero or more predictions which are similar to the only ground truth annotation in [`groundTruths`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.ground_truths) but not enough for a match.

The schema of the prediction is stored in \[ModelEvaluation.annotation_schema_uri\]\[\]

`groundTruths[]` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Output only. The ground truth Annotations, i.e. the Annotations that exist in the test data the Model is evaluated on.

For true positive, there is one and only one ground truth annotation, which matches the only prediction in [`predictions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.predictions) .

For false positive, there are zero or more ground truth annotations that are similar to the only prediction in [`predictions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.predictions) , but not enough for a match.

For false negative, there is one and only one ground truth annotation, which doesn't match any predictions created by the model.

The schema of the ground truth is stored in \[ModelEvaluation.annotation_schema_uri\]\[\]

`dataItemPayload` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Output only. The data item payload that the Model predicted this EvaluatedAnnotation on.

`evaluatedDataItemViewId` `string`

Output only. id of the EvaluatedDataItemView under the same ancestor ModelEvaluation. The EvaluatedDataItemView consists of all ground truths and predictions on [`dataItemPayload`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.data_item_payload) .

`explanations[]` `object ( `[`EvaluatedAnnotationExplanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotationExplanation)` )`

Explanations of [`predictions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.predictions) . Each element of the explanations indicates the explanation for one explanation method.

The attributions list in the [`EvaluatedAnnotationExplanation.explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotationExplanation.FIELDS.explanation) object corresponds to the [`predictions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#EvaluatedAnnotation.FIELDS.predictions) list. For example, the second element in the attributions list explains the second element in the predictions list.

`errorAnalysisAnnotations[]` `object ( `[`ErrorAnalysisAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#ErrorAnalysisAnnotation)` )`

Annotations of model error analysis results.

**JSON representation**

```
{
  "type": enum (EvaluatedAnnotationType),
  "predictions": [
    value
  ],
  "groundTruths": [
    value
  ],
  "dataItemPayload": value,
  "evaluatedDataItemViewId": string,
  "explanations": [
    {
      object (EvaluatedAnnotationExplanation)
    }
  ],
  "errorAnalysisAnnotations": [
    {
      object (ErrorAnalysisAnnotation)
    }
  ]
}
```

## EvaluatedAnnotationType

Describes the type of the EvaluatedAnnotation. The type is determined

| Enums                                   |                                                                                                                                                  |
|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `EVALUATED_ANNOTATION_TYPE_UNSPECIFIED` | Invalid value.                                                                                                                                   |
| `TRUE_POSITIVE`                         | The EvaluatedAnnotation is a true positive. It has a prediction created by the Model and a ground truth Annotation which the prediction matches. |
| `FALSE_POSITIVE`                        | The EvaluatedAnnotation is false positive. It has a prediction created by the Model which does not match any ground truth annotation.            |
| `FALSE_NEGATIVE`                        | The EvaluatedAnnotation is false negative. It has a ground truth annotation which is not matched by any of the model created predictions.        |

## EvaluatedAnnotationExplanation

Explanation result of the prediction produced by the Model.

Fields

`explanationType` `string`

Explanation type.

For AutoML Image Classification models, possible values are:

- `image-integrated-gradients`
- `image-xrai`

`explanation` `object ( `[`Explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Explanation)` )`

Explanation attribution response details.

**JSON representation**

```
{
  "explanationType": string,
  "explanation": {
    object (Explanation)
  }
}
```

## ErrorAnalysisAnnotation

Model error analysis for each annotation.

Fields

`attributedItems[]` `object ( `[`AttributedItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#AttributedItem)` )`

Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

`queryType` `enum ( `[`QueryType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/batchImport#QueryType)` )`

The query type used for finding the attributed items.

`outlierScore` `number`

The outlier score of this annotated item. Usually defined as the min of all distances from attributed items.

`outlierThreshold` `number`

The threshold used to determine if this annotation is an outlier or not.

**JSON representation**

```
{
  "attributedItems": [
    {
      object (AttributedItem)
    }
  ],
  "queryType": enum (QueryType),
  "outlierScore": number,
  "outlierThreshold": number
}
```

## AttributedItem

Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

Fields

`annotationResourceName` `string`

The unique id for each annotation. Used by FE to allocate the annotation in DB.

`distance` `number`

The distance of this item to the annotation.

**JSON representation**

```
{
  "annotationResourceName": string,
  "distance": number
}
```

## QueryType

The query type used for finding the attributed items.

| Enums                    |                                                                   |
|--------------------------|-------------------------------------------------------------------|
| `QUERY_TYPE_UNSPECIFIED` | Unspecified query type for model error analysis.                  |
| `ALL_SIMILAR`            | Query similar samples across all classes in the dataset.          |
| `SAME_CLASS_SIMILAR`     | Query similar samples from the same class of the input sample.    |
| `SAME_CLASS_DISSIMILAR`  | Query dissimilar samples from the same class of the input sample. |
