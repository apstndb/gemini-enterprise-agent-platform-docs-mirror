---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing
title: Analyze Vertex ML Metadata
description: Use Vertex ML Metadata to track and analyze the metadata produced by your machine learning (ML) systems.
data_source: docs.cloud.google.com
---

You can use Vertex ML Metadata to track and analyze the metadata produced by your machine learning (ML) systems. By tracking this metadata, it becomes easier to analyze the behavior of your ML system. This can help you understand changes in your system's performance, or it can help you compare the artifacts that your ML system produced.

If you are new to Vertex ML Metadata, read the introduction to Vertex ML Metadata to [learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) about tracking and analyzing your ML workflow's metadata.

Learn how to query for the Vertex ML Metadata that you want to analyze in the following ways:

  - [Query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#filtering) for all artifacts , executions , or context that match your filtering criteria.
  - [Query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#inputs-and-outputs) for an execution's input and output artifacts along with the events , used to connect the artifacts to the execution.
  - [Query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#lineage) for a context 's lineage subgraph. This query returns a context's artifacts and executions, along with the events that connect artifacts to executions.

> Are you using Gemini Enterprise Agent Platform Pipelines? Check out this [step-by-step tutorial](https://codelabs.developers.google.com/vertex-mlmd-pipelines#0) for a guide on analyzing metadata from pipeline executions.

## Query for artifacts, executions, and contexts

You can use the Vertex AI SDK for Python or the REST API to query for artifacts, executions, and contexts records using filters to create queries like the following:

  - Which versions of a trained model achieved a certain quality threshold?
  - Which dataset is used in a given pipeline?

The following sections demonstrate how to [create filters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#filters) and how to query for [artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#list-artifacts) , [executions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#list-executions) , and [contexts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#list-contexts) .

### Overview of filter syntax

The following sections describe how to use filters to query for artifacts, executions, and contexts.

#### Fields

The following fields are supported when filtering artifacts, executions, and contexts.

|                | Artifact | Execution | Context |
| -------------- | -------- | --------- | ------- |
| `name`         |          |           |         |
| `display_name` |          |           |         |
| `schema_title` |          |           |         |
| `create_time`  |          |           |         |
| `update_time`  |          |           |         |
| `metadata`     |          |           |         |
| `state`        |          |           |         |
| `uri`          |          |           |         |

Your filter must be wrapped in quotation marks. Any quotes that are a part of your filter must be escaped with a backslash.

#### Comparison operators

You can use the following comparison operators in your filters: `=` , `!=` , `<` , `>` , `>=` , `<=` .

For example, the following filters to find all artifacts where the display name is **my\_artifact** .

### REST

    display_name=\"my_artifact\"

### Python

    "display_name=\"my_artifact\""

For string fields, you can use wildcard filtering with the `*` character.

For timestamp fields such as `create_time` and `update_time` , you must format the date using RFC 3339 format — for example:

### REST

    create_time=\"2021-05-11T12:30:00-08:00\"

### Python

    "create_time=\"2021-05-11T12:30:00-08:00\""

#### Logical Operators

You can use `AND` and `OR` logical operators to combine filters to create a complex query.

The following example demonstrates how to query for artifacts of type `ai_platform.model` and a `metadata` field `precision` with a numeric value greater than 0.9.

### REST

    schema_title=\"ai_platform.Model\"+AND+metadata.precision.number_value>0.9

### Python

    "create_time=\"schema_title=\"ai_platform.Model\" AND metadata.precision.number_value>0.9"

#### Filter on metadata using the traversal operator

The `metadata` field is an instance of [`google.protobuf.Struct`](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Struct) whose format is defined in the schema specified in the `schema_title` field. `google.protobuf.Struct` is a data structure that maps keys to [`google.protobuf.Value`](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#value) instances. The [`google.protobuf.Value`](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#value) data structure stores values in different fields depending on their data type. For example:

  - strings are stored as `metadata. FIELD_NAME .string_value` ,
  - numbers are stored as `metadata. FIELD_NAME .number_value` ,
  - booleans are stored as `metadata. FIELD_NAME .bool_value` .

To filter on `metadata` , you must use the traversal operator to traverse to the field that you want to filter on. The traversal operator uses the following format.

### REST

    metadata.FIELD_NAME.TYPE_NAME=\"FILTER_VALUE\"

### Python

    "metadata.FIELD_NAME.TYPE_NAME=\"FILTER_VALUE\""

For example, consider a metadata structure like the following:

    {
       "field_1": 5,
       "field_2": "example",
       "field_3": {
         ...
       },
       "field_4": [],
       "field_5": true,
    }

The following queries illustrate how to use the traversal operator to filter on this example metadata.

  - Filter for records that have `metadata.field_1` with a value less than **5** .

### REST

    metadata.field_1.number_value<5

### Python

    "metadata.field_1.number_value<5"

  - Filter for records that have `metadata.field_2` with a value equal to **example** .

### REST

    metadata.field_2.string_value=\"example\"

### Python

    "metadata.field_2.string_value=\"example\""

  - Filter for records that have `metadata.field_5` with a value equal to **true** .

### REST

    metadata.field_5.bool_value=true

### Python

    "metadata.field_5.bool_value=true"

> **Note:** You can filter only on scalar value fields, such as strings, numbers, or booleans. You can't filter on struct or list fields.

#### Filter contexts by their parent and child relationships

You can use the *has* operator to find contexts that are the parent or child of a specified context.

The has operator uses the following format:

  - `"parent_contexts:\" CONTEXT_RESOURCE_NAME \""`
  - `"child_contexts:\" CONTEXT_RESOURCE_NAME \""`

The context name must be the context's full resource name, like the following: ` project/ PROJECT /locations/ LOCATION /metadataStores/ METADATA-STORE /contexts/ CONTEXT  ` .

The following filters demonstrate how to use the has operator:

  - Filter for all contexts that are children of the specified pipeline.

### REST

    parent_contexts:\"project/12345/locations/us-central1/metadataStores/default/contexts/pipeline_1\"

### Python

    "parent_contexts:\"project/12345/locations/us-central1/metadataStores/default/contexts/pipeline_1\""

  - Filter for all contexts that are a parent of the specified pipeline.

### REST

    child_contexts:\"project/12345/locations/us-central1/metadataStores/default/contexts/pipeline_1\"

### Python

    "child_contexts:\"project/12345/locations/us-central1/metadataStores/default/contexts/pipeline_1\""

#### Filter contexts, executions, and artifacts by association and attribution

You can use the `in_context()` function to filter for artifacts or executions that are associated with a context. You can use the `with_execution()` function to filter for specific artifacts or contexts that are associated with an execution. Similarly you can use the `with_artifact()` function to filter for specific executions or contexts that are associated with an artifact.

The filter functions are used in the following format.

  - `"in_context(\" CONTEXT_RESOURCE_NAME \")"`
  - `"with_execution(\" EXECUTION_RESOURCE_NAME \")"`
  - `"with_artifact(\" ARTIFACT_RESOURCE_NAME \")"`

The context, the execution, and the artifact names must be the full resource name, like the following.

  - ` project/ PROJECT_ID /locations/ LOCATION_ID /metadataStores/ METADATA-STORE /contexts/ CONTEXT  `
  - ` project/ PROJECT_ID /locations/ LOCATION_ID /metadataStores/ METADATA-STORE /executions/ EXECUTION  `
  - ` project/ PROJECT_ID /locations/ LOCATION_ID /metadataStores/ METADATA-STORE /artifacts/ ARTIFACT  `

The following example demonstrates how to filter for objects that are in the specified pipeline.

### REST

    in_context(\"project/12345/locations/us-central1/metadataStores/default/contexts/pipeline_1\")

### Python

    "in_context(\"project/12345/locations/us-central1/metadataStores/default/contexts/pipeline_1\")"

You can use a wildcard `*` in the filter functions to filter on parameters of each resource. For example you can use the following to filter all executions that act on a `system.model` artifact type.

### REST

    with_artifact(\"*\",\"schema_title='name.model'\")

### Python

    "with_artifact(\"*\",\"schema_title='name.model'\")"

Other supported parameters that you can filter on are as follows

  - `input=true/false` : Filter input or output artifact types.
  - `event_time` : Filter executions or artifacts event times.
  - All other [supported filter fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#filters)

You can combine the fields with [logical operands](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing#logical_operators) to construct complex filter queries. Note that the maximum supported nested function depth is 5.

### Query for artifacts

Artifacts, such as datasets and models, represent data used or produced by your ML workflow. Use the following instructions to query for artifacts.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - METADATA\_STORE : The metadata store ID where the artifact is created. The default metadata store is named `default` .

  - PAGE\_SIZE : (Optional) The maximum number of artifacts to return. If this value is not specified, the service returns a maximum of 100 records.

  - PAGE\_TOKEN : (Optional) A page token from a previous [MetadataService.ListArtifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/list) call. Specify this token to get the next page of results.

  - FILTER : Specifies the conditions required to include an artifact in the result set.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER" | Select-Object -Expand Content

You should see output similar to the following. ARTIFACT\_ID is the ID of the artifact record.

    {
      "artifacts": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/default/artifacts/ARTIFACT_ID",
          "displayName": "Example artifact",
          "uri": "gs://your_bucket_name/artifacts/dataset.csv",
          "etag": "67891011",
          "createTime": "2021-05-18T00:33:13.833Z",
          "updateTime": "2021-05-18T00:33:13.833Z",
          "state": "LIVE",
          "schemaTitle": "system.Dataset",
          "schemaVersion": "0.0.1",
          "metadata": {
            "payload_format": "CSV"
          },
          "description": "Description of the example artifact."
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "displayName": "Another example artifact",
          "uri": "gs://your_bucket_name/artifacts/dataset-2.csv",
          "etag": "67891012",
          "createTime": "2021-05-18T00:29:24.344Z",
          "updateTime": "2021-05-18T00:29:24.344Z",
          "state": "LIVE",
          "schemaTitle": "system.Dataset",
          "schemaVersion": "0.0.1",
          "metadata": {
            "payload_format": "CSV"
          },
          "description": "Description of the other example artifact."
        }
      ]
    }

### Python

### Python

    from typing import Optional
    
    from google.cloud import aiplatform
    
    
    def list_artifact_sample(
        project: str,
        location: str,
        display_name_filter: Optional[str] = "display_name=\"my_model_*\"",
        create_date_filter: Optional[str] = "create_time>\"2022-06-11\"",
        order_by: Optional[str] = None,
    ):
        aiplatform.init(project=project, location=location)
    
        combined_filters = f"{display_name_filter} AND {create_date_filter}"
        return aiplatform.Artifact.list(
            filter=combined_filters,
            order_by=order_by,
        )

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `display_name_filter` : Filter to be applied to display name while listing the resources with the format "display\_name=\\"my\_filter\\"" .
  - `create_date_filter` : Filter to be applied to create\_date name while listing the resources with the format "create\_time\>\\"2022-06-11T12:30:00-08:00\\"",.

### Query for executions

Executions represent a step in your ML workflow, such as preprocessing data or training a model. Use the following instructions to query for executions.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.

  - PROJECT\_ID : .

  - METADATA\_STORE : The metadata store ID where the execution is created. The default metadata store is named `default` .

  - PAGE\_SIZE : (Optional) The maximum number of artifacts to return. If this value is not specified, the service returns a maximum of 100 records.

  - PAGE\_TOKEN : (Optional) A page token from a previous [MetadataService.ListArtifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/list) call. Specify this token to get the next page of results.

  - FILTER : Specifies the conditions required to include an execution in the result set.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER" | Select-Object -Expand Content

You should see output similar to the following. EXECUTION\_ID is the ID of the execution record.

    {
      "executions": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "displayName": "Example execution 1",
          "etag": "67891011",
          "createTime": "2021-05-18T00:06:56.177Z",
          "updateTime": "2021-05-18T00:06:56.177Z",
          "schemaTitle": "system.Run",
          "schemaVersion": "0.0.1",
          "metadata": {},
          "description": "Description of the example execution."
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "displayName": "Example execution 2",
          "etag": "67891011",
          "createTime": "2021-05-18T00:04:49.659Z",
          "updateTime": "2021-05-18T00:04:49.659Z",
          "schemaTitle": "system.Run",
          "schemaVersion": "0.0.1",
          "metadata": {},
          "description": "Description of the example execution."
        }
      ]
    }

### Python

### Python

    from typing import Optional
    
    from google.cloud import aiplatform
    
    
    def list_execution_sample(
        project: str,
        location: str,
        display_name_filter: Optional[str] = "display_name=\"my_execution_*\"",
        create_date_filter:  Optional[str] = "create_time>\"2022-06-11T12:30:00-08:00\"",
    ):
        aiplatform.init(
            project=project,
            location=location)
    
        combined_filters = f"{display_name_filter} AND {create_date_filter}"
    
        return aiplatform.Execution.list(filter=combined_filters)

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `display_name_filter` : Filter to be applied to display name while listing the resources with the format "display\_name=\\"my\_filter\\"" .
  - `create_date_filter` : Filter to be applied to create\_date name while listing the resources with the format "create\_time\>\\"2022-06-11T12:30:00-08:00\\"",.

### Query for contexts

Contexts let you group sets of executions, artifacts, and other contexts. Use the following instructions to query for contexts.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.

  - PROJECT\_ID : .

  - METADATA\_STORE : The metadata store ID where the context is created. The default metadata store is named `default` .

  - PAGE\_SIZE : (Optional) The maximum number of artifacts to return. If this value is not specified, the service returns a maximum of 100 records.

  - PAGE\_TOKEN : (Optional) A page token from a previous [MetadataService.ListArtifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts/list) call. Specify this token to get the next page of results.

  - FILTER : Specifies the conditions required to include a context in the result set.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts?pageSize=PAGE_SIZE&pageToken=PAGE_TOKEN&filter=FILTER" | Select-Object -Expand Content

You should see output similar to the following. CONTEXT\_ID is the ID of the context record.

    {
      "contexts": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID",
          "displayName": "Experiment 1",
          "etag": "67891011",
          "createTime": "2021-05-18T22:36:02.153Z",
          "updateTime": "2021-05-18T22:36:02.153Z",
          "parentContexts": [],
          "schemaTitle": "system.Experiment",
          "schemaVersion": "0.0.1",
          "metadata": {}
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID",
          "displayName": "Pipeline run 1",
          "etag": "67891011",
          "createTime": "2021-05-18T22:35:02.600Z",
          "updateTime": "2021-05-18T22:35:02.600Z",
          "parentContexts": [],
          "schemaTitle": "system.PipelineRun",
          "schemaVersion": "0.0.1",
          "metadata": {}
        }
      ]
    }

## Query for an execution's input and output artifacts

Use the following instructions to query for the artifacts and executions in the specified context, along with the events that connect artifacts to executions.

### Agent Platform SDK for Python

### Input artifacts

This Python SDK sample involves querying for an execution's input artifacts.

### Python

    from google.cloud import aiplatform
    
    
    def get_execution_input_artifacts_sample(
        execution: aiplatform.Execution
    ):
        return execution.get_input_artifacts()

### Output artifacts

This Python SDK sample involves querying for an execution's output artifacts.

### Python

    from google.cloud import aiplatform
    
    
    def get_execution_output_artifacts_sample(
        execution: aiplatform.Execution
    ):
        return execution.get_output_artifacts()

### REST

This REST sample includes querying for both an execution's input and output artifacts.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the execution is created. The default metadata store is named `default` .
  - EXECUTION\_ID : The ID of the execution record.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID:queryExecutionInputsAndOutputs

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID:queryExecutionInputsAndOutputs"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID:queryExecutionInputsAndOutputs" | Select-Object -Expand Content

You should see output similar to the following. EXECUTION\_ID is The ID of the execution record. If the execution ID is not specified, Vertex ML Metadata created a unique identifier for this execution. ARTIFACT\_ID is the ID of the artifact record.

    {
      "artifacts": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "displayName": "Example artifact",
          "uri": "gs://your_bucket_name/artifacts/dataset.csv",
          "etag": "678901011",
          "createTime": "2021-05-18T00:29:24.344Z",
          "updateTime": "2021-05-18T00:29:24.344Z",
          "state": "LIVE",
          "schemaTitle": "system.Dataset",
          "schemaVersion": "0.0.1",
          "metadata": {
            "payload_format": "CSV"
          },
          "description": "Description of the example artifact."
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "displayName": "Example artifact 2",
          "uri": "gs://your_bucket_name/artifacts/dataset.csv",
          "etag": "678901011",
          "createTime": "2021-05-18T00:33:13.833Z",
          "updateTime": "2021-05-18T00:33:13.833Z",
          "state": "LIVE",
          "schemaTitle": "system.Dataset",
          "schemaVersion": "0.0.1",
          "metadata": {
            "payload_format": "CSV"
          },
          "description": "Description of the example artifact."
        }
      ],
      "executions": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "displayName": "Example execution 1",
          "etag": "678901011",
          "createTime": "2021-05-18T00:04:49.659Z",
          "updateTime": "2021-05-18T00:04:49.659Z",
          "schemaTitle": "system.Run",
          "schemaVersion": "0.0.1",
          "metadata": {},
          "description": "Description of the example execution."
        }
      ],
      "events": [
        {
          "artifact": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "execution": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "eventTime": "2021-05-18T00:04:49.659Z",,
          "type": "INPUT",
        },
        {
          "artifact": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "execution": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "eventTime": "2021-05-18T00:04:49.659Z",,
          "type": "OUTPUT",
        }
      ]
    }

## Query for a context's lineage subgraph

Use the following instructions to query for the artifacts and executions in the specified context, along with the events that connect artifacts to executions.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the execution is created. The default metadata store is named `default` .
  - CONTEXT\_ID : The ID of the context record

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID:queryContextLineageSubgraph

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID:queryContextLineageSubgraph"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID:queryContextLineageSubgraph" | Select-Object -Expand Content

You should see output similar to the following. EXECUTION\_ID is The ID of the execution record. If the execution ID is not specified, Vertex ML Metadata created a unique identifier for this execution. ARTIFACT\_ID is the ID of the artifact record.

    {
      "artifacts": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "displayName": "Example artifact",
          "uri": "gs://your_bucket_name/artifacts/dataset.csv",
          "etag": "678901011",
          "createTime": "2021-05-18T00:29:24.344Z",
          "updateTime": "2021-05-18T00:29:24.344Z",
          "state": "LIVE",
          "schemaTitle": "system.Dataset",
          "schemaVersion": "0.0.1",
          "metadata": {
            "payload_format": "CSV"
          },
          "description": "Description of the example artifact."
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "displayName": "Example artifact 2",
          "uri": "gs://your_bucket_name/artifacts/dataset.csv",
          "etag": "678901011",
          "createTime": "2021-05-18T00:33:13.833Z",
          "updateTime": "2021-05-18T00:33:13.833Z",
          "state": "LIVE",
          "schemaTitle": "system.Dataset",
          "schemaVersion": "0.0.1",
          "metadata": {
            "payload_format": "CSV"
          },
          "description": "Description of the example artifact."
        }
      ],
      "executions": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "displayName": "Example execution 1",
          "etag": "678901011",
          "createTime": "2021-05-18T00:04:49.659Z",
          "updateTime": "2021-05-18T00:04:49.659Z",
          "schemaTitle": "system.Run",
          "schemaVersion": "0.0.1",
          "metadata": {},
          "description": "Description of the example execution."
        }
      ],
      "events": [
        {
          "artifact": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "execution": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "eventTime": "2021-05-18T00:04:49.659Z",,
          "type": "INPUT",
        },
        {
          "artifact": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID",
          "execution": "projects/PROJECT_ID/locations/LOCATION/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
          "eventTime": "2021-05-18T00:04:49.659Z",,
          "type": "OUTPUT",
        }
      ]
    }

## What's next

  - [Get started tracking your Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/tracking) .
