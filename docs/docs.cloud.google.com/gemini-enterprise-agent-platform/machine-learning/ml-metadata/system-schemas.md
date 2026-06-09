---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/system-schemas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/system-schemas
title: System schemas
description: Access system schemas as MetadataSchema resources in the Vertex ML Metadata API.
data_source: docs.cloud.google.com
---

Each metadata resource is associated with a specific [MetadataSchema](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/data-model) . To simplify the metadata resource creation process Vertex ML Metadata publishes predefined types called system schemas for common ML concepts. System schemas live under the namespace `system` . You can access system schemas as MetadataSchema resources in the Vertex ML Metadata API. Schemas are always versioned. The format of system schemas is a subset of the [OpenAPI 3.0 specification](https://swagger.io/specification/#schema-object) .

## How to use system schemas

Gemini Enterprise Agent Platform uses system schemas to create metadata resources for tracking your ML workflows. You can then filter and group resources in metadata queries by using the `schema_title` field. For more information about how to use filter functions, see [Analyze Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing) .

You can also use system schemas through the Vertex ML Metadata API to create metadata resources directly. You can identify a system schema by its schema title and schema version. Fields in system schemas are always considered optional. You aren't restricted to the predefined fields of system schemas and can also log additional arbitrary metadata to any metadata resource. For more information about using system schemas to create metadata resources, see [Track Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/tracking) .

### List your schemas

To view a list of all your existing registered schemas using the following command.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/default/metadataSchemas?pageSize=100&filter=schema_title=%22system*%22+OR+schema_title=%22google*%22

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/default/metadataSchemas?pageSize=100&filter=schema_title=%22system*%22+OR+schema_title=%22google*%22"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/default/metadataSchemas?pageSize=100&filter=schema_title=%22system*%22+OR+schema_title=%22google*%22" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "metadataSchemas": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/default/metadataSchemas/system-resolver-execution-v0-0-1",
          "schemaVersion": "0.0.1",
          "schema": "title: system.ResolverExecution\ntype: object\n",
          "schemaType": "EXECUTION_TYPE",
          "createTime": "2022-07-27T17:41:35.634Z"
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID//metadataStores/default/metadataSchemas/system-html-v0-0-1",
          "schemaVersion": "0.0.1",
          "schema": "title: system.HTML\ntype: object\n",
          "schemaType": "ARTIFACT_TYPE",
          "createTime": "2022-07-27T17:41:35.602Z"
        }
    }

### Strict schema matching

Vertex ML Metadata supports two flags that allow schema authors to enforce strict schema matching.

**additionalProperties**

The `additionalProperties` value can be true or false. Consistent with JSON Schema, `additionalProperties` defaults to true. This flag is set at the top level of the schema. If it's set to false, no optional properties are allowed. For example in the below schema, only the fields `payload_format` and `container_format` are accepted in the metadata based on this schema.

    title: system.Dataset
    version: 0.0.1
    type: object
    additionalProperties: false
    properties:
      container_format:
        type: string
      payload_format:
        type: string

The above schema accepts the following metadata:

    fields {
      key: 'container_format'
      value: { string_value: 'Text' }
    }
    fields {
      key: 'payload_format'
      value: { string_value: 'CSV' }
    }

However following metadata will be rejected:

    fields {
      key: 'container_format'
      value: { string_value: 'Text' }
    }
    fields {
      key: 'payload_format'
      value: { string_value: 'CSV' }
    }
    fields {
      key: 'optional_field'
      value: { string_value: 'optional_value' }
    }

**required**

The `required` keyword takes an array of zero or more strings. Consistent with JSON Schema, the properties defined by the properties keyword are not required. You can provide a list of required properties using the `required` keyword. For example the following schema always requires `container_format` . Works on nested properties as well. For example following makes the `container_format` required.

    title: system.Dataset
    version: 0.0.1
    type: object
    required: ['container_format']
    properties:
      container_format:
        type: string
      payload_format:
        type: string

The above schema accepts the following metadata:

    fields {
      key: 'container_format'
      value: { string_value: 'Text' }
    }

However following metadata will be rejected:

    fields {
      key: 'payload_format'
      value: { string_value: 'CSV' }
    }

The schema supports nested properties where properties has a field of type object. In a nested schema, the nested properties node can have a `required` keyword. For example:

    title: system.Dataset
    version: 0.0.1
    type: object
    properties:
      container_format:
        type: string
      payload:
        type: string
      nested_property:
        type: object
        required: ['property_1']
        properties:
          property_1:
            type: integer
          property_2:
            type: integer

The above schema accepts the following metadata, since the `nested_property` field itself is not required.

    fields {
      key: 'container_format'
      value: { string_value: 'Text' }
    }

Following metadata is also valid.

    fields {
      key: 'nested_property'
      value: {
        struct_value {
          fields {
            key: 'property_1'
            value: { number_value: 1 }
          }
          fields {
            key: 'property_2'
            value: { number_value: 1 }
          }
        }
      }
    }

However following metadata will be rejected:

    fields {
      key: 'nested_property'
      value: {
        struct_value {
          fields {
            key: 'property_2'
            value: { number_value: 1 }
          }
        }
      }
    }

### System schema examples

The following examples are common system schemas that are available for immediate use.

**Artifact**

`system.Artifact` is a generic schema that can hold metadata about any artifact. No specific fields are defined in this schema.

    title: system.Artifact
    version: 0.0.1
    type: object

**Dataset**

`system.Dataset` represents a container of data that was either consumed or produced by an ML workflow step. A dataset can point to either a file location or a query, for example a BigQuery URI.

    title: system.Dataset
    version: 0.0.1
    type: object
    properties:
      container_format:
        type: string
        description: "Format of the container. Examples include 'TFRecord', 'Text', or 'Parquet'."
      payload_format:
        type: string
       description: "Format of the payload. For example, 'proto:TFExample', 'CSV', or 'JSON'."

**Model**

`system.Model` represents a trained model. The URI of the model can point to a file location (PPP, Cloud Storage bucket, local drive) or an API resource such as the Model resource in Agent Platform API.

    title: system.Model
    version: 0.0.1
    type: object
    properties:
      framework:
        type: string
        description: "The framework type. For example: 'TensorFlow' or 'Scikit-Learn'."
      framework_version:
        type: string
        description: "The framework version. For example: '1.15' or '2.1'."
      payload_format:
        type: string
        description: "The format of the Model payload, for example: 'SavedModel' or 'TFLite'."

**Metrics**

`system.Metrics` represents evaluation metrics produced during an ML workflow. Metrics are application and use case dependent and can consist of simple scalar metrics like accuracy or complex metrics that are stored elsewhere in the system.

    title: system.Metrics
    version: 0.0.1
    type: object
    properties:
      type:
      accuracy:
        type: number
        description: "Optional summary metric describing accuracy of a model."
      precision:
        type: number
        description: "Optional summary metric describing precision of a model."
      recall:
        type: number
        description: "Optional summary metric describing the recall of a model."
      f1score:
        type: number
        description: "Optional summary metric describing the f1-score of a model."
      mean_absolute_error:
        type: number
        description: "Optional summary metric describing the mean absolute error of a model."
      mean_squared_error:
        type: number
        description: "Optional summary metric describing the mean-squared error of a model."

## What's Next?

  - [Start tracking metadata with Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/tracking) .
  - [Review Vertex ML Metadata concepts and data model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/data-model) .
