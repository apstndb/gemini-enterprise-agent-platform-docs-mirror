---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/shut-down
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/shut-down
title: Shut down a Agent Platform Workbench instance
description: Learn how to shut down a Agent Platform Workbench instance
data_source: docs.cloud.google.com
---

# Shut down a Agent Platform Workbench instance

To stop any processing for a Agent Platform Workbench instance, you can shut down the instance.

You incur costs for running an instance, in addition to other potential costs (see [Pricing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing#notebooks) ). To stop incurring costs for running an instance, shut down the instance. You continue to incur other potential costs.

To shut down a Agent Platform Workbench instance, complete the following steps:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Select the instance that you want to open.

3.  Click **Open JupyterLab** .
    
    It is important to stop all running processes in case there are operations that need to complete before you shut down your Agent Platform Workbench instance, for example, I/O processes that are writing to disk.
    
    To stop all running processes:
    
    1.  To show all of the processes that are running, select the ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-running-terminals.png) **Running Terminals and Kernels** tab.
    
    2.  Next to each running process, click **Shutdown all** .

4.  Close the browser tab or window for your Agent Platform Workbench instance.

5.  In the Google Cloud console, return to the **Instances** page.

6.  Select the instance that you want to shut down, and then click square **Stop** .
