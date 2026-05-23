---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeploymentStage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeploymentStage
title: DeploymentStage
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Stage field indicating the current progress of a deployment.

Enums

`DEPLOYMENT_STAGE_UNSPECIFIED`

Default value. This value is unused.

`STARTING_DEPLOYMENT`

The deployment is initializing and setting up the environment.

`PREPARING_MODEL`

The deployment is preparing the model assets.

`CREATING_SERVING_CLUSTER`

The deployment is creating the underlying serving cluster.

`ADDING_NODES_TO_CLUSTER`

The deployment is adding nodes to the serving cluster.

`GETTING_CONTAINER_IMAGE`

The deployment is getting the container image for the model server.

`STARTING_MODEL_SERVER`

The deployment is starting the model server.

`FINISHING_UP`

The deployment is performing finalization steps.

`DEPLOYMENT_TERMINATED`

The deployment has terminated.

`SUCCESSFULLY_DEPLOYED`

The deployment has succeeded.

`FAILED_TO_DEPLOY`

The deployment has failed.
