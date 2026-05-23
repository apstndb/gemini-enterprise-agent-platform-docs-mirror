---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local
title: Containerize and run training code locally
description: Build a Docker container image based on your training code and run the image as a container on your local computer.
data_source: docs.cloud.google.com
---

You can use the [`gcloud ai custom-jobs local-run` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/local-run) to build a Docker container image based on your training code and run the image as a container on your local computer. This feature offers several benefits:

  - You can build a container image with minimal knowledge of Docker. You don't need to write your own Dockerfile. You can later push this image to [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/docker) and use it for [custom container training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) .
    
    For advanced use cases, you might still want to [write your own Dockerfile](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

  - Your container image can run a Python training application or a Bash script.
    
    You can use a Bash script to run training code written in another programming language (as long as you also specify a base container image that supports the other language).

  - Running a container locally executes your training code in a similar way to how it runs on Agent Platform.
    
    Running your code locally can help you debug problems with your code before you perform serverless training on Agent Platform.

## Before you begin

1.  [Set up your Agent Platform development environment.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment)

2.  [Install Docker Engine.](https://docs.docker.com/engine/install/)

3.  If you are using Linux, [configure Docker so you can run it without `sudo`](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user) .
    
    The `local-run` command requires this configuration in order to use Docker.

## Use the `local-run` command

Run the following command to build a container image based on your training code and run a container locally:

    gcloud ai custom-jobs local-run \
      --executor-image-uri=BASE_IMAGE_URI \
      --local-package-path=WORKING_DIRECTORY \
      --script=SCRIPT_PATH \
      --output-image-uri=OUTPUT_IMAGE_NAME

Replace the following:

  - BASE\_IMAGE\_URI : The URI of a Docker image to use as the base of the container. Choose a base image that includes dependencies required for your training code.
    
    You can use the URI to a [prebuilt training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) image or any other value that would be valid for a [Dockerfile `FROM` instruction](https://docs.docker.com/engine/reference/builder/#from) ; for example, a publicly available Docker image or a Docker image in [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/docker) that you have access to.

  - WORKING\_DIRECTORY : The lowest-level directory in your file system that contains all your training code and local dependencies that you need to use for training.
    
    By default, the command only copies the parent directory of the file specified by the `--script` flag (see the following list item) into the resulting Docker image. The Docker image does *not* necessarily include all the files within WORKING\_DIRECTORY ; to customize which files get included, see the section in this document about [including dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#dependencies) .
    
    If you omit the `--local-package-path` flag (and this placeholder), then the `local-run` command uses the current working directory for this value.

  - SCRIPT\_PATH : The path, relative to WORKING\_DIRECTORY on your local file system, to the script that is the entry point for your training code. This can be a Python script (ending in `.py` ) or a Bash script.
    
    For example, if you want to run `/hello-world/trainer/task.py` and WORKING\_DIRECTORY is `/hello-world` , then use `trainer/task.py` for this value.
    
    If you specify a Python script, then your base image must have Python installed, and if you specify a bash script, then your base image must have Bash installed. (All prebuilt training containers and many other publicly available Docker images include both of these dependencies.)
    
    #### Use `--python-module` instead of `--script`
    
    If you omit the `--script` flag (and SCRIPT\_PATH ), then you must instead use the `--python-module` flag to specify the name of a Python module in WORKING\_DIRECTORY to run as the entry point for training. For example, instead of `--script=trainer/task.py` , you might specify `--python-module=trainer.task` .
    
    In this case, the resulting Docker container [loads your code as a module](https://docs.python.org/3/using/cmdline.html#cmdoption-m) rather than as a script. You likely want to use this option if your entry point script imports other Python modules in WORKING\_DIRECTORY .

  - OUTPUT\_IMAGE\_NAME : A name for the resulting Docker image built by the command. You can use any value that is accepted by [`docker build` 's `-t` flag](https://docs.docker.com/engine/reference/commandline/build/#tag-an-image--t) .
    
    If you plan to later push the image to Artifact Registry, then you might want to use [an image name that meets the Artifact Registry requirements](https://docs.cloud.google.com/artifact-registry/docs/docker/pushing-and-pulling#tag) . (Alternatively, you can tag the image with additional names later).
    
    If you omit the `--output-image-uri` flag (and this placeholder), then the `local-run` command tags the image with a name based on the current time and the filename of your entry point script.

The command builds a Docker container image based on your configuration. After building the image, the command prints the following output:

    A training image is built.
    Starting to run ...

The command then immediately uses this container image to run a container on your local computer. When the container exits, the command prints the following output:

    A local run is finished successfully using custom image: OUTPUT_IMAGE_NAME

## Additional options

The following sections describe additional options that you can use to customize the behavior of the `local-run` command.

### Install dependencies

Your training code can rely on any dependencies installed on your base image (for example, [prebuilt training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) images include many Python libraries for machine learning), as well as any files that you include in the Docker image created by the `local-run` command.

When you specify a script with the `--script` flag or the `--python-module` flag, the command copies the script's parent directory (and its subdirectories) into the Docker image. For example, if you specify `--local-package-path=/hello-world` and `--script=trainer/task.py` , then the command copies `/hello-world/trainer/` into the Docker image.

You can also include additional Python dependencies or arbitrary files from your file system by completing the extra steps described in one of the following sections:

  - [Using a `requirements.txt` file for Python dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#requirements)
  - [Using a `setup.py` file for Python dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#setup)
  - [Specifying individual PyPI dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#pypi)
  - [Specifying local Python dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#local-dependencies)
  - [Including other files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#other-files)

#### Install additional Python dependencies

You can include additional Python dependencies in the Docker image in several ways:

##### Use a `requirements.txt` file

If there is a file named `requirements.txt` in the working directory, then the `local-run` command treats this as a [pip requirements file](https://pip.pypa.io/en/stable/user_guide/#requirements-files) and uses it to install Python dependencies in the Docker image.

##### Use a `setup.py` file

If there is a file named `setup.py` in the working directory, then the `local-run` command treats this as a [Python `setup.py` file](https://packaging.python.org/guides/distributing-packages-using-setuptools/#setup-py) , copies the file to the Docker image, and runs `pip install` on the directory in the Docker image that contains this file.

You can, for example, add an [`install_requires` argument](https://packaging.python.org/guides/distributing-packages-using-setuptools/#install-requires) to `setup.py` in order to install Python dependencies in the Docker image.

##### Specify individual PyPI dependencies

You can use the `--requirements` flag to install specific dependencies from [PyPI](https://pypi.org/) in the Docker image. For example:

    gcloud ai custom-jobs local-run \
      --executor-image-uri=BASE_IMAGE_URI \
      --local-package-path=WORKING_DIRECTORY \
      --script=SCRIPT_PATH \
      --output-image-uri=OUTPUT_IMAGE_NAME \
      --requirements=REQUIREMENTS

Replace REQUIREMENTS with a comma-separated list of [Python requirement specifiers](https://pip.pypa.io/en/stable/cli/pip_install/#requirement-specifiers) .

##### Specify additional local Python dependencies

You can use the `--extra-packages` flag to install specific local Python dependencies. These Python dependencies must be under the working directory, and each dependency must be in a format that [`pip install`](https://pip.pypa.io/en/stable/cli/pip_install) supports; for example, a [wheel file](https://pip.pypa.io/en/stable/user_guide/#installing-from-wheels) or a [Python source distribution](https://packaging.python.org/en/latest/overview/#python-source-distributions) .

For example:

    gcloud ai custom-jobs local-run \
      --executor-image-uri=BASE_IMAGE_URI \
      --local-package-path=WORKING_DIRECTORY \
      --script=SCRIPT_PATH \
      --output-image-uri=OUTPUT_IMAGE_NAME \
      --extra-packages=LOCAL_DEPENDENCIES

Replace LOCAL\_DEPENDENCIES with a comma-separated list of local file paths, expressed relative to the working directory.

#### Include other files

To copy additional directories to the Docker image (without installing them as Python dependencies), you can use the `--extra-dirs` flag. You may only specify directories under the working directory. For example:

    gcloud ai custom-jobs local-run \
      --executor-image-uri=BASE_IMAGE_URI \
      --local-package-path=WORKING_DIRECTORY \
      --script=SCRIPT_PATH \
      --output-image-uri=OUTPUT_IMAGE_NAME \
      --extra-dirs=EXTRA_DIRECTORIES

Replace EXTRA\_DIRECTORIES with a comma-separated list of local directories, expressed relative to the working directory.

### Training application arguments

If the entry point script for your training application expects command-line arguments, you can specify these when you run the `local-run` command. These arguments do not get saved in the Docker image; rathern they get passed as arguments when the image runs as a container.

To pass arguments to your entry point script, pass the `--` argument followed by your script's arguments to the `local-run` command after all the command's other flags.

For example, imagine a script that you run locally with the following command:

    python /hello-world/trainer/task.py \
      --learning_rate=0.1 \
      --input_data=gs://BUCKET/small-dataset/

When you use the `local-run` command, you can use the following flags to run the script in the container with the same arguments:

    gcloud ai custom-jobs local-run \\
      --executor-image-uri=BASE_IMAGE_URI \
      --local-package-path=/hello-world \
      --script=/trainer/task.py \
      --output-image-uri=OUTPUT_IMAGE_NAME \
      -- \
      --learning_rate=0.1 \
      --input_data=gs://BUCKET/small-dataset/

### Accelerate model training with GPUs

If you want to eventually deploy the Docker image created by the `local-run` command to Agent Platform and [use GPUs for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) , then make sure to [write training code that takes advantage of GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#gpus) and use a GPU-enabled Docker image for the value of the `--executor-image-uri` flag. For example, you can use one of the [prebuilt training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) images that supports GPUs.

If your local computer runs Linux and has GPUs, you can also configure the `local-run` command to use your GPUs when it runs a container locally. This is optional, but it can be useful if you want to test how your training code works with GPUs. Do the following:

1.  [Install the NVIDIA Container Toolkit ( `nvidia-docker` )](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#setting-up-nvidia-container-toolkit) on your local computer, if you haven't already.

2.  Specify the `--gpu` flag when you run the `local-run` command. For example:
    
        gcloud ai custom-jobs local-run \
          --executor-image-uri=BASE_IMAGE_URI \
          --local-package-path=WORKING_DIRECTORY \
          --script=SCRIPT_PATH \
          --output-image-uri=OUTPUT_IMAGE_NAME \
          --gpu

### Specify a custom service account

By default, when the `local-run` command runs your training code in a local container, it mounts the Google Cloud credentials available in your local environment through [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication#adc) into the container, so that your training code can use ADC for authentication with the same credentials. In other words, the credentials available by ADC in your local shell are also available by ADC to your code when you run the `local-run` command.

You can use the [`gcloud auth application-default login` command](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) to use your user account for ADC, or you can [set an environment variable in your shell to use a service account for ADC](https://docs.cloud.google.com/docs/authentication/production#passing_variable) .

If you want the container to run with Google Cloud credentials other than those available by ADC in your local shell, do the following:

1.  [Create or select a service account](https://docs.cloud.google.com/iam/docs/creating-managing-service-accounts) with the permissions you want your training code to have access to.

2.  [Download a service account key](https://docs.cloud.google.com/iam/docs/creating-managing-service-account-keys) for this service account to your local computer.

3.  When you run the `local-run` command, specify the `--service-account-key-file` flag. For example:
    
        gcloud ai custom-jobs local-run \
          --executor-image-uri=BASE_IMAGE_URI \
          --local-package-path=WORKING_DIRECTORY \
          --script=SCRIPT_PATH \
          --output-image-uri=OUTPUT_IMAGE_NAME \
          --service-account-key-file=KEY_PATH
    
    Replace KEY\_PATH with the path to the service account key in your local file system. This must be absolute or relative to the current working directory of your shell, *not* relative to the directory specified by the `--local-package-path` flag.

In the resulting container, your training code can use ADC to authenticate with the specified Service Account Credentials.

#### Comparison to training on Agent Platform

When you perform serverless training on Agent Platform, Agent Platform uses the [Gemini Enterprise Agent Platform Custom Code Service Agent for your project](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) by default to run your code. You can also [attach a different service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account) for serverless training.

When you use the `local-run` command, you can't authenticate as the Gemini Enterprise Agent Platform Custom Code Service Agent, but you can create a service account with similar permissions and use it locally.

## What's next

  - Learn about [requirements for your training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) .

  - Learn how to [push your Docker image to Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/docker/pushing-and-pulling) and [use it as a custom container for training on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) .
