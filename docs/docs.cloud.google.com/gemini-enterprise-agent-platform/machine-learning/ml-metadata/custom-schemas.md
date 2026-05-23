---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/custom-schemas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/custom-schemas
title: Create and use custom schemas
description: Use custom schemas to type check metadata properties and to query resources by schema
data_source: docs.cloud.google.com
---

In addition to the predefined system schemas, Vertex ML Metadata provides an extensible data model through custom schemas. Custom schemas are user-defined MetadataSchemas. Use custom schemas to type check metadata properties and to query resources by schema, for example, "list all Artifacts of type `MyCustomModel` .

To define a custom schema, you must create a MetadataSchema resource within a specific MetadataStore that describes the expected schema. The schema format is a subset of the [OpenAPI 3.0 specification](https://swagger.io/specification/#schema-object) {class: external}, with the restriction that the top-level schema must be of type `object` . All OpenAPI 3.0 supported [data types](https://swagger.io/docs/specification/data-models/data-types/) (for example, integer, number, string, boolean, array, object) are supported as properties of this top-level schema object. A restriction is that each field under the properties section can be assigned to only one data type. Mixed types are not supported. Advanced data requirements such as Minimum, Maximum, Multiples, and string formats are also not supported.

> **Note:** Fields in the schema are always considered optional when the system performs type checking. When you create new metadata resources, you can still include fields that are not defined in the schema.

## How to register your own custom schemas

The process to create a custom MetadataSchema is similar to creating new metadata resources. The following instructions show how to create a sample MetadataSchema. MetadataSchemas are scoped only to their associated MetadataStore.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region of your MetadataStore.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). or number.
  - METADATA\_STORE : The metadata store ID where the MetadataSchema is created. The default metadata store is named `default` . Unless a new MetadataStore is required, you can use the default store.
  - METADATA\_SCHEMA\_ID : (Optional) The ID of the MetadataSchema record. If the ID is not specified, Vertex ML Metadata creates a unique identifier for this MetadataSchema .
  - METADATA\_SCHEMA\_TITLE : The title of the schema that describes the metadata field. The title of the schema must meet the format \` . \`. The namespace must start with a lowercase letter, can contain lowercase characters and numbers, and can be two to twenty characters long. The schema name must start with an uppercase letter, can include letters and numbers, and can be two to fortynice characters long.
  - METADATA\_SCHEMA\_VERSION : (Optional) The version of the schema that describes the metadata field. `schema_version` must be a string of three numbers separated by periods, for example, 1.0.0, 1.0.1. This format helps order and compare versions..
  - METADATA\_SCHEMA\_TYPE : The type of metadata resource to which the created schema applies. Types are: `ARTIFACT_TYPE` , `EXECUTION_TYPE` , or `CONTEXT_TYPE` .
  - METADATA\_SCHEMA : The detailed schema to create.
  - DESCRIPTION : (Optional) A human readable string, that describes the purpose of the execution to be created..
  - ARTIFACT\_ID : (Optional) The ID of the artifact record. If the artifact ID is not specified, Vertex ML Metadata creates a unique identifier for this artifact..
  - DISPLAY\_NAME : (Optional) The user-defined name of the artifact..

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/metadataSchemas?metadata_schema_id=METADATA_SCHEMA_ID

Request JSON body:

    {
        "schemaVersion": "0.0.1",
        "schema": "title: test.Experiment\ntype: object",
        "schemaType": "CONTEXT_TYPE",
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
        "schemaVersion": "0.0.1",
        "schema": "title: test.Experiment\ntype: object",
        "schemaType": "CONTEXT_TYPE",
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/metadataSchemas?metadata_schema_id=METADATA_SCHEMA_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
        "schemaVersion": "0.0.1",
        "schema": "title: test.Experiment\ntype: object",
        "schemaType": "CONTEXT_TYPE",
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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/metadataSchemas?metadata_schema_id=METADATA_SCHEMA_ID" | Select-Object -Expand Content

You should see output similar to the following. You can use the METADATA\_SCHEMA\_ID is the ID of the MetadataSchema record.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/metadataStores/METADATA_STORE/metadataSchemas/METADATA_SCHEMA_ID",
      "schemaVersion": "0.0.1",
      "schema": "title: test.Experiment\ntype: object",
      "schemaType": "CONTEXT_TYPE",
      "createTime": "2021-04-06T05:24:04.575481815Z"
    }

Subsequent calls to create, get, or list Artifacts can then refer to this schema by specifying the name (demo.Artifact) in the schema\_title field and version (0.0.1) in the schema\_version of the Artifact resource. For more information about how to create, get, or list metadata resources, see [Track Vertex ML Metadata](https://docs.cloud.google.com/vertex-ai/docs/ml-metadata/tracking) .

## Version your schemas

All MetadataSchema resources are versioned. A user can create a schema that uses the same schema\_title as another schema but a different schema\_version. To create a metadataSchema resource with a different version, a user can provide a different version number and modified schema content.

The following example creates a 0.0.2 version of the demo.Artifact schema:

    sample_schema_versioned = aip.MetadataSchema()
    sample_schema_versioned.schema_type = aip.MetadataSchema.MetadataSchemaType.ARTIFACT_TYPE
    sample_schema_versioned.schema ="title: demo.Artifact\ntype: object\nproperties:\n  framework:\n    type: string\n    description: \"The framework type\"\n  model_version:\n    type: integer\n    description: \"The version of the model\""
    sample_schema_versioned.schema_version = "0.0.2"
    sample_schema_versioned.description = "sample schema 2"
    
    store_client.create_metadata_schema(parent=metadata_store.name, metadata_schema=sample_schema_versioned)

Fields in the schema are always considered optional, so there is no backward or forward compatibility between versions of the same schema\_title. Users can still use the schema\_title to filter and group resources for analysis. For more information about how to use filter functions, see [Analyzing Vertex ML Metadata](https://docs.cloud.google.com/vertex-ai/docs/ml-metadata/analyzing) .

## What's next

  - [Get started tracking your Vertex ML Metadata](https://docs.cloud.google.com/vertex-ai/docs/ml-metadata/tracking) .
