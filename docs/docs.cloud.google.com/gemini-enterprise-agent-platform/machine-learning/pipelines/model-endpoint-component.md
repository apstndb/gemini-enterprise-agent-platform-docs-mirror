---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-endpoint-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-endpoint-component
title: Model and endpoint components
description: Learn how to deploy and manage model endpoints as components within Gemini Enterprise Agent Platform Pipelines for online predictions.
data_source: docs.cloud.google.com
---

`Model` , this resource is available in Gemini Enterprise Agent Platform. You can deploy this `Model` to an `Endpoint` and then send prediction requests to this resource.

Learn more about how to [Import models to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) and [Request predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/getting-predictions) .

## Model operators

The Google Cloud SDK includes the following operators related to the `Model` resource:

  - [`ModelDeleteOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelDeleteOp)
  - [`ModelExportOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelExportOp)
  - [`ModelUploadOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelUploadOp)

## Endpoint operators

The Google Cloud SDK includes the following operators related to the `Endpoint` resource:

  - [`EndpointCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.EndpointCreateOp)
  - [`EndpointDeleteOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.EndpointDeleteOp)
  - [`ModelDeployOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.ModelDeployOp)
  - [`ModelUndeployOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.ModelUndeployOp)

## API reference

  - For component reference, see the following [Google Cloud SDK reference](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/index.html) pages:
    
      - [Model components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html)
    
      - [Endpoint components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html)

  - For Agent Platform API resource reference, see the following API reference pages:
    
      - [`model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource reference
    
      - [`endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) resource reference

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

## Technical support contacts

If you have any questions, reach out to [kubeflow-pipelines-components@google.com](mailto:%20kubeflow-pipelines-components@google.com) .
