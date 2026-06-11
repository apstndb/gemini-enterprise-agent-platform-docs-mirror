---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console
title: Train an AutoML Edge model using the Google Cloud console
description: Use the {{dynamic_data.site_values.cloud_name_short}} console to train an AutoML Edge model.
data_source: docs.cloud.google.com
---

You create an AutoML Edge (exportable) model directly in the UI for certain data types, or by starting a training pipeline job [programmatically](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api) . You create this model using a prepared dataset. Create this dataset in the Google Cloud console or using the [API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-api) . Agent Platform API uses the items from the dataset to train the model, test it, and evaluate model performance. Review the evaluations results, adjust the training dataset as needed, and create a new training job using the improved dataset.

Training jobs can take several hours to complete. The Agent Platform page of the Google Cloud console shows the status of training.

## Training an AutoML Edge model

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  Click the name of the dataset you want to use to train your model to open its details page.

3.  If your data type uses annotation sets, select the annotation set you want to use for this model.

4.  Click **Train new model** .

5.  In the **Train new model** page, complete the following steps:
    
    1.  Select radio\_button\_checked **AutoML Edge** for the training method and click **Continue** .
    
    2.  Enter the display name for your new model.
    
    3.  If you want manually set how your training data is split, expand *Advanced options* \* and select a data split option. For more information, see [About data splits for AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use) .
    
    4.  Click **Continue** .
    
    5.  Select the optimization goal that best suits your need. You can optimize for accuracy, latency, or both.
    
    6.  Click **Continue** .
    
    7.  In the **Compute and pricing** window, enter the maximum number of hours you want your model to train for.
        
        This setting helps you put a cap on the training costs. The actual time elapsed can be longer than this value, because there are other operations involved in creating a new model.

6.  If you want to stop training when the model is no longer improving, select **Enable early stopping** .

7.  Click **Start Training** .
    
    Model training can take many hours, depending on your training budget (image only) and the size and complexity of your data. You can close this tab and return to it later. You will receive an email when your model has completed training.

## What's next

  - [Evaluate AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#automl) .
  - [Export AutoML Edge models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-edge-model) .
