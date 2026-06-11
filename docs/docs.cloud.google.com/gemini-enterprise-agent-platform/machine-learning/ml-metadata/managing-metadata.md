---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/managing-metadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/managing-metadata
title: Manage Vertex ML Metadata
description: Manage the metadata of your ML workflow.
data_source: docs.cloud.google.com
---

This guide demonstrates how to manage your Vertex ML Metadata.

## Before you begin

The first time that you use Vertex ML Metadata in a Google Cloud project, Gemini Enterprise Agent Platform creates your project's metadata store.

If you want your metadata encrypted using a customer-managed encryption key (CMEK), you must create your metadata store using a CMEK before you use Vertex ML Metadata to track or analyze metadata. Use the [create a metadata store that uses a CMEK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/configure) instructions to configure your project's metadata store.

## Artifact management

### Create an artifact

Use either REST or the Vertex AI SDK for Python to create an artifact.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - METADATA\_STORE : The metadata store ID where the artifact is created. The default metadata store is named `default` .
  - ARTIFACT\_ID : (Optional) The ID of the artifact record. If the artifact ID is not specified, Vertex ML Metadata creates a unique identifier for this artifact.
  - DISPLAY\_NAME : (Optional) The user-defined name of the artifact.
  - URI : (Optional) The location where the artifact is stored
  - ARTIFACT\_STATE : (Optional) A value from the [State enumeration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts#Artifact.State) that represents the current state of the artifact. This field is managed by client applications. Vertex ML Metadata does not check the validity of state transitions.
  - METADATA\_SCHEMA\_TITLE : The title of the schema that describes the metadata field. The title of the schema must meet the format \` . \`. The namespace must start with a lowercase letter, can contain lowercase characters and numbers, and can be two to twenty characters long. The schema name must start with an uppercase letter, can include letters and numbers, and can be two to fortynice characters long.
  - METADATA\_SCHEMA\_VERSION : (Optional) The version of the schema that describes the metadata field. `schema_version` must be a string of three numbers separated by periods, for example, 1.0.0, 1.0.1. This format helps order and compare versions.
  - METADATA : (Optional.) Properties that describe the artifact, such as the type of dataset.
  - DESCRIPTION : (Optional) A human readable string, that describes the purpose of the execution to be created.
  - LABELS :Optional. User-defined metadata for organizing your artifacts.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts?artifactId=ARTIFACT_ID

Request JSON body:

    {
      "displayName": "DISPLAY_NAME",
      "uri": "URI",
      "state": "ARTIFACT_STATE",
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "displayName": "DISPLAY_NAME",
      "uri": "URI",
      "state": "ARTIFACT_STATE",
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts?artifactId=ARTIFACT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "displayName": "DISPLAY_NAME",
      "uri": "URI",
      "state": "ARTIFACT_STATE",
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts?artifactId=ARTIFACT_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/default/artifacts/ARTIFACT_ID",
      "displayName": "Example artifact",
      "uri": "gs://your_bucket_name/artifacts/dataset.csv",
      "etag": "67891011",
      "labels": {
        "test_label": "test_label_value"
      },
      "createTime": "2021-05-18T00:29:24.344Z",
      "updateTime": "2021-05-18T00:29:24.344Z",
      "state": "LIVE",
      "schemaTitle": "system.Dataset",
      "schemaVersion": "0.0.1",
      "metadata": {
        "payload_format": "CSV"
      },
      "description": "Description of the example artifact."
    }

### Python

### Python

    from typing import Dict, Optional
    
    from google.cloud.aiplatform.metadata.schema.system import artifact_schema
    
    
    def create_artifact_sample(
        project: str,
        location: str,
        uri: Optional[str] = None,
        artifact_id: Optional[str] = None,
        display_name: Optional[str] = None,
        schema_version: Optional[str] = None,
        description: Optional[str] = None,
        metadata: Optional[Dict] = None,
    ):
        system_artifact_schema = artifact_schema.Artifact(
            uri=uri,
            artifact_id=artifact_id,
            display_name=display_name,
            schema_version=schema_version,
            description=description,
            metadata=metadata,
        )
        return system_artifact_schema.create(project=project, location=location,)

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `uri` : (Optional) The Uniform Resource Identifier for the artifact file if one exists. May be empty if there is no actual artifact file.
  - `artifact_id` : (Optional) The ID of the artifact record. If the artifact ID is not specified, Vertex ML Metadata creates a unique identifier for this artifact.
  - `display_name` : (Optional) The user-defined name of the artifact.
  - `schema_version` : The version of the schema that describes the metadata field.
  - `description` : (Optional) A human readable string, that describes the purpose of the artifact to be created.
  - `metadata` : Properties that describe the artifact, such as the artifact parameters.

### Look up an existing artifact

Artifacts represent data used or produced by your ML workflow, such as datasets and models. To look-up an existing artifact, use either REST or the Agent Platform SDK for Python.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.

  - PROJECT\_ID : .

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

### Delete an existing artifact

Use either REST or the Vertex AI SDK for Python to delete an artifact.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the artifact is created. The default metadata store is named `default` .
  - ARTIFACT\_ID : The ID of the artifact record to delete.

HTTP method and URL:

    DELETE https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts/ARTIFACT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2021-07-21T20:05:30.179713Z",
          "updateTime": "2021-07-21T20:05:30.179713Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

### Python

### Python

    from google.cloud import aiplatform
    
    
    def delete_artifact_sample(
        artifact_id: str,
        project: str,
        location: str,
    ):
        artifact = aiplatform.Artifact.get(
            resource_id=artifact_id, project=project, location=location
        )
        artifact.delete()

  - `artifact_id` : The ID of the execution record.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Purge artifacts

Use the following instructions to delete multiple artifacts based on a filter condition.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the artifact is created. The default metadata store is named `default` .
  - FILTER : Specifies the conditions required by the artifacts to be deleted. For example:
      - Filters for all artifacts that contain **example** in the display name: `"display_name = \"*example*\""` .
      - Filters for all artifacts created before 2020-11-19T11:30:00-04:00: `"create_time < \"2020-11-19T11:30:00-04:00\""` .
  - FORCE : Indicates whether to perform the actual purge or not. If the flag is set to false, the method will return a sample of artifact names that would be deleted.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts:purge

Request JSON body:

    {
      "filter": "FILTER",
      "force": FORCE
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "filter": "FILTER",
      "force": FORCE
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts:purge"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "filter": "FILTER",
      "force": FORCE
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/artifacts:purge" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.PurgeArtifactsMetadata",
        "genericMetadata": {
          "createTime": "2021-07-21T21:02:33.757991Z",
          "updateTime": "2021-07-21T21:02:33.757991Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.PurgeArtifactsResponse",
        "purgeCount": "15"
      }
    }

## Execution management

### Create an execution

Executions represent a step in your ML workflow. Use either REST or the Vertex AI SDK for Python to create an execution.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the execution is created. The default metadata store is named `default` .
  - EXECUTION\_ID : The ID of the execution record. If the execution ID is not specified, Vertex ML Metadata creates a unique identifier for this execution.
  - DISPLAY\_NAME : The execution's display name. This field may contain up to 128 Unicode characters.
  - EXECUTION\_STATE : (Optional) A value from the [State enumeration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions#Execution.State) that represents the current state of the execution. This field is managed by client applications. Vertex ML Metadata does not check the validity of state transitions.
  - METADATA\_SCHEMA\_TITLE : The title of the schema that describes the metadata field. The title of the schema must meet the format \` . \`. The namespace must start with a lowercase letter, can contain lowercase characters and numbers, and can be two to twenty characters long. The schema name must start with an uppercase letter, can include letters and numbers, and can be two to fortynice characters long.
  - METADATA\_SCHEMA\_VERSION : (Optional) The version of the schema that describes the metadata field. `schema_version` must be a string of three numbers separated by periods, for example, 1.0.0, 1.0.1. This format helps order and compare versions.
  - METADATA : (Optional) Properties that describe the execution, such as the execution parameters.
  - DESCRIPTION : (Optional) A human readable string, that describes the purpose of the execution to be created..
  - LABELS : Optional. User-defined metadata for organizing your executions.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions?executionId=EXECUTION_ID

Request JSON body:

    {
      "displayName": "DISPLAY_NAME",
      "state": "EXECUTION_STATE",
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "displayName": "DISPLAY_NAME",
      "state": "EXECUTION_STATE",
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions?executionId=EXECUTION_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "displayName": "DISPLAY_NAME",
      "state": "EXECUTION_STATE",
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions?executionId=EXECUTION_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID",
      "displayName": "Example Execution",
      "etag": "67891011",
      "labels": {
        "test_label": "test_label_value"
      },
      "createTime": "2021-05-18T00:04:49.659Z",
      "updateTime": "2021-05-18T00:04:49.659Z",
      "schemaTitle": "system.Run",
      "schemaVersion": "0.0.1",
      "metadata": {},
      "description": "Description of the example execution."
    }

### Python

### Python

    from typing import Any, Dict, List, Optional
    
    from google.cloud import aiplatform
    from google.cloud.aiplatform.metadata.schema.system import execution_schema
    
    
    def create_execution_sample(
        display_name: str,
        input_artifacts: List[aiplatform.Artifact],
        output_artifacts: List[aiplatform.Artifact],
        project: str,
        location: str,
        execution_id: Optional[str] = None,
        metadata: Optional[Dict[str, Any]] = None,
        schema_version: Optional[str] = None,
        description: Optional[str] = None,
    ):
        aiplatform.init(project=project, location=location)
    
        with execution_schema.ContainerExecution(
            display_name=display_name,
            execution_id=execution_id,
            metadata=metadata,
            schema_version=schema_version,
            description=description,
        ).create() as execution:
            execution.assign_input_artifacts(input_artifacts)
            execution.assign_output_artifacts(output_artifacts)
            return execution

  - `display_name` : The execution's display name. This field may contain up to 128 Unicode characters.
  - `input_artifacts` : A list of one or more instances of aiplatform.Artifact representing an input artifact.
  - `output_artifacts` : A list of one or more instances of aiplatform.Artifact representing an output Artifact.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `execution_id` : The ID of the execution record. If the execution ID is not specified, Vertex ML Metadata creates a unique identifier for this execution.
  - `metadata` : Properties that describe the execution, such as the execution parameters.
  - `schema_version` :The version of the schema that describes the metadata field.
  - `description` : (Optional) A human readable string, that describes the purpose of the execution to be created.

### Look up an existing execution

Use either REST or the Vertex AI SDK for Python to look-up an existing execution.

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

    from google.cloud import aiplatform
    
    
    def get_execution_sample(
        execution_id: str,
        project: str,
        location: str,
    ):
        execution = aiplatform.Execution.get(
            resource_id=execution_id, project=project, location=location
        )
    
        return execution

  - `execution_id` : The ID of the execution record.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Delete an existing execution

Use either REST or the Vertex AI SDK for Python to delete an execution.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the execution is created. The default metadata store is named `default` .
  - EXECUTION\_ID : The ID of the execution record to delete.

HTTP method and URL:

    DELETE https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions/EXECUTION_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2021-07-21T20:05:30.179713Z",
          "updateTime": "2021-07-21T20:05:30.179713Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

### Python

### Python

    from google.cloud import aiplatform
    
    
    def delete_execution_sample(
        execution_id: str,
        project: str,
        location: str,
    ):
        execution = aiplatform.Execution.get(
            resource_id=execution_id, project=project, location=location
        )
        execution.delete()

  - `execution_id` : The ID of the execution record.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Purge executions

To delete multiple executions based on a filter, use the following instructions.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the execution is created. The default metadata store is named `default` .
  - FILTER : Specifies the conditions required by the executions to be deleted. For example:
      - Filters for all executions that contain **example** in the display name: `"display_name = \"*example*\""` .
      - Filters for all executions created before 2020-11-19T11:30:00-04:00: `"create_time < \"2020-11-19T11:30:00-04:00\""` .
  - FORCE : Indicates whether to perform the actual purge or not. If the flag is set to false, the method will return a sample of artifact names that would be deleted.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions:purge

Request JSON body:

    {
      "filter": "FILTER",
      "force": FORCE
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "filter": "FILTER",
      "force": FORCE
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions:purge"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "filter": "FILTER",
      "force": FORCE
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/executions:purge" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.PurgeExecutionsMetadata",
        "genericMetadata": {
          "createTime": "2021-07-21T21:02:45.757991Z",
          "updateTime": "2021-07-21T21:02:45.757991Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.PurgeExecutionsResponse",
        "purgeCount": "2"
      }
    }

## Context management

### Create a context

Contexts let you group sets of artifacts and executions together. Use either REST or the Vertex AI SDK for Python to create a context.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE :The metadata store ID where the execution is created. The default metadata store is named `default` .
  - CONTEXT\_ID : (Optional) The ID of the context record. If the context ID is not specified, Vertex ML Metadata created a unique identifier for this context
  - DISPLAY\_NAME : The context's display name. This field may contain up to 128 Unicode characters.
  - PARENT\_CONTEXT : Specify the resource name for any parent contexts. A context can not have more than 10 parent contexts.
  - METADATA\_SCHEMA\_TITLE : The title of the schema that describes the metadata field. The title of the schema must meet the format \` . \`. The namespace must start with a lowercase letter, can contain lowercase characters and numbers, and can be two to twenty characters long. The schema name must start with an uppercase letter, can include letters and numbers, and can be two to fortynice characters long.
  - METADATA\_SCHEMA\_VERSION : (Optional) The version of the schema that describes the metadata field. `schema_version` must be a string of three numbers separated by periods, for example, 1.0.0, 1.0.1. This format helps order and compare versions.
  - METADATA : Properties that describe the context, such as the context parameters..
  - DESCRIPTION :(Optional) A human readable string, that describes the purpose of the execution to be created.
  - LABELS : Optional. User-defined metadata for organizing your contexts.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts?contextId=CONTEXT_ID

Request JSON body:

    {
      "displayName": "DISPLAY_NAME:",
      "parentContexts": [
        "PARENT_CONTEXT_1",
        "PARENT_CONTEXT_2"
      ],
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "displayName": "DISPLAY_NAME:",
      "parentContexts": [
        "PARENT_CONTEXT_1",
        "PARENT_CONTEXT_2"
      ],
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts?contextId=CONTEXT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "displayName": "DISPLAY_NAME:",
      "parentContexts": [
        "PARENT_CONTEXT_1",
        "PARENT_CONTEXT_2"
      ],
      "schemaTitle": "METADATA_SCHEMA_TITLE",
      "schemaVersion": "METADATA_SCHEMA_VERSION",
      "metadata": {
        METADATA
      },
      "labels": {"LABEL_1":"LABEL_2"},
      "description": "DESCRIPTION"
    
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts?contextId=CONTEXT_ID" | Select-Object -Expand Content

You should see output similar to the following. CONTEXT\_ID is the ID of the context record.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID",
      "displayName": "Example context:",
      "etag": "67891011",
      "labels": {
        "test_label": "test_label_value"
      },
      "createTime": "2021-05-18T01:52:51.642Z",
      "updateTime": "2021-05-18T01:52:51.642Z",
      "schemaTitle": "system.Experiment",
      "schemaVersion": "0.0.1",
      "metadata": {},
      "description": "Description of the example context."
    }

### Python

### Python

    from typing import Any, Dict, Optional
    
    from google.cloud import aiplatform
    from google.cloud.aiplatform.metadata.schema.system import context_schema
    
    
    def create_context_sample(
        display_name: str,
        project: str,
        location: str,
        context_id: Optional[str] = None,
        metadata: Optional[Dict[str, Any]] = None,
        schema_version: Optional[str] = None,
        description: Optional[str] = None,
    ):
        aiplatform.init(project=project, location=location)
    
        return context_schema.Experiment(
            display_name=display_name,
            context_id=context_id,
            metadata=metadata,
            schema_version=schema_version,
            description=description,
        ).create()

  - `display_name` : The context's display name. This field may contain up to 128 Unicode characters.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `context_id` : (Optional) The ID of the context record.
  - `metadata` : Properties that describe the context, such as the context parameters.
  - `schema_version` : The version of the schema that describes the metadata field.
  - `description` : (Optional) A human readable string, that describes the purpose of the context to be created.

### Look up an existing context

Use either REST or the Vertex AI SDK for Python to look-up an existing context.

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

### Python

### Python

    from google.cloud import aiplatform
    
    
    def get_context_sample(
        context_id: str,
        project: str,
        location: str,
    ):
        context = aiplatform.Context.get(
            resource_id=context_id, project=project, location=location)
        return context

  - `context_id:` : The ID of the context record.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Delete an existing context

Use either REST or the Vertex AI SDK for Python to delete a context.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE : The metadata store ID where the context is created. The default metadata store is named `default` .
  - CONTEXT\_ID : (Optional) The ID of the context record.

HTTP method and URL:

    DELETE https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts/CONTEXT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2021-07-21T20:05:30.179713Z",
          "updateTime": "2021-07-21T20:05:30.179713Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

### Python

### Python

    from google.cloud import aiplatform
    
    
    def delete_context_sample(
        context_id: str,
        project: str,
        location: str,
    ):
        context = aiplatform.Context.get(
            resource_id=context_id, project=project, location=location
        )
        context.delete()

  - `context_id:` : The ID of the context record.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .

### Purge contexts

Use the following instructions to delete multiple contexts based on a filter condition.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : .
  - METADATA\_STORE :The metadata store ID where the context is created. The default metadata store is named `default` .
  - FILTER : Specifies the conditions required by the contexts to be deleted. For example:
      - Filters for all contexts that contain **example** in the display name: `"display_name = \"*example*\""` .
      - Filters for all contexts created before 2020-11-19T11:30:00-04:00: `"create_time < \"2020-11-19T11:30:00-04:00\""` .
  - FORCE : Indicates whether to perform the actual purge or not. If the flag is set to false, the method will return a sample of context names that would be deleted.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts:purge

Request JSON body:

    {
      "filter": "FILTER",
      "force": FORCE
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "filter": "FILTER",
      "force": FORCE
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts:purge"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "filter": "FILTER",
      "force": FORCE
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/contexts:purge" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.PurgeContextsMetadata",
        "genericMetadata": {
          "createTime": "2021-07-21T21:02:40.757991Z",
          "updateTime": "2021-07-21T21:02:40.757991Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.PurgeContextsResponse",
        "purgeCount": "5"
      }
    }

## What's next

  - [Get started tracking your Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/tracking) .
  - [Get started analyzing your Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing) .
