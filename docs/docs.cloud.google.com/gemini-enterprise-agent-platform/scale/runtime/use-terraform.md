---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-terraform
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-terraform
title: Provision agents with Terraform
description: Learn how to provision and manage Agent Runtime resources using Terraform, including source and Dockerfile deployments, prebuilt container image deployments, IAM permissions, and service accounts.
data_source: docs.cloud.google.com
---

You can use Terraform to provision and manage Agent Runtime instances declaratively. When deploying agents with Terraform, you manage the [`google_vertex_ai_reasoning_engine` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines) using the official Google Cloud Terraform provider ( [GA provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_reasoning_engine) or [Beta provider](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/vertex_ai_reasoning_engine) ).

The instructions on this page correspond to the sample containerized agent implementation described in the [Deploy a containerized agent with Agent Runtime](https://codelabs.developers.google.com/codelabs/agent-runtime-deploy-containerized-agent) codelab.

## Prerequisites

Before using Terraform to deploy an agent, ensure that you have completed the following setup:

1.  [Install Terraform](https://developer.hashicorp.com/terraform/downloads) (version 1.5.0 or later) and review the official HashiCorp Terraform Registry documentation for the `google_vertex_ai_reasoning_engine` resource ( [GA provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_reasoning_engine) and [Beta provider](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/vertex_ai_reasoning_engine) ).

2.  [Set up your Google Cloud environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup) and enable the Vertex AI API ( `aiplatform.googleapis.com` ), Artifact Registry API ( `artifactregistry.googleapis.com` ), and Cloud Build API ( `cloudbuild.googleapis.com` ).

3.  Authenticate your local environment using Google Cloud credentials:
    
        gcloud auth application-default login

4.  To keep your application code separate from infrastructure management, organize your agent workspace into dedicated application and Terraform directories:
    
        weather-agent-byoc/
        ├── main.py                # Python ADK agent entrypoint
        ├── requirements.txt       # Python dependencies
        ├── Dockerfile             # Container build definition
        └── terraform/             # Terraform configuration directory
            ├── main.tf            # Agent Runtime resources and specifications
            ├── variables.tf       # Project, region, and container variables
            └── outputs.tf         # Resource name outputs
    
      - **Application files** ( `main.py` , `requirements.txt` , `Dockerfile` ): Contain your agent logic, web framework wrapper (such as FastAPI or ADK App), Python dependencies, and container build instructions.
    
      - **Terraform directory** ( `terraform/` ): Contains all Terraform configuration files used to provision resources:
        
          - `variables.tf` : Declares input variables such as `project_id` , `location` , `repository_name` , and `image_tag` .
          - `main.tf` : Declares provider settings, local variables, IAM role bindings, and `google_vertex_ai_reasoning_engine` resource specifications.
          - `outputs.tf` : Exports provisioned resource attributes, such as the Agent Runtime ID and full resource name, after deployment.

5.  Grant the appropriate IAM roles depending on who is executing the deployment:
    
      - Human developer or CI/CD service account executing `terraform apply` and local build commands.
        
        #### Click to see required permissions
        
          - **Vertex AI User** ( `roles/aiplatform.user` ) or **Vertex AI Administrator** ( `roles/aiplatform.admin` ): Authorizes the deployer to execute Agent Runtime Control Plane RPC operations ( `CreateReasoningEngine` , `UpdateReasoningEngine` , `DeleteReasoningEngine` ).
          - **Service Account User** ( `roles/iam.serviceAccountUser` ): Granted on the custom runtime service account ( `google_service_account.agent_runtime_sa` ) attached to the agent. Authorizes the deployer to attach that service account identity to the provisioned `google_vertex_ai_reasoning_engine` resource.
          - **Storage Object Admin** ( `roles/storage.objectAdmin` ) or **Storage Object Viewer** ( `roles/storage.objectViewer` ): Required when using Python package staging ( `package_spec` ) to upload or read serialized agent pickles ( `agent.pkl` ) and dependency manifests in Cloud Storage.
          - **Artifact Registry Writer** ( `roles/artifactregistry.writer` ): Required when prebuilding and pushing custom container images ( `docker push` ) to Artifact Registry repositories.
    
      - System-managed Agent Runtime Service Agent ( `service-<var>PROJECT_NUMBER</var>@gcp-sa-aiplatform-re.iam.gserviceaccount.com` ).
        
        #### Click to see required permissions
        
          - **Artifact Registry Reader** ( `roles/artifactregistry.reader` ): Grants the background Agent Runtime platform infrastructure permission to authenticate with Artifact Registry and pull your custom container image during pod deployment and container cold starts.
        
        > **Important:** In Terraform, you must explicitly manage the IAM binding for the service agent and ensure the `google_vertex_ai_reasoning_engine` resource includes a `depends_on` reference to the IAM binding. Otherwise, pod provisioning may fail with `IMAGE_PULL_BACKOFF` due to a race condition.

## Prepare for deployment

Terraform supports the following deployment paths for Agent Runtime:

  - [**Deploy from prebuilt container image**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-terraform#deploy-byoc-agent) : Pre-build and push a container image to Artifact Registry ( `{region}-docker.pkg.dev/...` ) and deploy it using `container_spec` . Use this method when you require full control over the container build process, custom base images, or lower deployment latency.
  - [**Deploy from source files or Dockerfile**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-terraform#deploy-dockerfile) : Deploy your agent directly from local source files or a Dockerfile. Agent Runtime builds and provisions the container image automatically without requiring manual image management.
  - [**Deploy using Python package specs**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-terraform#deploy-package-agent) Deploy using ( `package_spec` ) staged in Cloud Storage. Agent Runtime builds and provisions the container image automatically without requiring manual image management.

### Deploy from a prebuilt container image

If you pre-build and push container images to Artifact Registry (for example, to include custom system libraries, optimize cold-start performance, or enforce organizational image build controls), you can deploy using `container_spec` . For details on image requirements, see [Deploy from Container Image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#from-container-image) .

Container images must be stored in Artifact Registry ( `{LOCATION}-docker.pkg.dev/{PROJECT_ID}/{REPOSITORY}/{IMAGE}:{TAG}` ), listen on port `8080` (or a custom port specified in `container_spec` ), and conform to the [runtime contract](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/runtime-contract) .

1.  Build your container image locally and push it to your Artifact Registry repository:
    
        # 1. Authenticate Docker with your Artifact Registry region
        gcloud auth configure-docker us-central1-docker.pkg.dev# 2. Build the container image from your application root directory
        cd weather-agent-byoc
        docker build -t us-central1-docker.pkg.dev/PROJECT_ID/agents-repo/weather-agent-image:latest .# 3. Push the container image to Artifact Registry
        docker push us-central1-docker.pkg.dev/PROJECT_ID/agents-repo/weather-agent-image:latest

2.  Configure your prebuilt container image for Terraform deployment. The following configuration demonstrates deploying a prebuilt container image hosted in Artifact Registry by creating the `variables.tf` , `main.tf` , and `outputs.tf` files in your `terraform/` directory:
    
    #### Input variables ( `terraform/variables.tf` )
    
        variable "project_id" {
          type        = string
          description = "The Google Cloud Project ID"
        }
        
        variable "project_number" {
          type        = string
          description = "The Google Cloud Project Number"
        }
        
        variable "location" {
          type        = string
          default     = "us-central1"
          description = "The region to deploy Agent Runtime"
        }
        
        variable "repository_name" {
          type        = string
          default     = "agents-repo"
          description = "The Artifact Registry repository name"
        }
        
        variable "image_tag" {
          type        = string
          default     = "latest"
          description = "The tag of the container image to deploy"
        }
    
    #### Resource specifications ( `terraform/main.tf` )
    
        terraform {
          required_providers {
            google = {
              source  = "hashicorp/google"
              version = ">= 5.28.0"
            }
          }
        }
        
        provider "google" {
          project = var.project_id
          region  = var.location
        }
        
        locals {
          class_methods = [
            { "name" = "get_session", "api_mode" = "" },
            { "name" = "list_sessions", "api_mode" = "" },
            { "name" = "create_session", "api_mode" = "" },
            { "name" = "delete_session", "api_mode" = "" },
            { "name" = "async_get_session", "api_mode" = "async" },
            { "name" = "async_list_sessions", "api_mode" = "async" },
            { "name" = "async_create_session", "api_mode" = "async" },
            { "name" = "async_delete_session", "api_mode" = "async" },
            { "name" = "async_add_session_to_memory", "api_mode" = "async" },
            { "name" = "async_search_memory", "api_mode" = "async" },
            { "name" = "stream_query", "api_mode" = "stream" },
            { "name" = "async_stream_query", "api_mode" = "async_stream" },
            { "name" = "streaming_agent_run_with_events", "api_mode" = "async_stream" }
          ]
        }
        
        # Grant Artifact Registry Reader permission to the Agent Runtime Service Agent
        resource "google_project_iam_member" "re_service_agent_ar_reader" {
          project = var.project_id
          role    = "roles/artifactregistry.reader"
          member  = "serviceAccount:service-${var.project_number}@gcp-sa-aiplatform-re.iam.gserviceaccount.com"
        }
        
        # Define the Agent Runtime resource with BYOC container configuration
        resource "google_vertex_ai_reasoning_engine" "byoc_weather_agent" {
          display_name = "byoc_weather_agent_tf"
          description  = "BYOC weather agent deployed using Terraform"
          project      = var.project_id
          location     = var.location
        
          spec {
            agent_framework = "google-adk"
        
            container_spec {
              image_uri = "${var.location}-docker.pkg.dev/${var.project_id}/${var.repository_name}/weather-agent-image:${var.image_tag}"
            }
        
            class_methods = jsonencode(local.class_methods)
          }
        
          # Ensure service agent permission exists before provisioning to prevent IMAGE_PULL_BACKOFF
          depends_on = [google_project_iam_member.re_service_agent_ar_reader]
        }
    
    #### Resource outputs ( `terraform/outputs.tf` )
    
        output "reasoning_engine_id" {
          value       = google_vertex_ai_reasoning_engine.byoc_weather_agent.id
          description = "The ID of the deployed Agent Runtime instance"
        }
        
        output "reasoning_engine_resource_name" {
          value       = google_vertex_ai_reasoning_engine.byoc_weather_agent.name
          description = "The resource name of the deployed Agent Runtime instance"
        }

### Deploy from Dockerfile or source repository

When deploying from a Dockerfile, specify your source archive in `source_code_spec` and set an empty `image_spec {}` block to instruct Agent Runtime to build the container image using your Dockerfile. The container built from your Dockerfile must adhere to the [runtime contract](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/runtime-contract) .

For more details about how deployment works, see [Deploy from Dockerfile](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#from-dockerfile) or [Deploy from source files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#from-source-files) .

1.  Compress your application code ( `main.py` ), Python dependency manifest ( `requirements.txt` ), and container build instructions ( `Dockerfile` ) into a gzipped tar file archive.

2.  Run the following command from your application root directory (the example uses the root directory `weather-agent-byoc/` and the tar file archive `weather_agent_source.tar.gz` ):
    
        cd weather-agent-byoc
        tar -czvf terraform/weather_agent_source.tar.gz main.py requirements.txt Dockerfile
    
    > **Note:** The `main.py` , `requirements.txt` , and `Dockerfile` files must reside directly at the root level of the tar file archive (not nested inside a parent directory like `weather-agent-byoc/main.py` ). When Agent Runtime provisions the build container, Cloud Build API unpacks `weather_agent_source.tar.gz` directly into the build workspace root and expects `Dockerfile` to be present at `./Dockerfile` during compilation.

3.  Create the `variables.tf` , `main.tf` , and `outputs.tf` files in your `terraform/` directory:
    
    ##### Input variables ( `terraform/variables.tf` )
    
        variable "project_id" {
          type        = string
          description = "The Google Cloud Project ID"
        }
        
        variable "location" {
          type        = string
          default     = "us-central1"
          description = "The region to deploy Agent Runtime"
        }
    
    #### Resource specifications ( `terraform/main.tf` )
    
        terraform {
          required_providers {
            google = {
              source  = "hashicorp/google"
              version = ">= 5.28.0"
            }
          }
        }
        
        provider "google" {
          project = var.project_id
          region  = var.location
        }
        
        resource "google_vertex_ai_reasoning_engine" "dockerfile_agent" {
          display_name = "dockerfile_weather_agent_tf"
          description  = "BYOC weather agent deployed using Dockerfile"
          project      = var.project_id
          location     = var.location
        
          spec {
            agent_framework = "google-adk"
        
            source_code_spec {
              inline_source {
                source_archive = filebase64("weather_agent_source.tar.gz")
              }
        
              # Empty image_spec instructs the runtime to build using the Dockerfile
              image_spec {}
            }
        
            class_methods = jsonencode([
              { "name" = "get_session", "api_mode" = "" },
              { "name" = "list_sessions", "api_mode" = "" },
              { "name" = "create_session", "api_mode" = "" },
              { "name" = "delete_session", "api_mode" = "" },
              { "name" = "async_get_session", "api_mode" = "async" },
              { "name" = "async_list_sessions", "api_mode" = "async" },
              { "name" = "async_create_session", "api_mode" = "async" },
              { "name" = "async_delete_session", "api_mode" = "async" },
              { "name" = "async_add_session_to_memory", "api_mode" = "async" },
              { "name" = "async_search_memory", "api_mode" = "async" },
              { "name" = "stream_query", "api_mode" = "stream" },
              { "name" = "async_stream_query", "api_mode" = "async_stream" },
              { "name" = "streaming_agent_run_with_events", "api_mode" = "async_stream" }
            ])
          }
        }
    
    #### Resource outputs ( `terraform/outputs.tf` )
    
        output "dockerfile_agent_id" {
          value       = google_vertex_ai_reasoning_engine.dockerfile_agent.id
          description = "Resource ID of the deployed Dockerfile agent"
        }

### Deploy using Python package spec

If your agent is built using Python SDK objects or pickled applications (such as ADK, LangChain, or custom Python agents), you can stage your serialized agent ( `.pkl` ) and dependency configuration ( `requirements.txt` ) in a Cloud Storage bucket and reference them using `package_spec` .

For more details about how deployment works, see [Deploy from Python object](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#python-object) .

1.  Run the following Python script to serialize your agent and stage the deployment artifacts in Cloud Storage:
    
        import cloudpickle
        from google.adk.agents import Agent
        from google.cloud import storage
        from vertexai.agent_engines import AdkApp
        PROJECT_ID = "PROJECT_ID"
        BUCKET_NAME = "BUCKET_NAME"
        GCS_DIR = "agents/weather_agent"
        
        # 1. Define agent logic
        root_agent = Agent(
            model="gemini-3.1-flash-lite",
            name="weather_agent",
            description="Agent deployed using Terraform package_spec.",
        )
        local_app = AdkApp(agent=root_agent)
        
        # 2. Upload pickle to Cloud Storage
        storage_client = storage.Client(project=PROJECT_ID)
        bucket = storage_client.bucket(BUCKET_NAME)
        
        pkl_blob = bucket.blob(f"{GCS_DIR}/agent.pkl")
        with pkl_blob.open("wb") as f:
            cloudpickle.dump(local_app, f)
        
        # 3. Upload requirements.txt
        requirements_content = """google-cloud-aiplatform[agent_engines,adk]>=1.144
        cloudpickle==3.0.0
        """
        req_blob = bucket.blob(f"{GCS_DIR}/requirements.txt")
        req_blob.upload_from_string(requirements_content)
        
        print(f"Artifacts uploaded to gs://{BUCKET_NAME}/{GCS_DIR}/")

2.  Create the `variables.tf` , `main.tf` , and `outputs.tf` files in your `terraform/` directory referencing the staged Cloud Storage URIs:
    
    ##### Input variables ( `terraform/variables.tf` )
    
        variable "project_id" {
          type        = string
          description = "The Google Cloud Project ID"
        }
        
        variable "location" {
          type        = string
          default     = "us-central1"
          description = "The region to deploy Agent Runtime"
        }
        
        variable "bucket_name" {
          type        = string
          description = "Cloud Storage bucket name containing agent artifacts"
        }
    
    ##### Resource specifications ( `terraform/main.tf` )
    
        terraform {
          required_providers {
            google = {
              source  = "hashicorp/google"
              version = ">= 5.28.0"
            }
          }
        }
        
        provider "google" {
          project = var.project_id
          region  = var.location
        }
        
        resource "google_vertex_ai_reasoning_engine" "package_agent" {
          display_name = "weather_agent_package_tf"
          description  = "Agent Runtime instance deployed using package_spec"
          project      = var.project_id
          location     = var.location
        
          spec {
            agent_framework = "google-adk"
            package_spec {
              python_version        = "3.11"
              pickle_object_gcs_uri = "gs://${var.bucket_name}/agents/weather_agent/agent.pkl"
              requirements_gcs_uri  = "gs://${var.bucket_name}/agents/weather_agent/requirements.txt"
            }
          }
        }
    
    ##### Resource outputs ( `terraform/outputs.tf` )
    
        output "package_agent_id" {
          value       = google_vertex_ai_reasoning_engine.package_agent.id
          description = "Resource ID of the deployed package agent"
        }

## Configure environment variables and secrets

Before deployment, you can attach a custom runtime service account to your agent and pass environment variables ( `env` ) or Secret Manager references ( `secret_env` ).

The following example configures environment variables ( `LOCATION` , `MODEL` , `MODEL_REGION` ) and passes an API key securely from Secret Manager to the runtime service account through the `terraform/main.tf` file:

    # 1. Dedicated Runtime Service Account
    resource "google_service_account" "agent_runtime_sa" {
      account_id   = "agent-runtime-sa"
      display_name = "Agent Runtime Identity"
      project      = var.project_id
    }
    
    # 2. Secret Manager Secret for Agent Credentials
    resource "google_secret_manager_secret" "api_key_secret" {
      secret_id = "agent-api-key"
      project   = var.project_id
    
      replication {
        auto {}
      }
    }
    
    resource "google_secret_manager_secret_version" "api_key_version" {
      secret      = google_secret_manager_secret.api_key_secret.id
      secret_data = var.api_key_value
    }
    
    # Grant Secret Accessor role to Runtime Service Account
    resource "google_secret_manager_secret_iam_member" "secret_accessor" {
      secret_id = google_secret_manager_secret.api_key_secret.id
      role      = "roles/secretmanager.secretAccessor"
      member    = "serviceAccount:${google_service_account.agent_runtime_sa.email}"
    }
    
    # Grant Artifact Registry Reader permission to the Agent Runtime Service Agent
    resource "google_project_iam_member" "re_service_agent_ar_reader" {
      project = var.project_id
      role    = "roles/artifactregistry.reader"
      member  = "serviceAccount:service-${var.project_number}@gcp-sa-aiplatform-re.iam.gserviceaccount.com"
    }
    
    # 3. Agent Runtime Resource with Environment Variables and Secret References
    resource "google_vertex_ai_reasoning_engine" "advanced_weather_agent" {
      display_name = "byoc_weather_agent_advanced_tf"
      description  = "BYOC weather agent with custom service account and secrets"
      project      = var.project_id
      location     = var.location
    
      spec {
        agent_framework = "google-adk"
        service_account = google_service_account.agent_runtime_sa.email
    
        container_spec {
          image_uri = "${var.location}-docker.pkg.dev/${var.project_id}/${var.repository_name}/weather-agent-image:${var.image_tag}"
        }
    
        deployment_spec {
          env {
            name  = "LOCATION"
            value = var.location
          }
          env {
            name  = "MODEL"
            value = "gemini-3.1-flash-lite"
          }
          env {
            name  = "MODEL_REGION"
            value = "global"
          }
    
          secret_env {
            name = "API_KEY"
            secret_ref {
              secret  = google_secret_manager_secret.api_key_secret.secret_id
              version = "latest"
            }
          }
        }
    
        class_methods = jsonencode([
          { "name" = "get_session", "api_mode" = "" },
          { "name" = "create_session", "api_mode" = "" },
          { "name" = "stream_query", "api_mode" = "stream" },
          { "name" = "async_stream_query", "api_mode" = "async_stream" }
        ])
      }
    
      depends_on = [
        google_secret_manager_secret_iam_member.secret_accessor,
        google_project_iam_member.re_service_agent_ar_reader
      ]
    }

## Execution and lifecycle

Execute the standard Terraform lifecycle to plan, deploy, invoke, and destroy your agent resources.

### Apply Terraform configuration

Deploy your agent by applying your Terraform configuration:

1.  Change into your Terraform directory (for example, `cd weather-agent-byoc/terraform` ):
    
        cd weather-agent-byoc/terraform

2.  Initialize the working directory:
    
        terraform init

3.  Preview the deployment plan:
    
        terraform plan -var="project_id=PROJECT_ID" -var="project_number=PROJECT_NUMBER"

4.  Apply the configuration to provision the agent:
    
        terraform apply -var="project_id=PROJECT_ID" -var="project_number=PROJECT_NUMBER"

### Query the deployed agent

After Terraform provisions the `google_vertex_ai_reasoning_engine` resource, send an HTTP `POST` request to the `:streamQuery?alt=sse` endpoint to stream response events in real time using Server-Sent Events (SSE):

> **Note:** For additional query methods, see [Use an ADK agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-adk-agent#stream-responses) .

    LOCATION="LOCATION"
    PROJECT_ID="PROJECT_ID"
    REASONING_ENGINE_ID="REASONING_ENGINE_ID"curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json; charset=utf-8" \
      -d '{
        "class_method": "async_stream_query",
        "input": {
          "user_id": "terraform_test_user",
          "message": "What is the temperature in Seattle?"
        }
      }' \
      "https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/reasoningEngines/${REASONING_ENGINE_ID}:streamQuery?alt=sse"

  - **OAuth Access Token** : `Authorization: Bearer $(gcloud auth print-access-token)` generates a short-lived OAuth 2.0 access token using your local Google Cloud credentials.
  - **JSON `input` envelope** : The request body requires a JSON payload containing an `input` object. When calling explicit class methods (such as `async_stream_query` ), include the `"class_method"` parameter alongside `"input"` .
  - **Response payload** : Responses are delivered continuously as `data: { ... }` Server-Sent Event (SSE) chunks.

### Destroy agent resources

To clean up resources and prevent unexpected billing charges, change into your `terraform/` directory (for example, `cd weather-agent-byoc/terraform` ) and run `terraform destroy` :

    cd weather-agent-byoc/terraform
    terraform destroy -var="project_id=PROJECT_ID" -var="project_number=PROJECT_NUMBER"

## What's next

  - [HashiCorp Terraform Registry — `google_vertex_ai_reasoning_engine` (GA)](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_reasoning_engine)
  - [HashiCorp Terraform Registry — `google_vertex_ai_reasoning_engine` (Beta)](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/vertex_ai_reasoning_engine)
  - [Google Cloud Generative AI — Agent Runtime Terraform Deployment Tutorial (GitHub)](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/tutorial_get_started_with_agent_engine_terraform_deployment.ipynb)
  - [Google Developer Forum — Deploy Your Agent Runtime with Terraform the Enterprise Way](https://discuss.google.dev/t/deploy-your-agent-engine-with-terraform-the-enterprise-way/271921)
