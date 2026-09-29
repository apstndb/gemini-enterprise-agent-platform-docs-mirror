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

  - [Advanced Slurm configuration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#slurm-config-maps-example) : Demonstrates setting `slurm.conf` parameters at cluster, partition, or node pool scope, and running prolog and epilog scripts.

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
      },
      "labels": { "example-key": "example-value" }
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
      "labels": { "example-key": "example-value" }
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
          "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
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
          "startup_script" : "#Example script\nsudo mkdir -p /data\necho 'Script Finished'\n"
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
          "startup_script" : "#Example script\nsudo mkdir -p /data\necho 'Script Finished'\n"
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

### Advanced Slurm configuration

This example gives fine-grained control over Slurm by setting `slurm.conf` parameters by name, and by running prolog and epilog scripts for automated job setup and cleanup. Parameters can be set cluster-wide, for a single partition, or for a single node pool.

There are three configuration maps, one for each `slurm.conf` record:

  - `config` on the Slurm spec for cluster-wide settings
  - `config` on a partition
  - `node_sets` entry for a node pool

For the rules on parameter names, values, and which parameters are refused, see [Slurm configuration maps](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#slurm-config-maps) .

You don't have to settle these at creation time. All three maps can be changed on a running cluster, without restarting nodes or disrupting queued jobs. See [Update Slurm configuration settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster#update-slurm-config-maps) .

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
          "config": {
            "PriorityType": "priority/multifactor",
            "PriorityWeightAge": "1000",
            "PriorityWeightFairshare": "10000",
            "PreemptType": "preempt/partition_prio",
            "PreemptMode": "SUSPEND,GANG",
            "SchedulerParameters": "bf_continue,bf_window=1440,bf_resolution=600",
            "AccountingStorageEnforce": "limits,qos"
          },
          "prolog_bash_scripts": [
            "#!/bin/bash\necho 'Prolog script running'"
          ],
          "epilog_bash_scripts": [
            "#!/bin/bash\necho 'Epilog script running'"
          ],
          "partitions": [
            {
              "id": "cpu",
              "node_pool_ids": [
                "cpu"
              ],
              "config": {
                "MaxTime": "4-00:00:00",
                "DefMemPerCPU": "4096",
                "PriorityTier": "20"
              }
            }
          ],
          "node_sets": [
            {
              "node_pool_id": "cpu",
              "config": {
                "Weight": "10",
                "Features": "cpu,spot"
              }
            }
          ],
          "login_node_pool_id": "login"
        }
      }
    }

The cluster-scoped map sets multifactor priority, partition-priority preemption and `SchedulerParameters` , whose `bf_continue` term shows the composite form: a bare term turns a flag on, and terms are comma-separated. The partition map bounds job runtime and default memory for the `cpu` partition only, and the `node_sets` entry labels that pool's nodes so jobs can select them with `--constraint` .

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
  - MACHINE\_TYPE : The machine type for the worker node (for example, `a3-highgpu-8g` , `a3-megagpu-8g` , `a3-ultragpu-8g` , `a4-highgpu-8g` ). For the full list of supported machine types, see [Compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/compute-resources) .
  - MIN\_NODE\_COUNT : The `MIN_NODE_COUNT` must be the same as the `MAX_NODE_COUNT` .
  - MAX\_NODE\_COUNT : For the login node pool, the `MAX_NODE_COUNT` must be the same as the `MIN_NODE_COUNT` .
  - ENABLE\_PUBLIC\_IPS : A boolean ( `true` or `false` ) to determine if the login node has a public IP address.
  - BOOT\_DISK\_TYPE : The boot disk type for the login node (for example, `pd-standard` , `pd-ssd` ).
  - BOOT\_DISK\_SIZE\_GB : The boot disk size in GB for the login node.
  - LABELS : A set of key/value pairs to label the node pool.
  - NODE\_IMAGE (corresponds to `node_image` inside a `node_pools` object): The VM image the node pool's nodes boot from, as a full image or image family resource path (for example, ` projects/ IMAGE_PROJECT /global/images/family/ IMAGE_FAMILY  ` ). If you omit it, the node pool uses the current default image for its machine type, which advances over time. Set it to keep the node pool on a specific image. Changing a node pool's image recreates its nodes.

#### Additional storage settings

  - FILESTORES (corresponds to `filestores` inside a `node_pools` object): A list of pre-existing Filestore instances to mount on the node pool for shared file access.
  - LUSTRES (corresponds to `lustres` inside a `node_pools` object): A list of pre-existing Lustre instances to mount on the node pool for high-performance file access.

### Worker-Specific Settings

  - ACCELERATOR\_TYPE : The corresponding GPU accelerator to attach to the worker nodes. Supported values are:
      - `NVIDIA_H100_80GB`
      - `NVIDIA_H100_MEGA_80GB`
      - `NVIDIA_H200_141GB`
      - `NVIDIA_B200`
  - ACCELERATOR\_COUNT : The number of accelerators to attach to each worker node.
  - RESERVATION\_AFFINITY\_TYPE (corresponds to `machine_spec.reservation_affinity.reservationAffinityType` ): The reservation affinity for the node pool. This parameter must be `SPECIFIC_RESERVATION` , which is the only supported value. When `SPECIFIC_RESERVATION` is used, you must specify the reservation in `machine_spec.reservation_affinity.values` .
  - RESERVATION\_NAME : The name of the reservation to use for the node pool. This is used in the full reservation resource name provided in `machine_spec.reservation_affinity.values` , for example ` projects/ PROJECT_ID /zones/ ZONE /reservations/ RESERVATION_NAME  ` . A reservation is required when RESERVATION\_AFFINITY\_TYPE is `SPECIFIC_RESERVATION` .

### Orchestrator and storage configuration

These fields are defined within the `orchestrator_spec.slurm_spec` block of the JSON file.

#### Core Slurm and Storage settings

  - HOME\_DIRECTORY\_STORAGE (corresponds to `home_directory_storage` ): The full resource name of the pre-existing storage instance to be mounted as the `/home` directory. Can be a Filestore or Lustre instance.
  - LOGIN\_NODE\_POOL\_ID (corresponds to `login_node_pool_id` ): The id of the node pool that should be used for login nodes.
  - `partitions` : A list of partition objects, where each object requires an `id` and a list of `node_pool_ids` . The first partition in the list is the cluster's default partition: Slurm jobs submitted without an explicit partition (for example, `sbatch` without `--partition` ) run on it. To set the default partition, reorder the list of partitions so that the default partition is at the top of the list. This applies to updates as well: reordering the partitions of an existing cluster changes its default partition.

#### Advanced Slurm settings

  - `prolog_bash_scripts` : A list of strings, where each string contains the full content of a Bash script to be executed before a job begins.
  - `epilog_bash_scripts` : A list of strings, where each string contains the full content of a Bash script to be executed after a job completes.
  - `config` , `partitions[].config` and `node_sets` : Slurm parameters set by name. See [Slurm configuration maps](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#slurm-config-maps) .
  - `scheduling` and `accounting` : Superseded. These two objects expose a fixed set of priority, preemption and accounting parameters, each of which can be set by name in the cluster-scoped `config` map instead ( `priority_type` as `"PriorityType"` , `preempt_mode` as `"PreemptMode"` , and so on). They still work for clusters that use them, but new clusters should use `config` , which reaches every `slurm.conf` parameter rather than this subset.

#### Slurm configuration maps

Slurm parameters are set by name, in three maps, one for each `slurm.conf` record:

  - `config` : Cluster-scoped settings, written as global `Key=Value` lines.
  - `partitions[].config` : Settings for one partition, written as extra pairs on that partition's `PartitionName=` line.
  - `node_sets` : A list of objects, each with a `node_pool_id` and a `config` map. The settings are written as extra pairs on the `NodeName=` line for that node pool's nodes. At most one entry per node pool, and the pool must be a compute pool of the cluster, not the login pool.

In all three, keys are Slurm parameter names as [SchedMD documents them](https://slurm.schedmd.com/slurm.conf.html) , without matching case and ignoring underscores, so `DefMemPerCPU` , `defmempercpu` and `def_mem_per_cpu` all mean the same parameter. Values are written the way `slurm.conf` writes them, including comma-separated lists such as `"PreemptMode": "SUSPEND,GANG"` and composite values such as `"SchedulerParameters": "bf_window=1440,bf_resolution=600"` .

A parameter that isn't supported in the scope you set it in, or a value that isn't legal for that parameter, is rejected when you make the request, and the error names the parameter. Nothing is silently dropped. Some parameters are refused for a specific reason:

  - The service manages node health checking and job requeueing, so `HealthCheckProgram` , `HealthCheckInterval` , `HealthCheckNodeState` and `RequeueExit` can't be set.
  - `Prolog` and `Epilog` are set through `prolog_bash_scripts` and `epilog_bash_scripts` instead.
  - `slurmdbd.conf` parameters, such as `StorageHost` and `PurgeJobAfter` , aren't configurable: the accounting database is managed by the service.
  - At partition scope, `Default` is refused. The default partition is a cluster-wide choice, made by ordering the `partitions` list.

> **Warning:** The service validates each parameter on its own, not whether the resulting `slurm.conf` is valid as a whole. Some accepted settings stop the Slurm controller from starting, such as `"PreemptType": "preempt/none"` with `"PreemptMode": "SUSPEND,GANG"` , or a partition `AllowQos` that names a QoS the cluster doesn't define. The create or update operation can still report success, but Slurm commands such as `sinfo` and `scontrol` then fail. Check your settings against the [slurm.conf reference](https://slurm.schedmd.com/slurm.conf.html) for your cluster's Slurm version. If Slurm commands fail after a create or update, reach out to your Gemini Enterprise Agent Platform training clusters contact, who can identify the setting that caused the failure.

> **Note:** The cluster-scoped `config` map supersedes the `scheduling` and `accounting` fields, so a cluster uses one or the other and a request that sets both is rejected. Note that every value is the literal `slurm.conf` text, so numbers are written as strings: `"priority_weight_age": 1000` becomes `"PriorityWeightAge": "1000"` . The partition- and node-scoped maps aren't affected: they describe different `slurm.conf` records and can be used alongside those fields.

### Runtime configuration

These fields are defined within the `runtime_spec` block of the JSON file.

  - `service_account` : The default service account used by the cluster when running any workloads on it. If unspecified, the default Compute Engine service account is used. This field can't be updated after cluster creation.

> **Caution:** Contact your Google account team before you create a cluster with a custom `service_account` . By default, your project's default Compute Engine service account has access to the Gemini Enterprise Agent Platform training clusters agent repositories. If you use a custom service account, your Google account team must grant it access separately.

## What's next

Use your active persistent training cluster to run your machine learning workloads.

  - Run a job on your cluster: Submit a `CustomJob` to run a training job on your persistent cluster.
      - [Learn how to run a distributed training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training)
  - Orchestrate your training with Gemini Enterprise Agent Platform Pipelines: For repeatable, production-grade workflows, automate the job submission process using Agent Platform Pipelines.
      - [Learn about orchestrating jobs on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)
  - View your cluster: List the existing clusters in your project, check their status, and view configuration details using the Google Cloud console or the Agent Platform API.
      - [Learn how to view your training clusters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/view-clusters)
  - Change your cluster: Update an existing cluster's configuration, such as its node counts or its Slurm partitions.
      - [Learn how to manage your training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster)
  - Delete your cluster to stop incurring costs: Training clusters are persistent and incur costs while active.
      - [Learn how to delete your training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster#delete-a-cluster)
