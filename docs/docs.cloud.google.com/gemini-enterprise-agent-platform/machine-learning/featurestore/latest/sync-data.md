---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data
title: Start a data sync
description: Learn how to manually initiate a data sync for a feature view in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

If your feature view is configured to use scheduled data sync, you can optionally skip the wait until the next scheduled sync operation by manually initiating the data sync.

You can't manually trigger a data sync if your feature view is configured to use continuous data sync. For more information about the types of data sync that Vertex AI Feature Store supports and how to configure the sync type for a feature view, see [Sync feature data in a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#sync_featuredata) .

Note that to sync the data for the entire online store, you need to sync the data for all of its feature views.

Data sync might involve costs for BigQuery resource usage. For information about how to optimize costs while setting the sync schedule for a feature view, see [Optimize costs during sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#sync_optimize_costs) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Manually start a data sync

Use the following sample to manually start the data sync in a feature view configured for scheduled data sync.

Note that only one data sync operation can be active at any point of time for a feature view. If you try to manually start the data sync while another sync is in progress, then the new sync operation starts only after the ongoing sync operation ends.

> **Caution:** You can't trigger the data sync if your feature view is configured for [continuous data sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#sync_featuredata) . If your feature view is configured for continuous data sync, then the feature data is refreshed whenever the feature data in the BigQuery data source is updated.

### REST

To manually start a data sync in a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) , send a `POST` request by using the [featureViews.sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/sync) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view where you want to manually start the data sync.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:sync

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:sync"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:sync" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "featureViewSync": "projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs/OPERATION_ID"
    }

## What's next

  - Learn how to [view a list of all data sync operations executed for a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-data-syncs) .

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview)
