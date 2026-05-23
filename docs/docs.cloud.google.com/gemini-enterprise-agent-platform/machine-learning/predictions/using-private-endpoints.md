---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints
title: Use private services access endpoints for online inference
description: Learn about using private services access endpoints for online inference.
data_source: docs.cloud.google.com
---

Using private services access endpoints to serve online inferences with Agent Platform provides a low-latency, secure connection to the Agent Platform online inference service. This guide shows how to configure private services access on Agent Platform by using [VPC Network Peering](https://docs.cloud.google.com/vpc/docs/vpc-peering) to peer your network with the Agent Platform online inference service.

## Overview

Before you serve online inference with private endpoints, you must [configure private services access to create peering connections between your network and Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-peering) . If you have already set this up, you can use your existing peering connections.

This guide covers the following tasks:

  - Verifying the status of your existing peering connections.
  - Verifying the necessary APIs are enabled.
  - Creating a private endpoint.
  - Deploying a model to a private endpoint.
      - Only support one model per private endpoint. This is different from a public Agent Platform endpoint where you can split traffic across multiple models deployed to one endpoint.
      - Private endpoint supports AutoML tabular and custom trained models.
  - Sending an inference to a private endpoint.
  - Cleaning up resources

## Check the status of existing peering connections

If you have existing peering connections you use with Agent Platform, you can list them to check status:

    gcloud compute networks peerings list --network NETWORK_NAME

You should see that the state of your peering connections is `ACTIVE` . Learn more about [active peering connections](https://docs.cloud.google.com/vpc/docs/peer-two-networks#peering-becomes-active) .

## Enable the necessary APIs

    gcloud services enable aiplatform.googleapis.com
    gcloud services enable dns.googleapis.com

## Create a private endpoint

To create a private endpoint, add the `--network` flag when you [create an endpoint using the Google Cloud CLI](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api#create-endpoint) :

    gcloud beta ai endpoints create \
      --display-name=ENDPOINT_DISPLAY_NAME \
      --network=FULLY_QUALIFIED_NETWORK_NAME \
      --region=REGION

Replace NETWORK\_NAME with the fully qualified network name:

    projects/PROJECT_NUMBER/global/networks/NETWORK_NAME

If you create the endpoint without specifying a network, then you create a public endpoint.

### Limitations of private endpoints

Note the following limitations for private endpoints:

  - Private endpoints don't support traffic splitting. As a workaround, you can create traffic splitting manually by deploying your model to multiple private endpoints, and splitting traffic among the resulting inference URLs for each private endpoint.
  - Private endpoints don't support SSL/TLS.
  - To enable access logging on a private endpoint, contact vertex-ai-feedback@google.com.
  - You can use only one network for all private endpoints in a Google Cloud project. If you want to change to another network, contact `vertex-ai-feedback@google.com` .
  - Client side retry on recoverable errors are highly recommended. These can include the following errors:
      - Empty response (HTTP error code `0` ), possibly due to a transient broken connection.
      - HTTP error codes `5xx` that indicate the service might be temporarily unavailable.
  - For the HTTP error code `429` that indicates the system is overloaded, consider slowing down traffic to mitigate this issue instead of retrying.
  - Inference requests from prediction services (such as [`PredictionServiceClient`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient) and [`PredictionServiceClient`](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1.PredictionServiceClient) ) aren't supported.
  - The Private Service Access endpoint does not support tuned foundation models. For a tuned foundation model, deploy it using a [Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vertex-psc-googleapis) .

### Monitor private endpoints

You can use the metrics dashboard to inspect the availability and latency of the traffic sent to a private endpoint.

To customize monitoring, query the following metrics in Cloud Monitoring:

  - `aiplatform.googleapis.com/prediction/online/private/response_count`
    
    The number of inference responses. You can filter this metric by `deployed_model_id` or HTTP response code.

  - `aiplatform.googleapis.com/prediction/online/private/prediction_latencies`
    
    The latency of the inference request in milliseconds. You can filter this metric by `deployed_model_id` , only for successful requests.

Learn [how to select, query, and display these metrics in Metrics Explorer](https://docs.cloud.google.com/monitoring/charts/metrics-selector) .

## Deploy a model

You can import a new model, or deploy an existing model that you have already uploaded. To upload a new model, use [`gcloud ai models upload`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload) . For more information, see [Import models to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .

1.  To deploy a model to a private endpoint, see the guide to [deploy models](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api#deploying_the_model) . Besides traffic splitting and manually enabling access logging, you can use any of the other options available for deploying custom-trained models. Refer to the [limitations of private endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints#limitations) to learn more about how they are different from public endpoints.

2.  After you deploy the endpoint, you can get the inference URI from the metadata of your private endpoint.
    
    1.  If you have the display name of your private endpoint, run this command to get the endpoint ID:
        
            ENDPOINT_ID=$(gcloud ai endpoints list \
                      --region=REGION \
                      --filter=displayName:ENDPOINT_DISPLAY_NAME \
                      --format="value(ENDPOINT_ID.scope())")
        
        Otherwise, to view the endpoint ID and display name for all of your endpoints, run the following command:
        
            gcloud ai endpoints list --region=REGION
    
    2.  Finally, to get the inference URI, run the following command:
        
            gcloud beta ai endpoints describe ENDPOINT_ID \
              --region=REGION \
              --format="value(deployedModels.privateEndpoints.predictHttpUri)"

### Private inference URI format

> **Note:** You might see `http://aiplatform HASH_ID .googleapis.com/v1/models/ DEPLOYED_MODEL_HASH_ID :predict` format for older private endpoints where: HASH\_ID is a hash ID in your inference URL that contains six alphanumeric characters and DEPLOYED\_MODEL\_HASH\_ID is a hash ID for your deployed model that contains 21 characters (two sets of 10 alphanumeric characters connected by a hyphen).

The inference URI looks different for private endpoints compared to Agent Platform public endpoints:

`http:// ENDPOINT_ID .aiplatform.googleapis.com/v1/models/ DEPLOYED_MODEL_ID :predict`

If you choose to undeploy the current model and redeploy with a new one, the domain name is reused but the path includes a different deployed model ID.

## Send an inference to a private endpoint

1.  [Create a Compute Engine instance](https://docs.cloud.google.com/compute/docs/instances/create-start-instance) in your VPC network. Make sure to [create the instance in the same VPC network that you have peered with Agent Platform](https://docs.cloud.google.com/compute/docs/instances/create-start-instance#creating_an_instance_in_a_specific_subnet) .

2.  SSH into your Compute Engine instance, and install your inference client, if applicable. Otherwise, you can use curl.

3.  When predicting, use the inference URL obtained from model deployment. In this example, you're sending the request from your inference client in your Compute Engine instance in the same VPC network:
    
        curl -X POST -d@PATH_TO_JSON_FILE  http://ENDPOINT_ID.aiplatform.googleapis.com/v1/models/DEPLOYED_MODEL_ID:predict
    
    In this sample request, PATH\_TO\_JSON\_FILE is the path to your inference request, saved as a JSON file. For example, `example-request.json` .

## Clean up resources

You can undeploy models and delete private endpoints [the same way as for public models and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/undeploy-model) .

## Example: Test private endpoints in Shared VPC

This example uses two Google Cloud projects with a Shared VPC network:

  - The *host project* hosts the Shared VPC network.
  - The *client project* hosts a Compute Engine instance where you run an inference client, such as curl, or your own REST client in the Compute Engine instance, to send inference requests.

When you create the Compute Engine instance in the client project, it must be within the custom subnet in the host project's Shared VPC network, and in the same region where the model gets deployed.

1.  Create the peering connections for private services access in the host project. Run [`gcloud services vpc-peerings connect`](https://docs.cloud.google.com/sdk/gcloud/reference/services/vpc-peerings/connect) :
    
        gcloud services vpc-peerings connect \
          --service=servicenetworking.googleapis.com \
          --network=HOST_SHARED_VPC_NAME \
          --ranges=PREDICTION_RESERVED_RANGE_NAME \
          --project=HOST_PROJECT_ID

2.  Create the endpoint in the client project, using the host project's network name. Run [`gcloud beta ai endpoints create`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/ai/endpoints/create) :
    
        gcloud beta ai endpoints create \
          --display-name=ENDPOINT_DISPLAY_NAME \
          --network=HOST_SHARED_VPC_NAME \
          --region=REGION \
          --project=CLIENT_PROJECT_ID

3.  [Send inference requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints#sending-inference-to-private-endpoint) , using the inference client within the client project.
