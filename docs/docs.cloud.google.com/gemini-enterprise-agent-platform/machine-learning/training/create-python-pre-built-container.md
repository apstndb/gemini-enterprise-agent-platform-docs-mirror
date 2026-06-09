---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container
title: Create a Python training application for a prebuilt container
description: Create a Python source distribution that contains your training application, and upload it to a Cloud Storage bucket that your {{dynamic_data.site_values.cloud_name_short}} project can access.
data_source: docs.cloud.google.com
---

Before you can perform Gemini Enterprise Agent Platform serverless training with a prebuilt container, you must create a [Python source distribution](https://packaging.python.org/en/latest/overview/#python-source-distributions) that contains your training application and upload it to a Cloud Storage bucket that your Google Cloud project can access.

> **Note:** Agent Platform and the Google Cloud console sometimes refer to a source distribution as a "package," which is short for ["distribution package"](https://packaging.python.org/glossary/#term-Distribution-Package) . Each source distribution can contain one or more ["import packages"](https://packaging.python.org/glossary/#term-Import-Package) . This document uses the term "package" to refer to import packages.

## Alternatives to creating a source distribution

This guide walks through manually creating a source distribution and uploading it to Cloud Storage. Before you follow the guide, consider the following alternative workflows, which might be more convenient for some cases:

  - If you want to train using code on your local computer and reduce the amount of manual packaging work as much as possible, then we recommend that you use the Google Cloud CLI's *autopackaging* feature. This feature lets you build a Docker container image, push it to Artifact Registry, and create a `CustomJob` resource based on the container image, all with a single command. Learn more in the [guide to creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) .
    
    To use autopackaging, you must install Docker on your local computer. This option only lets you create a `CustomJob` , not a `TrainingPipeline` or `HyperparameterTuningJob` resource. (Learn about the [differences between serverless training resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods) .)

  - To further customize your container image and to run your code in a container locally before running it on Agent Platform, you can use the gcloud CLI's `local-run` command to [containerize your code and run it locally](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local) . Then you can manually [push the image to Artifact Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container#build-and-push-container) .
    
    To use the `local-run` command, you must install Docker on your local computer.

  - If you can write your training code in a single Python script, then you can use the [Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) 's [`CustomJob` class](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) to create a custom job or [`CustomTrainingJob` class](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) to create a [custom `TrainingPipeline`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) . Your training code is automatically packaged as a source distribution and uploaded to Cloud Storage.

  - For the most flexibility, you can manually [create a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) and push it to Artifact Registry.

If none of the preceding options fit your use case, or if you prefer to manually package your training application as a source distribution, follow the rest of this guide.

## Before you begin

Before preparing your training application to run in the cloud, complete the the following steps:

1.  Develop your training application using a machine learning (ML) framework available in one of Agent Platform's [prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) . Make sure that your training application meets the [training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) .
    
    If you are writing the training application from scratch, we recommend that you organize your code according to the [application structure](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container#structure) described in a following section of this document.

2.  [Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) in the same Google Cloud project where you plan to use Agent Platform. You will store your training application in this bucket. (While it is possible to use a bucket in a different Google Cloud bucket, this requires additional configuration outside the scope of this guide.)
    
    For the best performance, ensure that the Cloud Storage bucket is in the [location](https://docs.cloud.google.com/vertex-ai/docs/general/locations) where you plan to use Agent Platform.

3.  Know all of the Python libraries that your training application depends on, whether they're custom dependencies or freely available through [PyPI](https://pypi.python.org/pypi) .

## Application structure

When you perform serverless training using a prebuilt container, you must specify your training code according to the following requirements:

  - Provide the code as one or more Python source distributions.
    
    If you use the Agent Platform API to start serverless training, specify these in the [`packageUris` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec) .

  - Create a module in one of these source distributions that acts as the entrypoint for training.
    
    If you use the Agent Platform API to start custom training, specify this in the [`pythonModule` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec) .

As long as you meet these requirements, you can structure your training application in any way you like. However, we recommend that you build a single Python source distribution by organizing your code in the following structure (which is frequently used in Agent Platform samples):

  - Use a main project directory, containing your `setup.py` file. See the following section for guidance about this file's contents.

  - Within the main project directory, create a subdirectory named `trainer/` that serves as the main package for your training code.

  - Within `trainer/` , create a module named `task.py` that serves as the entrypoint for your training code.

  - To support `trainer/task.py` , create any additional Python modules that you want in the `trainer/` package, and create any additional subdirectories with that additional code that you want in the main project directory.

  - Create an [`__init__.py` file](https://docs.python.org/3/reference/import.html#regular-packages) in each subdirectory to make it a package.

The rest of this guide assumes that your code is organized according to this structure.

## Create a source distribution

Building Python source distributions is an expansive topic that is largely beyond the scope of this documentation. For convenience, this section provides an overview of using [Setuptools](https://setuptools.readthedocs.io/en/latest/) to build a source distribution to use with Agent Platform. There are other libraries you can use to do the same thing.

1.  Create a `setup.py` file that tells Setuptools how to create the source distribution. A basic `setup.py` includes the following:
    
      - Import statements for `setuptools.find_packages` and `setuptools.setup` .
    
      - A call to `setuptools.setup` with (at a minimum) these parameters set:
        
          - `name` set to the name of your source distribution.
        
          - `version` set to the version number of this build of your source distribution.
        
          - `install_requires` set to a list of dependencies that are required by your application, with version requirements, like `'docutils>=0.3'` .
        
          - `packages` set to `find_packages()` . This tells Setuptools to include all subdirectories of the parent directory that contain an `__init__.py` file as packages.
        
          - `include_package_data` set to `True` .
    
    The following example shows a basic `setup.py` file for a training application:
    
        from setuptools import find_packages
        from setuptools import setup
        
        setup(
            name='trainer',
            version='0.1',
            packages=find_packages(),
            include_package_data=True,
            description='My training application.'
        )

2.  Run the following command to create a source distribution, `dist/trainer-0.1.tar.gz` :
    
        python setup.py sdist --formats=gztar

### Python application dependencies

Dependencies are packages that you `import` in your code. Your application may have many dependencies that it needs to make it work.

For each replica in your serverless training job, your code runs in a container with many common Python dependencies already installed. Check the dependencies included in the [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that you plan to use for training and note any of your dependencies that are not already installed. You only need to complete the following steps for dependencies that are not already installed in the prebuilt container.

There are 2 types of dependencies that you may need to add:

  - *Standard* dependencies, which are common distribution packages available on [PyPI](https://pypi.python.org/pypi)
  - *Custom* dependencies, such as packages that you developed yourself, or those internal to an organization.

The following sections describe the procedure for each type.

#### Standard (PyPI) dependencies

You can specify your application's standard dependencies as part of its `setup.py` script. Agent Platform uses `pip` to install your training application on the replicas that it allocates for your job. The [`pip install`](https://pip.pypa.io/en/stable/user_guide/#installing-packages) command looks for configured dependencies and installs them.

The following example shows a `setup.py` similar to the one from a previous section. However, this `setup.py` tells Agent Platform to install `some_PyPI_package` when it installs the training application:

    from setuptools import find_packages
    from setuptools import setup
    
    REQUIRED_PACKAGES = ['some_PyPI_package>=1.0']
    
    setup(
        name='trainer',
        version='0.1',
        install_requires=REQUIRED_PACKAGES,
        packages=find_packages(),
        include_package_data=True,
        description='My training application.'
    )

#### Custom dependencies

You can specify your application's custom dependencies by passing their paths as part of your job configuration. You need the URI of the source distribution of each dependency. The custom dependencies must be in a Cloud Storage location. Agent Platform uses [`pip install`](https://pip.pypa.io/en/stable/user_guide/#installing-packages) to install custom dependencies, so they can have standard dependencies of their own in their `setup.py` scripts.

Each URI you include is the path to a source distribution, formatted as a tar file ( `.tar.gz` ) or as a wheel ( `.whl` ). Agent Platform installs each dependency using [`pip install`](https://pip.pypa.io/en/stable/user_guide/#installing-packages) on each replica that it allocates for your training job.

If you use the Agent Platform API to start serverless training, specify the Cloud Storage URIs to these dependencies along with your training application in the [`packageUris` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec) .

## Python modules

Your application can contain multiple modules (Python files). You must identify the module that contains your application entry point. The training service runs that module by invoking Python, just as you would run it locally.

For example, if you follow the recommended structure from a preceding section, your main module is `task.py` . Since it's inside an import package (directory with an `__init__.py` file) named `trainer` , the fully qualified name of this module is `trainer.task` . So if you use the Agent Platform API to start custom training, set the [`moduleName` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec) to `trainer.task` .

Refer to the [Python guide to packages](https://docs.python.org/3/tutorial/modules.html#packages) for more information about modules.

## Upload your source distribution to Cloud Storage

You can use the [gcloud CLI](https://docs.cloud.google.com/cli) to upload your source distribution and any custom dependencies to a Cloud Storage bucket. For example:

    gcloud storage cp dist/trainer-0.1.tar.gz CLOUD_STORAGE_DIRECTORY

Replace CLOUD\_STORAGE\_DIRECTORY with the URI (beginning with `gs://` and ending with `/` ) of a Cloud Storage directory in a bucket that your Google Cloud project can access.

To learn about other ways to upload your source distribution to Cloud Storage, read [Uploading objects](https://docs.cloud.google.com/storage/docs/uploading-objects) in the Cloud Storage documentation.

## What's next

  - Learn about additional [training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) for serverless training.
  - Learn how to [create a serverless training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) or a [serverless training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) that uses your training application.
