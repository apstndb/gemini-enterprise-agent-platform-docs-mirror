---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/featureview-direct-write
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/featureview-direct-write
title: Update features in a feature view
description: Learn how to use the directWrite method to update the features in a feature view instance in real-time without updating the feature data source.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

If your online store uses Bigtable online serving, you can directly update feature values in a feature view without updating the feature data source in real-time. You can either update the feature values for an existing ID, or add a new entity ID along with the corresponding feature values. Use this capability in the following scenarios:

  - You want to write features to an online store faster than batch sync, while maintaining data freshness at 100ms or less.

  - You want to retrieve the timestamp when the feature is written to the online store.

Vertex AI Feature Store doesn't update the feature data source in BigQuery based on the feature data that written directly to a feature view instance. During data sync, Vertex AI Feature Store updates the feature view with the feature value having the most recent timestamp. For example, if you update a feature value directly in a feature view, and subsequently update the same feature in the BigQuery source, then Vertex AI Feature Store updates the feature view with the most recently updated feature value from BigQuery during the next data sync.

If you want to add or update feature values for a feature column that's used in multiple feature views, then you must make the same updates to each feature view separately.

If an online store instance is configured for Optimized online serving ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ), you can't write features directly to a feature view within that online store.

Note that this capability doesn't let you add or remove feature columns in a feature view. Also, you can't delete existing feature values or entity IDs.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Update features directly in a feature view

Use the following sample to write features to an entity within a feature view.

### REST

To write features values directly to a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `POST` request by using the [`featureViews.directWrite`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/directWrite) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region for the feature view where you want to write the features, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance containing the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view instance where you want to write the features.
  - ENTITY\_ID : The entity ID for which you want to add feature values.
  - FEATURE\_1 and FEATURE\_2 : The features you want to add.
  - FEATURE\_1\_VALUE and FEATURE\_2\_VALUE : The feature values for FEATURE\_1 and FEATURE\_2 , respectively.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:directWrite

Request JSON body:

    [
      {
          "feature_view": "LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME",
          "data_key_and_feature_values": {
            "data_key": {
              "key": "ENTITY_ID"
            },
            "features": [{
              "name": "FEATURE_1",
              "value_and_timestamp": {
                "value": {
                  "string_value": "FEATURE_1_VALUE"
                }
              }
            },
            {
              "name": "FEATURE_2",
              "value_and_timestamp": {
                "value": {
                  "string_value": "FEATURE_2_VALUE"
                }
              }
            }
          ]
        }
      }
    ]

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:directWrite"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:directWrite" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "status": {},
      "writeResponses": [
        {
          "dataKey": {
            "key": "ENTITY_ID"
          },
          "onlineStoreWriteTime": "2025-04-01T01:30:09.525061Z"
        }
      ]
    }

## What's next

  - Learn how to [manually start a data sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) .

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .
