---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster
title: Create cluster
description: Understand system capabilities. Activate features to leverage available platform resources.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

This page provides the direct, API-driven method for creating and managing a training cluster. You'll learn how to define your cluster's complete configuration, including login nodes, high-performance GPU partitions like the A4, and Slurm orchestrator settings—within a JSON file. Also included is how to use curl and REST API calls to deploy this configuration, creating the cluster and managing its lifecycle with `GET` , `LIST` , `UPDATE` and `DELETE` operations.

## Define the cluster configuration

Create a JSON file to define the complete configuration for your training cluster.

If your organizational policy prohibits Public IP addresses on compute instances, deploy the training cluster with the `enable_public_ips: false` parameter and utilize Cloud NAT for internet egress.

The first step in provisioning a training cluster is to define its complete configuration in a JSON file. This file acts as the blueprint for your cluster, specifying everything from its name and network settings to the hardware for its login and worker nodes.

The following section provides several complete JSON configuration files that serve as practical templates for a variety of common use cases. Consult this list to find the example that most closely matches your needs and use it as a starting point.

  - [GPU with Filestore only](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#gpu-filestore-only) : A standard configuration for general-purpose GPU training.

  - [GPU with Filestore and Managed Lustre](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#gpu-filestore-lustre) : An advanced setup for I/O-intensive jobs.

  - [GPU with startup script](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#gpu-startup) : Demonstrates how to run custom commands on nodes at startup.

  - [CPU only cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#cpu-only-cluster) : A basic configuration using only CPU resources.

  - [CPU with advanced Slurm config](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#cpu-slurm-config) : An example showing custom Slurm scheduler settings.

Each example is followed by a detailed description of the key parameters used within that specific configuration.

### GPU with Filestore only

This is the standard configuration. It provides a Filestore instance that serves as the `/home` directory for the cluster, suitable for general use and storing user data.

The following example shows the content of `gpu-filestore.json` . This specification creates a cluster with a GPU partition. You can use this as a template and modify values such as the `machineType` or `nodeCount` to fit your needs.

For a list of parameters, see [Parameter reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#param-reference) .

``` 
 {
  "display_name": "DISPLAY_NAME",
  "network": {
    "network": "projects/PROJECT_ID/global/networks/NETWORK",
    "subnetwork": "projects/PROJECT_ID/regions/REGION/subnetworks/SUBNETWORK"
  },
  "node_pools": [
    {
      "id": "login",
      "machine_spec": {
        "machine_type": "n2-standard-8"
      },
      "scaling_spec": {
        "min_node_count": MIN_NODE_COUNT,
        "max_node_count": MAX_NODE_COUNT
      },
      "enable_public_ips": true,
      "zone": "ZONE",
      "boot_disk": {
        "boot_disk_type": "pd-standard",
        "boot_disk_size_gb": 200
      }
    },
    {
      "id": "a4",
      "machine_spec": {
        "machine_type": "a4-highgpu-8g",
        "accelerator_type": "NVIDIA_B200",
        "accelerator_count": 8,
        "reservation_affinity": {
          "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
          "key": "compute.googleapis.com/reservation-name",
          "values": [
            "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION"
          ]
        }
      },
      "provisioning_model": "RESERVATION",
      "scaling_spec": {
        "min_node_count": MIN_NODE_COUNT,
        "max_node_count": MAX_NODE_COUNT
      },
      "enable_public_ips": true,
      "zone": "ZONE",
      "boot_disk": {
        "boot_disk_type": "hyperdisk-balanced",
        "boot_disk_size_gb": 200
      }
    }
  ],
  "orchestrator_spec": {
    "slurm_spec": {
      "home_directory_storage": "projects/PROJECT_ID/locations/ZONE/instances/FILESTORE",
      "partitions": [
        {
          "id": "a4",
          "node_pool_ids": [
            "a4"
          ]
        }
      ],
      "login_node_pool_id": "login"
    }
  }
}
```

### GPU with Filestore and Managed Lustre

This advanced configuration includes the standard Filestore instance in addition to a high-performance Lustre file system. Choose this option if your training jobs require high-throughput access to large datasets.

For a list of parameters, see [Parameter reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#param-reference) .

``` 
{
  "display_name": "DISPLAY_NAME",
  "network": {
    "network": "projects/PROJECT_ID/global/networks/NETWORK",
    "subnetwork": "projects/PROJECT_ID/regions/asia-sREGION/subnetworks/SUBNETWORK"
  },
  "node_pools": [
    {
      "id": "login",
      "machine_spec": {
        "machine_type": "n2-standard-8"
      },
      "scaling_spec": {
        "min_node_count": MIN_NODE_COUNT,
        "max_node_count": MAX_NODE_COUNT
      },
      "enable_public_ips": true,
      "zone": "ZONE",
      "boot_disk": {
        "boot_disk_type": "pd-standard",
        "boot_disk_size_gb": 200
      },
      "lustres": [
        "projects/PROJECT_ID/locations/ZONE/instances/LUSTRE"
      ]
    },
    {
      "id": "a4",
      "machine_spec": {
        "machine_type": "a4-highgpu-8g",
        "accelerator_type": "NVIDIA_B200",
        "accelerator_count": 8,
        "reservation_affinity": {
          "reservation_affinity_type": RESERVATION_AFFINITY_TYPE,
          "key": "compute.googleapis.com/reservation-name",
          "values": [
            "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME"
          ]
        }
      },
      "provisioning_model": "RESERVATION",
      "scaling_spec": {
        "min_node_count": MIN_NODE_COUNT,
        "max_node_count": MAX_NODE_COUNT
      },
      "enable_public_ips": true,
      "zone": "ZONE",
      "boot_disk": {
        "boot_disk_type": "hyperdisk-balanced",
        "boot_disk_size_gb": 200
      },
      "lustres": [
        "projects/PROJECT_ID/locations/ZONE/instances/LUSTRE"
      ]
    }
  ],
  "orchestrator_spec": {
    "slurm_spec": {
      "home_directory_storage": "projects/PROJECT_ID/locations/ZONE/instances/FILESTORE",
      "partitions": [
        {
          "id": "a4",
          "node_pool_ids": [
            "a4"
          ]
        }
      ],
      "login_node_pool_id": "login"
    }
  }
}
  
```

### GPU with startup script

This example demonstrates how to add a custom script to a node pool. This script executes on all nodes in that pool at startup. To configure this, add the relevant fields to your node pool's definition in addition to the general settings. For a list of parameters and their descriptions, see [Parameter reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#param-reference) .

    {
      "display_name": "DISPLAY_NAME",
      "network": {
        "network": "projects/PROJECT_ID/global/networks/NETWORK",
        "subnetwork": "projects/PROJECT_ID/regions/REGION/subnetworks/SUBNETWORK"
      },
      "node_pools": [
        {
          "id": "login",
          "machine_spec": {
            "machine_type": "n2-standard-8"
          },
          "scaling_spec": {
            "min_node_count": MIN_NODE_COUNT,
            "max_node_count": MAX_NODE_COUNT
          },
          "enable_public_ips": true,
          "zone": "ZONE",
          "boot_disk": {
            "boot_disk_type": "pd-standard",
            "boot_disk_size_gb": 200
          },
          "startup_script" : "#Example script\nsudo mkdir -p /data\necho 'Script Finished'\n",
        },
        {
          "id": "a4",
          "machine_spec": {
            "machine_type": "a4-highgpu-8g",
            "accelerator_type": "NVIDIA_B200",
            "accelerator_count": 8,
            "reservation_affinity": {
              "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
              "key": "compute.googleapis.com/reservation-name",
              "values": [
                "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME"
              ]
            }
          },
          "provisioning_model": "PROVISIONING_MODEL",
          "scaling_spec": {
            "min_node_count": MIN_NODE_COUNT,
            "max_node_count": MAX_NODE_COUNT
          },
          "enable_public_ips": true,
          "zone": "ZONE",
          "boot_disk": {
            "boot_disk_type": "hyperdisk-balanced",
            "boot_disk_size_gb": 200
          },
          "startup_script" : "#Example script\nsudo mkdir -p /data\necho 'Script Finished'\n",
        }
      ],
      "orchestrator_spec": {
        "slurm_spec": {
          "home_directory_storage": "projects/PROJECT_ID/locations/ZONE/instances/FILESTORE",
          "partitions": [
            {
              "id": "a4",
              "node_pool_ids": [
                "a4"
              ]
            }
          ],
          "login_node_pool_id": "login"
        }
      }
    }

### CPU only cluster

To provision a training cluster environment, you must first define its complete configuration in a JSON file. This file acts as the blueprint for your cluster, specifying everything from its name and network settings to the hardware for its login and worker nodes.

For a list of parameters, see [Parameter reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#param-reference) .

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
            "min_node_count": MIN_NODE_COUNT,
            "max_node_count": MAX_NODE_COUNT
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
          }
          "scaling_spec": {
            "min_node_count": MIN_NODE_COUNT,
            "max_node_count": MAX_NODE_COUNT
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

### CPU with advanced Slurm config

This example demonstrates how to customize the Slurm orchestrator with advanced parameters. Use this template if you need fine-grained control over job scheduling behavior, such as setting multifactor priority weights, configuring job preemption, and running prolog and epilog scripts for automated job setup and cleanup.

For a list of parameters, see [Parameter reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#param-reference) .

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
            "min_node_count": MIN_NODE_COUNT,
            "max_node_count": MAX_NODE_COUNT
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
            "machine_type": "n2-standard-8"
          },
          "scaling_spec": {
            "min_node_count": MIN_NODE_COUNT,
            "max_node_count": MAX_NODE_COUNT
          },
          "zone": "ZONE",
          "enable_public_ips": true,
          "boot_disk": {
            "boot_disk_type": "pd-standard",
            "boot_disk_size_gb": 120
          }
        }
      ],
      "orchestrator_spec": {
        "slurm_spec": {
          "home_directory_storage": "projects/PROJECT_ID/locations/ZONE/instances/FILESTORE",
          "accounting": {
            "accounting_storage_enforce": "ACCOUNTING_STORAGE_ENFORCE"
          },
          "scheduling": {
            "priority_type": "PRIORITY_TYPE",
            "priority_weight_age": PRIORITY_WEIGHT_AGE,
            "priority_weight_assoc": PRIORITY_WEIGHT_ASSOC,
            "priority_weight_fairshare": PRIORITY_WEIGHT_FAIRSHARE,
            "priority_weight_job_size": PRIORITY_WEIGHT_JOB_SIZE,
            "priority_weight_partition": PRIORITY_WEIGHT_PARTITION,
            "priority_weight_qos": PRIORITY_WEIGHT_QOS,
            "priority_weight_tres": "PRIORITY_WEIGHT_TRES",
            "preempt_type": "PREEMPT_TYPE",
            "preempt_mode": "PREEMPT_MODE",
            "preempt_exempt_time": "PREEMPT_EXEMPT_TIME"
          },
          "prolog_bash_scripts": [
            "#!/bin/bash\necho 'First prolog script running'",
            "#!/bin/bash\necho 'Second prolog script running'"
          ],
          "epilog_bash_scripts": [
            "#!/bin/bash\necho 'Epilog script running'"
          ]
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

Once your cluster is defined in a JSON file, use the following REST API commands to deploy and manage the cluster. The examples use a `gcurl` alias, which is a convenient, authenticated shortcut for interacting with the API endpoints. These commands cover the full lifecycle, from initially deploying your cluster to updating a cluster getting its status, listing all clusters, and ultimately deleting the cluster.

## Authentication

    alias gcurl='curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json"'

## Create a JSON file

Create a JSON file (for example, `@cpu-cluster.json` ) to specify the configuration for your Model Training cluster.

## Deploy the cluster

Once you've created the JSON configuration file, you can deploy the cluster using the REST API.

### Set environment variables

Before running the command, set the following environment variables. This makes the API command cleaner and easier to manage.

  - PROJECT\_ID : Your Google Cloud project ID where the cluster will be created.
  - REGION : The Google Cloud region for the cluster and its resources.
  - ZONE : The Google Cloud zone where the cluster resources will be provisioned.
  - CLUSTER\_ID : A unique identifier for your training cluster, which is also used as a prefix for naming related resources.

### Run the create command

Now, execute the following gcurl command. It uses the JSON file (in this example, `cpu-cluster.json` ) as the request body and the environment variables you just set to construct the API endpoint and query parameters.

``` 
  gcurl -X POST -d @cpu-cluster.json https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters?model_development_cluster_id=CLUSTER_ID
    
```

Once the deployment starts, an Operation ID will be generated. Be sure to copy this ID. You'll need it to validate your cluster in the next step.

``` 
  gcurl -X POST -d @cpu-cluster.json https://us-central1-aiplatform.googleapis.com/v1beta1/projects/managedtraining-project/locations/us-central1/modelDevelopmentClusters?model_development_cluster_id=training
  {
      "name": "projects/1059558423163/locations/us-central1/operations/2995239222190800896",
      "metadata": {
      "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.CreateModelDevelopmentClusterOperationMetadata",
      "genericMetadata": {
        "createTime": "2025-10-24T14:16:59.233332Z",
        "updateTime": "2025-10-24T14:16:59.233332Z"
      },
      "progressMessage": "Create Model Development Cluster request received, provisioning..."
  }
    
```

## Validate cluster deployment

Track the deployment's progress using the operation ID provided when you deployed the cluster. For example, `2995239222190800896` is the operation ID in the example cited earlier.

``` 
    gcurl https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/operations/OPERATION_ID
    
```

## In summary

Submitting your cluster configuration with the `gcurl` POST command initiates the provisioning of your cluster, which is an asynchronous, long-running operation. The API immediately returns a response containing an `Operation ID` . It's crucial to save this ID, since you'll use it in the following steps to monitor the deployment's progress, verify that the cluster has been created successfully, and manage its lifecycle.

## Parameter reference

The following list describes all parameters used in the configuration examples. The parameters are organized into logical groups based on the resource they configure.

### General and network settings

  - DISPLAY\_NAME : A unique name for your training cluster. The string can only contain lowercase alphanumeric characters, must begin with a letter, and is limited to 10 characters.
  - PROJECT\_ID : Your Google Cloud project ID.
  - REGION : The Google Cloud region where the cluster and its resources will be located.
  - NETWORK : The Virtual Private Cloud network to use for the cluster's resources.
  - ZONE : The Google Cloud zone for the cluster and its resources.
  - SUBNETWORK : The subnetwork to use for the cluster's resources.

### Node pool configuration

The following parameters are used to define the node pools for both login and worker nodes.

#### Common node pool settings

  - ID : A unique identifier for the node pool within the cluster (for example, " `login` ", " `a4` ", " `cpu` ").
  - PROVISIONING\_MODEL : The provisioning model for the worker node (for example, `ON_DEMAND` , `SPOT` , `RESERVATION` , `FLEX_START` ).
  - MACHINE\_TYPE : The machine type for the worker node. Supported values are `a3-megagpu-8g` , `a3-ultragpu-8g` , `a4-highgpu-8g` .
  - MIN\_NODE\_COUNT : The `MIN_NODE_COUNT` must be the same as the `MAX_NODE_COUNT` .
  - MAX\_NODE\_COUNT : For the login node pool, the `MAX_NODE_COUNT` must be the same as the `MIN_NODE_COUNT` .
  - ENABLE\_PUBLIC\_IPS : A boolean ( `true` or `false` ) to determine if the login node has a public IP address.
  - BOOT\_DISK\_TYPE : The boot disk type for the login node (for example, `pd-standard` , `pd-ssd` ).
  - BOOT\_DISK\_SIZE\_GB : The boot disk size in GB for the login node.

#### Additional storage settings

  - FILESTORES (corresponds to `filestores` inside a `node_pools` object): A list of pre-existing Filestore instances to mount on the node pool for shared file access.
  - LUSTRES (corresponds to `lustres` inside a `node_pools` object): A list of pre-existing Lustre instances to mount on the node pool for high-performance file access.

### Worker-Specific Settings

  - ACCELERATOR\_TYPE : The corresponding GPU accelerator to attach to the worker nodes. Supported values are:
      - `NVIDIA_H100_MEGA_80GB`
      - `NVIDIA_H200_141GB`
      - `NVIDIA_B200`
  - ACCELERATOR\_COUNT : The number of accelerators to attach to each worker node.
  - RESERVATION\_AFFINITY\_TYPE : The reservation affinity for the node pool (for example, `SPECIFIC_RESERVATION` ).
  - RESERVATION\_NAME : The name of the reservation to use for the node pool.

### Orchestrator and storage configuration

These fields are defined within the `orchestrator_spec.slurm_spec` block of the JSON file.

#### Core Slurm and Storage settings

  - HOME\_DIRECTORY\_STORAGE (corresponds to `home_directory_storage` ): The full resource name of the pre-existing storage instance to be mounted as the `/home` directory. Can be a Filestore or Lustre instance.
  - LOGIN\_NODE\_POOL\_ID (corresponds to `login_node_pool_id` ): The id of the node pool that should be used for login nodes.
  - `partitions` : A list of partition objects, where each object requires an `id` and a list of `node_pool_ids` .

#### Advanced Slurm settings

  - `prolog_bash_scripts` : A list of strings, where each string contains the full content of a Bash script to be executed before a job begins.
  - `epilog_bash_scripts` : A list of strings, where each string contains the full content of a Bash script to be executed after a job completes.
  - ACCOUNTING\_STORAGE\_ENFORCE : Enforces accounting limits for storage usage.
  - PRIORITY\_TYPE : The scheduling priority algorithm to be used (for example, `priority/multifactor` ).
  - `priority_weight_*` : A set of integer values that assign weight to different factors in the scheduling priority calculation (for example, `priority_weight_age` , `priority_weight_fairshare` ).
  - PREEMPT\_TYPE : The preemption plugin to use (for example, preempt/partition\_prio ).
  - PREEMPT\_MODE : The mode for the preemption plugin (for example, `REQUEUE` ).
  - PREEMPT\_EXEMPT\_TIME : The time after a job starts during which it can't be preempted.

### Runtime configuration

These fields are defined within the `runtime_spec` block of the JSON file.

  - `service_account` : The default service account used by the cluster when running any workloads on it. If unspecified, the default Compute Engine service account is used. This field can't be updated after cluster creation.

## What's next

Use your active persistent training cluster to run your machine learning workloads.

  - Run a job on your cluster: Submit a `CustomJob` to run a training job on your persistent cluster.
      - [Learn how to run a distributed training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training)
  - Orchestrate your training with Gemini Enterprise Agent Platform Pipelines: For repeatable, production-grade workflows, automate the job submission process using Agent Platform Pipelines.
      - [Learn about orchestrating jobs on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)
  - View and manage your cluster: List existing clusters, check their status, and view configuration details using the Google Cloud CLI or the Google Cloud console.
      - [Learn how to manage your training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster)
  - Delete your cluster to stop incurring costs: Training clusters are persistent and incur costs while active.
      - [Learn how to delete your training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster#delete-a-cluster:)
