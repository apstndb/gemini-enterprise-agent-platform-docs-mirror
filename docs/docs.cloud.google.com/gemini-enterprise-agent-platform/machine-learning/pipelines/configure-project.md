---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project
title: Configure your Google Cloud project for Gemini Enterprise Agent Platform Pipelines
description: Learn how to set up your {{dynamic_data.site_values.cloud_name}} project to use Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

Before you use Agent Platform Pipelines to orchestrate your machine learning (ML) pipelines, you must set up your Google Cloud project. Some resources, such as the metadata store used by Vertex ML Metadata, are created in your Google Cloud project the first time that you run a pipeline.

Use the following instructions to configure your project for Agent Platform Pipelines.

1.  [Create your Google Cloud project and configure it for use with Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#project) .

2.  If you don't specify a service account, Agent Platform Pipelines uses the Compute Engine default service account to run your pipelines. For more information about the Compute Engine default service account, see [Using the Compute Engine Default Service Account](https://docs.cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances#using_the_default_service_account) .
    
    We recommend that you [create a service account to run your pipelines and then grant this account granular permissions to the Google Cloud resources that are needed to run your pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) .

3.  Agent Platform Pipelines uses Cloud Storage to store the artifacts of your pipeline runs. [Create a Cloud Storage bucket and grant your service account access to this bucket](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#storage) .

4.  Agent Platform Pipelines uses Vertex ML Metadata to store the metadata created by your pipeline runs. When you run a pipeline for the first time, if the metadata store of your project doesn't exist, Gemini Enterprise Agent Platform creates your project's metadata store.
    
    If you want your data encrypted using a customer-managed encryption key (CMEK), you can manually [create your metadata store using a CMEK key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#create-metadata-store) before you run a pipeline. Otherwise, if there's no existing default metadata store in your project, Gemini Enterprise Agent Platform creates your project's metadata store using the CMEK key used when you run the pipeline for the first time. After the metadata store is created, it uses a CMEK key that's different from the CMEK key used in a pipeline run.

## Set up your Google Cloud project

Use the following instructions to create a Google Cloud project and configure it for use with Agent Platform Pipelines.

## Configure a service account with granular permissions

When you run a pipeline, you can specify a service account. Your pipeline run acts with the permissions of this service account.

If you don't specify a service account, your pipeline run uses the Compute Engine [default service account](https://docs.cloud.google.com/compute/docs/access/service-accounts#default_service_account) . For more information about the Compute Engine default service account, see [Using the Compute Engine Default Service Account](https://docs.cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances#using_the_default_service_account) .

  - Use the following instructions to create a service account and grant it granular permissions to Google Cloud resources.
    
    1.  Run the following command to create a service account.
        
            gcloud iam service-accounts create SERVICE_ACCOUNT_ID \
                --description="DESCRIPTION" \
                --display-name="DISPLAY_NAME" \
                --project=PROJECT_ID
        
        Replace the following values:
        
          - SERVICE\_ACCOUNT\_ID : The ID for the service account.
          - DESCRIPTION : (Optional.) A description of the service account.
          - DISPLAY\_NAME : The display name for this service account.
          - PROJECT\_ID : The project to create your service account in.
        
        Learn more about [creating a service account](https://docs.cloud.google.com/iam/docs/creating-managing-service-accounts) .
    
    2.  Grant your service account access to Gemini Enterprise Agent Platform. Note that it might take some time for the access change to propagate. For more information, see [Access change propagation](https://docs.cloud.google.com/iam/docs/access-change-propagation) .
        
            gcloud projects add-iam-policy-binding PROJECT_ID \
                --member="serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
                --role="roles/aiplatform.user"
        
        Replace the following values:
        
          - PROJECT\_ID : The project that your service account was created in.
          - SERVICE\_ACCOUNT\_ID : The ID for the service account.
        
        > **Note:** The minimum set of permissions that are required to use Agent Platform Pipelines to run a pipeline are **aiplatform.metadataStores.get** , **storage.buckets.get** , **storage.objects.create** , and **storage.objects.get** . The first time you run a pipeline in a new project you must also add the **aiplatform.metadataStores.create** permission. To run a pipeline with minimal permissions, use Identity and Access Management to [create a custom role](https://docs.cloud.google.com/iam/docs/creating-custom-roles) with these permissions, and grant your service account access to that role instead of **roles/aiplatform.user** .
    
    3.  You can use Artifact Registry to host container images and Kubeflow Pipelines templates.
        
        For more information about Artifact Registry, see the [Artifact Registry documentation](https://docs.cloud.google.com/artifact-registry/docs/overview) .
    
    4.  Grant your service account access to any Google Cloud resources that you use in your pipelines.
        
            gcloud projects add-iam-policy-binding PROJECT_ID \
                --member="serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
                --role="ROLE_NAME"
        
        Replace the following values:
        
          - PROJECT\_ID : The project that your service account was created in.
          - SERVICE\_ACCOUNT\_ID : The ID for the service account.
          - ROLE\_NAME : The Identity and Access Management role to grant to this service account.
    
    5.  To use Agent Platform Pipelines to run pipelines with this service account, run the following command to grant your user account the **roles/iam.serviceAccountUser** role for your service account.
        
            gcloud iam service-accounts add-iam-policy-binding \
                SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com \
                --member="user:USER_EMAIL" \
                --role="roles/iam.serviceAccountUser"
        
        Replace the following values:
        
          - SERVICE\_ACCOUNT\_ID : The ID for the service account.
          - PROJECT\_ID : The project that your service account was created in.
          - USER\_EMAIL : The email address of the user that runs pipelines as this service account.

  - If you prefer to use the Compute Engine default service account to run your pipelines, enable the Compute Engine API and grant your default service account access to Gemini Enterprise Agent Platform. Note that it might take some time for the access change to propagate. For more information, see [Access change propagation](https://docs.cloud.google.com/iam/docs/access-change-propagation) .
    
        gcloud projects add-iam-policy-binding PROJECT_ID \
            --member="serviceAccount:PROJECT_NUMBER-compute@developer.gserviceaccount.com" \
            --role="roles/aiplatform.user"
    
    Replace the following values:
    
      - PROJECT\_ID : The project that your default service account was created in.
      - PROJECT\_NUMBER : The project number that your default service account was created in.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

## Configure a Cloud Storage bucket for pipeline artifacts

Agent Platform Pipelines stores the artifacts of your pipeline runs using Cloud Storage. Use the following instructions to create a Cloud Storage bucket and grant your service account (or the Compute Engine default service account) access to read and write objects in that bucket.

1.  Run the following command to create a Cloud Storage bucket in the region that you want to run your pipelines in.
    
        gcloud storage buckets create gs://BUCKET_NAME --location=BUCKET_LOCATION --project=PROJECT_ID
    
    Replace the following values:
    
      - PROJECT\_ID : Specify the project that your bucket is associated with.
      - BUCKET\_LOCATION : Specify the [location](https://docs.cloud.google.com/storage/docs/locations) of your bucket — for example, `US-CENTRAL1` .
      - BUCKET\_NAME : The name you want to give your bucket, subject to [naming requirements](https://docs.cloud.google.com/storage/docs/buckets#naming) . For example, `my-bucket` .
    
    Learn more about [creating Cloud Storage buckets](https://docs.cloud.google.com/storage/docs/creating-buckets) .

2.  Run the following commands to grant your service account access to read and write pipeline artifacts in the bucket that you created in the previous step.
    
        gcloud storage buckets add-iam-policy-binding gs://BUCKET_NAME \
        --member=serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com \
        --role=roles/storage.objectUser
    
    Replace the following values:
    
      - SERVICE\_ACCOUNT\_ID : The ID for the service account.
      - PROJECT\_ID : The project that your service account was created in.
      - BUCKET\_NAME : The name of the bucket you are granting your service account access to.
    
    Alternatively, if you prefer to use the Compute Engine default service account to run your pipelines, run the [`gcloud iam service-accounts list`](https://docs.cloud.google.com/sdk/gcloud/reference/iam/service-accounts/list) command to locate the project number for that account.
    
        gcloud iam service-accounts list
    
    The Compute Engine default service account is named like the following: `  PROJECT_NUMBER -compute@developer.gserviceaccount.com ` .
    
    Run the following command to grant the Compute Engine default service account access to read and write pipeline artifacts in the bucket that you created in the previous step.
    
        gcloud storage buckets add-iam-policy-binding gs://BUCKET_NAME \
        --member=serviceAccount:PROJECT_NUMBER-compute@developer.gserviceaccount.com \
        --role=roles/storage.objectUser
    
    Replace the following values:
    
      - PROJECT\_NUMBER : The project number for the Compute Engine default service account.
      - BUCKET\_NAME : The name of the bucket you are granting your service account access to.
    
    Learn more about [controlling access to Cloud Storage buckets](https://docs.cloud.google.com/storage/docs/access-control) .

## Create a metadata store that uses a CMEK (optional)

Use the following instructions to create a CMEK and set up a Vertex ML Metadata metadata store that uses this CMEK.

1.  [Use Cloud Key Management Service to configure a customer-managed encryption key.](https://docs.cloud.google.com/vertex-ai/docs/general/cmek#configure-cmek)

2.  Use the following REST call to create your project's default metadata store using your CMEK.
    
    Before using any of the request data, make the following replacements:
    
      - LOCATION\_ID : Your region.
      - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
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
