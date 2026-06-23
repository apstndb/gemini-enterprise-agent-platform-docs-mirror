---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster
title: Manage cluster
description: 'Manage Agent Platform cluster lifecycle. Use REST API endpoints: Get, List, Update, Delete clusters in your {{dynamic_data.site_values.cloud_name}} project.'
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Once a cluster is deployed, you can manage its full lifecycle using the following REST API endpoints.

  - `List` : Views all active clusters in your project.
  - `Get` : Retrieves detailed information for a specific cluster.
  - `Update` : Modifies an existing cluster configuration.
  - `Delete` : Permanently removes a cluster and its resources.

#### Authentication

    alias gcurl='curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json"'

#### List clusters:

``` 
    gcurl -X GET https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters
    
```

The list method supports the following optional query parameters to control pagination.

  - `pageSize` (integer, optional): The maximum number of clusters to return in the response. The service may return fewer than this value, even if more items exist. If unspecified, a default page size will be used.
  - `pageToken (string, optional)` : A token received from a previous list call. Provide this token to retrieve the subsequent page of results.

The following example requests the first page of results with a maximum of 5 clusters per page.

``` 
    gcurl "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters?pageSize=5"
    
```

A successful response contains a clusters array with up to five cluster resources and may also include a `nextPageToken` string.

#### Get a cluster:

``` 
    gcurl -X GET https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID
    
```

#### Update a cluster:

`UPDATE_PAYLOAD` specifies the local path to a JSON file that defines the full `ModelDevelopmentCluster` you want to update to.

For example, to update the node count of a pool of a [CPU-only cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/managed-training/create-cluster#cpu-only-cluster) , use the following JSON payload:

    {
      "display_name": "DISPLAY_NAME",
      "network": {
        "network": "projects/PROJECT_ID/global/networks/NETWORK",
        "subnetwork": "projects/PROJECT_ID/regions/REGION/subnetworks/SUBNETWORK"
      },
      "node_pools": [
        {
          "id": "cpu",
          "machine_spec": {
            "machine_type": "n2-standard-8"
          },
          "scaling_spec": {
            "min_node_count": UPDATED_MIN_NODE_COUNT,
            "max_node_count": UPDATED_MAX_NODE_COUNT
          },
          "zone": "ZONE",
          "enable_public_ips": true,
          "boot_disk": {
            "boot_disk_type": "pd-standard",
            "boot_disk_size_gb": 120
          }
        },
        {
          "id": "login",
          "machine_spec": {
            "machine_type": "n2-standard-8",
          },
          "scaling_spec": {
            "min_node_count": 1,
            "max_node_count": 1
          },
             "zone": "ZONE",
             "enable_public_ips": true,
          "boot_disk": {
            "boot_disk_type": "pd-standard",
            "boot_disk_size_gb": 120
          }
        },
      ],
      "orchestrator_spec": {
          "slurm_spec": {
          "home_directory_storage": "projects/PROJECT_ID/locations/ZONE/instances/FILESTORE",
          "partitions": [
             {
              "id": "cpu",
              "node_pool_ids": [
                "cpu"
              ]
            }
          ],
          "login_node_pool_id": "login"
        }
      }
    }

    gcurl -X PATCH -d @UPDATE_PAYLOAD https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID

**Query Parameters**

  - `updateMask` (string, optional): A [FieldMask](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) that specifies which fields of the Model Development cluster resource to update. Only the fields listed in the `updateMask` are changed.
    
    The following fields within the `ModelDevelopmentCluster` resource can be specified in the `updateMask` :
    
      - `node_pools`
      - `orchestrator_spec.slurm_spec.partitions`
      - `orchestrator_spec.slurm_spec.login_node_pool_id`
      - `orchestrator_spec.slurm_spec.prolog_bash_scripts`
      - `orchestrator_spec.slurm_spec.epilog_bash_scripts`

  - `updateMode` (enum, optional): Specifies the update mode. Possible values are:
    
      - `UPDATE_MODE_UNSPECIFIED` : The default value, treated as `USER_AND_SERVICE` .
      - `USER_ONLY` : Apply only user-specified field changes from the request. The service won't refresh service-managed fields, like startup, prolog, or epilog scripts.
      - `USER_AND_SERVICE` : Apply user-specified field changes and let the service refresh service-managed fields.
    
    We recommend using `USER_AND_SERVICE` to ensure your cluster is up-to-date.

The command below updates both the node pool configuration and the Slurm partitions.

    gcurl -X PATCH -d @update-payload.json
    'https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID?updateMask=orchestrator_spec.slurm_spec.partitions,node_pools&updateMode=USER_AND_SERVICE'

**Important note on repeated fields**

For repeated fields, such as `node_pools` , `prolog_bash_scripts` , and `epilog_bash_scripts` , the API only supports a full replacement operation. The user must provide the entire, expected list of items in the request payload to replace the existing list completely.

**Post-update behavior and cluster status**

A successful request returns a Long Running Operation (LRO). You can then monitor the status of this operation using the following command:

    gcurl https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/operations/OPERATION_ID

Once the update operation completes successfully, most modifications take effect immediately (or within the 15s Slurm sync time) and require no further action. Only changes to the underlying cluster compute infrastructure—including modifications to storage sources and startup scripts—require the resources to be recreated.

#### Delete a cluster:

``` 
  gcurl -X DELETE https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID
  
```

This command returns a Long-Running Operation on success, which you can then monitor using the `operations describe` command.

    gcurl https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/operations/OPERATION_ID

## What's next

Managing your Gemini Enterprise Agent Platform training cluster lets you optimize its usage, integrate it into automated workflows, and prepare your trained models for deployment.

  - Orchestrate your training with Gemini Enterprise Agent Platform Pipelines: Automate the entire lifecycle of your training jobs, from data preparation to model registration, using pipelines that target your managed cluster.
      - [Learn about orchestrating jobs on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)
  - Monitor and debug your training jobs: Track progress and resource usage, and identify issues with your distributed training jobs running on the cluster.
      - [Monitor training jobs on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics)
  - Deploy your model for inference: After your models are trained and registered, deploy them to a Gemini Enterprise Agent Platform endpoint to serve online inference requests at scale.
      - [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment)
  - Optimize costs: Regularly review your cluster utilization and delete the cluster when it's not actively in use to minimize billing for reserved hardware.
