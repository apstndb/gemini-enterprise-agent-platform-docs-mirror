---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/control-access
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/control-access
title: Control access to resources
description: Learn how to apply IAM policies to control access to online store, feature views, and feature group resources in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can set Identity and Access Management (IAM) policies to control access to the following Vertex AI Feature Store resources:

  - Feature groups

  - Online store instances

  - Feature views

An IAM policy is a collection of bindings, which associates one or more members, or principals, to an IAM role. You can include the following types of members in an IAM policy binding:

  - Individual user accounts

  - Google groups

  - Domains

  - Service accounts

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Set an IAM policy for a feature group

Use the following sample to set an IAM policy for an existing feature group.

### REST

To assign an IAM policy to a [`FeatureGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups#resource:-featureGroup) resource, send a `POST` request by using the [featureGroups.setIamPolicy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/setIamPolicy) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store instance is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the online store instance for which you want to set the IAM policy.
  - IAM\_ROLE\_NAME : The name of the IAM role to assign to the members. For a complete list of IAM roles for Gemini Enterprise Agent Platform, see [Access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .
  - USER\_EMAIL : Optional. The email address of the user account to whom the role is assigned.
  - GROUP\_EMAIL : Optional. The email address of the Google group to which the role is assigned.
  - DOMAIN\_NAME : Optional. The domain name to which the role is assigned.
  - SERVICE\_ACCOUNT\_EMAIL : Optional. The email address of the service account to which the role is assigned..

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME:setIamPolicy

Request JSON body:

    {
      "policy": {
        "bindings": [
          {
            "role": "IAM_ROLE_NAME",
            "members": [
              "user:USER_EMAIL",
              "group:GROUP_EMAIL",
              "domain:DOMAIN_NAME",
              "serviceAccount:SERVICE_ACCOUNT_EMAIL"
            ]
          }
        ]
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME:setIamPolicy"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME:setIamPolicy" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "bindings": [
      {
        "role": "IAM_ROLE_NAME",
        "members": [
          "user:USER_EMAIL",
          "group:GROUP_EMAIL",
          "domain:DOMAIN_NAME",
          "serviceAccount:SERVICE_ACCOUNT_EMAIL"
        ]
      }
      ],
      "etag": "etag"
    }

## Set an IAM policy for an online store

Use the following sample to set an IAM policy for an existing online store instance.

### REST

To assign an IAM policy to a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource, send a `POST` request by using the [featureOnlineStores.setIamPolicy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/setIamPolicy) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store instance is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance for which you want to set the IAM policy.
  - IAM\_ROLE\_NAME : The name of the IAM role to assign to the members. For a complete list of IAM roles for Gemini Enterprise Agent Platform, see [Access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .
  - USER\_EMAIL : Optional. The email address of the user account to whom the role is assigned.
  - GROUP\_EMAIL : Optional. The email address of the Google group to which the role is assigned.
  - DOMAIN\_NAME : Optional. The domain name to which the role is assigned.
  - SERVICE\_ACCOUNT\_EMAIL : Optional.The email address of the service account to which the role is assigned..

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME:setIamPolicy

Request JSON body:

    {
      "policy": {
        "bindings": [
          {
            "role": "IAM_ROLE_NAME",
            "members": [
              "user:USER_EMAIL",
              "group:GROUP_EMAIL",
              "domain:DOMAIN_NAME",
              "serviceAccount:SERVICE_ACCOUNT_EMAIL"
            ]
          }
        ]
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME:setIamPolicy"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME:setIamPolicy" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "bindings": [
      {
        "role": "IAM_ROLE_NAME",
        "members": [
          "user:USER_EMAIL",
          "group:GROUP_EMAIL",
          "domain:DOMAIN_NAME",
          "serviceAccount:SERVICE_ACCOUNT_EMAIL"
        ]
      }
      ],
      "etag": "etag"
    }

## Set an IAM policy for a feature view

Use the following sample to set an IAM policy for an existing feature view.

### REST

To assign an IAM policy to a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource, send a `POST` request by using the [featureViews.setIamPolicy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/setIamPolicy) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the feature view is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view for which you want to set the IAM policy.
  - IAM\_ROLE\_NAME : The name of the IAM role to assign to the members. For a complete list of IAM roles for Gemini Enterprise Agent Platform, see [Access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .
  - USER\_EMAIL : Optional. The email address of the user account to whom the role is assigned.
  - GROUP\_EMAIL : Optional. The email address of the Google group to which the role is assigned.
  - DOMAIN\_NAME : Optional. The domain name to which the role is assigned.
  - SERVICE\_ACCOUNT\_EMAIL : Optional.The email address of the service account to which the role is assigned..

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:setIamPolicy

Request JSON body:

    {
      "policy": {
        "bindings": [
          {
            "role": "IAM_ROLE_NAME",
            "members": [
              "user:USER_EMAIL",
              "group:GROUP_EMAIL",
              "domain:DOMAIN_NAME",
              "serviceAccount:SERVICE_ACCOUNT_EMAIL"
            ]
          }
        ]
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:setIamPolicy"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:setIamPolicy" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "bindings": [
      {
        "role": "IAM_ROLE_NAME",
        "members": [
          "user:USER_EMAIL",
          "group:GROUP_EMAIL",
          "domain:DOMAIN_NAME",
          "serviceAccount:SERVICE_ACCOUNT_EMAIL"
        ]
      }
      ],
      "etag": "etag"
    }

## What's next

  - Learn how to [list all features in a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-features) .

  - Learn how to [update a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

  - Learn how to [delete a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-feature) .

  - Learn how to [update a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup) .

  - [Online serving types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types) in Vertex AI Feature Store.
