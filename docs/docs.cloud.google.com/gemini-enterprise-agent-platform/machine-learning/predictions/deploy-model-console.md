---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console
title: Deploy a model by using the Google Cloud console
description: Deploy a model to a public endpoint by using the {{dynamic_data.site_values.cloud_name_short}} console.
data_source: docs.cloud.google.com
---

In the Google Cloud console, you can create a [public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) and deploy a model to it.

Models can be deployed from the Online prediction page or the Model Registry page.

## Deploy a model from the Online prediction page

In the Online prediction page, you can create an endpoint and deploy one or more models to it as follows:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Online prediction** page.

2.  Click add **Create** .

3.  In the **New endpoint** pane:
    
    1.  Enter the **Endpoint name** .
    
    2.  Select **Standard** for the access type.
    
    3.  To create a dedicated (not shared) public endpoint, select the **Enable dedicated DNS** checkbox.
    
    4.  Click **Continue** .

4.  In the **Model settings** pane:
    
    1.  Select your model from the drop-down list.
    
    2.  Choose the model version from the drop-down list.
    
    3.  Enter the **Traffic split** percentage for the model.
    
    4.  Click **Done** .
    
    5.  Repeat these steps for any additional models to be deployed.

## Deploy a model from the Model Registry page

In the Model Registry page, you can deploy a model to one or more new or existing endpoints as follows:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  Click the name and version ID of the model you want to deploy to open its details page.

3.  Select the **Deploy & Test** tab.
    
    If your model is already deployed to any endpoints, they are listed in the **Deploy your model** section.

4.  Click **Deploy to endpoint** .

5.  To deploy your model to a new endpoint:
    
    1.  Select radio\_button\_checked **Create new endpoint**
    2.  Provide a name for the new endpoint.
    3.  To create a dedicated (not shared) public endpoint, select the **Enable dedicated DNS** checkbox.
    4.  Click **Continue** .
    
    To deploy your model to an existing endpoint:
    
    1.  Select radio\_button\_checked **Add to existing endpoint** .
    2.  Select the endpoint from the drop-down list.
    3.  Click **Continue** .
    
    You can deploy multiple models to an endpoint, or you can deploy the same model to multiple endpoints.

6.  If you deploy your model to an existing endpoint that has one or more models deployed to it, you must update the **Traffic split** percentage for the model you are deploying and the already deployed models so that all of the percentages add up to 100%.

7.  If you're deploying your model to a new endpoint, accept 100 for the **Traffic split** . Otherwise, adjust the traffic split values for all models on the endpoint so they add up to 100.

8.  Enter the **Minimum number of compute nodes** you want to provide for your model.
    
    This is the number of nodes that need to be available to the model at all times.
    
    You are charged for the nodes used, whether to handle inference load or for standby (minimum) nodes, even without inference traffic. See the [pricing page](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .
    
    The number of compute nodes can increase if needed to handle inference traffic, but it will never go higher than the maximum number of nodes.

9.  To use autoscaling, enter the **Maximum number of compute nodes** you want Agent Platform to scale up to.

10. Select your **Machine type** .
    
    Larger machine resources increase your inference performance and increase costs. [Compare the available machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine_type_comparison) .

11. Select an **Accelerator type** and an **Accelerator count** .
    
    If you enabled accelerator use when you [imported](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) or created the model, this option displays.
    
    For the accelerator count, refer to the [GPU table](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training%5Dconfigure-compute#gpus) to check for valid numbers of GPUs that you can use with each CPU machine type. The accelerator count refers to the number of accelerators per node, not the total number of accelerators in your deployment.

12. If you want to use a [custom service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account) for the deployment, select a service account in the **Service account** drop-down box.

13. Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .

14. Click **Done** for your model, and when all the **Traffic split** percentages are correct, click **Continue** .
    
    The region where your model deploys is displayed. This must be the region where you created your model.

15. Click **Deploy** to deploy your model to the endpoint.

## What's next

  - Learn how to [get an online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) .
  - Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .
