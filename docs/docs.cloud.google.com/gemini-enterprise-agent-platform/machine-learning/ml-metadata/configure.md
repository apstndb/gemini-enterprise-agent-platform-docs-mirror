---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/configure
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/configure
title: Configure your project's metadata store
description: Create a metadata store that uses a CMEK
data_source: docs.cloud.google.com
---

Vertex ML Metadata lets you track and analyze the metadata produced by your machine learning (ML) workflows. The first time you run a PipelineJob or create an experiment in the Vertex SDK, Gemini Enterprise Agent Platform creates your project's MetadataStore .

If you want your metadata encrypted using a [customer-managed encryption key (CMEK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) , you must create your metadata store using a CMEK *before* you use Vertex ML Metadata to track or analyze metadata.

After the metadata store has been created, the CMEK key that the metadata store uses is independent of the CMEK key used by processes that log metadata, for example, a pipeline run.

## Create a metadata store that uses a CMEK

Use the following instructions to create a CMEK and set up a Vertex ML Metadata metadata store that uses this CMEK.

1.  [Use Cloud Key Management Service to configure a customer-managed encryption key.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#configure-cmek)

2.  Use the following REST call to create your project's default metadata store using your CMEK.
    
    Before using any of the request data, make the following replacements:
    
      - LOCATION\_ID : Your region.
      - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
      - KEY\_RING : The name of the Cloud Key Management Service key ring that your encryption key is on.
      - KEY\_NAME : The name of the encryption key that you want to use for this metadata store.
    
    HTTP method and URL:
    
        POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores?metadata_store_id=default
    
    Request JSON body:
    
        {
          "encryption_spec": {
            "kms_key_name": "projects/PROJECT_ID/locations/LOCATION_ID/keyRings/KEY_RING/cryptoKeys/KEY_NAME"
          },
        }
    
    To send your request, expand one of these options:
    
    #### curl (Linux, macOS, or Cloud Shell)
    
    > **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .
    
    Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:
    
        cat > request.json << 'EOF'
        {
          "encryption_spec": {
            "kms_key_name": "projects/PROJECT_ID/locations/LOCATION_ID/keyRings/KEY_RING/cryptoKeys/KEY_NAME"
          },
        }
        EOF
    
    Then execute the following command to send your REST request:
    
        curl -X POST \
             -H "Authorization: Bearer $(gcloud auth print-access-token)" \
             -H "Content-Type: application/json; charset=utf-8" \
             -d @request.json \
             "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores?metadata_store_id=default"
    
    #### PowerShell (Windows)
    
    > **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .
    
    Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:
    
        @'
        {
          "encryption_spec": {
            "kms_key_name": "projects/PROJECT_ID/locations/LOCATION_ID/keyRings/KEY_RING/cryptoKeys/KEY_NAME"
          },
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
            -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/metadataStores?metadata_store_id=default" | Select-Object -Expand Content
    
    You should receive a JSON response similar to the following:
    
        {
          "name": "projects/PROJECT_ID/locations/LOCATION_ID/operations/OPERATIONS_ID",
          "metadata": {
            "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateMetadataStoreOperationMetadata",
            "genericMetadata": {
              "createTime": "2021-05-18T18:47:14.494997Z",
              "updateTime": "2021-05-18T18:47:14.494997Z"
            }
          }
        }
