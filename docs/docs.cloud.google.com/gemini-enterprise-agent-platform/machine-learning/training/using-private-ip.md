---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip
title: Use a private IP for Gemini Enterprise Agent Platform serverless training
description: How to run Gemini Enterprise Agent Platform serverless training jobs in your network after setting up VPC Network Peering to peer your network with a Gemini Enterprise Agent Platform CustomJob, HyperparameterTuningJob, or custom TrainingPipeline resource.
data_source: docs.cloud.google.com
---

> **Note:** Vertex AI Training doesn't support VPC Peering with H100-mega, H200 and B200 accelerators. A [network attachment with PSC-I](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress) can be used as an alternative for VPC Peering.

Using private IP to connect to your training jobs provides more network security and lower network latency than using public IP. To use private IP, you use [Virtual Private Cloud (VPC)](https://docs.cloud.google.com/vpc/docs/vpc-peering) to peer your network with any type of [Gemini Enterprise Agent Platform serverless training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods) . This allows your training code to access private IP addresses inside your Google Cloud or on-premises networks.

This guide shows how to run serverless training jobs in your network after you have already [set up VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) to peer your network with an Agent Platform `CustomJob` , `HyperparameterTuningJob` , or custom `TrainingPipeline` resource.

## Overview

Before you submit a serverless training job using private IP, you must [configure private services access to create peering connections between your network and Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) . If you have already set this up, you can use your existing peering connections.

This guide covers the following tasks:

  - Understanding which IP ranges to reserve for serverless training.
  - Verify the status of your existing peering connections.
  - Perform Gemini Enterprise Agent Platform serverless training on your network.
  - Check for active training occurring on one network before training on another network.
  - Test that your training code can access private IPs in your network.

### Reserve IP ranges for serverless training

When you reserve an IP range for service producers, the range can be used by Agent Platform and other services. This table shows the maximum number of parallel training jobs that you can run with reserved ranges from /16 to /18, assuming the range is used almost exclusively by Agent Platform. If you connect with other service producers using the same range, allocate a larger range to accommodate them, in order to avoid IP exhaustion.

**Machine configuration for training job**

**Reserved range**

**Maximum number of parallel jobs**

Up to 8 nodes.  
For example: 1 primary replica in the first worker pool, 6 replicas in the second worker pool, and 1 worker in the third worker pool (to act as a parameter server)

/16

63

/17

31

/18

15

Up to 16 nodes.  
For example: 1 primary replica in the first worker pool, 14 replicas in the second worker pool, and 1 worker in the third worker pool (to act as a parameter server)

/16

31

/17

15

/18

7

Up to 32 nodes.  
For example: 1 primary replica in the first worker pool, 30 replicas in the second worker pool, and 1 worker in the third worker pool (to act as a parameter server)

/16

15

/17

7

/18

3

Learn more about [configuring worker pools for distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) .

## Check the status of existing peering connections

If you have existing peering connections you use with Agent Platform, you can list them to check status:

    gcloud compute networks peerings list --network NETWORK_NAME

You should see that the state of your peering connections are `ACTIVE` . Learn more about [active peering connections](https://docs.cloud.google.com/vpc/docs/peer-two-networks#peering-becomes-active) .

## Perform serverless training

When you perform serverless training, you must specify the name of the network that you want Agent Platform to have access to.

Depending on how you perform serverless training, specify the network in one of the following API fields:

  - **If you are creating a [`CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs) ,** specify the `CustomJob.jobSpec.network` field.
    
    If you are using the Google Cloud CLI, then you can use the `--config` flag on the [`gcloud ai custom-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create) to specify the `network` field.
    
    Learn more about [creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

  - **If you are creating a [`HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs) ,** specify the `HyperparameterTuningJob.trialJobSpec.network` field.
    
    If you are using the gcloud CLI, then you can use the `--config` flag on the [`gcloud ai hpt-tuning-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/create) to specify the `network` field.
    
    Learn more about [creating a `HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .

  - **If you are creating a [`TrainingPipeline`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines) without hyperparameter tuning,** specify the `TrainingPipeline.trainingTaskInputs.network` field.
    
    Learn more about [creating a custom `TrainingPipeline`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

  - **If you are creating a `TrainingPipeline` with hyperparameter tuning** , specify the `TrainingPipeline.trainingTaskInputs.trialJobSpec.network` field.

If you don't specify a network name, then Agent Platform runs your serverless training without a peering connection, and without access to private IPs in your project.

### Example: Creating a `CustomJob` with the gcloud CLI

The following example shows how to specify a network when you use the gcloud CLI to run a `CustomJob` that uses a prebuilt container. If you are perform serverless training in a different way, add the `network` field [as described for the type of serverless training job you're using](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip#perform-serverless-training) .

1.  Create a `config.yaml` file to specify the network. If you're using Shared VPC, use your VPC host project number.
    
    Make sure the network name is formatted correctly:
    
        PROJECT_NUMBER=$(gcloud projects describe $PROJECT_ID --format="value(projectNumber)")
        
        cat <<EOF > config.yaml
        network: projects/PROJECT_NUMBER/global/networks/NETWORK_NAME
        EOF

2.  [Create a training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) to run on Agent Platform.

3.  Create the `CustomJob` , passing in your `config.yaml` file:
    
        gcloud ai custom-jobs create \
          --region=LOCATION \
          --display-name=JOB_NAME \
          --python-package-uris=PYTHON_PACKAGE_URIS \
          --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,executor-image-uri=PYTHON_PACKAGE_EXECUTOR_IMAGE_URI,python-module=PYTHON_MODULE \
          --config=config.yaml

To learn how to replace the placeholders in this command, read [Creating custom training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

### Run jobs on different networks

You can't perform serverless training on a new network while you are still performing serverless training on another network. Before you switch to a different network, you must wait for all submitted `CustomJob` , `HyperparameterTuningJob` , and custom `TrainingPipeline` resources to finish, or you must cancel them.

## Test training job access

This section explains how to test that a serverless training resource can access private IPs in your network.

1.  Create a Compute Engine instance in your VPC network.
2.  [Check your firewall rules](https://docs.cloud.google.com/vpc/docs/using-firewalls#listing-rules-vm) to make sure that they don't restrict ingress from the Agent Platform network. If so, add a rule to ensure the Agent Platform network can access the IP range you reserved for Agent Platform (and other service producers).
3.  Set up a local server on the VM instance in order to create an endpoint for an Agent Platform `CustomJob` to access.
4.  Create a Python training application to run on Agent Platform. Instead of model training code, create code that accesses the endpoint you set up in the previous step.
5.  Follow the previous example to create a `CustomJob` .

## Common problems

This section lists some common issues for configuring VPC Network Peering with Agent Platform.

  - When you configure Agent Platform to use your network, specify the full network name:
    
    "projects/ YOUR\_PROJECT\_NUMBER /global/networks/ YOUR\_NETWORK\_NAME "

  - Make sure you are not performing serverless training on a network before performing serverless training on a different network.

  - Make sure that you've allocated a sufficient IP range for all service producers your network connects to, including Agent Platform.

For additional troubleshooting information, refer to the [VPC Network Peering troubleshooting guide](https://docs.cloud.google.com/vpc/docs/using-vpc-peering#troubleshooting) .

## What's next

  - Learn more about [VPC Network Peering](https://docs.cloud.google.com/vpc/docs/vpc-peering) .
  - See [reference architectures and best practices](https://docs.cloud.google.com/solutions/best-practices-vpc-design#shared-service) for VPC design.
