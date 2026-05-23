---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/undeploy-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/undeploy-model
title: Undeploy a model and delete the endpoint
description: Undeploy a model and delete the endpoint in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Use one of the following methods to undeploy a model and delete the endpoint.

> **Note:** You can only delete the endpoint after all models have been undeployed from it.

### Google Cloud console

1.  Undeploy the model as follows:
    
    1.  In the Google Cloud console, in the Agent Platform section, go to the **Endpoints** page.
    
    2.  Click the name and version ID of the model you want to undeploy to open its details page.
    
    3.  On the row for your model, click more\_vert **Actions** , and then click **Undeploy model from endpoint** .
    
    4.  In the **Undeploy model from endpoint** dialog, click **Undeploy** .
    
    5.  To delete additional models, repeat the preceding steps.

2.  Optional: Delete the online inference endpoint as follows:
    
    1.  In the Google Cloud console, in the **Gemini Enterprise Agent Platform** section, go to the **Online prediction** page.
    
    2.  Select the endpoint.
    
    3.  To delete the endpoint, click more\_vert **Actions** , and then click **Delete endpoint** .

### gcloud

1.  List the endpoint IDs for all endpoints in your project:
    
        gcloud ai endpoints list \
            --project=PROJECT_ID \
            --region=LOCATION_ID
    
    Replace PROJECT\_ID with your project name and LOCATION\_ID with the region where you are using Gemini Enterprise Agent Platform.

2.  List the model IDs for the models that are deployed to an endpoint:
    
        gcloud ai endpoints describe ENDPOINT_ID \
            --project=PROJECT_ID \
            --region=LOCATION_ID
    
    Replace ENDPOINT\_ID with the endpoint ID.

3.  Undeploy a model from the endpoint:
    
        gcloud ai endpoints undeploy-model ENDPOINT_ID \
            --project=PROJECT_ID \
            --region=LOCATION_ID \
            --deployed-model-id=DEPLOYED_MODEL_ID
    
    Replace DEPLOYED\_MODEL\_ID with the model ID.

4.  Optional: Delete the online inference endpoint:
    
        gcloud ai endpoints delete ENDPOINT_ID \
            --project=PROJECT_ID \
            --region=LOCATION_ID
