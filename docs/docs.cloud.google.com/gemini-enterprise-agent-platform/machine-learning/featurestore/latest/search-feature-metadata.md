---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-feature-metadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-feature-metadata
title: Search for resource metadata in Data Catalog
description: Learn how to use the netadata search capability of Knowledge Catalog to discover Vertex AI Feature Store resources in Data Catalog.
data_source: docs.cloud.google.com
---

> **Caution:** Data Catalog is [deprecated](https://docs.cloud.google.com/data-catalog/docs/deprecations) in favor of [Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/catalog-overview) . Knowledge Catalog is also integrated with Vertex AI Feature Store, offering similar capabilities.

Data Catalog catalogs metadata from Vertex AI Feature Store resources. Using the metadata search capability of Knowledge Catalog, you can discover these resources and view their metadata. For more information about the Data Catalog metadata search capability, see [Search and view data assets with Data Catalog](https://docs.cloud.google.com/data-catalog/docs/how-to/search) .

Alternatively, to search for Vertex AI Feature Store resources from Gemini Enterprise Agent Platform, see [Search for Vertex AI Feature Store resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-resources) .

## Before you begin

[Authenticate yourself to Data Catalog](https://docs.cloud.google.com/data-catalog/docs/concepts/authentication) , unless you've done so already.

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

## Vertex AI Feature Store resources in Data Catalog

Data Catalog lets you discover Google Cloud resources as data assets. The following Vertex AI Feature Store resources are categorized as data types in the Knowledge Catalog search filter:

  - `FeatureOnlineStore`

  - `FeatureView`
    
    > **Note:** If your project name contains `:` , Knowledge Catalog catalogs `FeatureOnlineStore` resources, but doesn't catalog `FeatureView` and `Feature` resources created in the project.

  - `FeatureGroup`

Note that `Feature` is not listed as a data type in the search filters. However, you can view the list of features and feature metadata by viewing the metadata of the parent feature groups.

## IAM permissions required

Using the Knowledge Catalog search, you can view Vertex AI Feature Store resources if you have the IAM permissions to view those Vertex AI Feature Store resources in your Google Cloud project. You don't need additional permissions for viewing the resource metadata in Data Catalog.

> **Note:** If you have the permission to view a feature group, you can view the features, including feature metadata, within that feature group using Data Catalog.

## View metadata for an online store

To search for a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource, follow these steps:

### Console

1.  To launch a search query in the Google Cloud console, go to the Knowledge Catalog **Search** page.

2.  Use the following **Filters** to define your search parameters:
    
      - **Projects** : Click **Add project** to search for and select a specific project.
    
      - **Data types** : Select **FeatureOnlineStore** .
        
        You can also define your query in the search field. To learn how to define your search query in Data Catalog, see [Data Catalog search syntax](https://docs.cloud.google.com/data-catalog/docs/how-to/search-reference) .

3.  To view the resource metadata, in the filtered list of data assets, click the name of the online store instance.

## View metadata for a feature view

To search for a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource, follow these steps:

### Console

1.  To launch a search query in the Google Cloud console, go to the Knowledge Catalog **Search** page.

2.  Use the following **Filters** to define your search parameters:
    
      - **Projects** : Click **Add project** to search for and select a specific project.
    
      - **Data types** : Select **FeatureView** .
        
        You can also define your query in the search field. To learn how to define your search query in Data Catalog, see [Data Catalog search syntax](https://docs.cloud.google.com/data-catalog/docs/how-to/search-reference) .

3.  To view the resource metadata, in the filtered list of data assets, click the name of the feature view.

## View metadata for a feature group

To search for a [`FeatureGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups#resource:-featuregroup) resource, follow these steps:

### Console

1.  To launch a search query in the Google Cloud console, go to the Knowledge Catalog **Search** page.

2.  Use the following **Filters** to define your search parameters:
    
      - **Projects** : Click **Add project** to search for and select a specific project.
    
      - **Data types** : Select **FeatureGroup** .
        
        You can also define your query in the search field. To learn how to define your search query in Data Catalog, see [Data Catalog search syntax](https://docs.cloud.google.com/data-catalog/docs/how-to/search-reference) .

3.  To view the resource metadata, in the filtered list of data assets, click the name of the feature group.

## View metadata for features within a feature group

To view the list of [`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#resource:-feature) resources and their metadata within a feature group, follow these steps:

### Console

1.  To launch a search query in the Google Cloud console, go to the Knowledge Catalog **Search** page.

2.  Use the following **Filters** to define your search parameters:
    
      - **Projects** : Click **Add project** to search for and select a specific project.
    
      - **Data types** : Select **FeatureGroup** .
        
        You can also define your query in the search field. To learn how to define your search query in Data Catalog, see [Data Catalog search syntax](https://docs.cloud.google.com/data-catalog/docs/how-to/search-reference) .

3.  In the filtered list of data assets, click the name of the parent feature group containing the features.

4.  To view the list of features and feature metadata within the feature group, click **Schema** .

## What's next

  - Perform an [advanced search for Vertex AI Feature Store resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-resources) .

  - Learn more about [Data Catalog](https://docs.cloud.google.com/data-catalog/docs/concepts/overview) .
