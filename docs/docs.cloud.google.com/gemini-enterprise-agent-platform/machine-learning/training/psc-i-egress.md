---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress
title: Use Private Service Connect interface for Vertex AI Training
description: Use Private Service Connect interface for Vertex AI Training.
data_source: docs.cloud.google.com
---

Private Service Connect interface is recommended for private connectivity since it reduces the chance of IP exhaustion and allows for transitive peering.

Private Service Connect interface is supported on Agent Platform custom jobs and persistent resources.

## Overview

Private Service Connect interface is supported on Vertex AI Training custom jobs and persistent resources. To use Private Service Connect interface, you need to set up a VPC network, subnetwork, and network attachment in your user project. See [Set up a Private Service Connect interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup) . The network attachment name must be included in the request to create a custom job or persistent resource to enable Private Service Connect interface.

## Gemini Enterprise Agent Platform Private Service Connect egress connectivity to other networks

Gemini Enterprise Agent Platform has integrated the egress network connectivities that are supported by Private Service Connect (see [Connecting to workloads in other networks](https://docs.cloud.google.com/vpc/docs/about-private-service-connect-interfaces#other-networks) ), with the following architectural behaviors.

### Reaching Google APIs and internal-only services

When Gemini Enterprise Agent Platform sends traffic to Google APIs, it's resolved locally within the producer environment and doesn't use the Private Google Access settings or routing of your consumer VPC network.

*Note:*

  - VPC identity requirement: Because local resolution bypasses the consumer VPC network path, the traffic doesn't carry your VPC network's identity. This will cause requests to internal-only Google services, such as Cloud Run services configured with internal ingress, to fail with a 404 or 403 error.
  - Private Service Connect endpoint solution: To reach these internal services privately, you must configure a Private Service Connect endpoint for Google APIs in your VPC network.
  - DNS configuration: You must ensure that the service domain (e.g., \*.run.app) resolves to the internal IP address of your Private Service Connect endpoint to ensure traffic stays on a purely private path.

### Internet egress and Cloud NAT

By default, Gemini Enterprise Agent Platform uses Google-managed internet gateways for outbound traffic rather than your VPC network's routes. Egress using a consumer's Cloud NAT gateway is only utilized when the project is part of a VPC Service Control perimeter.

This perimeter blocks default internet access, forcing traffic through the Private Service Connect interface and your VPC network's routing rules. If you aren't using VPC Service Control, outbound internet traffic will bypass your VPC network and Cloud NAT gateway entirely.

## Limitations

For features and limitations of Private Service Connect interfaces, see [About accessing Gemini Enterprise Agent Platform services through Private Service Connect interfaces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-interfaces#limitations) .

## Pricing

Pricing for Private Service Connect interfaces is described in the "Using a Private Service Connect interface for access to a producer or consumer VPC network" section in the [All networking pricing](https://cloud.google.com/vpc/network-pricing) page.

## Before you begin

[Set up your resources for Private Service Connect interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup) on your user project.

## Create a Gemini Enterprise Agent Platform serverless training job with a Private Service Connect interface

You can create a serverless training job with Private Service Connect interface by using the Agent Platform SDK for Python or the REST API.

### Python

To create a serverless training job with PSC-I using the Agent Platform SDK for Python, configure the job using the [`aiplatform_v1/services/job_service`](https://github.com/googleapis/python-aiplatform/tree/main/google/cloud/aiplatform_v1/services/job_service) definition.

### Python

    from google.cloud import aiplatform
    
    
    def create_custom_job_psci_sample(
        project: str,
        location: str,
        bucket: str,
        display_name: str,
        machine_type: str,
        replica_count: int,
        image_uri: str,
        network_attachment: str,
        domain: str,
        target_project: str,
        target_network: str,
    ):
        """Custom training job sample with PSC Interface Config."""
        aiplatform.init(project=project, location=location, staging_bucket=bucket)
    
        worker_pool_specs = [{
            "machine_spec": {
                "machine_type": machine_type,
            },
            "replica_count": replica_count,
            "container_spec": {
                "image_uri": image_uri,
                "command": [],
                "args": [],
            },
        }]
        psc_interface_config = {
            "network_attachment": network_attachment,
            "dns_peering_configs": [
                {
                    "domain": domain,
                    "target_project": target_project,
                    "target_network": target_network,
                },
            ],
        }
        job = aiplatform.CustomJob(
            display_name=display_name,
            worker_pool_specs=worker_pool_specs,
        )
    
        job.run(psc_interface_config=psc_interface_config)

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [list of available locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) .
  - `bucket` : Replace `bucket` with the name of a bucket you have access to.
  - `display_name` : The display name of the persistent resource.
  - `machine_type` : [Specify the compute resources](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute#specify) .
  - `replica_count` : The number of worker replicas to use for each trial.
  - `service_attachment` : The name of the service attachment resource. Populated if Private Service Connect is enabled.
  - `image_uri` : The URI of a Docker container image with your training code. Learn how to [create a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .
  - `network_attachment` : The name or full path of the network attachment you created when setting up your resources for [Private Service Connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress) .
  - `domain` : The DNS name of the private Cloud DNS zone you created when setting up the Private DNS Peering.
  - `target_project` : The project that hosts the VPC network.
  - `target_network` : The VPC network name.

### REST

To create a serverless training job, send a POST request by using the [customJobs.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the container or Python package will be run.
  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - JOB\_NAME : A display name for the `CustomJob` .
  - REPLICA\_COUNT : The number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
  - If your training application runs in a custom container, specify the following:
      - IMAGE\_URI : the URI of a Docker container image with your training code. Learn how to [create a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .
      - NETWORK\_ATTACHMENT : The name or full path of the network attachment you created when you [set up the Private Service Connect interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup) .
      - If you need private DNS peering, the `dns_peering_configs` field is required. For this list, each item contains:
          - DOMAIN\_SUFFIX : The dns name of the private Cloud DNS zone that you created when setting up the Private DNS Peering.
          - TARGET\_PROJECT : The project that hosts the VPC network.
          - TARGET\_NETWORK : The VPC network name.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs

Request JSON body:

    "display_name": JOB_NAME,
    "job_spec": {
        "worker_pool_specs": [
          {
            "machine_spec": {
              "machine_type": "n2-standard-4",
            },
            "replica_count": REPLICA_COUNT,
            "container_spec": {
              "image_uri": IMAGE_URI,
            },
          },
        ],
        "psc_interface_config": {
          "network_attachment": NETWORK_ATTACHMENT,
          "dns_peering_configs": [
             {
              "domain": DOMAIN_SUFFIX,
              "target_project": TARGET_PROJECT,
              "target_network": TARGET_NETWORK
             }
          ],
        },
        "enable_web_access": 1
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID",
      "displayName": "JOB_NAME",
      "jobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "MACHINE_TYPE"
            },
            "replicaCount": "REPLICA_COUNT",
            "diskSpec": DISK_SPEC,
            "containerSpec": {
              "imageUri": "IMAGE_URI"
            }
          }
        ],
        "enableWebAccess": True,
        "pscInterfaceConfig": {
          "networkAttachment": "NETWORK_ATTACHMENT"
          "dns_peering_configs": [
            {
              "domain": "DOMAIN_SUFFIX",
              "targetProject": "TARGET_PROJECT",
              "targetNetwork": "TARGET_NETWORK"
            }
    ]
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "CREATE_TIME",
      "updateTime": "UPDATE_TIME"
    }
