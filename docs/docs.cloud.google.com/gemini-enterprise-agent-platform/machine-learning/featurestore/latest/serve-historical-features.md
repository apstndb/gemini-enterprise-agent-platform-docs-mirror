---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-historical-features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-historical-features
title: Serve historical feature values
description: Learn how to serve current and historical feature data from the feature data source in BigQuery for model training.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

If you need to retrieve or serve current as well as historical feature data, use offline serving to fetch feature values from BigQuery. For example, you can use offline serving to retrieve the feature values for specific timestamps to train a model.

All feature data, including historical feature data, is maintained in BigQuery, which constitutes the offline store for your feature values. To use offline serving, you must first register your BigQuery data source by creating feature groups and feature values. Also, in the case of offline serving, every row containing the same entity ID must have a different timestamp. For more information about data source preparation guidelines, see [Prepare data source](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/prepare-data-source) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the Python samples on this page in a local development environment, install and initialize the gcloud CLI, and then set up Application Default Credentials with your user credentials.

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#local-development) .

## Fetch historical feature values

Use the following sample to fetch historical values from a feature from multiple entity IDs and timestamps.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    import bigframes
    import bigframes.pandas
    import pandas as pd
    from google.cloud import bigquery
    from vertexai.resources.preview.feature_store import (Feature, FeatureGroup, offline_store)
    from vertexai.resources.preview.feature_store import utils as fs_utils
    
    fg = FeatureGroup("FEATURE_GROUP_NAME")
    f1 = fg.get_feature("FEATURE_NAME_1")
    f2 = fg.get_feature("FEATURE_NAME_2")
    
    entity_df = pd.DataFrame(
      data={
        "ENTITY_ID_COLUMN": [
          "ENTITY_ID_1",
          "ENTITY_ID_2",
        ],
        "timestamp": [
          pd.Timestamp("FEATURE_TIMESTAMP_1"),
          pd.Timestamp("FEATURE_TIMESTAMP_2"),
        ],
      },
    )
    
    offline_store.fetch_historical_feature_values(
      entity_df=entity_df,
      features=[f1,f2],
    )

Replace the following:

  - FEATURE\_GROUP\_NAME : The name of the existing feature group containing the feature.

  - FEATURE\_NAME\_1 and FEATURE\_NAME\_2 : The names of the registered features from which you want to retrieve the feature values.

  - ENTITY\_ID\_COLUMN : The name of the column containing the entity IDs. You can specify a column name only if it's registered in the feature group.

  - ENTITY\_ID\_1 and ENTITY\_ID\_2 : The entity IDs for which you want to fetch the feature values. If you want to retrieve feature values for the same entity ID at different timestamps, specify the same entity ID corresponding to each timestamp.

  - FEATURE\_TIMESTAMP\_1 and FEATURE\_TIMESTAMP\_2 : The timestamps corresponding to the historical feature values you want to retrieve. FEATURE\_TIMESTAMP\_1 corresponds to ENTITY\_ID\_1 , FEATURE\_TIMESTAMP\_2 corresponds to ENTITY\_ID\_2 , and so on. Specify the timestamps in the datetime format—for example, `2024-05-01T12:00:00` .
