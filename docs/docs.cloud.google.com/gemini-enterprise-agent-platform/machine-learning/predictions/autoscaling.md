---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling
title: Scale inference nodes by using autoscaling
description: Learn about options for configuring Agent Platform inference resources to optimize cost.
data_source: docs.cloud.google.com
---

When you deploy a model for online inference as a [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#deployedmodel) , you can configure inference nodes to automatically scale. To do this, set [`dedicatedResources.maxReplicaCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DedicatedResources) to a greater value than `dedicatedResources.minReplicaCount` .

When you configure a `DeployedModel` , you must set `dedicatedResources.minReplicaCount` to at least 1. In other words, you cannot configure the `DeployedModel` to scale to 0 inference nodes when it is unused.

Alternatively, if you accept using the Scale To Zero feature ( [Preview](https://cloud.google.com/products#product-launch-stages) ), the `dedicatedResources.minReplicaCount` field can be set to 0 and the workload scales to zero replicas when there is no traffic on the endpoint. For more details, see [Scale To Zero](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling#scale-to-zero) .

By default, the deployment operation is only considered successful if the number of inference nodes reaches `dedicatedResources.minReplicaCount` before the deployment request timeout value. Otherwise, the deployment is marked as failed, and the underlying resources are released.

### Partially successful deployment and mutation

You can modify the default deployment behavior by setting `dedicatedResources.requiredReplicaCount` to a value that is less than `dedicatedResources.minReplicaCount` . In this case, when the number of inference nodes reaches `dedicatedResources.requiredReplicaCount` , the deployment operation is marked as successful, even though it is not yet complete. Deployment continues until `dedicatedResources.minReplicaCount` is reached. If `dedicatedResources.minReplicaCount` isn't reached before the deployment request time, the operation is still successful, but an error message for the failed replicas is returned in `DeployedModel.status.message` .

Quota for *Custom model serving* is calculated based on your [deployed model's](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#scaling) real-time usage of compute resources. If the sum of `maxReplicaCount` for all the deployments in your project is more than your project's quota, some deployments may fail to autoscale due to quota being exhausted.

Endpoints are scaled up and down per machine, but quota is calculated per CPU or GPU. For example, if your model is deployed to `a2-highgpu-2g` machine type, each active replica counts as 24 CPUs and 2 GPUs against your project's quota. For more information, see [Quota and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#serving) .

The inference nodes for batch inference don't automatically scale. Agent Platform uses [`BatchDedicatedResources.startingReplicaCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchDedicatedResources) and ignores `BatchDedicatedResources.maxReplicaCount` .

### Target utilization and configuration

By default, if you deploy a model without dedicated GPU resources, Gemini Enterprise Agent Platform automatically scales the number of replicas up or down so that CPU usage matches the default 60% target value.

By default, if you deploy a model with dedicated GPU resources (if [`machineSpec.accelerator_count`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec#FIELDS.accelerator_count) is greater than 0), Gemini Enterprise Agent Platform will automatically scale the number of replicas up or down so that the CPU or GPU usage, whichever is higher, matches the default 60% target value. Therefore, if your inference throughput is causing high GPU usage, but not high CPU usage, Agent Platform will scale up, and the CPU utilization will be very low, which will be visible in monitoring. Conversely, if your custom container is underutilizing the GPU, but has an unrelated process that raise CPU utilization higher than 60%, Agent Platform will scale up, even if this may not have been needed to achieve QPS and latency targets.

You can override the default threshold metric and target by specifying [`autoscalingMetricSpecs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DedicatedResources#autoscalingmetricspec) . Note that if your deployment is configured to scale based only on CPU usage, it won't scale up even if GPU usage is high.

The following autoscaling metrics are supported:

  - **CPU utilization** ( `aiplatform.googleapis.com/prediction/online/cpu/utilization` ): Scales based on CPU usage. Its unit is CPU utilization per replica. The target value is a percentage (0-100). The default target value is 60%.
  - **GPU utilization** ( `aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle` ): Scales based on GPU usage. Its unit is GPU utilization per replica. The target value is a percentage (0-100). The default target value is 60%.
  - **DCGM GPU utilization** ( [Preview](https://cloud.google.com/products#product-launch-stages) )( `prometheus.googleapis.com/vertex_dcgm_fi_dev_gpu_util` ): Scales based on DCGM metrics for GPU utilization. Its unit is GPU utilization per replica. The target value is a percentage (0-100). This metric is disabled by default.
  - **vLLM GPU KV cache usage percentage** ( [Preview](https://cloud.google.com/products#product-launch-stages) )( `prometheus.googleapis.com/vertex_vllm_gpu_cache_usage_perc` ): Scales based on vLLM metrics for GPU KV cache usage percentage. Its unit is GPU KV cache usage percentage per replica. The target value is a percentage (0-100). This metric is disabled by default.
  - **vLLM number of requests waiting** ( [Preview](https://cloud.google.com/products#product-launch-stages) )( `prometheus.googleapis.com/vertex_vllm_num_requests_waiting` ): Scales based on vLLM metrics for number of requests waiting. Its unit is number of requests waiting per replica. The target value is an integer. This metric is disabled by default.
  - **Request count** ( `aiplatform.googleapis.com/prediction/online/request_count` ): Scales based on the number of requests. Its unit is requests per minute per replica. The target value is an integer. This metric is disabled by default.
  - **Pub/Sub Queue Size** ( [Preview](https://cloud.google.com/products#product-launch-stages) , no Google Cloud CLI support) ( `pubsub.googleapis.com/subscription/num_undelivered_messages` ): Scales based on the number of undelivered messages of a Pub/Sub subscription. Its unit is undelivered messages per replica. The target value is an integer. This metric is disabled by default.

When configuring autoscaling, use METRIC\_NAME for the metric identifier and TARGET\_THRESHOLD for the target value.

#### Configure autoscaling during deployment

To configure autoscaling when deploying a model, use one of the following interfaces:

### gcloud

To configure autoscaling when deploying a model using the gcloud CLI, use the [`gcloud ai endpoints deploy-model`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) command.

Note that for Google Cloud CLI, the metric keyword is slightly different. Use the following:

  - cpu-usage
  - gpu-duty-cycle
  - dcgm-fi-dev-gpu-util
  - vllm-gpu-cache-usage-perc
  - vllm-num-requests-waiting
  - request-counts-per-minute

Before using any of the command data, make the following replacements:

  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **MODEL\_ID** : The ID of the model to deploy.
  - **MACHINE\_TYPE** : The machine type for the deployed model (e.g., `n1-standard-4` ).
  - **ACCELERATOR\_TYPE** : Optional. The type of GPU accelerator to attach (e.g., `NVIDIA_L4` ).
  - **ACCELERATOR\_COUNT** : Optional. The number of accelerators to attach to each machine.
  - **MIN\_REPLICA\_COUNT** : The minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The maximum number of replicas for autoscaling.
  - **METRIC\_NAME\_GCLOUD** : The identifier of the autoscaling metric.
  - **TARGET\_THRESHOLD** : The target value for the specified metric.

<!-- end list -->

    gcloud ai endpoints deploy-model ENDPOINT_ID \
        --project=PROJECT_ID \
        --region=LOCATION \
        --model=MODEL_ID \
        --display-name=DEPLOYED_MODEL_DISPLAY_NAME \
        --machine-type=MACHINE_TYPE \
        --accelerator-type=ACCELERATOR_TYPE \
        --accelerator-count=ACCELERATOR_COUNT \
        --min-replica-count=MIN_REPLICA_COUNT \
        --max-replica-count=MAX_REPLICA_COUNT \
        --autoscaling-metric-specs=METRIC_NAME_GCLOUD=TARGET_THRESHOLD

### REST

To configure autoscaling when deploying a model using the REST API, use the [`projects.locations.endpoints.deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) method.

Before using any of the request data, make the following replacements:

  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **MODEL\_ID** : The ID of the model to deploy.
  - **DEPLOYED\_MODEL\_DISPLAY\_NAME** : A display name for the deployed model.
  - **MACHINE\_TYPE** : The machine type for the deployed model (e.g., `n1-standard-4` ).
  - **ACCELERATOR\_TYPE** : Optional. The type of GPU accelerator to attach (e.g., `NVIDIA_L4` ).
  - **ACCELERATOR\_COUNT** : Optional. The number of accelerators to attach to each machine.
  - **MIN\_REPLICA\_COUNT** : The minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The maximum number of replicas for autoscaling.
  - **METRIC\_NAME** : The identifier of the autoscaling metric.
  - **TARGET\_THRESHOLD** : The target value for the specified metric.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_DISPLAY_NAME",
        "dedicatedResources": {
          "machineSpec": {
            "machineType": "MACHINE_TYPE",
            "acceleratorType": "ACCELERATOR_TYPE",
            "acceleratorCount": ACCELERATOR_COUNT
          },
          "minReplicaCount": MIN_REPLICA_COUNT,
          "maxReplicaCount": MAX_REPLICA_COUNT,
          "autoscalingMetricSpecs": [
            {
              "metricName": "METRIC_NAME",
              "target": TARGET_THRESHOLD
            }
          ]
        }
      }
    }

For Pub/Sub Queue Size metrics based autoscaling ( [Preview](https://cloud.google.com/products#product-launch-stages) ), additional Pub/Sub subscription information is needed:

  - **PUBSUB\_SUBSCRIPTION\_PROJECT\_ID** : The project ID of the Pub/Sub subscription.
  - **PUBSUB\_SUBSCRIPTION\_ID** : The ID of the Pub/Sub subscription. This field has a maximum length of 63 characters.

<!-- end list -->

``` 
      "autoscalingMetricSpecs": [
        {
          "metricName": "METRIC_NAME",
          "target": TARGET_THRESHOLD,
          "monitoredResourceLabels": {
            "project_id": "PUBSUB_SUBSCRIPTION_PROJECT_ID",
            "subscription_id": "PUBSUB_SUBSCRIPTION_ID"
          },
        }
      ]
```

### Python

The Python SDK autoscaling is configured through parameter names in the `deploy()` function call. The sample command uses concurrency-based autoscaling as an example. The configurable autoscaling parameters are:

  - autoscaling\_target\_cpu\_utilization
  - autoscaling\_target\_accelerator\_duty\_cycle
  - autoscaling\_target\_dcgm\_fi\_dev\_gpu\_util
  - autoscaling\_target\_vllm\_gpu\_cache\_usage\_perc
  - autoscaling\_target\_vllm\_num\_requests\_waiting
  - autoscaling\_target\_request\_count\_per\_minute

To configure autoscaling when deploying a model using the Agent Platform SDK for Python:

Before running the code, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **MODEL\_ID** : The ID of the model to deploy.
  - **DEPLOYED\_MODEL\_DISPLAY\_NAME** : A display name for the deployed model.
  - **MACHINE\_TYPE** : The machine type for the deployed model (e.g., `n1-standard-4` ).
  - **ACCELERATOR\_TYPE** : Optional. The type of GPU accelerator to attach (e.g., `NVIDIA_L4` ).
  - **ACCELERATOR\_COUNT** : Optional. The number of accelerators to attach to each machine.
  - **MIN\_REPLICA\_COUNT** : The minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The maximum number of replicas for autoscaling.
  - **METRIC\_NAME** : The identifier of the autoscaling metric.
  - **TARGET\_THRESHOLD** : The target value for the specified metric.

<!-- end list -->

    from google.cloud import aiplatform
    
    # Initialize Agent Platform
    aiplatform.init(project="PROJECT_ID", location="LOCATION")
    
    # Get the model from Model Registry
    model = aiplatform.Model("MODEL_ID")
    
    # Get the endpoint
    endpoint = aiplatform.Endpoint("ENDPOINT_ID")
    
    # Deploy the model to the endpoint
    model.deploy(
      endpoint=endpoint,
      machine_type="MACHINE_TYPE",
      accelerator_type="ACCELERATOR_TYPE",
      accelerator_count=ACCELERATOR_COUNT,
      min_replica_count=MIN_REPLICA_COUNT,
      max_replica_count=MAX_REPLICA_COUNT,
      autoscaling_target_request_count_per_minute=TARGET_THRESHOLD,
    )

For Pub/Sub Queue Size metrics based autoscaling ( [Preview](https://cloud.google.com/products#product-launch-stages) , only aiplatform\_v1beta1 is supported), additional Pub/Sub subscription information is needed:

  - **PUBSUB\_SUBSCRIPTION\_PROJECT\_ID** : The project ID of the Pub/Sub subscription.
  - **PUBSUB\_SUBSCRIPTION\_ID** : The ID of the Pub/Sub subscription.

<!-- end list -->

    from google.cloud import aiplatform_v1beta1 as aiplatform
    from google.api_core.client_options import ClientOptions
    
    # Initialize the EndpointServiceClient
    client_options = ClientOptions(api_endpoint="LOCATION-aiplatform.googleapis.com")
    client = aiplatform.EndpointServiceClient(client_options=client_options)
    
    # Specify the location
    location = "projects/PROJECT_NUMBER/locations/LOCATION"
    
    model_name = "projects/PROJECT_NUMBER/locations/LOCATION/models/MODEL_ID"
    autoscaling_metric_specs = [
        {"metric_name": "pubsub.googleapis.com/subscription/num_undelivered_messages", "target": TARGET_THRESHOLD, "monitored_resource_labels":{"project_id": "PUBSUB_SUBSCRIPTION_PROJECT_ID","subscription_id": "PUBSUB_SUBSCRIPTION_ID"}}
    ]
    
    deployed_model = aiplatform.DeployedModel(
        model=model_name,
        display_name="DEPLOYED_MODEL_DISPLAY_NAME",
        dedicated_resources=aiplatform.DedicatedResources(
            machine_spec=aiplatform.MachineSpec(
                machine_type="MACHINE_TYPE"
            ),
            min_replica_count=MIN_REPLICA_COUNT,
            max_replica_count=MAX_REPLICA_COUNT,
            autoscaling_metric_specs=autoscaling_metric_specs
        )
    )
    
    deploy_request = aiplatform.DeployModelRequest(
        deployed_model=deployed_model,
        endpoint="projects/PROJECT_NUMBER/locations/LOCATION/endpoints/ENDPOINT_ID",
        traffic_split={"0": 100}
    )
    
    deploy_operation = client.deploy_model(deploy_request)
    print("Long-running operation initiated to deploy model.")
    deploy_operation.result()
    
    print("Model deployed to endpoint.")

#### Update autoscaling configuration

To update an existing autoscaling configuration, use one of the following interfaces:

### REST

To update the autoscaling configuration of a deployed model using the REST API, use the [`projects.locations.endpoints.mutateDeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) method.

Before using any of the request data, make the following replacements:

  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **DEPLOYED\_MODEL\_ID** : The ID of the deployed model to update.
  - **MIN\_REPLICA\_COUNT** : The new minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The new maximum number of replicas for autoscaling.
  - **METRIC\_NAME** : The identifier of the autoscaling metric.
  - **TARGET\_THRESHOLD** : The target value for the specified metric.

HTTP method and URL:

    PATCH https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:mutateDeployedModel

Request JSON body:

    {
      "deployedModel": {
        "id": "DEPLOYED_MODEL_ID",
        "dedicatedResources": {
          "minReplicaCount": MIN_REPLICA_COUNT,
          "maxReplicaCount": MAX_REPLICA_COUNT,
          "autoscalingMetricSpecs": [
            {
              "metricName": "METRIC_NAME",
              "target": TARGET_THRESHOLD
            }
          ]
        }
      },
      "updateMask": {
        "paths": [
          "dedicated_resources.min_replica_count",
          "dedicated_resources.max_replica_count",
          "dedicated_resources.autoscaling_metric_specs"
        ]
      }
    }

For Pub/Sub Queue Size metrics based autoscaling ( [Preview](https://cloud.google.com/products#product-launch-stages) ), additional Pub/Sub subscription information is needed:

  - **PUBSUB\_SUBSCRIPTION\_PROJECT\_ID** : The project ID of the Pub/Sub subscription.
  - **PUBSUB\_SUBSCRIPTION\_ID** : The ID of the Pub/Sub subscription.

<!-- end list -->

``` 
      "autoscalingMetricSpecs": [
        {
          "metricName": "METRIC_NAME",
          "target": TARGET_THRESHOLD,
          "monitoredResourceLabels": {
            "project_id": "PUBSUB_SUBSCRIPTION_PROJECT_ID",
            "subscription_id": "PUBSUB_SUBSCRIPTION_ID"
          },
        }
      ]
```

### Scale To Zero ( [Preview](https://cloud.google.com/products#product-launch-stages) )

The Scale To Zero feature lets you automatically scale your model server deployments to zero replicas when there is no traffic, resulting in no billing during this time.

When traffic reaches the target scaled-down endpoint, a `429 - Model is not yet ready for inference. Please wait while model completes scale-up from zero, then try your request again` response is received, the request is dropped, and a scale-up signal is sent to the target model server.

This results in the model server scaling up from zero to whatever value is specified in the `DedicatedResources.initial_replica_count` field. The default value is 1.

This feature is designed for the following use cases:

  - Deployments with long periods of no traffic on a regular basis.
  - Endpoints that typically receive traffic during business hours and idle at other times.

#### Enablement and usage

The Scale To Zero feature **cannot** be enabled on shared public endpoints. All other endpoint types are compatible.

To enable Scale To Zero, specify `min_replica_count=0` in the `DedicatedResources` section of your deploy-model request (targeting the v1beta1 version of the Vertex Prediction API).

**Optional parameters**

In `DedicatedResources` , you can specify and `initial_replica_count` value between 1 and `max_replica_count` (inclusive).

There is also a new `ScaleToZeroSpec` section added to `DedicatedResources` which allows for configuration over two parameters related to Scale to Zero:

  - `min_scaleup_period` : duration (in seconds) before a model server is enrolled in Scale to Zero evaluation. The deployment won't try to scale back down to zero replicas until this duration has passed, even if there is no traffic. This enables for a buffer value during initial deployment and subsequent scale-up events before traffic is checked against the target endpoint (which may result in the scaling down of the deployment).
      - Default value: 1 hour (3600s)
      - Minimum value: 5 minutes (300s)
      - Max value: 8 hours (28800s).
  - `idle_scaledown_period` : duration (in seconds) of no traffic before scaling down the target model server to zero replicas.
      - Default value: 1 hour (3600s)
      - Minimum value: 5 minutes (300s)
      - Max value: 8 hours (28800s).

**Expected behaviors**

A request sent to a scaled-down model will return a 429 response with `Model is not yet ready for inference. Please wait and then try your request again` .

Wait and then try your request again. Note that any requests sent in this phase will be dropped.

**Limitations**

  - Scale To Zero is only compatible with single model deployments and one model per endpoint.

  - Scale To Zero doesn't support multi-host GPU or multi-host TPU deployments. However, single-host GPU or TPU deployments are compatible.

  - Scale To Zero cannot be enabled on shared public endpoints, all other endpoint types are compatible.

  - Without reservations, it is possible to experience stockouts when scaling back up from a scaled-down state (depending on machine type).

  - DeployedModels which are scaled to zero for longer than 30 days (due to receiving no traffic) are automatically undeployed.

### gcloud

To configure scale-to-zero when deploying a model using the gcloud CLI, use the [`gcloud beta ai endpoints deploy-model`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) command.

Before using any of the command data, make the following replacements:

  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **MODEL\_ID** : The ID of the model to deploy.
  - **MACHINE\_TYPE** : The machine type for the deployed model (e.g., `n1-standard-4` ).
  - **ACCELERATOR\_TYPE** : Optional. The type of GPU accelerator to attach (e.g., `NVIDIA_L4` ).
  - **ACCELERATOR\_COUNT** : Optional. The number of accelerators to attach to each machine.
  - **MIN\_REPLICA\_COUNT** : The minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The maximum number of replicas for autoscaling.

<!-- end list -->

    gcloud beta ai endpoints deploy-model ENDPOINT_ID \
        --project=PROJECT_ID \
        --region=LOCATION \
        --model=MODEL_ID \
        --display-name=DEPLOYED_MODEL_DISPLAY_NAME \
        --machine-type=MACHINE_TYPE \
        --accelerator-type=ACCELERATOR_TYPE \
        --accelerator-count=ACCELERATOR_COUNT \
        --min-replica-count=MIN_REPLICA_COUNT \
        --max-replica-count=MAX_REPLICA_COUNT \
        --min-scaleup-period=300s \
        --idle-scaledown-period=300s

### REST

To configure scale-to-zero when deploying a model using the REST API, use the [`projects.locations.endpoints.deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) method.

Before using any of the request data, make the following replacements:

  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **MODEL\_ID** : The ID of the model to deploy.
  - **DEPLOYED\_MODEL\_DISPLAY\_NAME** : A display name for the deployed model.
  - **MACHINE\_TYPE** : The machine type for the deployed model (e.g., `n1-standard-4` ).
  - **ACCELERATOR\_TYPE** : Optional. The type of GPU accelerator to attach (e.g., `NVIDIA_L4` ).
  - **ACCELERATOR\_COUNT** : Optional. The number of accelerators to attach to each machine.
  - **MIN\_REPLICA\_COUNT** : The minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The maximum number of replicas for autoscaling.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_DISPLAY_NAME",
        "dedicatedResources": {
          "machineSpec": {
            "machineType": "MACHINE_TYPE",
            "acceleratorType": "ACCELERATOR_TYPE",
            "acceleratorCount": ACCELERATOR_COUNT
          },
          "minReplicaCount": MIN_REPLICA_COUNT,
          "maxReplicaCount": MAX_REPLICA_COUNT,
          "scale_to_zero_spec": {
              "min_scaleup_period": "300s",
              "idle_scaledown_period": "300s",
          },
        }
      }
    }

### Python

The Python SDK scale-to-zero is configured through the v1beta1 API client.

Before running the code, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region of your endpoint.
  - **ENDPOINT\_ID** : The ID of your endpoint.
  - **MODEL\_ID** : The ID of the model to deploy.
  - **DEPLOYED\_MODEL\_DISPLAY\_NAME** : A display name for the deployed model.
  - **MACHINE\_TYPE** : The machine type for the deployed model (e.g., `n1-standard-4` ).
  - **ACCELERATOR\_TYPE** : Optional. The type of GPU accelerator to attach (e.g., `NVIDIA_L4` ).
  - **ACCELERATOR\_COUNT** : Optional. The number of accelerators to attach to each machine.
  - **MIN\_REPLICA\_COUNT** : The minimum number of replicas for autoscaling.
  - **MAX\_REPLICA\_COUNT** : The maximum number of replicas for autoscaling.
  - **METRIC\_NAME** : The identifier of the autoscaling metric.
  - **TARGET\_THRESHOLD** : The target value for the specified metric.

<!-- end list -->

    from google.cloud import aiplatform
    
    # Initialize Agent Platform
    aiplatform.init(project="PROJECT_ID", location="LOCATION")
    
    # Get the model from Model Registry
    model = aiplatform.Model("MODEL_ID")
    
    # Get the endpoint
    endpoint = aiplatform.Endpoint("ENDPOINT_ID")
    
    # Deploy the model to the endpoint
    model.deploy(
      endpoint=endpoint,
      machine_type="MACHINE_TYPE",
      accelerator_type="ACCELERATOR_TYPE",
      accelerator_count=ACCELERATOR_COUNT
      min_replica_count=MIN_REPLICA_COUNT,
      max_replica_count=MAX_REPLICA_COUNT,
      autoscaling_target_request_count_per_minute=TARGET_THRESHOLD,
    )
    
    import google.auth.transport.requests
    import urllib3
    
    # pip install google-cloud-aiplatform for this dependency
    from google.cloud import aiplatform
    from google.cloud.aiplatform_v1beta1.services import endpoint_service # For EndpointServiceClient
    from google.cloud.aiplatform_v1beta1 import types as aiplatform_v1beta1_types # For message types
    
    PROJECT_NUMBER = "PROJECT_ID"
    LOCATION = "LOCATION"
    ENDPOINT_DISPLAY_NAME = "stz-sdk-test"
    MODEL_ID="MODEL_ID"
    
    # Full resource name of your existing model in Model Registry
    # e.g., "projects/your-gcp-project-id/locations/us-central1/models/your-model-id"
    MODEL_RESOURCE_NAME = f"projects/{PROJECT_NUMBER}/locations/{LOCATION}/models/{MODEL_ID}"
    
    # Deployment settings
    MACHINE_TYPE = "MACHINE_TYPE"
    ACCELERATOR_TYPE ="ACCELERATOR_TYPE",
    ACCELERATOR_COUNT =ACCELERATOR_COUNT
    
    # Disable InsecureRequestWarning for the requests part as in your snippet
    urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
    
    # The AI Platform services require regional API endpoints.
    client_options = {"api_endpoint": f"{LOCATION}-aiplatform.googleapis.com"}
    endpoint_service_client = endpoint_service.EndpointServiceClient(client_options=client_options)
    
    def main():
        aiplatform.init(project=PROJECT_NUMBER, location=LOCATION)
        model_to_deploy = aiplatform.Model(model_name=MODEL_RESOURCE_NAME) # Initialize model object
    
        try:
            # # --- 1. Create an Endpoint ---
            print(f"\nCreating endpoint '{ENDPOINT_DISPLAY_NAME}'...")
            endpoint = aiplatform.Endpoint.create(
                display_name=ENDPOINT_DISPLAY_NAME,
                project=PROJECT_NUMBER,
                location=LOCATION,
                sync=True, # Wait for creation to complete
                dedicated_endpoint_enabled=True,
            )
            print(f"Endpoint created: {endpoint.resource_name}")
            endpoint_numeric_id = endpoint.name # This is the numeric ID
            print(f"Numeric Endpoint ID for URL: {endpoint_numeric_id}")
    
            print(f"\nFetching model details for: {MODEL_RESOURCE_NAME}")
            model_to_deploy = aiplatform.Model(model_name=MODEL_RESOURCE_NAME)
    
            # --- 2. Deploy the Model ---
            print(f"\nDeploying model '{model_to_deploy.resource_name}' to endpoint '{endpoint.display_name}'...")
            deployed_model_config = aiplatform_v1beta1_types.DeployedModel(
                model=model_to_deploy.resource_name,
                dedicated_resources=aiplatform_v1beta1_types.DedicatedResources(
                    machine_spec=aiplatform_v1beta1_types.MachineSpec(
                        machine_type=MACHINE_TYPE,
                        accelerator_type=ACCELERATOR_TYPE,
                        accelerator_count=ACCELERATOR_COUNT,
                    ),
                    initial_replica_count=1,
                    min_replica_count=0,
                    max_replica_count=1,
                    scale_to_zero_spec=aiplatform_v1beta1_types.DedicatedResources.ScaleToZeroSpec(
                        min_scaleup_period=300,
                        idle_scaledown_period=300,
                    )
                ),
            )
    
            deploy_model_request = aiplatform_v1beta1_types.DeployModelRequest(
                endpoint=endpoint.resource_name,
                deployed_model=deployed_model_config,
            )
    
            # Alternatively, if you've got an existing endpoint, use:
            # endpoint_path = endpoint_service_client.endpoint_path(
            #     project=PROJECT_NUMBER, location=LOCATION, endpoint={ENDPOINT_ID}
            # )
    
            # deploy_model_request = aiplatform_v1beta1_types.DeployModelRequest(
            #     endpoint=endpoint_path,
            #     deployed_model=deployed_model_config,
            # )
    
            print("\nSending v1beta1 DeployModelRequest...")
            operation = endpoint_service_client.deploy_model(request=deploy_model_request)
    
            print("Waiting for v1beta1 update deploy model operation to complete (this can take several minutes)...")
            operation.result()
            print("Model deployed successfully.")
    
        except Exception as e:
            print(f"\nAn error occurred: {e}")
    
    if __name__ == "__main__":
        main()

### Manage resource usage

You can [monitor your endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics#endpoint_monitoring_metrics) to track metrics like CPU and accelerator usage, number of requests, latency, and the current and target number of replicas. This information can help you understand your endpoint's resource usage and scaling behavior.

Keep in mind that each replica runs only a single container. This means that if an inference container can't fully use the selected compute resource, such as single threaded code for a multi-core machine, or a custom model that calls another service as part of making the inference, your nodes may not scale up.

For example, if you're using [FastAPI](https://fastapi.tiangolo.com/) , or any model server that has a configurable number of workers or threads, there are many cases where having more than one worker can increase resource utilization, which improves the ability for the service to automatically scale the number of replicas.

We generally recommend starting with one worker or thread per core. If you notice that CPU utilization is low, especially under high load, or your model isn't scaling up because CPU utilization is low, then increase the number of workers. On the other hand, if you notice that utilization is too high and your latencies increase more than expected under load, try using fewer workers. If you're already using only a single worker, try using a smaller machine type.

### Scaling behavior and lag

Gemini Enterprise Agent Platform adjusts the number of replicas every 15 seconds using data from the previous 5-minute window. For each 15-second cycle, the system measures the server utilization and generates a target number of replicas based on the following formula:

`target # of replicas = Ceil(current # of replicas * (current utilization / target utilization))`

For example, if you have two replicas that are being utilized at 100%, the target is 4:

`4 = Ceil(3.33) = Ceil(2 * (100% / 60%))`

Another example, if you have 10 replicas and utilization drops to 1%, the target is 1:

`1 = Ceil(.167) = Ceil(10 * (1% / 60%))`

At the end of each 15-second cycle, the system adjusts the number of replicas to match the highest target value from the previous 5-minute window. Notice that because the highest target value is chosen, your endpoint won't scale down if there is a sudden increase in utilization during that 5 minute window, even if overall utilization is very low. On the other hand, if the system needs to be scaled up, it will do that within 15 seconds, because the highest target value is chosen instead of the average.

Keep in mind that even after Gemini Enterprise Agent Platform adjusts the number of replicas, it takes time to start up or turn down the replicas. Thus there is an additional delay before the endpoint can adjust to the traffic. The main factors that contribute to this time include the following:

  - The time to provision and start the Compute Engine VMs
  - The time to download the container from the registry
  - The time to load the model from storage

The best way to understand the real world scaling behavior of your model is to run a load test and optimize the characteristics that matter for your model and your use case. If the autoscaler isn't scaling up fast enough for your application, provision enough `min_replicas` to handle your expected baseline traffic.

### Update the scaling configuration

If you specified either [`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DedicatedResources) or [`AutomaticResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/AutomaticResources) when you deployed the model, you can update the scaling configuration without redeploying the model by calling [`mutateDeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) .

For example, the following request updates `max_replica` , `autoscaling_metric_specs` , and disables container logging.

    {
      "deployedModel": {
        "id": "2464520679043629056",
        "dedicatedResources": {
          "maxReplicaCount": 9,
          "autoscalingMetricSpecs": [
            {
              "metricName": "aiplatform.googleapis.com/prediction/online/cpu/utilization",
              "target": 50
            }
          ]
        },
        "disableContainerLogging": true
      },
      "update_mask": {
        "paths": [
          "dedicated_resources.max_replica_count",
          "dedicated_resources.autoscaling_metric_specs",
          "disable_container_logging"
        ]
      }
    }

Usage notes:

  - You can't change the machine type or switch from `DedicatedResources` to `AutomaticResources` or the other way around. The only scaling configuration fields you can change are: `min_replica` , `max_replica` , `required_replica` , and `AutoscalingMetricSpec` ( `DedicatedResources` only).
  - You must list every field you need to update in `updateMask` . Unlisted fields are ignored.
  - The [DeployedModel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel) must be in a `DEPLOYED` state. There can be at most one active mutate operation per deployed model.
  - [`mutateDeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) also lets you enable or disable container logging. For more information, see [Online inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging) .
