---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-resources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-resources
title: Search for Vertex AI Feature Store resources
description: Learn how to perform an advanced search for feature groups, features, online store instances, and feature views in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can use the advanced search in Vertex AI Feature Store to search for online store instances, feature views, and features.

The following resources are included in the search results:

  - Vertex AI Feature Store resources on which you have the read permissions.

  - Feature views that are associated with feature groups and features, and aren't directly associated with the BigQuery data source. The metadata for these feature views aren't managed in Knowledge Catalog and aren't included in the search results.

For information on how to search for resource metadata in Data Catalog, see [Search for resource metadata in Data Catalog](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-feature-metadata) .

## Before you begin

Before you use the advanced search in Vertex AI Feature Store, you must complete the following steps:

1.  Enable the Dataplex API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

2.  Ensure that you have the following IAM permissions in the project:  
    `dataplex.projects.search`  
    Note that you don't need this permission in all the projects that you want to include within the scope of your search.

## Search for resources

To search for a Vertex AI Feature Store resource, follow these steps:

### Console

1.  Go to the **Advanced search** page.

2.  Enter the following search parameters:
    
      - **Keyword** : Optional. Enter the search keywords to search based on the resource name or metadata.
    
      - **Resource type** : Click the type of resource to search for. The available options include the following:
        
          - **All** —Include online stores, feature views, and feature groups in the search results.
        
          - **Online store** —Include only online store instances in the search results. You can optionally select a **Storage type** to filter the search results based on the type of online serving.
        
          - **Feature view** —Include only feature views in the search results. You can optionally provide a **Feature name** to filter the search results to include feature views associated with the feature name.
        
          - **Feature group** —Include only feature groups in the search results. You can optionally provide a **Feature name** to filter the search results based on the names of the features within the feature groups.
    
      - **Search all projects** : To search for resources in all Google Cloud projects, select this check box. To search for resources only in the project that you have selected, clear the check box.

3.  Click **Search** .
    
    To view the metadata for a resource in Knowledge Catalog, click the resource name in the search results, and then click **View in Dataplex** .

## What's next

  - Learn how to [search for resource metadata in Data Catalog](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/search-feature-metadata) .

  - Learn more about [Data Catalog](https://docs.cloud.google.com/data-catalog/docs/concepts/overview) .
