---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-environment
title: Manage the conda environment in your Agent Platform Workbench instance
description: Learn how to modify and delete the conda environment in your Agent Platform Workbench instance
data_source: docs.cloud.google.com
---

# Manage your conda environment

This page describes how to manage a conda environment in your Gemini Enterprise Agent Platform Workbench instance.

## Overview

If you've added a conda environment to your Agent Platform Workbench instance, it appears as a [kernel](https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html) in your instance's JupyterLab interface.

You might have added a conda environment to your instance to use a kernel that isn't available in a default Agent Platform Workbench instance. This page describes how to modify and delete that kernel.

## Open JupyterLab

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your Agent Platform Workbench instance's name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

## Modify a conda kernel

Gemini Enterprise Agent Platform Workbench instances come with pre-installed frameworks such as PyTorch and TensorFlow. If you need a different version, you can modify the libraries by using pip in the relevant conda environment.

For example, if you want to upgrade PyTorch:

    # Check the name of the conda environment for PyTorch
    conda env list
    
    # Activate the environment for PyTorch
    conda activate pytorch
    
    # Display the PyTorch version
    python -c "import torch; print(torch.__version__)"
    
    # Make sure to use pip from the conda environment for PyTorch
    # This should be `/opt/conda/envs/pytorch/bin/pip`
    which pip
    
    # Upgrade PyTorch
    pip install --upgrade torch

## Delete a conda kernel

Some conda packages add default kernels to your environment when the packages are installed. For example, when you install R, conda might also add a `python3` kernel. This can cause a duplication of kernels in your environment. To avoid duplicated kernels, delete the default kernel before you create a new kernel with the same name.

    rm -rf /opt/conda/envs/CONDA_ENVIRONMENT_NAME/share/jupyter/kernels/python3

## Troubleshoot

To diagnose and resolve issues related to managing a conda environment in your Agent Platform Workbench instance, see [Troubleshooting Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#instances) .

## What's next

  - Learn more about [conda](https://docs.conda.io/en/latest/) .
