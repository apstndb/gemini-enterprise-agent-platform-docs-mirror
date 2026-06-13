---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/rolling-deployment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/rolling-deployment
title: Use a rolling deployment to replace a deployed model
description: Learn about using a rolling deployment to replace a deployed model.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

In a *rolling deployment* , a deployed model is replaced with a new version of the same model. The new model reuses the compute resources from the previous one.

In the rolling deployment request, the traffic split and `dedicatedResources` values are the same as for the previous deployment. After the rolling deployment completes, the traffic split is updated to show that all of the traffic from the previous `DeployedModel` has migrated to the new deployment.

Other configurable fields in `DeployedModel` (such as `serviceAccount` , `disableContainerLogging` , and `enableAccessLogging` ) are set to the same values as for the previous `DeployedModel` by default. However, you can optionally specify new values for these fields.

When a model is deployed using a rolling deployment, a new `DeployedModel` is created. The new `DeployedModel` receives a new ID that is different from that of the previous one. It also receives a new `revisionNumber` value in the `rolloutOptions` field.

If there are multiple rolling deployments targeting the same backing resources, the `DeployedModel` with the highest `revisionNumber` is treated as the intended final state.

As the rolling deployment progresses, all the existing replicas for the previous `DeployedModel` are replaced with replicas of the new `DeployedModel` . This happens quickly, and replicas are updated whenever the deployment has enough available replicas or enough surge capacity to bring up additional replicas.

Additionally, as the rolling deployment progresses, the traffic for the old `DeployedModel` is gradually migrated to the new `DeployedModel` . The traffic is load-balanced in proportion to the number of ready-to-serve replicas of each `DeployedModel` .

If the rolling deployment's new replicas never become ready because their health route consistently returns a non-200 response code, traffic isn't sent to those unready replicas. In this case, the rolling deployment eventually fails, and the replicas are reverted to the previous `DeployedModel` .

## Start a rolling deployment

To start a rolling deployment, include the `rolloutOptions` field in the model deployment request as shown in the following example.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - PREVIOUS\_DEPLOYED\_MODEL : The `DeployedModel` ID of a model on the same endpoint. This specifies the `DeployedModel` whose backing resources are to be reused. You can call `GetEndpoint` to get a list of deployed models on an endpoint along with their numeric IDs.
  - MAX\_UNAVAILABLE\_REPLICAS : The number of model replicas that can be taken down during the rolling deployment.
  - MAX\_SURGE\_REPLICAS : The number of additional model replicas that can be brought up during the rolling deployment. If this is set to zero, then only the existing capacity is used.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
        "rolloutOptions": {
          "previousDeployedModel": "PREVIOUS_DEPLOYED_MODEL",
          "maxUnavailableReplicas": "MAX_UNAVAILABLE_REPLICAS",
          "maxSurgeReplicas": "MAX_SURGE_REPLICAS"
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel"

#### PowerShell (Windows)

Save the request body in a file named `request.json` , and execute the following command:

    $headers = @{  }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

If desired, you can replace `maxSurgeReplicas` and `maxUnavailableReplicas` , or both, with percentage values, as shown in the following example.

### REST

Before using any of the request data, make the following replacements:

  - MAX\_UNAVAILABLE\_PERCENTAGE : The percentage of model replicas that can be taken down during the rolling deployment.
  - MAX\_SURGE\_PERCENTAGE : The percentage of additional model replicas that can be brought up during the rolling deployment. If this is set to zero, then only the existing capacity is used.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT/locations/LOCATION_ID/models/MODEL_ID",
        "rolloutOptions": {
          "previousDeployedModel": "PREVIOUS_DEPLOYED_MODEL",
          "maxUnavailablePercentage": "MAX_UNAVAILABLE_PERCENTAGE",
          "maxSurgePercentage": "MAX_SURGE_PERCENTAGE"
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel"

#### PowerShell (Windows)

Save the request body in a file named `request.json` , and execute the following command:

    $headers = @{  }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

## Roll back a rolling deployment

To roll back a rolling deployment, start a new rolling deployment of the previous model, using the ongoing rolling deployment's `DeployedModel` ID as the `previousDeployedModel` .

To get the `DeployedModel` ID for an ongoing deployment, set the parameter `allDeploymentStates=true` in the call to `GetEndpoint` , as shown in the following example.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - ENDPOINT\_ID : The ID for the endpoint.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID?allDeploymentStates=true

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID?allDeploymentStates=true"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID?allDeploymentStates=true" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID",
      "displayName": "rolling-deployments-endpoint",
      "deployedModels": [
        {
          "id": "2718281828459045",
          "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID@1",
          "displayName": "rd-test-model",
          "createTime": "2024-09-11T21:37:48.522692Z",
          "dedicatedResources": {
            "machineSpec": {
              "machineType": "e2-standard-2"
            },
            "minReplicaCount": 5,
            "maxReplicaCount": 5
          },
          "modelVersionId": "1",
          "state": "BEING_DEPLOYED"
        }
      ],
      "etag": "AMEw9yMs3TdZMn8CUg-3DY3wS74bkIaTDQhqJ7-Ld_Zp7wgT8gsEfJlrCOyg67lr9dwn",
      "createTime": "2024-09-11T21:22:36.588538Z",
      "updateTime": "2024-09-11T21:27:28.563579Z",
      "dedicatedEndpointEnabled": true,
      "dedicatedEndpointDns": "ENDPOINT_ID.LOCATION_ID-PROJECT_ID.prediction.vertexai.goog"
    }

## Constraints and limitations

  - The previous `DeployedModel` must be on the same endpoint as the new `DeployedModel` .
  - You can't create multiple rolling deployments with the same `previousDeployedModel` .
  - You can't create rolling deployments on top of a `DeployedModel` that isn't fully deployed. Exception: If `previousDeployedModel` is itself an in-progress rolling deployment, then a new rolling deployment can be created on top of it. This allows for rolling back deployments that start to fail.
  - Previous models don't automatically undeploy after a rolling deployment completes successfully. You can [undeploy the model manually](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/undeployModel) .
  - For rolling deployments on shared public endpoints, the `predictRoute` and `healthRoute` for the new model must be the same as for the previous model.
  - Rolling deployments aren't compatible with [model cohosting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/model-co-hosting) .
  - Rolling deployments can't be used for models that require [online explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/explainable-ai/getting-explanations) .
