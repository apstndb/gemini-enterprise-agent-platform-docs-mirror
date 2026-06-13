---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/troubleshooting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/troubleshooting
title: Troubleshooting machine learning services
description: Troubleshoot and resolve common issues when using Gemini Enterprise Agent Platform machine learning services.
data_source: docs.cloud.google.com
---

This page describes troubleshooting steps that you might find helpful if you run into problems when you use machine learning services on Gemini Enterprise Agent Platform.

To filter this page's content, click a topic:

## Troubleshooting with Cloud Assist Investigations

When connecting Agent Platform with other Google Cloud products, you may find [Cloud Assist Investigations](https://docs.cloud.google.com/cloud-assist/investigations) to be helpful in troubleshooting complex integration issues.

  - Enable and configure the Cloud Assist Investigations API.
  - Determine which of the products that your workload name depends on appears on the list of [supported products](https://docs.cloud.google.com/cloud-assist/investigations#products)
  - Create an investigation and describe the symptoms in detail. Be sure to mention any resources that the pipeline relies on.
  - As you type, you will notice the dialog suggesting resources to add to the investigation. Review this list and add any relevant resources before running the investigation.

## AutoML models

This section describes troubleshooting steps that you might find helpful if you run into problems with AutoML.

### Missing labels in the test, validation, or training set

**Issue**

When you use the default data split when training an AutoML classification model, Agent Platform might assign too few instances of a class to a particular set (test, validation, or training), which causes an error during training. This issue more frequently occurs when you have imbalanced classes or a small amount of training data.

**Solution**

To resolve this issue, add more training data, manually split your data to assign enough classes to every set, or remove the less frequently occurring labels from your dataset. For more information, see [About data splits for AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use) .

## Vertex AI Studio

When working with Vertex AI Studio you might receive the following errors:

### Attempting to tune a model returns `Internal error encountered`

**Issue**

You encounter an `Internal error encountered` error when trying to tune a model.

**Solution**

Run the following curl command to create an empty Gemini Enterprise Agent Platform dataset. Ensure that you configure your project ID in the command.

    PROJECT_ID=PROJECT_ID
    
    curl \
    -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://europe-west4-aiplatform.googleapis.com/ui/projects/$PROJECT_ID/locations/europe-west4/datasets \
    -d '{
        "display_name": "test-name1",
        "metadata_schema_uri": "gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml",
        "saved_queries": [{"display_name": "saved_query_name", "problem_type": "IMAGE_CLASSIFICATION_MULTI_LABEL"}]
    }'

After the command completes, wait five minutes and try model tuning again.

### Error code: 429

**Issue**

You encounter the following error:

    429: The online prediction request quota is exceeded for
    PUBLIC_BASE_MODEL_NAME.

**Solution**

Try again later with backoff. If you still experience errors, contact Gemini Enterprise Agent Platform support.

### Error code: 410

**Issue**

You encounter the following error:

    410: The request is missing the required authentication credential. Expected
    OAuth 2.0 access token, login cookie, or other valid authentication credential.

**Solution**

See the [Authentication overview](https://developers.google.com/identity/gsi/web/guides/overview) to learn more.

### Error code: 403

**Issue**

You encounter the following error:

    403: Permission denied.

**Solution**

Ensure that the account accessing the API has the right permissions.

## Agent Platform Pipelines

This section describes troubleshooting steps that you might find helpful if you run into problems with Agent Platform Pipelines.

### You don't have permission to act as service account

**Issue**

When you run your Gemini Enterprise Agent Platform Pipelines workflow, you might encounter the following error message:

    You do not have permission to act as service account: SERVICE_ACCOUNT. (or it may not exist).

**Solution**

This error means that the service account running your workflow doesn't have access to the resources that it needs to use.

To resolve this issue, grant the user the `iam.serviceAccounts.actAs` permission on the service account.

### Error: Python package hashes are mismatched in Gemini Enterprise Agent Platform Pipelines component

**Issue**

When you run your Gemini Enterprise Agent Platform Pipelines workflow, you might encounter the following error:

`ERROR: THESE PACKAGES DO NOT MATCH THE HASHES FROM THE REQUIREMENTS FILE. If you have updated the package versions, please update the hashes. Otherwise, examine the package contents carefully; someone may have tampered with them.`

This is caused by version conflicts between the Python libraries in the base image for the Gemini Enterprise Agent Platform Pipelines component and those that the pipeline tries to install.

**Solution**

Build any dependencies listed along with this message into the image used by the Gemini Enterprise Agent Platform Pipelines component.

### Error `Internal error happened`

**Issue**

If your pipeline fails with an `Internal error happened` message, check Logs Explorer and search for the pipeline's name. You might see an error like the following:

```java
java.lang.IllegalStateException: Failed to validate vpc
network projects/PROJECT_ID/global/networks/VPC_NETWORK.

APPLICATION_ERROR;google.cloud.servicenetworking.v1/ServicePeeringManagerV1.GetConsumerConfig;Reserved
range: 'RANGE_NAME' not found for consumer project:
'PROJECT_ID' network: 'VPC_NETWORK'.
com.google.api.tenant.error.TenantManagerException: Reserved range:
'RANGE_NAME' not found for consumer project
```

This means that VPC peering for Agent Platform includes an IP range that has been deleted.

**Solution**

To resolve this issue, update VPC peering using the [update command](https://docs.cloud.google.com/sdk/gcloud/reference/services/vpc-peerings/update) and include valid IP ranges.

### Invalid OAuth scope or ID token audience provided

**Issue**

When you run your Gemini Enterprise Agent Platform Pipelines workflow, you encounter the following error message:

    google.auth.exceptions.RefreshError: ('invalid_scope: Invalid OAuth scope
    or ID token audience provided.', {'error': 'invalid_scope',
    'error_description': 'Invalid OAuth scope or ID token audience provided.'})

**Solution**

This means that you haven't provided credentials in one of the pipeline's components or didn't use `ai_platform.init()` to set credentials.

To resolve this issue, set the credentials for the relevant pipeline component or set the environment credentials and use `ai_platform.init()` at the beginning of your code.

    os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = PATH_TO_JSON_KEY

### Agent Platform Pipelines components require more disk space than 100 GB

**Issue**

The default disk space allocated to Agent Platform Pipelines components is 100 GB and increasing the disk space isn't supported. See the [Public Issue Tracker](https://issuetracker.google.com/issues/232875719) for this issue.

**Solution**

For a component to use more than 100 GB disk space, convert the component to a custom job by using [components method](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-0.2.0/google_cloud_pipeline_components.experimental.custom_job.html#module-google_cloud_pipeline_components.experimental.custom_job.utils) . With this operator, you can assign the machine type and disk size that the component uses.

For an example of how to use this operator, see [Agent Platform Pipelines: Custom training with prebuilt Google Cloud Pipeline Components](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb) , in the **Convert the component to an Agent Platform Custom Job** section.

## Agent Platform networking issues

This section describes troubleshooting steps that you might find helpful if you run into problems with networking for Agent Platform.

> **Note:** Enabling VPC Service Controls for Peerings will change the forwarding behavior in the Agent Platform producer project that peered to your VPC. Be sure to read the discussion on [Service perimeter creation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vpc-service-controls#service_perimeter_creation) for Agent Platform and confirm the configuration by running following command;

    gcloud services vpc-peerings get-vpc-service-controls \
      --network YOUR_NETWORK

### Workloads can't access endpoints in your VPC network when using privately-used public IP ranges for Gemini Enterprise Agent Platform

**Issue**

Privately used public IP ranges are not imported by default.

**Solution**

To use privately used public IP ranges, you must [enable import of privately used public IP ranges](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#import-export-pub)

### `com.google.api.tenant.error.TenantManagerException: Reserved range: nnn not found for consumer project`

**Issue**

You receive errors of the form `com.google.api.tenant.error.TenantManagerException: Reserved range: nnn not found for consumer project` when running workloads or deploying endpoints.

This occurs when you change the [private services access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access) reservations for your workloads. Any deleted ranges may not have been registered with the Agent Platform API.

**Solution**

Run [`gcloud services vpc-peerings update`](https://docs.cloud.google.com/sdk/gcloud/reference/services/vpc-peerings/update) for `servicenetworking` after updating private services access allocations.

### Pipeline or job can't access endpoints within your peered VPC network

**Issue**

Your Gemini Enterprise Agent Platform pipeline times out when it attempts to connect to resources in your VPC network.

**Solution**

Try the following to resolve the problem:

  - Ensure that you have completed all of the steps in [Set up VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) .

  - Review the configuration of your peered VPC network. Ensure that your network imports routes from the correct service networking range while your job is running.

  - Ensure that you have a firewall rule that allows connections from this range to the target in your network.

  - If the peering connection does not import any routes while your job is running, this means the service networking configuration is not being used. This is likely because you completed the peering configuration with a network other than the default network. If this is the case, ensure that you specify your network when you launch a job. Use the fully qualified network name in the following format: `projects/$PROJECT_ID/global/networks/$NETWORK_NAME` .
    
    For more information, see the [Routes overview](https://docs.cloud.google.com/vpc/docs/routes) .

### Pipeline or job can't access to reach endpoints in other networks beyond your network

**Issue**

Your Pipeline or job is unable to access endpoints in networks beyond your network.

**Solution**

By default, your peering configuration only exports routes to the local subnets in your VPC.

Additionally, [transitive peering](https://docs.cloud.google.com/vpc/docs/vpc-peering#specifications) is not supported and only directly peered networks can communicate.

  - To allow Gemini Enterprise Agent Platform to connect through your network and reach endpoints in other networks, you must export your network routes to your peering connection. Edit the configuration of your peered VPC network and enable [`Export custom routes`](https://docs.cloud.google.com/vpc/docs/using-vpc-peering#creating_a_peering_configuration) .

Because transitive peering is not supported, the Gemini Enterprise Agent Platform does not learn routes to other peered networks and services, even with `Export Custom Routes` enabled. For information about workarounds, see [Extending network reachability of Agent Platform Pipelines](https://cloud.google.com/blog/products/ai-machine-learning/extending-network-reachability-of-vertex-pipelines) .

### `No route to host` without route conflicts evident in Google Cloud console

**Issue**

The only routes you can see in the Google Cloud console are those known to your own VPC as well as the ranges reserved when you complete the [VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vpc-peering) configuration.

On rare occasions, a Gemini Enterprise Agent Platform job might throw a `no route to host` complaint when trying to reach an IP address that your VPC is exporting to the Gemini Enterprise Agent Platform network.

This might be because Gemini Enterprise Agent Platform jobs run within a networking namespace in a managed GKE cluster whose IP range conflicts with the target IP. See [GKE networking fundamentals](https://github.com/GoogleCloudPlatform/community/blob/master/archived/gke-networking-fundamentals/index.md) for further discussion.

> **Note:** The source IP addresses for outbound connections from these workloads are still translated to the peering range that you configured.

Under these conditions, the workload tries to connect to the IP within its own networking namespace and throws the error if it's unable to reach it.

**Solution**

Craft your workload to return its local namespace IP addresses and confirm that this doesn't conflict with any routes you are exporting over the peering connection. If there is a conflict, pass a list of [`reservedIpRanges[]`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec) in the job parameters that don't overlap with any ranges in your VPC network. The job uses these ranges for the workload's internal IP addresses.

### `RANGES_EXHAUSTED` , `RANGES_NOT_RESERVED`

**Issue**

Errors of the form `RANGES_EXHAUSTED` and `RANGES_NOT_RESERVED` and `RANGES_DELETED_LATER` indicate a problem with the underlying [VPC network peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vpc-peering) configuration. These are networking errors and not errors from the Agent Platform service itself.

> **Note:** If you have created several ranges in the same VPC, these IP Ranges should be contiguous. Gemini Enterprise Agent Platform won't consume IP addresses from non-contiguous ranges within the same region.

**Solution**

When faced with a `RANGES_EXHAUSTED` error, you should first consider whether this complaint is valid.

  - Refer to the [Subnet recommendations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/private-services-access#subnet-recommendations) table to ensure that the IP reservation for Private Services Access is wide enough accommodate your workload.

  - Visit [Network Analyzer](https://docs.cloud.google.com/network-intelligence-center/docs/network-analyzer/insight-groups-types) in cloud console and look for insights of the form "Summary of IP address allocation" in the VPC network. If these indicate that the allocation is at or near 100%, you can can take one of the following steps:
    
      - [Add a new range](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#modify-ip-range) to the reservation or extend the existing one. Recall that all ranges must be contiguous.
      - If you have non-contiguous IP ranges that are allocated but *not* being consumed, launch new Gemini Enterprise Agent Platform workloads in a different region.

  - Also consider the [maximum number of parallel jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/training/using-private-ip#reserving-ip-ranges) that can be run with an reservation of a given size.

For more information, see [Service Infrastructure Validation Errors](https://docs.cloud.google.com/service-infrastructure/docs/service-networking/reference/rest/v1/services/validate#validationerror)

If the error persists, [contact support](https://docs.cloud.google.com/vertex-ai/docs/support/getting-support) .

### `Router status is temporarily unavailable`

**Issue**

When you launch Agent Platform Pipelines, you receive an error message similar to the following:

    Router status is temporarily unavailable. Please try again later

**Solution**

The error message indicates that this is a temporary condition. Try launching Agent Platform Pipelines again.

If the error persists, [contact support](https://docs.cloud.google.com/vertex-ai/docs/support/getting-support) .

### Workloads are unable to resolve the hostnames for DNS domains in your VPC

**Issue**

Gemini Enterprise Agent Platform workloads fail to connect to hostnames configured in your VPC. You have already confirmed that these hostnames are accessible from clients within your VPC.

This is because the workloads run in a Google-managed project. The VPC in this managed environment must be peered to yours in order to consume any of your networking resources. In addition to this, any DNS zones that these workloads need access to must specifically be shared with the Google-managed VPC.

**Solution**

  - Ensure that you have [set up VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) for Gemini Enterprise Agent Platform in your VPC network.

  - Complete the steps to share your private DNS zone with the Gemini Enterprise Agent Platform producer network. Note that the procedure for this depends on your use case:
    
      - [Peer DNS with Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#dns-peering)
      - [Peer DNS with Private Service Connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect#create-pipeline-run-2)

  - Ensure that your Gemini Enterprise Agent Platform workloads are launched with the `--network` flag specifying your VPC network. This allows them to run in the Google-managed network and access the DNS zones that you have shared.

  - Enable [DNS logging](https://docs.cloud.google.com/dns/docs/monitoring) in your DNS server policy, reproduce the issue, and then run another test. If the workload's DNS response is successful, a Cloud Logging filter for `resource.type="dns_query"` will show entries of this form;
    
        "resource": {
          "type": "dns_query",
          "labels": {
            "location": REGION,
            "project_id": PROJECT_ID,
            "source_type": "peering-zone",
            "target_name": "QUERY_TARGET,
            "target_type": "forwarding-zone"
          }
        }

  - Confirm that a DNS query from an instance in the *same* subnet can resolve hostnames by using your DNS server.

  - If the DNS server is not in Google Cloud, ensure that remote firewall rules allow connections from [`35.199.192.0/19`](https://docs.cloud.google.com/dns/docs/zones/forwarding-zones#firewall-rules) .

  - Run a [connectivity test](https://docs.cloud.google.com/network-intelligence-center/docs/connectivity-tests/how-to/running-connectivity-tests) from the test instance to and port `53/UDP` on the DNS server's IP address. If, for example, the path leads to a [forwarding rule](https://docs.cloud.google.com/load-balancing/docs/forwarding-rule-concepts) , ensure the following:
    
      - If it is a regional forwarding rule, it must be in the same region as the client.
      - It accepts connections on `53/UDP` and forwards those to the correct DNS server.

### Connectivity issues caused by client side behaviors

If you experience connectivity issues when attempting to use Google Cloud APIs, the root cause could be on the client side. This section suggests client-side solutions that might improve your experience.

#### Connection resets and dropped packets

**Issue**

When you attempt to use Google Cloud APIs, you experience connection resets and dropped packets.

**Solution**

To help resolve this issue, consider the following:

  - For high volume traffic of transactions that have low-latency requirements, consider whether any known issues with the line cards of on-premises clients might cause reset TCP connections or dropped packets.
  - Consider whether any client-side services in the request path use [iptables](https://en.wikipedia.org/wiki/Iptable) . These can include kubernetes clusters or some stateful firewalls and NAT devices. By default, the Linux connection tracking (conntrack) subsystem will strictly follow the TCP protocol specifications and, for example, drop out-of-sequence TCP packets. To turn off this behavior, turn on the Linux kernel parameter [`net.netfilter.nf_conntrack_tcp_be_liberal`](https://docs.kernel.org/networking/nf_conntrack-sysctl.html) or its equivalent.

#### Incomplete connections

**Issue**

When you attempt to use Google Cloud APIs, you experience incomplete connections.

**Solution**

To help resolve this issue, consider the following:

  - When the forwarding path has multiple routes back to the client, ensure that you understand the concept of [Reverse Path Forwarding](https://en.wikipedia.org/wiki/Reverse-path_forwarding) . Turn off this behavior if you suspect it is blocking connections.
  - For load-balanced connections, consider whether your inbound firewall rules allow response packets to both load-balancers.

#### Other non-API connection issues

To help resolve non-API connection issues, consider the following:

  - If any proxies are in the request path, consider whether they can introduce any of the issues you are experiencing. Review the documentation and be sure to troubleshoot the proxy when faced with issues like unexplained latency, dropped connections, DNS overrides, cross-origin blocks, and other similar issues.
  - Especially when handling [`429` responses](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#429) from Google Cloud APIs, client-side logic that immediately retries the connection can make the issue worse. Ensure that you understand and implement [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) when implementing retries.

## Agent Platform inference

This section describes troubleshooting steps that you might find helpful if you run into problems with Agent Platform inference.

### Exceeded batch quota error

**Issue**

You get an error such as the following when running batch inference jobs.

    Quota exhausted. Please reach out to ai-platform-unified-feedback@google.com for
    batch prediction quota increase.

A Gemini Enterprise Agent Platform batch prediction job consumes the quota from the batch prediction tenant project. For further information about requesting a quota increase, see [Gemini Enterprise Agent Platform quotas and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#quota_increases) .

### Exceeded retries error

**Issue**

You get an error such as the following when running batch inference jobs, indicating that the machine running the custom model might not be able to complete the inferences within the time limit.

    ('Post request fails. Cannot get predictions. Error: Exceeded retries: Non-OK
    result 504 (upstream request timeout) from server, retry=3, elapsed=600.04s.', 16)

This can happen when the Agent Platform inference service registers itself with the [Google Front End service](https://docs.cloud.google.com/docs/security/infrastructure/design#google-frontend-service) , which proxies connections from the client to the Agent Platform Inference API.

The Google Front End service times out the connection and returns a 500 HTTP response code to the client if it doesn't receive a response from the API within 10 minutes.

**Solution**

To resolve this issue, you try either of the following;

  - Increase the compute nodes, or change the machine type.
  - Craft your inference container to send periodic 102 HTTP response codes. This resets the 10 minute timer on the Google Front End service.

### Project already linked to VPC

**Issue**

When deploying an endpoint, you might see an error message such as the following, which indicates that your Agent Platform endpoints have previously used a Virtual Private Cloud network and the resources were not appropriately cleaned.

    Currently only one VPC network per user project is supported. Your project is
    already linked to
    "projects/YOUR_SHARED_VPC_HOST_PROJECT/global/networks/YOUR_SHARED_VPC_NETWORK".
    To change the VPC network, please undeploy all Agent Platform deployment
    resources, delete all endpoint resources, and then retry creating resources in
    30 mins.

**Solution**

To resolve this issue, try running this command in Cloud Shell.

    gcloud services vpc-peerings delete \
        --service=servicenetworking.googleapis.com \
        --network=YOUR_SHARED_VPC_NETWORK \
        --project=YOUR_SHARED_VPC_HOST_PROJECT

This manually disconnects your old VPC network from the Service Networking VPC.

### Unexpected deployment failure or endpoint deletion

**Issue**

A model deployment unexpectedly fails, an endpoint is found to be deleted, or a previously deployed model has become undeployed.

Your billing account may be invalid. If it remains invalid for a long time, some resources might be removed from the projects associated with your account. For example, your endpoints and models might be deleted. Removed resources aren't recoverable.

**Solution**

To resolve this issue, you can try the following:

  - [Verify the billing status of your projects](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled) .
  - [Contact Cloud Billing Support](https://docs.cloud.google.com/support/billing) to request help with billing questions.

For more information, see [Billing questions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/support/billing-questions) .

## Agent Platform custom service account issues

This section describes troubleshooting steps that you might find helpful if you run into problems with service accounts.

### Model deployment fails with service account `serviceAccountAdmin` error

**Issue**

Your model deployment fails with an error such as the following:

`Failed to deploy model MODEL_NAME to endpoint ENDPOINT_NAME due to the error: Failed to add IAM policy binding. Please grant SERVICE_ACC_NAME @gcp-sa-aiplatform.iam.gserviceaccount.com the iam.serviceAccountAdmin role on service account vertex-prediction-role@ PROJECT_INFO .iam.gserviceaccount.com`

**Solution**

This error means that your custom service account might not have been configured correctly. To create a custom service account with the correct IAM permissions, see [Use a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#configure) .

### Unable to fetch identity token when using custom service account

**Issue**

When using a custom service account, training jobs that run on a single replica are not able to reach the Compute Engine metadata service required to retrieve a token.

You will see an error similar to:

    Failed to refresh jwt, retry number 0: ("Failed to retrieve http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/identity?audience=...&format=full
    from the Google Compute Engine Metadata service. Status: 404 Response:
    \nb'Not Found\n'", <google.auth.transport.requests._Response object at
    0x7fb19f058c50>)

**Solution**

To fetch the identity token with a custom service account, you must use [iamcredentials.googleapis.com](https://docs.cloud.google.com/iam/docs/reference/credentials/rest/v1/projects.serviceAccounts/generateIdToken) .

## Custom-trained models

This section describes troubleshooting steps that you might find helpful if you run into problems with custom-trained models.

### Custom training issues

The following issues can occur during custom training. The issues apply to [`CustomJob` and `HyperparameterTuningJob` resources, including those created by `TrainingPipeline` resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods) .

#### Error code: 400

**Issue**

You encounter the following error:

    400 Machine type MACHINE_TYPE is not supported.

You may see this error message if the selected machine type isn't supported for Gemini Enterprise Agent Platform training, or if a specific resource isn't available in the selected region.

**Solution**

Use only [available machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) in the appropriate [regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

#### Replica exited with a non-zero status code

**Issue**

During [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) , an error from any worker causes training to fail.

**Solution**

To check the stack trace for the worker, [view your custom training logs in the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#monitor) .

View the other troubleshooting topics to fix common errors and then create a new `CustomJob` , `HyperparameterTuningJob` , or `TrainingPipeline` resource. In many cases, the error codes are caused by problems in your training code, not by the Agent Platform service. To determine if this is the case, you can run your training code on your local machine or on [Compute Engine](https://docs.cloud.google.com/compute/docs) .

#### Replica ran out of memory

**Issue**

An error can occur if a training virtual machine (VM) instance runs out of memory during training.

**Solution**

You can view the memory usage of your training VMs in the Google Cloud console.

Even when you get this error, you might not see 100% memory usage on the VM, because services other than your training application that run on the VM also consume resources. For [machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_machine_types) that have less memory, other services might consume a relatively large percentage of memory. For example, on an `n1-standard-4` VM, services can consume up to 40% of the memory.

You can optimize the memory consumption of your training application, or you can choose a larger machine type with more memory.

#### Insufficient resources in a region

**Issue**

You encounter a stockout issue in a region.

**Solution**

Agent Platform trains your models by using Compute Engine resources. Agent Platform can't schedule your workload if Compute Engine is at capacity for a certain CPU or GPU in a region. This issue is unrelated to your project quota.

When reaching Compute Engine capacity, Agent Platform automatically retries your `CustomJob` or `HyperparameterTuningJob` up to three times. The job fails if all retries fail.

A stockout usually occurs when you are using GPUs. If you encounter this error when using GPUs, try switching to a different [GPU type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) . If you can use another region, try training in a different region.

#### Permission error when accessing another Google Cloud service

If you encounter a permission error when accessing another Google Cloud service from your training code (for example: `google.api_core.exceptions.PermissionDenied: 403` ), then you might have one of the following issues:

  - **Issue**
    
    The service agent or service account running your code (either the Gemini Enterprise Agent Platform Custom Code Service Agent for your project or a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) ) doesn't have the required permission.
    
    **Solution**
    
    Learn how to [give the Gemini Enterprise Agent Platform Custom Code Service Agent permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#grant_service_agents_access_to_other_resources) or [configure a custom service account with the necessary permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account#configure) .

  - **Issue**
    
    The service agent or service account running your code does have the required permission, but your code is trying to access a resource in the wrong project. This is especially likely to be the problem if the error message references a project ID ending with `-tp` .
    
    **Solution**
    
    Due to the way Agent Platform runs your training code, this problem can occur inadvertently if you don't explicitly specify a project ID or project number in your code.
    
    Learn how to fix this problem by [specifying a project ID or project number](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#other-services) .

  - **Issue**
    
    Your Vertex AI Training job runs successfully with local data, but not with data from Cloud Storage.
    
    **Solution**
    
    Add `storage.buckets.create` permission to your Gemini Enterprise Agent Platform Custom Code Service Agent role for the project.
    
    Learn how to fix this problem by [adding specific roles to Agent Platform's service agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#grant_service_agents_access_to_other_resources) .

#### Performance issues when using Cloud Storage FUSE

**Issue**

[Cloud Storage FUSE](https://docs.cloud.google.com/storage/docs/gcs-fuse) jobs are running slowly.

**Solution**

See "Performance optimization guidelines" in [Use Cloud Storage as a mounted file system](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/cloud-storage-file-system#performance_optimization_guidelines) .

#### `pip install` fails when using KFP with VPC Service Controls

**Issue**

You see the following error:

    ModuleNotFoundError: No module named MODULE_NAME. WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(&lt;pip._vendor.urllib3.connection.HTTPSConnection object at 0x7f70250bac10&gt;, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/nltk/

**Solution**

The VPC Service Controls service perimeter blocks access from Agent Platform to third-party APIs and services on the internet. To install the packages, use [packageUris](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#pythonpackagespec) to install the dependencies from Cloud Storage buckets. For a general discussion of using this technique, see "Use custom containers" in [VPC Service Controls with Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls#custom-containers) .

#### Internal error

**Issue**

Your training failed because of a system error.

**Solution**

The issue might be transient; try to resubmit the `CustomJob` , `HyperparameterTuningJob` , or `TrainingPipeline` . If the error persists, [contact support](https://docs.cloud.google.com/vertex-ai/docs/support/getting-support) .

#### Error code 500 when using a custom container image

**Issue**

You see a 500 error in your logs.

**Solution**

This type of error is likely to be a problem with your custom container image and not an Agent Platform error.

#### Service account can't access Cloud Storage bucket when deploying to an endpoint

**Issue**

When you try to deploy a model to an endpoint and your service account doesn't have [`storage.objects.list`](https://docs.cloud.google.com/storage/docs/access-control/iam-permissions#object_permissions) access to the related Cloud Storage bucket, you might see the following error:

    custom-online-prediction@TENANT_PROJECT_ID.iam.gserviceaccount.com
    does not have storage.objects.list access to the Cloud Storage bucket.

By default, the custom container that deploys your model uses a service account that doesn't have access to your Cloud Storage bucket.

**Solution**

To resolve this, try one of the following:

  - Copy the file that you are trying to access from the container into [model artifacts](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#artifacts) when uploading the model. Gemini Enterprise Agent Platform will copy it to a location the default service account has access to, similar to all the other model artifacts.

  - Copy the file into the container as part of the container build process.

  - Specify a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .

## Agent Platform Neural Architecture Search

### Known issues

  - After cancelling the NAS job, the main job (the parent) stops, but some of the child trials keep showing a **Running** state. Ignore the child trial state that shows **Running** in this case. The trials have stopped, but the UI continues to show the **Running** state. As long as the main job has stopped, you won't be charged extra.

  - After reporting rewards in the trainer, wait (sleep) for 10 minutes before the trial jobs exit.

  - When using Cloud Shell to run `TensorBoard` , the generated output link might not work. In this case, write down the port number, use the **Web Preview** tool, and select the correct port number to display the plots.
    
    Accessing the `Web Preview` tool:
    
    ![A feature attribution chart for one predicted bike ride duration.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/images/web_preview.png)

  - If you see error messages like the following in the trainer logs:
    
        gcsfuse errors: fuse: writeMessage: no such file or directory [16 0 0 0 218 255 255 255 242 25 111 1 0 0 0 0]
    
    use a machine with more RAM, because an OOM condition is causing this error.

  - If your custom trainer isn't able to find the job directory `job-dir` FLAG, import `job_dir` with an underscore rather than a hyphen. A note in tutorial-1 explains this.

  - *NaN error during training* There might be NaN errors in the training job like `NaN : Tensor had NaN values` . The learning rate might be too big for the suggested architecture. For more information, see [Out-of-memory (OOM) and learning rate related errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/proxy-task-design#oom_error) .

  - *OOM error during training* There might be OOM (out-of-memory) errors in the training job. The batch size might be too large for the accelerator memory. For more information, see [Out-of-memory (OOM) and learning rate related errors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/proxy-task-design#oom_error) .

  - *Proxy-task model selection controller job dies* In the rare case that the proxy-task model selection controller job dies, you can resume the job by following [these steps](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/proxy-task-design#resume_model_selection) .

  - *Proxy-task search controller job dies* In the rare case that the proxy-task search controller job dies, you can resume the job by following [these steps](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/proxy-task-design#resume_proxy_task_search) .

  - *Service account does not have permission to access Artifact Registry or bucket.* If you get an error such as `Agent Platform Service Agent service-123456789@gcp-sa-aiplatform-cc.iam.gserviceaccount.com does not have permission to access Artifact Registry repository projects/my-project/locations/my-region/repositories/nas` or a similar error for bucket access, give this service account a storage editor role in your project.

## Agent Platform Neural Architecture Search Feature Store

This section describes troubleshooting steps that you might find helpful if you run into problems with Agent Platform Neural Architecture Search Feature Store.

### `Resource not found` error when sending a streaming ingestion or online serving request

**Issue**

After you set up a featurestore, entity type, or feature resources, there's a delay before those resources are propagated to the `FeaturestoreOnlineServingService` service. Sometimes this delayed propagation might cause a `resource not found` error when you submit a streaming ingestion or online serving request immediately after you create a resource.

**Solution**

If you receive this error, wait a few minutes and then try your request again.

### Batch ingestion succeeded for newly created features but online serving request returns empty values

**Issue**

For newly created features only, there is a delay before those features are propagated to the `FeaturestoreOnlineServingService` service. The features and values exist but take time to propagate. This might result in your online serving request returning empty values.

**Solution**

If you do see this inconsistency, wait a few minutes and then try your online serving request again.

### CPU utilization is high for an online serving node

**Issue**

Your CPU utilization for an online serving node is high.

**Solution**

To mitigate this issue, you can either increase the number of online serving nodes by manually increasing the node count or by enabling autoscaling. Note that even if auto scaling is enabled, Vertex AI Feature Store needs time to rebalance the data when nodes are added or removed. For information about how to view feature value distribution metrics over time, see [View feature value metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/monitoring#view_feature_value_distributions) .

### CPU utilization is high for the hottest online serving node

**Issue**

If the CPU utilization is high for the hottest node, you can either increase the number of serving nodes or change the entity access pattern to pseudo-random.

**Solution**

Setting the entity access pattern to pseudo-random mitigates high CPU utilization resulting from frequently accessing entities that are located near to each other in the featurestore. If neither solution is effective, implement a client-side cache to avoid accessing the same entities repeatedly.

### Online serving latency is high when QPS is low

**Issue**

The period of inactivity or low activity at low QPS might result in some server-side caches expiring. This can result in high latency when traffic to online serving nodes resumes at regular or higher QPS.

**Solution**

To mitigate this issue, you need to keep the connection active by sending artificial traffic of at least 5 QPS to the featurestore.

### Batch ingestion job fails after six hours

**Issue**

The batch ingestion job can fail because the read session expires after six hours.

**Solution**

To avoid the timeout, increase the number of workers to complete the ingestion job within the six hour time limit.

### `Resource exceeded` error when exporting feature values

**Issue**

Exporting a high volume of data can fail with a resource exceeded error if the export job exceeds the internal quota.

**Solution**

To avoid this error, you can configure the time range parameters, `start_time` and `end_time` , to process smaller amounts of data at a time. For information about full export, see [Full export](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/export-features#full_export_2) .

## Agent Platform Neural Architecture Search Vizier

When using Agent Platform Neural Architecture Search Vizier, you might get the following issues.

#### Internal error

**Issue**

The internal error occurs when there is a system error.

**Solution**

It might be transient. Try to resend the request, and if the error persists, [contact support](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/support/getting-support) .

### Permissions errors when using service account roles with Agent Platform Neural Architecture Search

**Issue**

You get general permissions errors when you use service account roles with Agent Platform Neural Architecture Search.

These errors can appear in Cloud Logging in either the product component logs or audit logs. They may also appear in any combination of the affected projects.

These issues can be caused by one or both of the following:

  - Use of the `Service Account Token Creator` role when the `Service Account User` role should have been used, or the other way around. These roles grant different permissions on a service account and aren't interchangeable. To learn about the differences between the `Service Account Token Creator` and `Service Account User` roles, see [Service account roles](https://docs.cloud.google.com/iam/docs/service-account-permissions#roles) .

  - You've granted a service account permissions across multiple projects, which isn't permitted by default.

**Solution**

To resolve the issue, try one or more of the following:

  - Determine whether the `Service Account Token Creator` or `Service Account User` role is needed. To learn more, read the IAM documentation for the Agent Platform Neural Architecture Search services you are using, as well as any other product integrations that you are using.

  - If you have granted a service account permissions across multiple projects, enable service accounts to be attached across projects by ensuring that [`iam.disableCrossProjectServiceAccountUsage`](https://docs.cloud.google.com/iam/docs/attach-service-accounts#enabling-cross-project) . isn't enforced. To ensure that `iam.disableCrossProjectServiceAccountUsage` isn't enforced, run the following command:
    
        gcloud resource-manager org-policies disable-enforce \
          iam.disableCrossProjectServiceAccountUsage \
          --project=PROJECT_ID
