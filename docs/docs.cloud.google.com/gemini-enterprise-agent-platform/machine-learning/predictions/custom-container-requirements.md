---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements
title: Custom container requirements for inference
description: Learn about Gemini Enterprise Agent Platform inference custom container requirements.
data_source: docs.cloud.google.com
---

> To see an example of using a custom container, run the "Vertex AI Inference: Deploying Iris-detection model using FastAPI and custom container serving" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/SDK_Custom_Container_Prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2FSDK_Custom_Container_Prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2FSDK_Custom_Container_Prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/SDK_Custom_Container_Prediction.ipynb)

> **Note:** This is version 1.0.0 of this document. The document is updated according to [semantic versioning](https://semver.org/) .

To use a custom container to serve inferences from a custom-trained model, you must provide Gemini Enterprise Agent Platform with a Docker container image that runs an HTTP server. This document describes the requirements that a container image must meet to be compatible with Gemini Enterprise Agent Platform. The document also describes how Agent Platform interacts with your custom container once it starts running. In other words, this document describes what you need to consider when designing a container image to use with Agent Platform.

To walk through using a custom container image to serve inferences, read [Using a custom container](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) .

## Container image requirements

When your Docker container image runs as a container, the container must run an HTTP server. Specifically, the container must listen and respond to liveness checks, health checks, and inference requests. The following subsections describe these requirements in detail.

You can implement the HTTP server in any way, using any programming language, as long as it meets the requirements in this section. For example, you can write a custom HTTP server using a web framework like [Flask](https://flask.palletsprojects.com/) or use machine learning (ML) serving software that runs an HTTP server, like [TensorFlow Serving](https://www.tensorflow.org/tfx/guide/serving) , [TorchServe](https://pytorch.org/serve/) , or [KServe Python Server](https://github.com/kserve/kserve/tree/master/python/kserve#kserve-python-server) .

### Run the HTTP server

You can run an HTTP server by using an [`ENTRYPOINT` instruction](https://docs.docker.com/engine/reference/builder/#entrypoint) , a [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) , or both in the Dockerfile that you use to build your container image. Read about the [interaction between `CMD` and `ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) .

Alternatively, you can specify the [`containerSpec.command`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.command) and [`containerSpec.args`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.args) fields when you create your `Model` resource in order to override your container image's `ENTRYPOINT` and `CMD` respectively. Specifying one of these fields lets you use a container image that would otherwise not meet the requirements due to an incompatible (or nonexistent) `ENTRYPOINT` or `CMD` .

However you determine which command your container runs when it starts, ensure that this `ENTRYPOINT` instruction runs indefinitely. For example, don't run a command that starts an HTTP server in the background and then exits; if you do, the container will exit immediately after it starts running.

Your HTTP server must listen for requests on `0.0.0.0` , on a port of your choice. When you create a `Model` , specify this port in the [`containerSpec.ports` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.ports) . To learn how the container can access this value, read [the section of this document about the `AIP_HTTP_PORT` environment variable](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#aip-variables) .

### Liveness checks

Agent Platform performs a liveness check when your container starts to ensure that your server is running. When you [deploy a custom-trained model to an `Endpoint` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) , Agent Platform uses a [TCP liveness probe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-tcp-liveness-probe) to attempt to establish a TCP connection to your container on the configured port. The probe makes up to 4 attempts to establish a connection, waiting 10 seconds after each failure. If the probe still hasn't established a connection at this point, Agent Platform restarts your container.

Your HTTP server doesn't need to perform any special behavior to handle these checks. As long as it is listening for requests on the configured port, the liveness probe is able to make a connection.

### Health checks

You can optionally specify [`startup_probe`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec#FIELDS.startup_probe) or [`health_probe`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec#FIELDS.health_probe) .

The **startup probe** checks whether the container application has started. If startup probe isn't provided, there is no startup probe and health checks begin immediately. If startup probe is provided, health checks aren't performed until startup probe succeeds.

Legacy applications that might require additional startup time on their first initialization should configure a startup probe. For example, if the application needs to copy the model artifacts from an external source, a startup probe should be configured to return success when that initialization is completed.

The **health probe** checks whether a container is ready to accept traffic. If health probe isn't provided, Agent Platform uses the default health checks as described in [Default health checks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#default-health) .

Legacy applications that don't return `200 OK` to indicate the model is loaded and ready to accept traffic should configure a health probe. For example, an application might return `200 OK` to indicate success even though the actual model load status that's in the response body indicates that the model might not be loaded and might therefore not be ready to accept traffic. In this case, a health probe should be configured to return success only when the model is loaded and ready to serve traffic.

To perform a probe, Agent Platform executes the specified `exec` command in the target container. If the command succeeds, it returns 0, and the container is considered to be alive and healthy.

#### Default health checks

By default, Agent Platform intermittently performs health checks on your HTTP server while it's running to make sure that it is ready to handle inference requests. The service uses a health probe to send HTTP `GET` requests to a configurable health check path on your server. Specify this path in the [`containerSpec.healthRoute` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.health_route) when you create a `Model` . To learn how the container can access this value, read [the section of this document about the `AIP_HEALTH_ROUTE` environment variable](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#aip-variables) .

Configure the HTTP server to respond to each health check request as follows:

  - **If the server is ready to handle inference requests,** respond to the health check request within 10 seconds with status code `200 OK` . The contents of the response body don't matter; Agent Platform ignores them.
    
    This response signifies that the server is healthy.

  - **If the server isn't ready to handle inference requests,** don't respond to the health check request within 10 seconds, or respond with any status code except for `200 OK` . For example, respond with status code `503 Service Unavailable` .
    
    This response (or lack of a response) signifies that the server is unhealthy.

If the health probe receives an unhealthy response from your server (including no response within 10 seconds), it sends up to 3 additional health checks at 10 second intervals. During this period, Agent Platform still considers your server healthy. If the probe receives a healthy response to any of these checks, the probe immediately returns to its intermittent schedule of health checks. However, if the probe receives 4 consecutive unhealthy responses, Agent Platform stops routing inference traffic to the container. (If the `DeployedModel` resource is scaled to use multiple inference nodes, Agent Platform routes inference requests to other, healthy containers.)

Agent Platform doesn't restart the container; instead the health probe continues sending intermittent health check requests to the unhealthy server. If it receives a healthy response, it marks that container as healthy and starts to route inference traffic to it again.

#### Practical guidance

In some cases, it is sufficient for the HTTP server in your container to always respond with status code `200 OK` to health checks. If your container loads resources before starting the server, the container is unhealthy during the startup period and during any periods when the HTTP server fails. At all other times, it responds as healthy.

For a more sophisticated configuration, you might want to purposefully design the HTTP server to respond to health checks with an unhealthy status at certain times. For example, you might want to block inference traffic to a node for a period so that the container can perform maintenance.

### Inference requests

There are two patterns for configuring routes to the model server. One defined by Gemini Enterprise Agent Platform ( `/predict` ), and the other that allows full customization so that you can simply drop in your model server of choice ( `/invoke` ).

#### Vertex defined /predict route

When a client sends a [`projects.locations.endpoints.predict` request](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) to the Agent Platform API, Agent Platform forwards this request as an HTTP `POST` request to a configurable inference path on your server. Specify this path in the [`containerSpec.predictRoute` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.predict_route) when you create a `Model` . To learn how the container can access this value, read [the section of this document about the `AIP_PREDICT_ROUTE` environment variable](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#aip-variables) .

##### Request requirements

If the model is deployed to a shared public endpoint, each inference request must be 1.5 MB or smaller. The HTTP server must accept inference requests that have the `Content-Type: application/json` HTTP header and JSON bodies with the following format:

    {
      "instances": INSTANCES,
      "parameters": PARAMETERS
    }

In these requests:

  - INSTANCES is an array of one or more JSON values of any type. Each values represents an instance that you are providing an inference for.

  - PARAMETERS is a JSON object containing any parameters that your container requires to help serve inferences on the instances. Agent Platform considers the `parameters` field optional, so you can design your container to require it, only use it when provided, or ignore it.

Learn more about the [request body requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#request-body) .

##### Response requirements

If the model is deployed to a shared public endpoint, each inference response must be 1.5 MB or smaller. The HTTP server must send responses with JSON bodies that meet the following format:

    {
      "predictions": INFERENCES
    }

In these responses, replace INFERENCES with an array of JSON values representing the inferences that your container has generated for each of the INSTANCES in the corresponding request.

After your HTTP server sends this response, Agent Platform adds a [`deployedModelId` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#body.PredictResponse.FIELDS.deployed_model_id) to the response before returning it to the client. This field specifies which [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#deployedmodel) on an `Endpoint` is sending the response. Learn more about the [response body format](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#response-body) .

> **Note:** If your container doesn't meet these requirements for receiving requests and sending responses, you can still use the container for [raw inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict) .

#### Custom inference routes

If the model server implements multiple inference routes, using invoke API to access multiple inference routes is recommended. Invoke API can be enabled during model upload by setting [`Model.containerSpec.invokeRoutePrefix` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec#FIELDS.invoke_route_prefix) to "/\*". Once deployed, a HTTP request to `/invoke/foo/bar` route will be forwarded as to the model server's `/foo/bar` path. To learn the details about it, read [using arbitrary custom routes](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-arbitrary-custom-routes) .

## Container image publishing requirements

You must push your container image to [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) in order to use it with Agent Platform. Learn how to [push a container image to Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/docker/pushing-and-pulling) .

In particular, you must push the container image to a repository that meets the following location and permissions requirements.

### Location

When you use Artifact Registry, the repository must use [a region](https://docs.cloud.google.com/artifact-registry/docs/repo-locations) that matches the [locational endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) where you plan to create a `Model` . For example, if you plan to create a `Model` on the `us-central1-aiplatform.googleapis.com` endpoint, the full name of your container image must start with `us-central1-docker.pkg.dev/` . Don't use a multi-regional repository for your container image.

### Permissions

Agent Platform must have permission to pull the container image when you create a `Model` . Specifically, the Agent Platform Service Agent for your project must have the permissions of the [Artifact Registry Reader role ( `roles/artifactregistry.reader` )](https://docs.cloud.google.com/artifact-registry/docs/access-control#roles) for the container image's repository.

Agent Platform uses the Agent Platform Service Agent for your project to interact with other Google Cloud services. This service account has the email address `service- PROJECT_NUMBER @gcp-sa-aiplatform.iam.gserviceaccount.com` , where PROJECT\_NUMBER is replaced with the [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) of your Agent Platform project.

If you have pushed your container image to the same Google Cloud project where you are using Agent Platform, you don't have to configure any permissions. The default permissions granted to the Agent Platform Service Agent are sufficient.

On the other hand, if you have pushed your container image to a different Google Cloud project from the one where you are using Agent Platform, you must [grant the Artifact Registry Reader role for the Artifact Registry repository](https://docs.cloud.google.com/artifact-registry/docs/access-control#grant-repo) to the Agent Platform Service Agent.

> **Note:** Even if you plan to [use a custom service account in your custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) , there is no need to grant your custom service account Artifact Registry permissions; only the service agent needs these permissions. Agent Platform doesn't use your custom service account to pull container images. It only uses the custom service account to run your model serving code.

## Access model artifacts

When you create a custom-trained `Model` without a custom container, you must specify the URI of a Cloud Storage directory with [model artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) as the [`artifactUri` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.artifact_uri) . When you create a `Model` with a custom container, providing model artifacts in Cloud Storage is optional.

If the container image includes the model artifacts that you need to serve inferences, there is no need to load files from Cloud Storage. However, if you do provide model artifacts by specifying the `artifactUri` field, the container must load these artifacts when it starts running. When Agent Platform starts your container, it sets the `AIP_STORAGE_URI` environment variable to a Cloud Storage URI that begins with `gs://` . Your container's `ENTRYPOINT` instruction can download the directory specified by this URI in order to access the model artifacts.

Note that the value of the `AIP_STORAGE_URI` environment variable isn't identical to the Cloud Storage URI that you specify in the `artifactUri` field when you create the `Model` . Rather, `AIP_STORAGE_URI` points to a copy of your model artifact directory in a different Cloud Storage bucket, which Agent Platform manages. Agent Platform populates this directory when you create a `Model` . You can't update the contents of the directory. If you want to use new model artifacts, you must create a new `Model` .

The service account that your container uses by default has permission to read from this URI.

On the other hand, if you [specify a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) when you deploy the `Model` to an `Endpoint` , Agent Platform automatically grants your specified service account the [Storage Object Viewer ( `roles/storage.objectViewer` ) role](https://docs.cloud.google.com/storage/docs/access-control/iam-roles) for the URI's Cloud Storage bucket.

Use any library that supports [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication#adc) to load the model artifacts; you don't need to explicitly configure authentication.

## Environment variables available in the container

When running, the container's `ENTRYPOINT` instruction can reference environment variables that you have configured manually, as well as environment variables set automatically by Agent Platform. This section describes each way that you can set environment variables, and it provides details about the variables set automatically by Agent Platform.

### Variables set in the container image

To set environment variables in the container image when you build it, use Docker's [`ENV` instruction](https://docs.docker.com/engine/reference/builder/#env) . Don't set any environment variables that begin with the prefix `AIP_` .

The container's `ENTRYPOINT` instruction can use these environment variables, but you can't reference them in any of your [`Model` 's API fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) .

### Variables set by Agent Platform

When Agent Platform starts running the container, it sets the following environment variables in the container environment. Each variable begins with the prefix `AIP_` . Don't manually set any environment variables that use this prefix.

The container's `ENTRYPOINT` instruction can access these variables. To learn which Agent Platform API fields can also reference these variables, read the [API reference for `ModelContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#modelcontainerspec) .

> **Note:** Docker instructions used to build the container image, like [`RUN`](https://docs.docker.com/engine/reference/builder/#run) , can't access these variables, because you must build the container image before you provide it to Agent Platform.

> **Note:** Agent Platform sets the values of some of the following variables when you deploy your `Model` as a `DeployedModel` to an `Endpoint` . You can reference in other API fields when you create the `Model` , and the values get expanded each time you deploy the `Model` .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Variable name</th>
<th>Default value</th>
<th>How to configure value</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AIP_ACCELERATOR_TYPE</td>
<td>Unset</td>
<td>When you deploy a <code dir="ltr" translate="no">Model</code> as a <code dir="ltr" translate="no">DeployedModel</code> to an <code dir="ltr" translate="no">Endpoint</code> resource, set the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec#FIELDS.accelerator_type"><code dir="ltr" translate="no">dedicatedResources.machineSpec.acceleratorType</code> field</a> .</td>
<td>If applicable, this variable specifies the type of accelerator used by the virtual machine (VM) instance that the container is running on.</td>
</tr>
<tr class="even">
<td>AIP_DEPLOYED_MODEL_ID</td>
<td>A string of digits identifying the <code dir="ltr" translate="no">DeployedModel</code> to which this container's <code dir="ltr" translate="no">Model</code> has been deployed.</td>
<td>Not configurable</td>
<td>This value is the <code dir="ltr" translate="no">DeployedModel</code> 's <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.id"><code dir="ltr" translate="no">id</code> field</a> .</td>
</tr>
<tr class="odd">
<td>AIP_ENDPOINT_ID</td>
<td>A string of digits identifying the <code dir="ltr" translate="no">Endpoint</code> on which the container's <code dir="ltr" translate="no">Model</code> has been deployed.</td>
<td>Not configurable</td>
<td>This value is the last segment of the <code dir="ltr" translate="no">Endpoint</code> 's <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.name"><code dir="ltr" translate="no">name</code> field</a> (following <code dir="ltr" translate="no">endpoints/</code> ).</td>
</tr>
<tr class="even">
<td>AIP_FRAMEWORK</td>
<td><code dir="ltr" translate="no">CUSTOM_CONTAINER</code></td>
<td>Not configurable</td>
<td></td>
</tr>
<tr class="odd">
<td>AIP_HEALTH_ROUTE</td>
<td><code dir="ltr" translate="no">/v1/endpoints/         ENDPOINT        /deployedModels/         DEPLOYED_MODEL       </code><br />
<br />
In this string, replace ENDPOINT with the value of the <code dir="ltr" translate="no">AIP_ENDPOINT_ID</code> variable and replace DEPLOYED_MODEL with the value of the <code dir="ltr" translate="no">AIP_DEPLOYED_MODEL_ID</code> variable.</td>
<td>When you create a <code dir="ltr" translate="no">Model</code> , set the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.health_route"><code dir="ltr" translate="no">containerSpec.healthRoute</code> field</a> .</td>
<td>This variables specifies the HTTP path on the container that Agent Platform sends <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#health">health checks</a> to.</td>
</tr>
<tr class="even">
<td>AIP_HTTP_PORT</td>
<td><code dir="ltr" translate="no">8080</code></td>
<td>When you create a <code dir="ltr" translate="no">Model</code> , set the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.ports"><code dir="ltr" translate="no">containerSpec.ports</code> field</a> . The first entry in this field becomes the value of <code dir="ltr" translate="no">AIP_HTTP_PORT</code> .</td>
<td>Agent Platform sends liveness checks, health checks, and inference requests to this port on the container. Your container's HTTP server must listen for requests on this port.</td>
</tr>
<tr class="odd">
<td>AIP_MACHINE_TYPE</td>
<td>No default, must be configured</td>
<td>When you deploy a <code dir="ltr" translate="no">Model</code> as a <code dir="ltr" translate="no">DeployedModel</code> to an <code dir="ltr" translate="no">Endpoint</code> resource, set the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec#FIELDS.machine_type"><code dir="ltr" translate="no">dedicatedResources.machineSpec.machineType</code> field</a> .</td>
<td>This variable specifies the type of VM that the container is running on.</td>
</tr>
<tr class="even">
<td>AIP_MODE</td>
<td><code dir="ltr" translate="no">PREDICTION</code></td>
<td>Not configurable</td>
<td>This variable signifies that the container is running on Agent Platform to serve online inferences. You can use this environment variable to add custom logic to your container, so that it can run in multiple computing environments but only use certain code paths on when run on Agent Platform.</td>
</tr>
<tr class="odd">
<td>AIP_MODE_VERSION</td>
<td><code dir="ltr" translate="no">1.0.0</code></td>
<td>Not configurable</td>
<td>This variable signifies the version of the custom container requirements (this document) that Agent Platform expects the container to meet. This document updates according to <a href="https://semver.org">semantic versioning</a> .</td>
</tr>
<tr class="even">
<td>AIP_MODEL_NAME</td>
<td>The value of the <code dir="ltr" translate="no">AIP_ENDPOINT_ID</code> variable</td>
<td>Not configurable</td>
<td>See the <code dir="ltr" translate="no">AIP_ENDPOINT_ID</code> row. This variable exists for compatibility reasons.</td>
</tr>
<tr class="odd">
<td>AIP_PREDICT_ROUTE</td>
<td><code dir="ltr" translate="no">/v1/endpoints/         ENDPOINT        /deployedModels/         DEPLOYED_MODEL        :predict</code><br />
<br />
In this string, replace ENDPOINT with the value of the <code dir="ltr" translate="no">AIP_ENDPOINT_ID</code> variable and replace DEPLOYED_MODEL with the value of the <code dir="ltr" translate="no">AIP_DEPLOYED_MODEL_ID</code> variable.</td>
<td>When you create a <code dir="ltr" translate="no">Model</code> , set the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.predict_route"><code dir="ltr" translate="no">containerSpec.predictRoute</code> field</a> .</td>
<td>This variable specifies the HTTP path on the container that Agent Platform <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#inference">forwards inference requests</a> to.</td>
</tr>
<tr class="even">
<td>AIP_PROJECT_NUMBER</td>
<td>The <a href="https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects">project number</a> of the Google Cloud project where you are using Agent Platform</td>
<td>Not configurable</td>
<td></td>
</tr>
<tr class="odd">
<td>AIP_STORAGE_URI</td>
<td><ul>
<li><strong>If you don't set the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.artifact_uri"><code dir="ltr" translate="no">artifactUri</code> field</a> when you create a <code dir="ltr" translate="no">Model</code> :</strong> an empty string</li>
<li><strong>If you do set the <code dir="ltr" translate="no">artifactUri</code> field when you create a <code dir="ltr" translate="no">Model</code> :</strong> a Cloud Storage URI (starting with <code dir="ltr" translate="no">gs://</code> ) specifying a directory in a bucket managed by Agent Platform</li>
</ul></td>
<td>Not configurable</td>
<td>This variable specifies the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#artifacts">directory that contains a copy of your model artifacts</a> , if applicable.</td>
</tr>
<tr class="even">
<td>AIP_VERSION_NAME</td>
<td>The value of the <code dir="ltr" translate="no">AIP_DEPLOYED_MODEL_ID</code> variable</td>
<td>Not configurable</td>
<td>See the <code dir="ltr" translate="no">AIP_DEPLOYED_MODEL_ID</code> row. This variable exists for compatibility reasons.</td>
</tr>
</tbody>
</table>

### Variables set in the `Model` resource

When you create a `Model` , you can set additional environment variables in the [`containerSpec.env` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelContainerSpec.FIELDS.env) .

The container's `ENTRYPOINT` instruction can access these variables. To learn which Agent Platform API fields can also reference these variables, read the [API reference for `ModelContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#modelcontainerspec) .

> **Note:** Docker instructions used to build the container image, like [`RUN`](https://docs.docker.com/engine/reference/builder/#run) , can't access these variables, because you must build the container image before you provide it to Agent Platform.

## What's next

  - [Learn more about serving inferences using a custom container](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) , including how to specify container-related API fields when you import a model.
