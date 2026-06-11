---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/endpoint-access-control
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/endpoint-access-control
title: Control access to Agent Platform endpoints
description: Learn how to control access to a Gemini Enterprise Agent Platform endpoint by setting an IAM policy on it.
data_source: docs.cloud.google.com
---

This page discusses how to control access to a Gemini Enterprise Agent Platform endpoint by setting an IAM policy on it. It assumes that you're already familiar with IAM concepts such as policies, roles, permissions, and principals as described in [Agent Platform access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) and [Concepts related to access management](https://docs.cloud.google.com/iam/docs/overview#concepts_related_to_access_management) .

An IAM [policy](https://docs.cloud.google.com/iam/docs/policies#structure) includes one or more role bindings that define which IAM roles are associated with which principals. A role is a collection of permissions that you grant to a [principal](https://docs.cloud.google.com/iam/docs/overview#concepts_related_identity) . Gemini Enterprise Agent Platform provides [predefined roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#predefined-roles) that you can use in your policies. Or you can create your own custom roles.

## Get an IAM policy

You can view the current IAM policy on a Gemini Enterprise Agent Platform endpoint by using the REST API. To do so, you must have `endpoints.getIamPolicy` permission on the endpoint or the project. The Agent Platform Administrator role ( `roles/aiplatform.admin` ) grants this permission.

### REST

To get the IAM policy from a resource, send a `POST` request that uses the [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/getIamPolicy) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where the endpoint is located, for example, `us-central1` .
  - PROJECT\_ID : Your Google Cloud project ID.
  - ENDPOINT\_ID : The ID for the endpoint.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:getIamPolicy

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:getIamPolicy"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:getIamPolicy" | Select-Object -Expand Content

You should receive a JSON response with the current IAM policy:

    {
      "version": 1,
      "etag": "BwXTmICm7mI",
      "bindings": [
        {
          "role": "roles/aiplatform.user",
          "members": [
            "user:example@example.com"
          ]
        }
      ]
    }

## Set an IAM policy

You can set an IAM policy on an endpoint by using the REST API. To do so, you must have `endpoints.setIamPolicy` permission on the endpoint or the project. The Agent Platform Administrator role ( `roles/aiplatform.admin` ) grants this permission.

### REST

To set the IAM policy on a resource, send a `POST` request that uses the [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/setIamPolicy) method.

Setting an IAM policy overrides any existing policy; changes are not appended. To modify a resource's existing policy, use the `getIamPolicy` method to get its existing policy and then make modifications. Include your modified policy along with the `etag` in your `setIamPolicy` request.

If you receive a `409` error code, this means that a concurrent `setIamPolicy` request already updated the policy. Use the `getIamPolicy` method to get the policy's updated `etag` , and then retry the `setIamPolicy` request with the new `etag` .

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where the endpoint is located, for example, `us-central1` .
  - PROJECT\_ID : Your Google Cloud project ID.
  - ENDPOINT\_ID : The ID for the endpoint.
  - ROLE : An IAM role that includes the permissions to grant, such as `roles/aiplatform.user` .
  - PRINCIPAL : The principal that is granted the role's permissions, such as `user:myuser@example.com` .
  - ETAG : A string value that is used to prevent simultaneous updates of a policy from overwriting each other. This value is returned as part of the `getIamPolicy` response.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:setIamPolicy

Request JSON body:

    {
      "policy": {
        "bindings": [
          {
            "role": "ROLE",
            "members": [
              "PRINCIPAL"
            ]
          },
          ...
        ],
        "etag": "ETAG"
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:setIamPolicy"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:setIamPolicy" | Select-Object -Expand Content

You should receive a JSON response with the current IAM policy:

    {
      "version": 1,
      "etag": "BwXTmICm7mI",
      "bindings": [
        {
          "role": "roles/aiplatform.user",
          "members": [
            "user:example@example.com"
          ]
        }
      ]
    }

## Verify a user's IAM permissions for an endpoint

You can verify whether the currently authenticated user has specific IAM permissions for an endpoint.

### REST

To verify whether a user has specific IAM permissions for a resource, send a `POST` request that uses the [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/testIamPermissions) method. The following example lets you test whether the currently authenticated user has a set of IAM permissions for an endpoint.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where the endpoint is located, for example, `us-central1` .
  - PROJECT\_ID : Your Google Cloud project ID.
  - ENDPOINT\_ID : The ID for the endpoint.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:testIamPermissions

Request JSON body:

    {
      "permissions": [
        "aiplatform.googleapis.com/aiplatform.endpoints.get",
        "aiplatform.googleapis.com/aiplatform.endpoints.predict"
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:testIamPermissions"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:testIamPermissions" | Select-Object -Expand Content

You should receive a JSON response similar to the following. The response includes only those permissions from the request JSON body that are available to the currently authenticated user.

    {
      "permissions": [
        "aiplatform.googleapis.com/aiplatform.endpoints.get",
        "aiplatform.googleapis.com/aiplatform.endpoints.predict"
      ]
    }

## What's next

To learn more about how to set up projects with more secure access control of endpoints, see [Set up a project for a team](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/set-up-project) .
