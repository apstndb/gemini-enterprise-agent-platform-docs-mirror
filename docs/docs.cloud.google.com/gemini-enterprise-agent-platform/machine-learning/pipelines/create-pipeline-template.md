---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/create-pipeline-template
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/create-pipeline-template
title: Create, upload, and use a pipeline template
description: Learn how to compile reusable pipeline templates in to share your ML workflow definitions.
data_source: docs.cloud.google.com
---

A pipeline template is a resource that you can use to publish a workflow definition so that it can be reused multiple times, by a single user or by [multiple users](https://docs.cloud.google.com/artifact-registry/docs/access-control#grant-repo) .

The Kubeflow Pipelines SDK registry client is a new client interface that you can use with a compatible registry server, such as Artifact Registry, for version control of your Kubeflow Pipelines (KFP) templates. For more information, see [Use the template in a Kubeflow Pipelines SDK registry client](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/create-pipeline-template#use-the-template-in-kfp-client) .

This page shows you how to:

  - Create a KFP pipeline template
  - Use the Kubeflow Pipelines SDK registry client to upload the template to a pipeline template repository
  - Use the template in the Kubeflow Pipelines client

## Before you begin

Before you build and run your pipeline, use the following instructions to set up your Google Cloud project and development environment in the Google Cloud console.

1.  Install v2 or later of the Kubeflow Pipelines SDK.
    
        pip install --upgrade "kfp>=2,<3"

> **Note:** To upgrade to the latest version of the Kubeflow Pipelines SDK, run the following command:  
> `pip install kfp --upgrade`  
> If an updated version is available, running this command uninstalls KFP and installs the latest version.

1.  Install v1.15.0 or later of the [Agent Platform SDK for Python](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .  
    (Optional) Before installing, run the following command to see which version of the [Agent Platform SDK for Python](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) is installed:
    
    ``` 
      pip freeze | grep google-cloud-aiplatform
    ```
    
    > **Note:** To upgrade to the latest version of the [Agent Platform SDK for Python](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) , run the following command:  
    > `pip install google-cloud-aiplatform --upgrade`  
    > If an updated version is available, running this command uninstalls your installed version and installs the latest version.

2.  (Optional) Install 390.0.0 or later of the [Google Cloud CLI](https://docs.cloud.google.com/sdk/docs/install) .

3.  [Enable the Artifact Registry API](https://docs.cloud.google.com/artifact-registry/docs/enable-service) .

## Configuring permissions

If you have not already set up your gcloud CLI project for Gemini Enterprise Agent Platform Pipelines, follow the instructions in [Configure your Google Cloud project for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project) .

Additionally, assign the following predefined Identity and Access Management permissions to use Artifact Registry as the template registry:

  - `roles/artifactregistry.admin` : Assign this role to create and manage a repository.
  - `roles/artifactregistry.repoAdmin` or `roles/artifactregistry.writer` : Assign any of these roles to manage templates inside a repository.
  - `roles/artifactregistry.reader` : Assign this role to download templates from a repository.
  - `roles/artifactregistry.reader` : Assign this role to a [service account associated with Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) to create a pipeline run from a template.

For more information about predefined Identity and Access Management roles for Artifact Registry, see [Predefined Artifact Registry roles](https://docs.cloud.google.com/artifact-registry/docs/access-control#roles) .

Use the following sample to assign roles:

    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member=PRINCIPAL \
        --role=ROLE

Replace the following:

  - PROJECT\_ID : The project where you want to create the pipeline.
  - PRINCIPAL : The principal to which you are adding permissions.
  - ROLE : The Identity and Access Management role that you want to grant to the principal.

See [Roles and permissions](https://docs.cloud.google.com/artifact-registry/docs/access-control#permissions) in the [Artifact Registry documentation](https://docs.cloud.google.com/artifact-registry/docs) for more information about the following:

  - [Granting project-wide permissions](https://docs.cloud.google.com/artifact-registry/docs/access-control#grant-project)
  - [Granting repository-specific permissions](https://docs.cloud.google.com/artifact-registry/docs/access-control#grant-repo)
  - [Granting basic Identity and Access Management roles to individual users](https://docs.cloud.google.com/artifact-registry/docs/access-control#basic)

## Create a repository in Artifact Registry

Next you'll create a repository in Artifact Registry for your pipeline templates.

### Console

1.  Open **Agent Platform Pipelines** in the Google Cloud console.

2.  Click the **Your templates** tab.

3.  To open the **Select repository** pane, click **Select repository** .

4.  Click **Create repository** .

5.  Specify `quickstart-kfp-repo` as the repository name.

6.  Under **Format** , select `Kubeflow Pipelines` .

7.  Under **Location Type** , select **Region** .

8.  In the **Region** drop-down list, select `us-central1` .
    
    > **Note:** The example commands and configuration in these instructions use `us-central1` , but you can use any of the supported regions.

9.  Click **Create** .

### Google Cloud CLI

Run the following command to create a repository.

Before using any of the command data below, make the following replacements:

  - LOCATION : The location or region where you want to create the repository, for example, `us-central1`

Execute the [gcloud artifacts repositories create](https://docs.cloud.google.com/sdk/gcloud/reference/artifacts/repositories/create) command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud artifacts repositories create quickstart-kfp-repo --location=LOCATION_ID --repository-format=KFP

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud artifacts repositories create quickstart-kfp-repo --location=LOCATION_ID --repository-format=KFP

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud artifacts repositories create quickstart-kfp-repo --location=LOCATION_ID --repository-format=KFP

## Create a template

Use the following code sample to define a pipeline with a single component. For information about how to define a pipeline using KFP, see [Build a Pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

    from kfp import dsl
    from kfp import compiler
    
    @dsl.component()
    def hello_world(text: str) -> str:
        print(text)
        return text
    
    @dsl.pipeline(name='hello-world', description='A simple intro pipeline')
    def pipeline_hello_world(text: str = 'hi there'):
        """Pipeline that passes small pipeline parameter string to consumer op."""
    
        consume_task = hello_world(
            text=text)  # Passing pipeline parameter as argument to consumer op
    
    compiler.Compiler().compile(
        pipeline_func=pipeline_hello_world,
        package_path='hello_world_pipeline.yaml')

When you run the sample, the `compiler.Compiler().compile(...)` statement compiles the "hello-world" pipeline into the local YAML file named `hello_world_pipeline.yaml` .

## Upload the template

### Console

1.  Open **Agent Platform Pipelines** in the Google Cloud console.

2.  Click **Upload** to open the **Upload pipeline or component** pane.

3.  In the **Repository** drop-down list, select the `quickstart-kfp-repo` repository.

4.  Specify a **Name** for the pipeline template.

5.  In the **File** field, click **Choose** to select and upload the compiled pipeline template YAML from your local file system.

6.  After you upload the pipeline template, it is listed on the **Your templates** page.

### Kubeflow Pipelines SDK client

1.  To configure your Kubeflow Pipelines SDK registry client, run the following commands:
    
        from kfp.registry import RegistryClient
        
        client = RegistryClient(host=f"https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo")

2.  Upload the compiled YAML file to your repository in Artifact Registry.
    
        templateName, versionName = client.upload_pipeline(
          file_name="hello_world_pipeline.yaml",
          tags=["v1", "latest"],
          extra_headers={"description":"This is an example pipeline template."})

3.  To verify that the template was uploaded:
    
    1.  Open **Agent Platform Pipelines** in the Google Cloud console.
    
    2.  Click the **Your templates** tab.
    
    3.  Click **Select repository** .
    
    4.  From the list, select the `quickstart-kfp-repo` repository, and then click **Select** .
    
    5.  You should find the uploaded template package `hello-world` from the list.
    
    6.  To view list of versions of the pipeline template, click the `hello-world` template.
    
    7.  To view the pipeline topology, click the version.

## Use the template in Agent Platform

After you've uploaded your pipeline template to your repository in Artifact Registry, it is ready to be used in Agent Platform Pipelines.

### Create a staging bucket for your template

Before you can use your pipeline template, you'll need to create a Cloud Storage bucket for staging pipeline runs.

To create the bucket, follow the instructions in [Configure a Cloud Storage bucket for pipeline artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#storage) and then run the following command:

    STAGING_BUCKET="gs://BUCKET_NAME"

Replace BUCKET\_NAME with the name of the bucket you just created.

### Create a pipeline run from your template

You can use the Agent Platform SDK for Python or the Google Cloud console to create a pipeline run from your template in Artifact Registry.

### Console

1.  Open **Agent Platform Pipelines** in the Google Cloud console.

2.  Click the **Your templates** tab.

3.  To open the **Select repository** pane, click **Select repository** .

4.  Select the `quickstart-kfp-repo` repository, and then click **Select** .

5.  Click the `hello-world` package.

6.  Next to the `4f245e8f9605` version, click **Create Run** .

7.  Click **Runtime Configuration** .

8.  Enter the following under **Cloud Storage location** :
    
        gs://BUCKET_NAME
    
    Replace BUCKET\_NAME with the name of the bucket you created for staging your pipeline runs.

9.  Click **Submit** .

### Agent Platform SDK for Python

Use the following sample to create a pipeline run from your template:

    from google.cloud import aiplatform
    
    # Initialize the aiplatform package
    aiplatform.init(
        project="PROJECT_ID",
        location='us-central1',
        staging_bucket=STAGING_BUCKET)
    
    # Create a pipeline job using a version ID.
    job = aiplatform.PipelineJob(
        display_name="hello-world-latest",
        template_path="https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo/hello-world@SHA256_TAG" + \
            versionName)
    
    # Alternatively, create a pipeline job using a tag.
    job = aiplatform.PipelineJob(
        display_name="hello-world-latest",
        template_path="https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo/hello-world/TAG")
    
    job.submit()

Replace the following:

  - PROJECT\_ID : The Google Cloud project that this pipeline runs in.

  - SHA256\_TAG : The sha256 hash value of the template version.

  - TAG : The version tag of the template.

### View created pipeline runs

You can view the runs created by a specific pipeline version in the Agent Platform SDK for Python.

### Console

1.  Open **Agent Platform Pipelines** in the Google Cloud console.

2.  Click the **Your templates** tab.

3.  Click **Select repository** .

4.  From the list, select the `quickstart-kfp-repo` repository, and then click **Select** .

5.  To view list of versions for the `hello-world` pipeline template, click the `hello world` template.

6.  Click the desired version for which you want to view pipeline runs.

7.  To view pipeline runs for the selected version, click **View Runs** and then click the **Runs** tab.

### Agent Platform SDK for Python

To list the pipelines runs, run the [pipelineJobs.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/list) command as shown in one or more of the following examples:

``` 
  from google.cloud import aiplatform

  # To filter all runs created from a specific version
  filter = 'template_uri:"https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo/hello-world/*" AND ' + \
           'template_metadata.version="%s"' % versionName
  aiplatform.PipelineJob.list(filter=filter)

  # To filter all runs created from a specific version tag
  filter = 'template_uri="https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo/hello-world/latest"'
  aiplatform.PipelineJob.list(filter=filter)

  # To filter all runs created from a package
  filter = 'template_uri:"https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo/hello-world/*"'
  aiplatform.PipelineJob.list(filter=filter)

  # To filter all runs created from a repo
  filter = 'template_uri:"https://us-central1-kfp.pkg.dev/PROJECT_ID/quickstart-kfp-repo/*"'
  aiplatform.PipelineJob.list(filter=filter)
```

## Use the template in a Kubeflow Pipelines SDK registry client

You can use a Kubeflow Pipelines SDK registry client together with Artifact Registry to download and use your pipeline template.

  - To list the resources in the repository, run the following commands:
    
        templatePackages = client.list_packages()
        templatePackage = client.get_package(package_name = "hello-world")
        
        versions = client.list_versions(package_name="hello-world")
        version = client.get_version(package_name="hello-world", version=versionName)
        
        tags = client.list_tags(package_name = "hello-world")
        tag = client.get_tag(package_name = "hello-world", tag="latest")
    
    For the complete list of available methods and documents, see the `proto` files in the Artifact Registry [GitHub repo](https://github.com/googleapis/googleapis/tree/master/google/devtools/artifactregistry/v1) .

  - To download the template to your local file system, run the following commands:
    
        # Sample 1
        filename = client.download_pipeline(
          package_name = "hello-world",
          version = versionName)
        # Sample 2
        filename = client.download_pipeline(
          package_name = "hello-world",
          tag = "v1")
        # Sample 3
        filename = client.download_pipeline(
          package_name = "hello-world",
          tag = "v1",
          file_name = "hello-world-template.yaml")

## Use the Artifact Registry REST API

The following sections summarize how to use the [Artifact Registry REST API](https://docs.cloud.google.com/artifact-registry/docs/reference/rest) to manage your pipeline templates in your Artifact Registry repository.

### Upload a pipeline template using the Artifact Registry REST API

You can upload a pipeline template by creating an HTTP request using the parameter values described in this section, where:

  - PROJECT\_ID is the Google Cloud project that this pipeline runs in.
  - REPO\_ID is the ID of your Artifact Registry repository.

#### Example curl request

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -F tags=v1,latest \
        -F content=@pipeline_spec.yaml \
        https://us-central1-kfp.pkg.dev/PROJECT_ID/REPO_ID

#### Constructing the upload request

The request is an HTTP or HTTPS multipart request. It must include the authentication token in the request header. For more information, see [gcloud auth print-access-token](https://docs.cloud.google.com/sdk/gcloud/reference/auth/print-access-token) .

The payload of the request is the contents of the `pipeline_spec.yaml` file (or .zip package). The recommended size limit is 10 MiB.

The package name is taken from the `pipeline_spec.pipeline_info.name` entry in the `pipeline_spec.yaml` file. The package name uniquely identifies the package and is immutable across versions. It can be between 4 and 128 characters long and must match the following regular expression: `^[a-z0-9][a-z0-9-]{3,127}$` .

The package `tags` are a list of up to eight comma-separated tags. Each tag must match the following regular expression: `^[a-zA-Z0-9\-._~:@+]{1,128}$` .

If a tag exists and points to a pipeline that's already been uploaded, the tag is updated to point to the pipeline that you're uploading. For example, if the `latest` tag points to a pipeline you've already uploaded, and you upload a new version with `--tag=latest` , the `latest` tag is removed from the previously uploaded pipeline and assigned to the new pipeline you're uploading.

If the pipeline you're uploading is identical to a pipeline you've previously uploaded, the upload succeeds. The uploaded pipeline's metadata, including its version tags, is updated to match the parameter values of your upload request.

#### Upload response

If the upload request succeeds, it returns an `HTTP OK` status. The body of the response is as follows:

    {packageName}/{versionName=sha256:abcdef123456...}

where `versionName` is the sha256 digest of `pipeline_spec.yaml` formatted as a hex string.

### Download a pipeline template using the Artifact Registry REST API

You can download a pipeline template by creating an HTTP request using the parameter values described in this section, where:

  - PROJECT\_ID is the Google Cloud project that this pipeline runs in.
  - REPO\_ID is the ID of your Artifact Registry repository.
  - PACKAGE\_ID is the package ID of your uploaded template.
  - TAG is the version tag.
  - VERSION is the template version in the format of `sha256:abcdef123456...` .

For standard Artifact Registry download, you should form the download link as follows:

    url = https://us-central1-kfp.pkg.dev/PROJECT_ID/REPO_ID/PACKAGE_ID/VERSION
    url = https://us-central1-kfp.pkg.dev/PROJECT_ID/REPO_ID/PACKAGE_ID/TAG

#### Example curl requests

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        https://us-central1-kfp.pkg.dev/PROJECT_ID/REPO_ID/PACKAGE_ID/VERSION

You can replace VERSION with TAG and download the same template, as shown in the following example:

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        https://us-central1-kfp.pkg.dev/PROJECT_ID/REPO_ID/PACKAGE_ID/TAG

#### Download response

If the download request succeeds, it returns an `HTTP OK` status. The body of the response is the contents of the `pipeline_spec.yaml` file.

## Reference links

  - [Artifact Registry - Repository overview](https://docs.cloud.google.com/artifact-registry/docs/repositories) for more information about how to manage your repositories.
  - [Repository API](https://docs.cloud.google.com/artifact-registry/docs/reference/rest/v1/projects.locations.repositories)
      - [format](https://docs.cloud.google.com/artifact-registry/docs/reference/rest/v1/projects.locations.repositories#format) keyword is "KFP"
  - [Package API](https://docs.cloud.google.com/artifact-registry/docs/reference/rest/v1/projects.locations.repositories.packages)
  - [Version API](https://docs.cloud.google.com/artifact-registry/docs/reference/rest/v1/projects.locations.repositories.packages.versions)
  - [Tag API](https://docs.cloud.google.com/artifact-registry/docs/reference/rest/v1/projects.locations.repositories.packages.tags)
  - [Proto definitions on GitHub](https://github.com/googleapis/googleapis/tree/master/google/devtools/artifactregistry/v1)
