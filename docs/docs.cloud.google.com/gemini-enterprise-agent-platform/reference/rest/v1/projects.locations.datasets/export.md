---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export
title: 'Method: datasets.export'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.export

Exports data from a Dataset.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:export`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Request body

The request body contains data with the following structure:

Fields

`exportConfig` `object ( `[`ExportDataConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig)` )`

Required. The desired output location.

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

## ExportDataConfig

Describes what part of the Dataset is to be exported, the destination of the export and how to export.

Fields

`annotationsFilter` `string`

An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in [`ListAnnotations`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.dataItems.annotations/list#google.cloud.aiplatform.v1.DatasetService.ListAnnotations) .

`savedQueryId` `string`

The id of a SavedQuery (annotation set) under the Dataset specified by [`ExportDataRequest.name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#body.PATH_PARAMETERS.name) used for filtering Annotations for training.

Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries.

Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with [`annotationsFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.annotations_filter) , the Annotations used for training are filtered by both [`savedQueryId`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.saved_query_id) and [`annotationsFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.annotations_filter) .

Only one of [`savedQueryId`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.saved_query_id) and [`annotationSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.annotation_schema_uri) should be specified as both of them represent the same thing: problem type.

`annotationSchemaUri` `string`

The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with [`metadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets#Dataset.FIELDS.metadata_schema_uri) of the Dataset specified by [`ExportDataRequest.name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#body.PATH_PARAMETERS.name) .

Only used for custom training data export use cases. Only applicable to Datasets that have DataItems and Annotations.

Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on.

When used in conjunction with [`annotationsFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.annotations_filter) , the Annotations used for training are filtered by both [`annotationsFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.annotations_filter) and [`annotationSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportDataConfig.FIELDS.annotation_schema_uri) .

`exportUse` `enum ( `[`ExportUse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportUse)` )`

Indicates the usage of the exported files.

`destination` `Union type`

The destination of the output. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsDestination` `object ( `[`GcsDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec#GcsDestination)` )`

The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: `export-data-<dataset-display-name>-<timestamp-of-export-call>` where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format. All export output will be written into that directory. Inside that directory, annotations with the same schema will be grouped into sub directories which are named with the corresponding annotations' schema title. Inside these sub directories, a schema.yaml will be created to describe the output format.

End of mutually exclusive fields.

`split` `Union type`

The instructions how the export data should be split between the training, validation and test sets. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`fractionSplit` `object ( `[`ExportFractionSplit`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportFractionSplit)` )`

Split based on fractions defining the size of each set.

`filterSplit` `object ( `[`ExportFilterSplit`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#ExportFilterSplit)` )`

Split based on the provided filters for each set.

End of mutually exclusive fields.

**JSON representation**

```
{
  "annotationsFilter": string,
  "savedQueryId": string,
  "annotationSchemaUri": string,
  "exportUse": enum (ExportUse),

  // destination
  "gcsDestination": {
    object (GcsDestination)
  }
  // Union type

  // split
  "fractionSplit": {
    object (ExportFractionSplit)
  },
  "filterSplit": {
    object (ExportFilterSplit)
  }
  // Union type
}
```

## ExportFractionSplit

Assigns the input data to training, validation, and test sets as per the given fractions. Any of `trainingFraction` , `validationFraction` and `testFraction` may optionally be provided, they must sum to up to 1. If the provided ones sum to less than 1, the remainder is assigned to sets as decided by Agent Platform. If none of the fractions are set, by default roughly 80% of data is used for training, 10% for validation, and 10% for test.

Fields

`trainingFraction` `number`

The fraction of the input data that is to be used to train the Model.

`validationFraction` `number`

The fraction of the input data that is to be used to validate the Model.

`testFraction` `number`

The fraction of the input data that is to be used to evaluate the Model.

**JSON representation**

```
{
  "trainingFraction": number,
  "validationFraction": number,
  "testFraction": number
}
```

## ExportFilterSplit

Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.

Fields

`trainingFilter` `string`

Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in [`DatasetService.ListDataItems`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.dataItems/list#google.cloud.aiplatform.v1.DatasetService.ListDataItems) may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order.

`validationFilter` `string`

Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in [`DatasetService.ListDataItems`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.dataItems/list#google.cloud.aiplatform.v1.DatasetService.ListDataItems) may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order.

`testFilter` `string`

Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in [`DatasetService.ListDataItems`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.dataItems/list#google.cloud.aiplatform.v1.DatasetService.ListDataItems) may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order.

**JSON representation**

```
{
  "trainingFilter": string,
  "validationFilter": string,
  "testFilter": string
}
```

## ExportUse

ExportUse indicates the usage of the exported files. It restricts file destination, format, annotations to be exported, whether to allow unannotated data to be exported and whether to clone files to temp Cloud Storage bucket.

| Enums                    |                                  |
|--------------------------|----------------------------------|
| `EXPORT_USE_UNSPECIFIED` | Regular user export.             |
| `CUSTOM_CODE_TRAINING`   | Export for custom code training. |
