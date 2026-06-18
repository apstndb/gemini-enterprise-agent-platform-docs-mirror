---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container
title: Create a Agent Platform Workbench instance using a custom container
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to create a Gemini Enterprise Agent Platform Workbench instance based on a custom container.

## Overview

Agent Platform Workbench instances support using a custom container derived from one of the Google-provided base containers. You can modify these base containers to make a custom container image and use these custom containers to create a Agent Platform Workbench instance.

The base containers are configured with a [Container-Optimized OS](https://docs.cloud.google.com/container-optimized-os/docs/concepts/features-and-benefits) in the host virtual machine (VM). The host image is built from the `cos-stable` [image family](https://docs.cloud.google.com/container-optimized-os/docs/concepts/versioning#choosing_the_right_version) .

## Limitations

Consider the following limitations when planning your project:

  - <span id="derivative"></span> The custom container must be derived from a [Google-provided base container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#base-containers) . Using a container that isn't derived from a base container increases the risk of compatibility issues and limits our ability to support your usage of Agent Platform Workbench instances.

  - Use of more than one container with a Agent Platform Workbench instance isn't supported.

  - The VM hosting the custom container is running off of a [Container-Optimized OS](https://docs.cloud.google.com/container-optimized-os/docs/concepts/features-and-benefits) , which restricts how you can interact with the host machine. For example, Container-Optimized OS doesn't include a package manager. This means that packages acting on the host must be performed on a container with mounts.

  - Agent Platform Workbench instances uses `nerdctl` (a containerd CLI) for running the custom container. This is required for compatibility with the Image streaming service. Any container parameters that are added using a metadata value need to adhere to what is supported by `nerdctl` .

  - Agent Platform Workbench instances are configured to pull either from Artifact Registry or a public container repository. To configure an instance to pull from a private repository, you must manually configure the credentials used by the containerd.

## Base containers

### Standard base container

The standard base container supports all Agent Platform Workbench features and includes the following:

  - Pre-installed [data science packages](https://docs.cloud.google.com/deep-learning-vm/docs/introduction#pre-installed_packages) .
  - [Cuda libraries](https://hub.docker.com/r/nvidia/cuda) similar to [Deep Learning Containers](https://docs.cloud.google.com/deep-learning-containers/docs/overview) .
  - Google Cloud JupyterLab integrations such as the [Managed Service for Apache Spark](https://docs.cloud.google.com/dataproc-serverless/docs/quickstarts/jupyterlab-sessions) and [BigQuery](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/bigquery) integrations.
  - Common system packages such as `curl` or `git` .
  - Metadata-based JupyterLab configuration.
  - Micromamba-based kernel management.

### Specifications

The standard base container has the following specifications:

  - Base image: `nvidia/cuda:12.6.1-cudnn-devel-ubuntu24.04`
  - Image size: Approximately 22 GB
  - URI: `us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container:latest`

### Slim base container

The slim base container provides a minimal set of configurations that permit a proxy connection to the instance. Standard Agent Platform Workbench features and packages aren't included, except for the following:

  - JupyterLab
  - Metadata-based JupyterLab configuration
  - Micromamba-based kernel management

Additional packages or JupyterLab extensions must be installed and managed independently.

### Specifications

The slim base container has the following specifications:

  - Base image: `marketplace.gcr.io/google/ubuntu24.04`
  - Image size: Approximately 2 GB
  - URI: `us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container-slim:latest`

## Before you begin

### Required roles

To get the permissions that you need to create a Agent Platform Workbench instance with a custom container, ask your administrator to grant you the following IAM roles:

  - [Notebooks Runner](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.runner) ( `roles/notebooks.runner` ) on the user account
  - To pull images from the Artifact Registry repository: [Artifact Registry Reader](https://docs.cloud.google.com/iam/docs/roles-permissions/artifactregistry#artifactregistry.reader) ( `roles/artifactregistry.reader` ) on the service account

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a custom container

To create a custom container for use with Agent Platform Workbench instances:

1.  Create a derivative container derived from a [Google-provided base container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#base-containers) .

2.  Build and push the container to Artifact Registry. You'll use the container's URI when you create your Agent Platform Workbench instance. For example, the URI might look like this: ` gcr.io/ PROJECT_ID / IMAGE_NAME  ` .

## Create the instance

You can create a Agent Platform Workbench instance based on a custom container by using the Google Cloud console or the Google Cloud CLI.

### Console

To create a Agent Platform Workbench instance based on a custom container, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Environment** section, select **Use custom container** .

5.  For **Docker container image** , click **Select** .

6.  In the **Select container image** dialog, navigate to the container image that you want to use, and then click **Select** .

7.  Optional. For **Post-startup script** , enter a path to a post-startup script that you want to use.

8.  Optional. Add metadata for your instance. To learn more, see [Custom container metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#metadata) .

9.  Optional. In the **Networking section** , customize your network settings. To learn more, see [Network configuration options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#network-options) .

10. Complete the rest of the instance creation dialog, and then click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

### gcloud

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance; must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where you want your instance to be located
  - `  CUSTOM_CONTAINER_PATH  ` : the path to the container image repository, for example: ` gcr.io/ PROJECT_ID / IMAGE_NAME  `
  - `  METADATA  ` : custom metadata to apply to this instance; for example, to specify a post-startup-script, you can use the `post-startup-script` metadata tag, in the format: `"--metadata=post-startup-script=gs:// BUCKET_NAME /hello.sh"`

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --container-repository=CUSTOM_CONTAINER_URL \
        --container-tag=latest \
        --metadata=METADATA

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --container-repository=CUSTOM_CONTAINER_URL `
        --container-tag=latest `
        --metadata=METADATA

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --container-repository=CUSTOM_CONTAINER_URL ^
        --container-tag=latest ^
        --metadata=METADATA

For more information about the command for creating an instance from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/create) .

Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

## Network configuration options

In addition to the [general network options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#network-options) , a Agent Platform Workbench instance with a custom container must have access to the Artifact Registry service.

If you have turned off public IP access for your VPC, ensure that you have enabled Private Google Access.

## Enable Image streaming

The custom container host is provisioned to interact with Image streaming in Google Kubernetes Engine (GKE), which pulls containers faster and reduces initialization time for large containers once they are cached in the GKE remote file system.

To view the requirements for enabling Image streaming, see [Requirements](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/image-streaming#requirements) . Often, Image streaming can be used with Agent Platform Workbench instances by enabling the Container File System API.

### How the host VM runs the custom container

Instead of using Docker to run the custom container, the host VM uses `nerdctl` under the Kubernetes namespace to load and run the container. This lets Agent Platform Workbench use Image streaming for custom containers.

    # Runs the custom container.
    sudo /var/lib/google/nerdctl/nerdctl --snapshotter=gcfs -n k8s.io run --name payload-container

## Example installation: custom container with a custom default kernel

The following example shows how to create a new kernel with a pip package pre-installed.

1.  Create a new custom container:
    
        FROM us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container:latest
        
        ENV MAMBA_ROOT_PREFIX=/opt/micromamba
        
        RUN micromamba create -n ENVIRONMENT_NAME -c conda-forge python=PYTHON_VERSION -y
        
        SHELL ["micromamba", "run", "-n", "ENVIRONMENT_NAME", "/bin/bash", "-c"]
        
        RUN micromamba install -c conda-forge pip -y
        RUN pip install PACKAGE
        RUN pip install ipykernel
        RUN python -m ipykernel install --prefix /opt/micromamba/envs/ENVIRONMENT_NAME --name ENVIRONMENT_NAME --display-name KERNEL_NAME
        # Creation of a micromamba kernel automatically creates a python3 kernel
        # that must be removed if it's in conflict with the new kernel.
        RUN rm -rf "/opt/micromamba/envs/ENVIRONMENT_NAME/share/jupyter/kernels/python3"

2.  Add the new container to Artifact Registry:
    
        gcloud auth configure-docker REGION-docker.pkg.dev
        docker build -t REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY_NAME/IMAGE_NAME .
        docker push REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY_NAME/IMAGE_NAME:latest

3.  Create an instance:
    
        gcloud workbench instances create INSTANCE_NAME  \
            --project=PROJECT_ID \
            --location=ZONE \
            --container-repository=REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY_NAME/IMAGE_NAME \
            --container-tag=latest

## Persistent kernels for custom containers

Agent Platform Workbench custom containers only mount a data disk to the ` /home/ USER  ` directory within each container, where `jupyter` is the default user. This means that any change outside of ` /home/ USER  ` is ephemeral and won't persist after a restart. If you need installed packages to persist for a specific kernel, you can create a kernel in the ` /home/ USER  ` directory.

> **Note:** Base containers are configured with a mount point on ` /home/ USER  ` . To create a persistent kernel when building a custom image, you must enable Docker BuildKit. See [Notes about specifying volumes](https://docs.docker.com/reference/dockerfile/#notes-about-specifying-volumes) . To learn more about BuildKit, see the [BuildKit documentation](https://docs.docker.com/build/buildkit/) .

To create a kernel in the ` /home/ USER  ` directory:

1.  Create a micromamba environment:
    
        micromamba create -p /home/USER/ENVIRONMENT_NAME -c conda-forge python=3.11 -y
        micromamba activate /home/USER/ENVIRONMENT_NAME
        pip install ipykernel
        pip install -r ~/requirement.txt
        python -m ipykernel install --prefix "/home/USER/ENVIRONMENT_NAME" --display-name "Example Kernel"
    
    Replace the following:
    
      - USER : the user directory name, which is `jupyter` by default
      - ENVIRONMENT\_NAME : the name of the environment
      - PYTHON\_VERSION : the Python version, for example `3.11`

2.  Wait 30 seconds to 1 minute for the kernels to refresh.

## Updating the startup of the base container

The base container for a Agent Platform Workbench instance ( `us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container:latest` ) starts JupyterLab by running `/run_jupyter.sh` .

If you modify the container's startup in a derivative container, you must append `/run_jupyter.sh` to run the default configuration of JupyterLab.

The following is an example of how the Dockerfile might be modified:

    # DockerFile
    FROM us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container:latest
    
    CP startup_file.sh /
    # Ensure that you have the correct permissions and startup is executable.
    RUN chmod 755 /startup_file.sh && \
        chown jupyter:jupyter /startup_file.sh
    
    # Override the existing CMD directive from the base container.
    CMD ["/startup_file.sh"]

    # /startup_file.sh
    
    echo "Running startup scripts"
    ...
    
    /run_jupyter.sh

## Updating the JupyterLab Configuration within the base container

If you need to modify the JupyterLab configuration on the base container you must do the following:

  - Ensure that JupyterLab is configured to port 8080. Our proxy agent is configured to forward any request to port 8080 and if the jupyter server isn't listening to the correct port, the instance encounters provisioning issues.

  - Modify JupyterLab packages under the `jupyterlab` micromamba environment. We provide a separate package environment to run JupyterLab and its plugin to ensure that there aren't any dependency conflicts with the kernel environment. If you want to install an additional JupyterLab extension, you must install it within the `jupyterlab` environment. For example:
    
        # DockerFile
        FROM us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container:latest
        RUN micromamba activate jupyterlab && \
          jupyter nbextension install nbdime

## Custom Container Metadata

In addition to the standard list of [metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata) that can be applied to a Gemini Enterprise Agent Platform Workbench instance, instances with custom containers include the following metadata for managing the instantiation of the payload container:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Description</th>
<th>Metadata key</th>
<th>Accepted values and defaults</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Enables Cloud Storage FUSE on a container image</td>
<td><p>Mounts <code dir="ltr" translate="no">/dev/fuse</code> onto the container and enables <code dir="ltr" translate="no">gcsfuse</code> for use on the container.</p></td>
<td><code dir="ltr" translate="no">container-allow-fuse</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Enables Cloud Storage FUSE.</li>
<li><code dir="ltr" translate="no">false</code> (default): Doesn't enable Cloud Storage FUSE.</li>
</ul></td>
</tr>
<tr class="even">
<td>Additional container run parameters</td>
<td><p>Appends additional container parameters to <code dir="ltr" translate="no">nerdctl run</code> , where <code dir="ltr" translate="no">nerdctl</code> is the Containerd CLI.</p></td>
<td><code dir="ltr" translate="no">container-custom-params</code></td>
<td><p>A string of container run parameters. Example: <code dir="ltr" translate="no">--v /mnt/disk1:/mnt/disk1</code> .</p></td>
</tr>
<tr class="odd">
<td>Additional container environment flags</td>
<td><p>Stores Environment variables into a flag under <code dir="ltr" translate="no">/mnt/stateful_partition/workbench/container_env</code> and appends it to <code dir="ltr" translate="no">nerdctl run</code> .</p></td>
<td><code dir="ltr" translate="no">container-env-file</code></td>
<td><p>A string of container environment variables. Example: <code dir="ltr" translate="no">CONTAINER_NAME=derivative-container</code> .</p></td>
</tr>
</tbody>
</table>

## Upgrade a Custom Container

When your instance starts for the first time, it pulls the container image from a URI stored in the `custom-container-payload` metadata. If you use the `:latest` tag, the container is updated at every restart. The `custom-container-payload` metadata value can't be modified directly because it's a [protected metadata key](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata#protected) .

To update your instance's custom container image, you can use the following methods supported by the Google Cloud CLI, Terraform, or the Notebooks API.

### gcloud

You can update the custom container image metadata on a Agent Platform Workbench instance by using the following command:

    gcloud workbench instances update INSTANCE_NAME \
        --container-repository=CONTAINER_URI \
        --container-tag=CONTAINER_TAG

### Terraform

You can change the `container_image` field in the terraform configuration to update the container payload.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

    resource "google_workbench_instance" "default" {
      name     = "workbench-instance-example"
      location = "us-central1-a"
    
      gce_setup {
        machine_type = "n1-standard-1"
        container_image {
          repository = "us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container"
          family  = "latest"
        }
      }
    }

### Notebooks API

Use the [`instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method with changes to `gce_setup.container_image.repository` and `gce_setup.container_image.tag` in the `updateMask` .

## Run the diagnostic tool

The diagnostic tool checks and verifies the status of various Agent Platform Workbench services. To learn more, see [Tasks performed by the diagnostic tool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health#tasks_performed_by_the_diagnostic_tool) .

When you create a Agent Platform Workbench instance using a custom container, the diagnostic tool isn't available as a script in the host environment that users can run. Instead, it is compiled into a binary and loaded onto a Google runtime container that is built to run diagnostic services in a Container-Optimized OS environment. See [Container-Optimized OS Overview](https://docs.cloud.google.com/container-optimized-os/docs/concepts/features-and-benefits) .

To run the diagnostic tool, complete the following steps:

1.  [Use ssh to connect to your Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/ssh-access) .

2.  In the SSH terminal, run the following command:
    
        sudo docker exec diagnostic-service ./diagnostic_tool

3.  To view additional command options, run the following command:
    
        sudo docker exec diagnostic-service ./diagnostic_tool --help

For more information about the diagnostic tool's options, see the [monitoring health status documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health#run_the_diagnostic_tool) .

To run the diagnostic tool by using the REST API, see the [REST API documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/diagnose) .

## Access your instance

You can access your instance through a proxy URL.

After your instance has been created and is active, you can get the proxy URL by using the gcloud CLI.

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance
  - `  PROJECT_ID  ` : your project ID
  - `  LOCATION  ` : the zone where your instance is located

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances describe INSTANCE_NAME \
    --project=PROJECT_ID \
    --location=LOCATION | grep proxy-url

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances describe INSTANCE_NAME `
    --project=PROJECT_ID `
    --location=LOCATION | grep proxy-url

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances describe INSTANCE_NAME ^
    --project=PROJECT_ID ^
    --location=LOCATION | grep proxy-url

    proxy-url: 7109d1b0d5f850f-dot-datalab-vm-staging.googleusercontent.com

The `describe` command returns your proxy URL. To access your instance, open the proxy URL in a web browser.

For more information about the command for describing an instance from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/describe) .
