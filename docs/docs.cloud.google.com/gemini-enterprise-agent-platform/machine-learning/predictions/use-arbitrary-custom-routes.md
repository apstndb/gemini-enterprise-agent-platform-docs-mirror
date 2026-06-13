---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-arbitrary-custom-routes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-arbitrary-custom-routes
title: Use arbitrary custom routes on a single deployment
description: Learn about using arbitrary custom routes on a single deployment.
data_source: docs.cloud.google.com
---

> ****
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

In modern LLM serving, model servers implement and support multiple inference routes for different purposes. For those use cases, Vertex Inference recommends to use the `invoke` method to access multiple routes on a single deployment.

The `invoke` method can be enabled when uploading a [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) by setting `invokeRoutePrefix` as `"/*"` . Once the Model is deployed to an endpoint, any non-root route on the model server will be accessible with invoke HTTP call. Such as, "/invoke/foo/bar" would be forwarded as "/foo/bar" to the model server.

This feature is in the public preview stage and has the following restrictions:

  - Invoke enabled models can only be deployed to dedicated endpoint.
  - Only HTTP calls are supported for invoke enabled models, and RPC is not supported.
  - When uploading a model, only one of `predictRoute` or `invokeRoutePrefix` can be set. The default value is `predictRoute` . If `invokeRoutePrefix` field is set on a Model, all other Vertex routes besides `invoke` (e.g. `:predict` , `:rawPredict` ..) will be disabled once deployed.
  - `"/*"` is the only allowed value for `invokeRoutePrefix` , and it exposes all non-root path. Cautious handling for routes that you don't want to expose is advised.

## Uploading an invoke enabled Model

    from google.cloud import aiplatform
    
    invoke_enabled_model = aiplatform.Model.upload(
        display_name="invoke-enabled-model",
        serving_container_image_uri=IMAGE_URI,
        serving_container_invoke_route_prefix="/*",
        serving_container_health_route=HEALTH_ROUTE,
        serving_container_environment_variables={"KEY": "VALUE"},
        serving_container_args=[],
        sync=True,
    )

## Deploying an invoke enabled Model

    dedicated_endpoint = aiplatform.Endpoint.create(
        display_name="dedicated-endpoint-for-invoke-enabled-model",
        dedicated_endpoint_enabled=True,
        sync=True,
    )
    
    dedicated_endpoint.deploy(
        model=invoke_enabled_model,
        traffic_percentage=100,
        machine_type=MACHINE_TYPE,
        accelerator_type=ACCELERATOR_TYPE,
        accelerator_count=1,
        max_replica_count=1,
    )

## Making an inference request on an arbitrary custom route

Invoke route allows access to all non-root request paths in the deployment. For example, `/invoke/foo/bar` will be forwarded as `/foo/bar` to the model server. There are two ways to access the route.

#### Custom route request to a dedicated endpoint

Invoke request to a dedicated endpoint will be routed to one of deployed models based on the traffic split configuration.

    def invoke_tabular_sample(
        project: str,
        location: str,
        endpoint_id: str,
        request_path: str,
        http_request_body: Dict[str, Any],
        stream: bool = False,
    ):
        aiplatform.init(project=project, location=location)
    
        dedicated_endpoint = aiplatform.Endpoint(endpoint_id)
        if stream:
            for chunk in dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
                stream=True,
            ):
                print(chunk)
        else:
            response = dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
            )
            print(response)

#### Custom route request to a deployed model

Invoke request can be made to target a specific deployed model. It can be useful for testing and debugging.

    def invoke_direct_deployed_model_inference_tabular_sample(
        project: str,
        location: str,
        endpoint_id: str,
        request_path: str,
        http_request_body: Dict[str, Any],
        deployed_model_id: str,
        stream: bool = False,
    ):
        aiplatform.init(project=project, location=location)
    
        dedicated_endpoint = aiplatform.Endpoint(endpoint_id)
        if stream:
            for chunk in dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
                deployed_model_id=deployed_model_id,
                stream=True,
            ):
                print(chunk)
        else:
            response = dedicated_endpoint.invoke(
                request_path=request_path,
                body=json.dumps(http_request_body).encode("utf-8"),
                headers={"Content-Type": "application/json"},
                deployed_model_id=deployed_model_id,
            )
            print(response)
