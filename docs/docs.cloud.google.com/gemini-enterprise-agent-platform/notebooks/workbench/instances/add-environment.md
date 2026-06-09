---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/add-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/add-environment
title: Add a conda environment to a Vertex AI Workbench instance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to add a conda environment to your Vertex AI Workbench instance.

## Overview

When you add a conda environment to your Vertex AI Workbench instance, it appears as a [kernel](https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html) in your instance's JupyterLab interface.

You might add a conda environment to your Vertex AI Workbench instance to use kernels that aren't available in Vertex AI Workbench instances. For example, you can add conda environments for R and Apache Beam. Or you can add conda environments for specific earlier versions of the available frameworks, such as TensorFlow, PyTorch, or Python.

## Before you begin

If you haven't already, [create a Vertex AI Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart) .

## Open JupyterLab

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your Vertex AI Workbench instance's name, click **Open JupyterLab** .
    
    Your Vertex AI Workbench instance opens JupyterLab.

## Add a conda environment

You can add a conda environment by entering commands in your instance's JupyterLab terminal.

1.  In JupyterLab, select **File \> New \> Terminal** .

2.  In the **Terminal** window, enter the following commands:
    
        # Creates a conda environment.
        conda create -n CONDA_ENVIRONMENT_NAME -y
        conda activate CONDA_ENVIRONMENT_NAME
        
        # Install packages using a pip local to the conda environment.
        conda install pip
        pip install PACKAGE
        pip install ipykernel
        
        # Adds the conda kernel.
        DL_ANACONDA_ENV_HOME="${DL_ANACONDA_HOME}/envs/CONDA_ENVIRONMENT_NAME"
        python -m ipykernel install --prefix "${DL_ANACONDA_ENV_HOME}" --name CONDA_ENVIRONMENT_NAME --display-name KERNEL_DISPLAY_NAME
    
    Replace the following:
    
      - `  CONDA_ENVIRONMENT_NAME  ` : your choice of name for the environment
      - `  PACKAGE  ` : the package that you want to install
      - `  KERNEL_DISPLAY_NAME  ` : the display name for the tile of the kernel in the JupyterLab interface

3.  A default kernel can be created when installing to a given conda environment. You can remove the default kernel with the following command:
    
        rm -rf "/opt/micromamba/envs/CONDA_ENVIRONMENT_NAME/share/jupyter/kernels/python3

4.  To see your new kernel, do the following:
    
    1.  Refresh the page.
    
    2.  Select **File \> New Launcher** .
    
    The kernel is listed among the others in the **Launcher** window.

By default, conda might use pip packages in the system `pip` folder (for example, `/usr/bin/pip` ). Running `conda install pip` ensures that the setup uses a pip local to the environment.

## Example installation: R Essentials

The following example installs R Essentials in a conda environment named `r` .

    conda create -n r
    conda activate r
    conda install -c r r-essentials

## Example installation: pip package

The following example installs pip packages from a `requirements.txt` file.

    conda create -n myenv
    conda activate myenv
    conda install pip
    pip install -r requirements.txt
    pip install ipykernel
    DL_ANACONDA_ENV_HOME="${DL_ANACONDA_HOME}/envs/myenv"
    python -m ipykernel install --prefix "${DL_ANACONDA_ENV_HOME}" --name myenv --display-name myenv

## Troubleshoot

To diagnose and resolve issues related to adding a conda environment, see [Troubleshooting Vertex AI Workbench](https://docs.cloud.google.com/vertex-ai/docs/general/troubleshooting-workbench#pip-packages-missing-instances) .

## What's next

  - Learn more about [conda](https://docs.conda.io/en/latest/) .

  - To modify your conda environment, see [Manage your conda environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-environment) .
