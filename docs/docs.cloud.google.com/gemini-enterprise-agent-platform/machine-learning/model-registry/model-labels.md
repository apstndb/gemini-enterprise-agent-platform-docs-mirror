---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-labels
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-labels
title: Apply model labels
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

From the Gemini Enterprise Agent Platform Model Registry landing page, you can see all your models and default model versions in a single view. Adding labels can help you identify and organize your models by lightweight key identifiers. You can add labels at the model level and also at the version level.

Labels can't begin with `vertex-ai-` or `goog-` .

### Console

Use the following instructions to add a label to a model.

1.  In the Google Cloud console, go to the **Model Registry** page.  
2.  From the Gemini Enterprise Agent Platform Model Registry, locate the name of the model you want to label. Select the **More actions** menu more\_vert for the specific model.
3.  From the drop-down, select **Edit labels** .
4.  Click the **Add label** action button and add your key and value. For example, the key can represent a value like **created\_by** and the value can be **datascientist1** .
5.  Click **Save** .

Add a label to a model version

1.  In the Google Cloud console, go to the **Model Registry** page.  
2.  From the Gemini Enterprise Agent Platform Model Registry, select the name of the model which has the version you want to label. The model details page opens.
3.  Select the **More actions** menu more\_vert for the specific model version you want to label.
4.  Click **Edit labels** . Enter the name of the new label you want to apply to the model version.
5.  Click **Save** .
