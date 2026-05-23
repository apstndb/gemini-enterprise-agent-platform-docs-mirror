---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/use-components
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/use-components
title: Use Google Cloud Pipeline Components
description: Learn how to use and integrate components in ML workflows.
data_source: docs.cloud.google.com
---

When you use Google Cloud Pipeline Components (GCPC), you can use the following Gemini Enterprise Agent Platform and Google Cloud features to secure your components and artifacts.

## Specify a service account for a component

When you use a component, you can optionally specify a service account. Your component launches and acts with the permissions of this service account. For example, you can use the following code to specify the service account of a `ModelDeploy` component:

    model_deploy_op = ModelDeployOp(model=training_job_run_op.outputs["model"],
        endpoint=endpoint_op.outputs["endpoint"],
        automatic_resources_min_replica_count=1,
        automatic_resources_max_replica_count=1,
        service_account="SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com")

Replace the following:

  - SERVICE\_ACCOUNT\_ID : The ID for the service account.
  - PROJECT\_ID : The ID of the project.

Learn more about [using a custom service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account) and [configuring a service account](https://docs.cloud.google.com/vertex-ai/docs/pipelines/configure-project#service-account) for use with Gemini Enterprise Agent Platform Pipelines.

## Use VPC Service Controls to prevent data exfiltration

[VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) can help you mitigate the risk of data exfiltration from Gemini Enterprise Agent Platform Pipelines. When you use VPC Service Controls to create a service perimeter, resources and data that are created by Gemini Enterprise Agent Platform Pipelines and the Google Cloud Pipeline Components are automatically protected. For example, when you use VPC Service Controls to protect your pipeline, the following artifacts can't leave your service perimeter:

  - Training data for an AutoML model
  - Models that you created
  - Results from a batch prediction request

Learn more about [VPC Service Controls with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-service-controls) .

## Set up VPC Network Peering

You can configure Google Cloud Pipeline Components to peer with a Virtual Private Cloud by providing extra parameters. For example, you can use the following code to specify a VPC network for an `EndpointCreate` component:

    endpoint_create_op = EndpointCreateOp(
        project="PROJECT_ID",
        location="REGION",
        display_name="endpoint-display-name",
        network="NETWORK")

Replace the following:

  - PROJECT\_ID : The ID of the project.
  - REGION : The region where you are using Gemini Enterprise Agent Platform.
  - NETWORK : The VPC network, for example, `"projects/12345/global/networks/myVPC"` .

Learn more about [VPC Network Peering in Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-peering) .

## Use customer-managed encryption keys (CMEK)

By default, Google Cloud automatically [encrypts data when at rest](https://docs.cloud.google.com/docs/security/encryption/default-encryption) using encryption keys managed by Google. If you have specific compliance or regulatory requirements related to the keys that protect your data, you can use customer-managed encryption keys (CMEK) for your resources. Before you start to use customer-managed encryption keys, learn about the [benefits of CMEK on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/general/cmek#benefits) and [current CMEK supported resources](https://docs.cloud.google.com/vertex-ai/docs/general/cmek#resource-list) .

### Configuring your component with CMEK

After you create a key ring and key in [Cloud Key Management Service](https://docs.cloud.google.com/vertex-ai/docs/general/cmek#configure-cmek) , and grant Gemini Enterprise Agent Platform encrypter and decrypter permissions for your key, you can create a new CMEK-supported component by specifying your key as one of the create parameters. For example, you can use the following code to specify a key for a `ModelBatchPredict` component:

    model_batch_predict_op = ModelBatchPredictOp(project="PROJECT_ID",
        model=model_upload_op.outputs["model"],
        encryption_spec_key_name="projects/PROJECT_ID/locations/LOCATION_ID/keyRings/KEY_RING_NAME/cryptoKeys/KEY_NAME")

Replace the following:

  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION\_ID : A valid location or region identifier, for example, `us-central1` .
  - KEY\_RING\_NAME : The name of the key ring for your CMEK. For more information about key rings, see [Cloud KMS resources](https://docs.cloud.google.com/kms/docs/resource-hierarchy#key_rings) .
  - KEY\_NAME : The CMEK key name.

**Note:** Google Cloud components that aren't Gemini Enterprise Agent Platform components might require additional permissions. For example, a BigQuery component might require [encryption and decryption permission](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption#grant_permission) . In addition, the location of the CMEK key must be the same as the location of the component. For example, if a BigQuery component loads data from a dataset that's based in the [multi-region US location](https://docs.cloud.google.com/bigquery/docs/locations#multi-regional_locations) , the CMEK key must also be based in the multi-region US location.

## Consume or produce artifacts in your component

The Google Cloud SDK defines a set of [ML metadata artifact types](https://docs.cloud.google.com/vertex-ai/docs/pipelines/artifact-types) that serve as component input and output. Some Google Cloud Pipeline Components consume these artifacts as input or produce them as output.

This page shows how to consume and produce these artifacts.

### Consume an ML artifact

#### Consume an artifact in component YAML

The artifact's metadata can serve as input to a component. To prepare an artifact to be consumed as input, you must extract it and put it in a component YAML file.

For example, the [`ModelUploadOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelUploadOp) component generates a `google.VertexModel` artifact which can be consumed by a [`ModelDeployOp`](https://github.com/kubeflow/pipelines/blob/google-cloud-pipeline-components-0.1.9/components/google-cloud/google_cloud_pipeline_components/aiplatform/endpoint/deploy_model/component.yaml#L137) component. Use the following code in a component YAML file to retrieve the a Gemini Enterprise Agent Platform `Model` resource from the inputs (reference):

    "model": "',"{{$.inputs.artifacts['model'].metadata['resourceName']}}", '"'

For the complete schema of the artifact's metadata, see the [`artifact_types.py` file](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/google_cloud_pipeline_components/types/artifact_types.py) in the Kubeflow GitHub repo.

#### Consume an artifact in a lightweight Python component

    from kfp.dsl import Artifact, Input
    
    @dsl.component
    def classification_model_eval_metrics(
        project: str,
        location: str,  # "us-central1",
        model: Input[Artifact],
    ) :
       # Consumes the `resourceName` metadata
       model_resource_path = model.metadata["resourceName"]

For an example of how to consume the Vertex ML Metadata artifacts types, see [Train a classification model using tabular data and Agent Platform AutoML](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/automl_tabular_classification_beans.ipynb) .

### Create an ML artifact

The following code examples show how to create a Vertex ML Metadata artifact that a GCPC component can accept as input.

#### Use an importer node

The following example creates an Importer node that registers a new artifact entry to Vertex ML Metadata. The importer node takes the artifact's URI and metadata as primitives and packages them into an artifact.

    from google_cloud_pipeline_components import v1
    from google_cloud_pipeline_components.types import artifact_types
    from kfp.components import importer_node
    from kfp import dsl
    
    @dsl.pipeline(name=_PIPELINE_NAME)
    def pipeline():
      # Using importer and UnmanagedContainerModel artifact for model upload
      # component.
      importer_spec = importer_node.importer(
          artifact_uri='gs://managed-pipeline-gcpc-e2e-test/automl-tabular/model',
          artifact_class=artifact_types.UnmanagedContainerModel,
          metadata={
              'containerSpec': {
                  'imageUri':
                      'us-docker.pkg.dev/vertex-ai/automl-tabular/prediction-server:prod'
              }
          })
    
      # Consuming the UnmanagedContainerModel artifact for the previous step
      model_upload_with_artifact_op = v1.model.ModelUploadOp(
          project=_GCP_PROJECT_ID,
          location=_GCP_REGION,
          display_name=_MODEL_DISPLAY_NAME,
          unmanaged_container_model=importer_spec.outputs['artifact'])

#### Use Python function-based components

The following example shows how to output a Vertex ML Metadata artifact directly from a Python component.

    from google_cloud_pipeline_components import v1
    from kfp.components import importer_node
    from kfp import dsl
    
    @dsl.component(
        base_image='python:3.9',
        packages_to_install=['google-cloud-aiplatform'],
    )
    # Note currently KFP SDK doesn't support outputting artifacts in `google` namespace.
    # Use the base type dsl.Artifact instead.
    def return_unmanaged_model(model: dsl.Output[dsl.Artifact]):
      model.metadata['containerSpec'] = {
          'imageUri':
              'us-docker.pkg.dev/vertex-ai/automl-tabular/prediction-server:prod'
      }
      model.uri = f'gs://automl-tabular-pipeline/automl-tabular/model'
    
    @dsl.pipeline(name=_PIPELINE_NAME)
    def pipeline():
    
      unmanaged_model_op = return_unmanaged_model()
    
      # Consuming the UnmanagedContainerModel artifact for the previous step
      model_upload_with_artifact_op = v1.model.ModelUploadOp(
          project=_GCP_PROJECT_ID,
          location=_GCP_REGION,
          display_name=_MODEL_DISPLAY_NAME,
          unmanaged_container_model=unmanaged_model_op.outputs['model'])

#### Use your own container-based component

The following example shows how to generate a [`VertexBatchPredictionJob`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/artifact_types.html#google_cloud_pipeline_components.types.artifact_types.VertexBatchPredictionJob) artifact as output from a container-based component using the [`artifact_types.py`](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/google_cloud_pipeline_components/types/artifact_types.py) utility class.

    bp_job_artifact = VertexBatchPredictionJob(
        'batchpredictionjob', vertex_uri_prefix + get_job_response.name,
        get_job_response.name, get_job_response.output_info.bigquery_output_table,
        get_job_response.output_info.bigquery_output_dataset,
        get_job_response.output_info.gcs_output_directory)
    
        output_artifacts = executor_input_json.get('outputs', {}).get('artifacts', {})
        executor_output['artifacts'] = bp_job_artifact.to_executor_output_artifact(output_artifacts[bp_job_artifact.name])
