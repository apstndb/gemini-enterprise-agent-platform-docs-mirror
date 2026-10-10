---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec
title: ModelContainerSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specification of a container for serving predictions. Some fields in this message correspond to fields in the [Kubernetes Container v1 core specification](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

Fields

`imageUri` `string`

Required. Immutable. URI of the Docker image to be used as the custom container for serving predictions. This URI must identify an image in Artifact Registry. Learn more about the [container publishing requirements](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#publishing) , including permissions requirements for the Agent Platform service Agent.

The container image is ingested upon [`ModelService.UploadModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/upload#google.cloud.aiplatform.v1beta1.ModelService.UploadModel) , stored internally, and this original path is afterwards not used.

To learn about the requirements for the Docker image itself, see [Custom container requirements](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#) .

You can use the URI to one of Agent Platform's [pre-built container images for prediction](https://cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) in this field.

`command[]` `string`

Immutable. Specifies the command that runs when the container starts. This overrides the container's [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) . Specify this field as an array of executable and arguments, similar to a Docker `ENTRYPOINT` 's "exec" form, not its "shell" form.

If you do not specify this field, then the container's `ENTRYPOINT` runs, in conjunction with the [`args`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.args) field or the container's [`CMD`](https://docs.docker.com/engine/reference/builder/#cmd) , if either exists. If this field is not specified and the container does not have an `ENTRYPOINT` , then refer to the Docker documentation about [how `CMD` and `ENTRYPOINT` interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) .

If you specify this field, then you can also specify the `args` field to provide additional arguments for this command. However, if you specify this field, then the container's `CMD` is ignored. See the [Kubernetes documentation about how the `command` and `args` fields interact with a container's `ENTRYPOINT` and `CMD`](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#notes) .

In this field, you can reference [environment variables set by Agent Platform](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) and environment variables set in the [`env`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.env) field. You cannot reference environment variables set in the Docker image. In order for environment variables to be expanded, reference them by using the following syntax:

`$( `` VARIABLE_NAME `` )`

Note that this differs from Bash variable expansion, which does not use parentheses. If a variable cannot be resolved, the reference in the input string is used unchanged. To avoid variable expansion, you can escape this syntax with `$$` ; for example:

`$$( `` VARIABLE_NAME `` )`

This field corresponds to the `command` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`args[]` `string`

Immutable. Specifies arguments for the command that runs when the container starts. This overrides the container's [`CMD`](https://docs.docker.com/engine/reference/builder/#cmd) . Specify this field as an array of executable and arguments, similar to a Docker `CMD` 's "default parameters" form.

If you don't specify this field but do specify the [`command`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.command) field, then the command from the `command` field runs without any additional arguments. See the [Kubernetes documentation about how the `command` and `args` fields interact with a container's `ENTRYPOINT` and `CMD`](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#notes) .

If you don't specify this field and don't specify the `command` field, then the container's [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#cmd) and `CMD` determine what runs based on their default behavior. See the Docker documentation about [how `CMD` and `ENTRYPOINT` interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) .

In this field, you can reference [environment variables set by Agent Platform](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) and environment variables set in the [`env`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.env) field. You cannot reference environment variables set in the Docker image. In order for environment variables to be expanded, reference them by using the following syntax:

`$( `` VARIABLE_NAME `` )`

Note that this differs from Bash variable expansion, which does not use parentheses. If a variable cannot be resolved, the reference in the input string is used unchanged. To avoid variable expansion, you can escape this syntax with `$$` ; for example:

`$$( `` VARIABLE_NAME `` )`

This field corresponds to the `args` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`env[]` `object ( ``EnvVar`` )`

Immutable. List of environment variables to set in the container. After the container starts running, code running in the container can read these environment variables.

Additionally, the [`command`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.command) and [`args`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.args) fields can reference these variables. Later entries in this list can also reference earlier entries. For example, the following example sets the variable `VAR_2` to have the value `foo bar` :

```json
[
  {
    "name": "VAR_1",
    "value": "foo"
  },
  {
    "name": "VAR_2",
    "value": "$(VAR_1) bar"
  }
]
```

If you switch the order of the variables in the example, then the expansion does not occur.

This field corresponds to the `env` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

At most 200 environment variables can be specified. Each variable ( `NAME=value` ) must be smaller than 128 KiB, and the total size of all variables must not exceed 512 KiB.

`ports[]` `object ( `[`Port`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#Port)` )`

Immutable. List of ports to expose from the container. Agent Platform sends any prediction requests that it receives to the first port on this list. Agent Platform also sends [liveness and health checks](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#liveness) to this port.

If you do not specify this field, it defaults to following value:

```json
[
  {
    "containerPort": 8080
  }
]
```

Agent Platform does not use ports other than the first one listed. This field corresponds to the `ports` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`predictRoute` `string`

Immutable. HTTP path on the container to send prediction requests to. Agent Platform forwards requests sent using [`projects.locations.endpoints.predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1beta1.PredictionService.Predict) to this path on the container's IP address and port. Agent Platform then returns the container's response in the API response.

For example, if you set this field to `/foo` , then when Agent Platform receives a prediction request, it forwards the request body in a POST request to the `/foo` path on the port of your container specified by the first value of this `ModelContainerSpec` 's [`ports`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.ports) field.

If you don't specify this field, it defaults to the following value when you [`deploy this Model to an Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1beta1.EndpointService.DeployModel) :

`/v1/endpoints/ `` ENDPOINT `` /deployedModels/ `` DEPLOYED_MODEL `` :predict`

The placeholders in this value are replaced as follows:

- ` ENDPOINT ` : The last segment (following `endpoints/` )of the Endpoint.name\]\[\] field of the Endpoint where this Model has been deployed. (Agent Platform makes this value available to your container code as the [`AIP_ENDPOINT_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

- ` DEPLOYED_MODEL ` : [`DeployedModel.id`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints#DeployedModel.FIELDS.id) of the `DeployedModel` . (Agent Platform makes this value available to your container code as the [`AIP_DEPLOYED_MODEL_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

`healthRoute` `string`

Immutable. HTTP path on the container to send health checks to. Agent Platform intermittently sends GET requests to this path on the container's IP address and port to check that the container is healthy. Read more about [health checks](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#health) .

For example, if you set this field to `/bar` , then Agent Platform intermittently sends a GET request to the `/bar` path on the port of your container specified by the first value of this `ModelContainerSpec` 's [`ports`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#FIELDS.ports) field.

If you don't specify this field, it defaults to the following value when you [`deploy this Model to an Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1beta1.EndpointService.DeployModel) :

`/v1/endpoints/ `` ENDPOINT `` /deployedModels/ `` DEPLOYED_MODEL `` :predict`

The placeholders in this value are replaced as follows:

- ` ENDPOINT ` : The last segment (following `endpoints/` )of the Endpoint.name\]\[\] field of the Endpoint where this Model has been deployed. (Agent Platform makes this value available to your container code as the [`AIP_ENDPOINT_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

- ` DEPLOYED_MODEL ` : [`DeployedModel.id`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints#DeployedModel.FIELDS.id) of the `DeployedModel` . (Agent Platform makes this value available to your container code as the [`AIP_DEPLOYED_MODEL_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

`invokeRoutePrefix` `string`

Immutable. Invoke route prefix for the custom container. "/\*" is the only supported value right now. By setting this field, any non-root route on this model will be accessible with invoke http call eg: "/invoke/foo/bar", however the \[PredictionService.Invoke\] RPC is not supported yet.

Only one of `predictRoute` or `invokeRoutePrefix` can be set, and we default to using `predictRoute` if this field is not set. If this field is set, the Model can only be deployed to dedicated endpoint.

`grpcPorts[]` `object ( `[`Port`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#Port)` )`

Immutable. List of ports to expose from the container. Agent Platform sends gRPC prediction requests that it receives to the first port on this list. Agent Platform also sends liveness and health checks to this port.

If you do not specify this field, gRPC requests to the container will be disabled.

Agent Platform does not use ports other than the first one listed. This field corresponds to the `ports` field of the Kubernetes Containers v1 core API.

`deploymentTimeout` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Immutable. Deployment timeout. Limit for deployment timeout is 2 hours.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`sharedMemorySizeMb` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Immutable. The amount of the VM memory to reserve as the shared memory for the model in megabytes.

`startupProbe` `object ( `[`Probe`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#Probe)` )`

Immutable. Specification for Kubernetes startup probe.

`healthProbe` `object ( `[`Probe`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#Probe)` )`

Immutable. Specification for Kubernetes readiness probe.

`livenessProbe` `object ( `[`Probe`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#Probe)` )`

Immutable. Specification for Kubernetes liveness probe.

**JSON representation**

```
{
  "imageUri": string,
  "command": [
    string
  ],
  "args": [
    string
  ],
  "env": [
    {
      object (EnvVar)
    }
  ],
  "ports": [
    {
      object (Port)
    }
  ],
  "predictRoute": string,
  "healthRoute": string,
  "invokeRoutePrefix": string,
  "grpcPorts": [
    {
      object (Port)
    }
  ],
  "deploymentTimeout": string,
  "sharedMemorySizeMb": string,
  "startupProbe": {
    object (Probe)
  },
  "healthProbe": {
    object (Probe)
  },
  "livenessProbe": {
    object (Probe)
  }
}
```

## Port

Represents a network port in a container.

Fields

`containerPort` `integer`

The number of the port to expose on the pod's IP address. Must be a valid port number, between 1 and 65535 inclusive.

**JSON representation**

```
{
  "containerPort": integer
}
```

## Probe

Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

Fields

`periodSeconds` `integer`

How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Must be less than timeoutSeconds.

Maps to Kubernetes probe argument 'periodSeconds'.

`timeoutSeconds` `integer`

Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Must be greater or equal to periodSeconds.

Maps to Kubernetes probe argument 'timeoutSeconds'.

`failureThreshold` `integer`

Number of consecutive failures before the probe is considered failed. Defaults to 3. Minimum value is 1.

Maps to Kubernetes probe argument 'failureThreshold'.

`successThreshold` `integer`

Number of consecutive successes before the probe is considered successful. Defaults to 1. Minimum value is 1.

Maps to Kubernetes probe argument 'successThreshold'.

`initialDelaySeconds` `integer`

Number of seconds to wait before starting the probe. Defaults to 0. Minimum value is 0.

Maps to Kubernetes probe argument 'initialDelaySeconds'.

`probe_type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`exec` `object ( `[`ExecAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#ExecAction)` )`

ExecAction probes the health of a container by executing a command.

`httpGet` `object ( `[`HttpGetAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#HttpGetAction)` )`

HttpGetAction probes the health of a container by sending an HTTP GET request.

`grpc` `object ( `[`GrpcAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#GrpcAction)` )`

GrpcAction probes the health of a container by sending a gRPC request.

`tcpSocket` `object ( `[`TcpSocketAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#TcpSocketAction)` )`

TcpSocketAction probes the health of a container by opening a TCP socket connection.

End of mutually exclusive fields.

**JSON representation**

```
{
  "periodSeconds": integer,
  "timeoutSeconds": integer,
  "failureThreshold": integer,
  "successThreshold": integer,
  "initialDelaySeconds": integer,

  // probe_type
  "exec": {
    object (ExecAction)
  },
  "httpGet": {
    object (HttpGetAction)
  },
  "grpc": {
    object (GrpcAction)
  },
  "tcpSocket": {
    object (TcpSocketAction)
  }
  // Union type
}
```

## ExecAction

ExecAction specifies a command to execute.

Fields

`command[]` `string`

Command is the command line to execute inside the container, the working directory for the command is root ('/') in the container's filesystem. The command is simply exec'd, it is not run inside a shell, so traditional shell instructions ('\|', etc) won't work. To use a shell, you need to explicitly call out to that shell. Exit status of 0 is treated as live/healthy and non-zero is unhealthy.

**JSON representation**

```
{
  "command": [
    string
  ]
}
```

## HttpGetAction

HttpGetAction describes an action based on HTTP Get requests.

Fields

`path` `string`

Path to access on the HTTP server.

`port` `integer`

Number of the port to access on the container. Number must be in the range 1 to 65535.

`host` `string`

host name to connect to, defaults to the model serving container's IP. You probably want to set "host" in httpHeaders instead.

`scheme` `string`

Scheme to use for connecting to the host. Defaults to HTTP. Acceptable values are "HTTP" or "HTTPS".

`httpHeaders[]` `object ( `[`HttpHeader`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec#HttpHeader)` )`

Custom headers to set in the request. HTTP allows repeated headers.

**JSON representation**

```
{
  "path": string,
  "port": integer,
  "host": string,
  "scheme": string,
  "httpHeaders": [
    {
      object (HttpHeader)
    }
  ]
}
```

## HttpHeader

HttpHeader describes a custom header to be used in HTTP probes

Fields

`name` `string`

The header field name. This will be canonicalized upon output, so case-variant names will be understood as the same header.

`value` `string`

The header field value

**JSON representation**

```
{
  "name": string,
  "value": string
}
```

## GrpcAction

GrpcAction checks the health of a container using a gRPC service.

Fields

`port` `integer`

Port number of the gRPC service. Number must be in the range 1 to 65535.

`service` `string`

service is the name of the service to place in the gRPC HealthCheckRequest. See <https://github.com/grpc/grpc/blob/master/doc/health-checking.md> .

If this is not specified, the default behavior is defined by gRPC.

**JSON representation**

```
{
  "port": integer,
  "service": string
}
```

## TcpSocketAction

TcpSocketAction probes the health of a container by opening a TCP socket connection.

Fields

`port` `integer`

Number of the port to access on the container. Number must be in the range 1 to 65535.

`host` `string`

Optional: host name to connect to, defaults to the model serving container's IP.

**JSON representation**

```
{
  "port": integer,
  "host": string
}
```
