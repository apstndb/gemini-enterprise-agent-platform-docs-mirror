---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect
title: Configure Private Service Connect interface for a pipeline
description: Learn how to configure a Private Service Connect interface for an ML pipeline in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

You can configure private connectivity for your pipeline run using a *Private Service Connect interface* . Google recommends using Gemini Enterprise Agent Platform Private Service Connect for private connectivity, since it reduces the chances of IP exhaustion and supports transitive peering.

Gemini Enterprise Agent Platform Pipelines uses the underlying Private Service Connect interface infrastructure for training to pass the connection details to the custom training job. To learn more about the limitations and pricing of using Private Service Connect interfaces with custom training, see [Use Private Service Connect interface for Gemini Enterprise Agent Platform Training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress) .

## Limitations

Private Service Connect interfaces don't support external IP addresses.

## Pricing

Pricing for Private Service Connect interfaces is described on the [All networking pricing](https://cloud.google.com/vpc/network-pricing) page.

## Before you begin

To use a Private Service Connect interface with Agent Platform Pipelines, you must first [Set up a Private Service Connect interface for Gemini Enterprise Agent Platform resources](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-psc-i-setup) .

## Create a pipeline run with Private Service Connect interfaces

To create a pipeline run, you must first create a pipeline spec. A pipeline spec is an in-memory object that you create by converting a compiled pipeline definition.

### Create a pipeline spec

Follow these instructions to create an in-memory pipeline spec that you can use to create the pipeline run:

1.  Define a pipeline and compile it into a YAML file. For more information about defining and compiling a pipeline, see [Build a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

2.  Use the following code sample to convert the compiled pipeline YAML file to an in-memory pipeline spec.
    
        import yaml
        with open("COMPILED_PIPELINE_PATH", "r") as stream:
          try:
            pipeline_spec = yaml.safe_load(stream)
            print(pipeline_spec)
          except yaml.YAMLError as exc:
            print(exc)
    
    Replace COMPILED\_PIPELINE\_PATH with the local path to your compiled pipeline YAML file.

### Create the pipeline run

Use the following samples to create a pipeline run using Private Service Connect interfaces:

### Python

To create a pipeline run with Private Service Connect interfaces using the Agent Platform SDK for Python, configure the run using the `  aiplatform_v1/services/pipeline_service  ` definition.

    # Import aiplatform and the appropriate API version v1
    from google.cloud import aiplatform, aiplatform_v1
    
    # Initialize the Vertex SDK using PROJECT_ID and LOCATION
    aiplatform.init(project="PROJECT_ID", location="LOCATION")
    
    # Create the API endpoint
    client_options = {
    "api_endpoint": f"LOCATION-aiplatform.googleapis.com"
    }
    
    # Initialize the PipelineServiceClient
    client = aiplatform_v1.PipelineServiceClient(client_options=client_options)
    
    PSCI_INTERFACE_CONFIG = {
        "network_attachment": "NETWORK_ATTACHMENT_NAME",
        "dns_peering_configs": [
          {
            "domain": "DNS_DOMAIN",
            "target_project": "TARGET_PROJECT",
            "target_network": "TARGET_NETWORK"
          }
        ]
    }
    
    # Construct the request
    request = aiplatform_v1.CreatePipelineJobRequest(
    parent=f"projects/PROJECT_ID/locations/LOCATION",
    pipeline_job=aiplatform_v1.PipelineJob(
        display_name="DISPLAY_NAME",
        pipeline_spec=PIPELINE_SPEC,
        runtime_config=aiplatform_v1.PipelineJob.RuntimeConfig(
            gcs_output_directory="OUTPUT_DIRECTORY",
        ),
        psc_interface_config=aiplatform_v1.PscInterfaceConfig(
            PSCI_INTERFACE_CONFIG
        ),
    )
    
    # Make the API call
    response = client.create_pipeline_job(request=request)
    
    # Print the response
    print(response)

Replace the following:

  - PROJECT\_ID : The project ID of the project where you want to create the pipeline run.
  - LOCATION : The region where you want to create the pipeline run.
  - DISPLAY\_NAME : The name of the pipeline job. The maximum length for a display name is 128 UTF-8 characters.
  - PIPELINE\_SPEC : The pipeline spec you created in [Create a pipeline spec](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect#create-spec) .
  - OUTPUT\_DIRECTORY : The URI of the Cloud Storage bucket for storing output artifacts. This path is the root output directory for the pipeline and is used to generate the paths of output artifacts.
  - NETWORK\_ATTACHMENT\_NAME : The name of the Compute Engine network attachment to attach to the `PipelineJob` resource. To obtain the network attachment, you must have completed the steps in the [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect#before-you-begin) section. For more information about the network attachment, see [Set up a VPC network, subnet, and network attachment](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-psc-i-setup#set_up_a_network_subnet_and_network_attachment) .
  - DNS\_DOMAIN : The DNS name of the private cloud DNS zone you created when you set up private DNS peering.
  - TARGET\_PROJECT : The project hosting the VPC network.
  - TARGET\_NETWORK : The VPC network name.

### REST

To create a pipeline run, send a `POST` request by using the [pipelineJobs.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/create) method.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The project ID of the project where you want to create the pipeline run.
  - LOCATION : The region where you want to create the pipeline run.
  - DISPLAY\_NAME : The name of the pipeline job. The maximum length for a display name is 128 UTF-8 characters.
  - PIPELINE\_SPEC : The pipeline spec you created in [Create a pipeline spec](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect#create-spec) .
  - OUTPUT\_DIRECTORY : The URI of the Cloud Storage bucket for storing output artifacts. This path is the root output directory for the pipeline and is used to generate the paths of output artifacts.
  - NETWORK\_ATTACHMENT\_NAME : The name of the Compute Engine network attachment to attach to the `PipelineJob` resource. To obtain the network attachment, you must have completed the steps in the [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect#before-you-begin) section. For more information about the network attachment, see [Set up a VPC network, subnet, and network attachment](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-psc-i-setup#set_up_a_network_subnet_and_network_attachment) .
  - DNS\_DOMAIN : The DNS name of the private cloud DNS zone you created when you set up private DNS peering.
  - TARGET\_PROJECT : The project hosting the VPC network.
  - TARGET\_NETWORK : The VPC network name.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs

Request JSON body:

    {
      "display_name": "DISPLAY_NAME",
      "pipeline_spec": "PIPELINE_SPEC",
      "runtime_config": {
           "gcs_output_directory": "OUTPUT_DIRECTORY",
       },
       "psc_interface_config": {
          "network_attachment": "NETWORK_ATTACHMENT_NAME",
          "dns_peering_configs": [
          {
            "domain": "DNS_DOMAIN",
            "target_project": "TARGET_PROJECT",
            "target_network": "TARGET_NETWORK"
          }
        ]
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs" | Select-Object -Expand Content

You should see output similar to the following. PIPELINE\_JOB\_ID represents the ID of the pipeline run and SERVICE\_ACCOUNT\_NAME represents the service account used to run the pipeline.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_JOB_ID",
      "displayName": "DISPLAY_NAME",
      "createTime": "20xx-01-01T00:00:00.000000Z",
      "updateTime": "20xx-01-01T00:00:00.000000Z",
      "pipelineSpec": PIPELINE_SPEC,
      "state": "PIPELINE_STATE_PENDING",
      "labels": {
        "vertex-ai-pipelines-run-billing-id": "VERTEX_AI_PIPELINES_RUN_BILLING_ID"
      },
      "runtimeConfig": {
        "gcsOutputDirectory": "OUTPUT_DIRECTORY"
      },
      "serviceAccount": "SERVICE_ACCOUNT_NAME"
      "pscInterfaceConfig": {
        "networkAttachment": "NETWORK_ATTACHMENT_NAME",
        "dnsPeeringConfigs": [
          {
            "domain": "DNS_DOMAIN",
            "targetProject": "TARGET_PROJECT",
            "targetNetwork": "TARGET_NETWORK"
          }
        ]
      }
    }
