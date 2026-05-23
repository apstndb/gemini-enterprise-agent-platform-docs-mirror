---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/make-prediction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/make-prediction
title: Make an inference
description: Use a model to create inferences to complete a tutorial that shows you how to use the Agent Platform SDK for Python to create and deploy a custom-trained model.
data_source: docs.cloud.google.com
---

You're now ready to use the test data in `df_for_prediction` to make an inference request. The inference request invokes your model to predict what species of penguin is represented by the penguin characteristics in each row in `df_for_prediction` .

## Prepare inference test data

Before you can use the test data to create inferences, you remove the `species` column. Because the species of penguin is what you're predicting, it can't be included in the test data used to create an inference. After you remove the `species` column, you convert the data to a Python list because that's what the `predict` method takes as input. Run the following code convert your data to a Python list:

    # Remove the species column
    df_for_prediction.pop(LABEL_COLUMN)
    
    # Convert data to a Python list
    test_data_list = df_for_prediction.values.tolist()

## (Optional) View test data

To help you understand the test data, you can run the following line of code to view it:

    test_data_list

In each row, the respective values in each of the six columns refer to the following characteristics of one penguin:

| Column | Penguin characteristic                                                                                                                                |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0      | `island` - The island where a species of penguin is found. The island value mapping is `0` for `Dream` , `1` for `Biscoe` , and `2` for `Torgersen` . |
| 1      | `culmen_length_mm` - The length of the ridge along the top of the bill of a penguin.                                                                  |
| 2      | `culmen_depth_mm` - The height of the bill of a penguin.                                                                                              |
| 3      | `flipper_length_mm` - The length of the flipper-like wing of a penguin.                                                                               |
| 4      | `body_mass_g` - The mass of the body of a pen.                                                                                                        |
| 5      | `sex` - The sex of the penguin. `0` is `FEMALE` and `1` is `MALE` .                                                                                   |

## Send the inference request

To create an inference request, pass the Python list of test data you created to the `endpoint` 's [`predict`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_predict) method.

The `predict` method evaluates the characteristics in each row and uses them to predict what kind of penguin they represent. Run the following code to create your inferences. The returned inferences contain a list of rows, where each row has three columns ( *Adelie Penguin (Pygoscelis adeliae)* (column 1), *Chinstrap penguin (Pygoscelis antarctica)* (column 2), or *Gentoo penguin (Pygoscelis papua)* (column 3)).

    # Get your inferences.
    predictions = endpoint.predict(instances=test_data_list)
    
    # View the inferences
    predictions.predictions

Each column in a row contains a value, and the higher the value, the greater the confidence that the species of the penguin represented by that column is a correct inference. For example, in the following sample inference output row, the model uses the characteristics of the sample penguin data row to predict that the penguin is most likely of the *Adelie Penguin (Pygoscelis adeliae)* species. This is because the highest value, `0.732703805` , is in the first column.

`[0.732703805, 0.233752429, 0.0335437432]`

In the following code, the NumPy `argmax` method returns the column for each row that contains the highest value. The highest value corresponds to the inference that is most likely correct. The second line displays the array of inferences.

    # Get the inference for each set of input data.
    species_predictions = np.argmax(predictions.predictions, axis=1)
    
    # View the best inference for the penguin characteristics in each row.
    species_predictions

Each result in the `species_predictions` array predicts which penguin species the values in the corresponding row of test data corresponds to. For example, the first value is `0` , which maps to the *Adelie Penguin (Pygoscelis adeliae)* species. This means that your model predicts that the species of a penguin with the characteristics in the first row of your test data is *Adelie Penguin (Pygoscelis adeliae)* .

## Clean up resources

Now that you're done, you can continue to use your notebook to explore and learn more about the resources you created and how they work.

### Delete your resources

When you're ready, we recommend that you delete the Google Cloud resources you created during this tutorial so that you don't incur unnecessary charges. There are two ways to delete your resources:

  - Delete your project, which also deletes all the resources associated with your project. For more information, see [Shutting down (deleting) projects](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects) .

  - Run code that deletes your training job (a `CustomTrainingJob` object), model (a `Model` object), endpoint (an `Endpoint` object), and Cloud Storage bucket. This option retains your project and any other resources you might have created that you don't explicitly delete with your code.
    
    You must undeploy your model before you can delete it by passing `force=True` to the [`endpoint.delete`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_delete) method.
    
    To retain your project and delete only resources you created during this tutorial, run the following code in your notebook:

<!-- end list -->

    import os
    
    # Delete the training job
    job.delete()
    
    # Delete the endpoint and undeploy the model from it
    endpoint.delete(force=True)
    
    # Delete the model
    model.delete()
    
    # Delete the storage bucket and its contents
    bucket.delete(force=True)

### Delete your Vertex AI Workbench instance

You can keep your Vertex AI Workbench instance to use for future work. If you keep it, make sure you are aware of its cost. For more information, see [Vertex AI Workbench pricing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing#notebooks) .

If you want to delete the Vertex AI Workbench instance, do the following:

1.  In the Google Cloud console, go to the Vertex AI Workbench **Instances** page.

2.  Select your Vertex AI Workbench instance.

3.  In the upper menu, click delete **Delete** .

4.  In the **Delete instance** confirmation dialog, click **Confirm** . It takes a few minutes for the deletion to complete.
