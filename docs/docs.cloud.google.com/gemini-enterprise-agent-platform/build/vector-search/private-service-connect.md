---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect
title: Set up Vector Search with Private Service Connect
description: Learn how to set up Vector Search with Private Service Connect.
data_source: docs.cloud.google.com
---

Private Service Connect allows private consumption of services across VPC networks that belong to different groups, teams, projects, and organizations. You can publish and consume services using IP addresses that you define and that are internal to your VPC network, and for Vector Search endpoints to perform vector similarity searches.

Enabling Private Service Connect on a Vector Search endpoint is suited for use cases that:

1.  Require low latency and a secure connection to Vector Search serving backends.
2.  Have limited IP space for exclusive VPC peering reservation.
3.  Need to access the serving backends from multiple user VPC networks.

To learn more about setting up Private Service Connect, go to [Private Service Connect Overview](https://docs.cloud.google.com/vpc/docs/private-service-connect) in the Virtual Private Cloud (VPC) documentation.

## Create the index endpoint

You must enable Private Service Connect when you create your endpoint. This procedure is similar to creating other endpoints in Gemini Enterprise Agent Platform.

### REST

  - PROJECT : The ID of the service project where you are creating Gemini Enterprise Agent Platform resources.

  - REGION : The network region.

  - DISPLAY\_NAME : A display name to give the endpoint. This name is used to create an ID for the endpoint and cannot be updated later.

  - VPC\_PROJECTS : For Shared VPC setup, this is a comma-separated list of VPC host projects. For standalone VPC setup, this is the same as PROJECT .

<!-- end list -->

    PROJECT=PROJECT_ID
    VPC_PROJECT=VPC_PROJECT_ID
    REGION=us-central1
    VERTEX_ENDPOINT=REGION-aiplatform.googleapis.com
    curl -H "Content-Type: application/json" \
      -H "Authorization: Bearer `gcloud auth print-access-token`" \
      https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/REGION/indexEndpoints \
      -d '{
         "displayName": "DISPLAY_NAME",
         "privateServiceConnectConfig": {
           "enablePrivateServiceConnect": true,
           "projectAllowlist": [ "VPC_PROJECT_1", "VPC_PROJECT_2", "VPC_PROJECT_N"]
         }
       }

### Console

To create your endpoint:

1.  Click the following button to go to Vector Search in the Google Cloud console. A list of your active indexes appears.

2.  Select the **Index endpoints** tab. Your index endpoints appear.

3.  Click add\_box **Create new endpoint** . The **Create a new index endpoint** panel opens.

4.  In **Display name** , enter a display name for the index endpoint. This name is used to create an ID for the endpoint and cannot be updated later.

5.  Select a region from the **Region** drop-down.

6.  Under **Access** , click **Private Service Connect (Preview)** .

7.  A text field appears where you can specify which VPC projects to use. Add the IDs or numbers of the VPC projects you want to use.

8.  Click **Create** .

## About index deployment options

> **Note:** If your `DeployedIndex` uses fewer than two replicas per shard, then it is excluded from the [Agent Platform Service Level Agreement](https://cloud.google.com/terms/vector-search/sla) . For your `DeployedIndex` to be covered by the SLA, you must set `minReplicaCount` to at least 2 or greater, and must be adequately provisioned for workload size. To be adequately provisioned we recommend adding additional replicas if CPU/Memory usage consistency operates 60%.

You can deploy your index with automatic or manual service connectivity.

  - [Deploy with Private Service Connect automation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect#automate) : Set up a service connection policy and deploy your indexes. Setting up a service connection policy lets you deploy to a specific network without creating a compute address and forwarding rule each time.
  - [Deploy with manual connection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect#manual-connect) : Deploy your index and manually create a compute address and forwarding rule. You might choose this option if you need to use multiple IP addresses for the same service attachment URI, although this is not a common use case.

## Deploy with Private Service Connect automation

You can set up a service connection policy so that you don't have to manually create a compute address and forwarding rule after each index deployment.

1.  First, [create a service connection policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect#create-scp) that specifies the network, service class, and region to deploy indexes to. This is a one-time setup. If you've already done this, skip to the next procedure.
2.  [Deploy the index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect#deploy-index-automatic) .

### Limitations

Automation allows only one IP address per project per network. If you need to use multiple IP addresses, see [Manually deploy the index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/private-service-connect#manual-connect) .

### Create a service connection policy

You must be a network administrator to create a service connection policy for automating index deployment.

To automate index deployment, follow these steps:

1.  Create your service connection policy.
    
      - PROJECT : The service project where you are creating Gemini Enterprise Agent Platform resources.
    
      - VPC\_PROJECT : The project where your client VPC is. For single VPC setup, this is the same as $PROJECT. For Shared VPC setup, this is the VPC host project.
    
      - NETWORK\_NAME : The name of the network to deploy to, in the format ` projects/ /global/networks/  ` .
    
      - REGION : The network region.
    
      - PSC\_SUBNETS : The Private Service Connect subnets to use.
    
    <!-- end list -->
    
        gcloud network-connectivity service-connection-policies create <policy_name> \
        --project=<vpc_project> --network=<network_name> # in the format projects/<project_id>/global/networks/<network_name> \
        --service-class=gcp-vertexai --region=<region> --subnets=<psc subnets>

2.  View your service connection policy.
    
        gcloud network-connectivity service-connection-policies list --project=<vpc_project> -–region=<region>

For more information about service connection policies, go to [Configure service connection policies](https://docs.cloud.google.com/vpc/docs/configure-service-connection-policies) .

### Deploy the index

### REST

  - PROJECT : The service project where you are creating Gemini Enterprise Agent Platform resources.

  - VPC\_PROJECT : The project where your client VPC is. For Shared VPC setup, this is the VPC host project.

  - DISPLAY\_NAME : A display name to give the endpoint. This name is used to create an ID for the endpoint and cannot be updated later.

  - NETWORK\_NAME : The name of the network to deploy to, in the format ` projects/ /global/networks/  ` .

  - REGION : The network region.

  - PSC\_SUBNETS : The Private Service Connect subnet to use.

<!-- end list -->

    PROJECT=PROJECT
    VPC_PROJECTS=VPC_PROJECTS
    REGION=REGION
    curl -X POST -H "Authorization: Bearer $(gcloud auth print-access-token)"
    -H "Content-Type: application/json; charset=utf-8" "https://LOCATIONAL_ENDPOINT.googleapis.com/v1/projects/PROJECT_NUMBER/locations/REGION/indexEndpoints/INDEX_ENDPOINT_ID:deployIndex"
    -d '{
      "deployedIndex": {
        "id": "DEPLOYED_INDEX_ID",
        "index": "projects/PROJECT/locations/us-central1/indexes/INDEX_ID ",
        "displayName": "DISPLAY_NAME",
        "psc_automation_configs": [
          { "project_id": "PROJECT_1", "network": "NETWORK_NAME_1" },
          { "project_id": "PROJECT_2", "network": "NETWORK_NAME_2" },
          { "project_id": "PROJECT_N", "network": "NETWORK_NAME_N" }]
        }
    }'

### Console

To deploy your endpoint:

1.  Click the button following button to go to Vector Search in the Google Cloud console. A list of your active indexes appears.

2.  Click the **Deploy** button for the Private Service Connect-enabled Vector Search endpoint you want to deploy. The **Deploy index** slide-out panel appears.

3.  In **Display name** , enter a display name for the deployed index. This name is used to create the ID and cannot be updated later.

4.  Click **Endpoint** and choose the index endpoint you want to deploy to.

5.  Optionally, click **Machine type** to manually choose the type of machine to deploy the index to. By default, the machine type is automatically selected based on index shard size.

You now need to add Private Service Connect automation configurations. To do so:

1.  In the **PSC automation configs** section, click add\_box **Add new config** .

2.  Enter the name of the VPC project to connect with.

3.  Enter the network name of the VPC project to connect. It must be in the format `projects/` **`<project_number>`** `/global/networks/` **`<network_name>`** .

4.  Optionally, click add\_box **Add new config** and continue adding Private Service Connect automation configurations.

5.  Click **Deploy** to finish.

> **Note:** Deployment can take more than 30 minutes to complete.

### Delete service connection policy

If you need to delete the service connection policy, run the following command:

    gcloud network-connectivity service-connection-policies delete --project=<vpc_project> –-region=<region> <policy_name>

For more information about service connection policies, go to [Configure service connection policies](https://docs.cloud.google.com/vpc/docs/configure-service-connection-policies) .

## Deploy with manual connection

Deploy the index and create a forwarding rule in your VPC project.

### Deploy the index

Now that the index is ready, in this step, you deploy the index to the endpoint you created with Private Service Connect enabled.

### gcloud

This example uses the [`gcloud ai index-endpoints deploy-index` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/index-endpoints/deploy-index) .

Before using any of the command data below, make the following replacements:

  - INDEX\_ENDPOINT\_ID : The ID of the index endpoint.
  - DEPLOYED\_INDEX\_ID : A user specified string to uniquely identify the deployed index. It must start with a letter and contain only letters, numbers or underscores. See [DeployedIndex.id](https://cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.DeployedIndex) for format guidelines.
  - DEPLOYED\_INDEX\_ENDPOINT\_NAME : Display name of the deployed index endpoint.
  - INDEX\_ID : The ID of the index.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai index-endpoints deploy-index INDEX_ENDPOINT_ID \
        --deployed-index-id=DEPLOYED_INDEX_ID \
        --display-name=DEPLOYED_INDEX_ENDPOINT_NAME \
        --index=INDEX_ID \
        --region=LOCATION \
        --project=PROJECT_ID

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai index-endpoints deploy-index INDEX_ENDPOINT_ID `
        --deployed-index-id=DEPLOYED_INDEX_ID `
        --display-name=DEPLOYED_INDEX_ENDPOINT_NAME `
        --index=INDEX_ID `
        --region=LOCATION `
        --project=PROJECT_ID

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai index-endpoints deploy-index INDEX_ENDPOINT_ID ^
        --deployed-index-id=DEPLOYED_INDEX_ID ^
        --display-name=DEPLOYED_INDEX_ENDPOINT_NAME ^
        --index=INDEX_ID ^
        --region=LOCATION ^
        --project=PROJECT_ID

### REST

Before using any of the request data, make the following replacements:

  - INDEX\_ENDPOINT\_ID : The ID of the index endpoint.
  - DEPLOYED\_INDEX\_ID : A user specified string to uniquely identify the deployed index. It must start with a letter and contain only letters, numbers or underscores. See [DeployedIndex.id](https://cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.DeployedIndex) for format guidelines.
  - DEPLOYED\_INDEX\_ENDPOINT\_NAME : Display name of the deployed index endpoint.
  - INDEX\_ID : The ID of the index.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/indexEndpoints/INDEX_ENDPOINT_ID:deployIndex

Request JSON body:

    {
     "deployedIndex": {
       "id": "DEPLOYED_INDEX_ID",
       "index": "projects/PROJECT_ID/locations/LOCATION/indexes/INDEX_ID",
       "displayName": "DEPLOYED_INDEX_ENDPOINT_NAME"
     }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/indexEndpoints/INDEX_ENDPOINT_ID:deployIndex"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/indexEndpoints/INDEX_ENDPOINT_ID:deployIndex" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
     "name": "projects/PROJECT_NUMBER/locations/LOCATION/indexEndpoints/INDEX_ENDPOINT_ID/operations/OPERATION_ID",
     "metadata": {
       "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeployIndexOperationMetadata",
       "genericMetadata": {
         "createTime": "2022-10-19T17:53:16.502088Z",
         "updateTime": "2022-10-19T17:53:16.502088Z"
       },
       "deployedIndexId": "DEPLOYED_INDEX_ID"
     }
    }

### Terraform

The following sample uses the [`vertex_ai_index_endpoint_deployed_index`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_index_endpoint_deployed_index) Terraform resource to create a deployed index endpoint.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

    provider "google" {
      region = "us-central1"
    }
    
    resource "google_vertex_ai_index_endpoint_deployed_index" "default" {
      depends_on        = [google_vertex_ai_index_endpoint.default]
      index_endpoint    = google_vertex_ai_index_endpoint.default.id
      index             = google_vertex_ai_index.default.id
      deployed_index_id = "deployed_index_for_psc"
    }
    
    resource "google_vertex_ai_index_endpoint" "default" {
      display_name = "sample-endpoint"
      description  = "A sample index endpoint with Private Service Connect enabled"
      region       = "us-central1"
      private_service_connect_config {
        enable_private_service_connect = true
        project_allowlist = [
          data.google_project.project.project_id,
        ]
      }
    }
    
    data "google_project" "project" {}
    
    # Cloud Storage bucket name must be unique
    resource "random_id" "default" {
      byte_length = 8
    }
    
    # Create a Cloud Storage bucket
    resource "google_storage_bucket" "bucket" {
      name                        = "vertex-ai-index-bucket-${random_id.default.hex}"
      location                    = "us-central1"
      uniform_bucket_level_access = true
    }
    
    # Create index content
    resource "google_storage_bucket_object" "data" {
      name    = "contents/data.json"
      bucket  = google_storage_bucket.bucket.name
      content = <<EOF
    {"id": "42", "embedding": [0.5, 1.0], "restricts": [{"namespace": "class", "allow": ["cat", "pet"]},{"namespace": "category", "allow": ["feline"]}]}
    {"id": "43", "embedding": [0.6, 1.0], "restricts": [{"namespace": "class", "allow": ["dog", "pet"]},{"namespace": "category", "allow": ["canine"]}]}
    EOF
    }
    
    resource "google_vertex_ai_index" "default" {
      region       = "us-central1"
      display_name = "sample-index-batch-update"
      description  = "A sample index for batch update"
      labels = {
        foo = "bar"
      }
    
      metadata {
        contents_delta_uri = "gs://${google_storage_bucket.bucket.name}/contents"
        config {
          dimensions                  = 2
          approximate_neighbors_count = 150
          distance_measure_type       = "DOT_PRODUCT_DISTANCE"
          algorithm_config {
            tree_ah_config {
              leaf_node_embedding_count    = 500
              leaf_nodes_to_search_percent = 7
            }
          }
        }
      }
      index_update_method = "BATCH_UPDATE"
    
      timeouts {
        create = "2h"
        update = "1h"
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def vector_search_deploy_index(
        project: str,
        location: str,
        index_name: str,
        index_endpoint_name: str,
        deployed_index_id: str,
    ) -> None:
        """Deploy a vector search index to a vector search index endpoint.
    
        Args:
            project (str): Required. Project ID
            location (str): Required. The region name
            index_name (str): Required. The index to update. A fully-qualified index
              resource name or a index ID.  Example:
              "projects/123/locations/us-central1/indexes/my_index_id" or
              "my_index_id".
            index_endpoint_name (str): Required. Index endpoint to deploy the index
              to.
            deployed_index_id (str): Required. The user specified ID of the
              DeployedIndex.
        """
        # Initialize the Vertex AI client
        aiplatform.init(project=project, location=location)
    
        # Create the index instance from an existing index
        index = aiplatform.MatchingEngineIndex(index_name=index_name)
    
        # Create the index endpoint instance from an existing endpoint.
        index_endpoint = aiplatform.MatchingEngineIndexEndpoint(
            index_endpoint_name=index_endpoint_name
        )
    
        # Deploy Index to Endpoint
        index_endpoint = index_endpoint.deploy_index(
            index=index, deployed_index_id=deployed_index_id
        )
    
        print(index_endpoint.deployed_indexes)

### Console

Use these instructions to deploy your index.

1.  In the Agent Platform section of the Google Cloud console, go to the **Deploy and Use** section. Select **Vector Search** .
    
    . A list of your active indexes is displayed.

2.  Select the name of the index you want to deploy. The index details page opens.

3.  From the index details page, click **add\_box Deploy to endpoint** . The index deployment panel opens.

4.  Enter a display name - this name acts as an ID and can't be updated.

5.  From the **Endpoint** drop-down, select the endpoint you want to deploy this index to. Note: The endpoint is unavailable if the index is already deployed to it.

6.  Optional: In the **Machine type** field, select either standard or high-memory.

7.  Optional. Select **Enable autoscaling** to automatically resize the number of nodes based on the demands of your workloads. The default number of replicas is 2 if autoscaling is disabled.

8.  Click **Deploy** to deploy your index to the endpoint. Note: It takes around 30 minutes to be deployed.

### Create a forwarding rule in the VPC project

After index deployment is done, the index endpoint returns a service attachment URI *instead* of an IP address. You need to create a compute address, as well as a forwarding rule in the VPC project targeting the service attachment using the created compute address. To create a compute address, use the following example:

    gcloud compute addresses create ${ADDRESS_NAME:?} \
        --region=${REGION:?} \
        --subnet=${SUBNET_NAME:?} \
        --project=${VPC_PROJECT:?}

To create a forwarding rule targeting the service attachment URI using the created compute address, use the following example:

    SERVICE_ATTACHMENT_URI=`gcloud ai index-endpoints describe {INDEX_ENDPOINT_ID}
    --format="value(deployedIndexes.privateEndpoints.serviceAttachment)"`
    
    gcloud compute forwarding-rules create ${ENDPOINT_NAME:?} \
        --network=${NETWORK_NAME:?} \
        --address=${ADDRESS_NAME:?} \
        --target-service-attachment=${SERVICE_ATTACHMENT_URI:?} \
        --project=${VPC_PROJECT:?} \
        --region=${REGION:?}

#### (Optional) Create DNS record for the IP address

If you want to connect and load without memorizing the actual IP address, you can create a DNS record. This step is optional.

    DNS_NAME_SUFFIX=matchingengine.vertexai.goog. # Don't forget the "." in the end.
    DNS_NAME=${INDEX_ENDPOINT_ID:?}.${REGION:?}.${DNS_NAME_SUFFIX:?}
    
    gcloud dns managed-zones create ${DNS_ZONE_NAME:?} \
        --dns-name=${DNS_NAME_SUFFIX:?} \
        --visibility=private \
        --project=${VPC_PROJECT:?} \
        --region=${REGION:?}
    
    gcloud dns record-sets create ${DNS_NAME:?} \
        --rrdatas=${IP_ADDRESS:?} \
        --type=A --ttl=60 \
        --zone=${DNS_ZONE_NAME:?} \
        --project=${VPC_PROJECT:?} \
        --region=${REGION:?}

## Send queries to the index endpoint

Now that you've created an endpoint with Private Service Connect and created the index, you can begin running queries.

To query your index, see [Query indexes to get nearest neighbors](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/query-index-vpc) .

## What's next

  - Learn how to [Update and rebuild your index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/update-rebuild-index)
  - Learn how to [Monitor the index endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/monitor)
