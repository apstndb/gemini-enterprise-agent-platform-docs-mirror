---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-dataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-dataset
title: Create a Gemini Enterprise Agent Platform tabular dataset
description: Download a publicly available BigQuery dataset, then use it to create an Agent Platform tabular dataset, as part of a tutorial that shows you how to use the Agent Platform SDK for Python to create a custom-trained model.
data_source: docs.cloud.google.com
---

The model you create later in this tutorial requires a *dataset* to train it. The data that this tutorial uses is a publicly available dataset that contains details about three species of penguins. The following data are used to predict which of the three species a penguin is.

  - `island` - The island where a species of penguin is found.
  - `culmen_length_mm` - The length of the ridge along the top of the bill of a penguin.
  - `culmen_depth_mm` - The height of the bill of a penguin.
  - `flipper_length_mm` - The length of the flipper-like wing of a penguin.
  - `body_mass_g` - The mass of the body of a penguin.
  - `sex` - The sex of the penguin.

## Download, preprocess, and split the data

In this section, you download the publicly available BigQuery dataset and prepare its data. To prepare the data, you do the following:

  - Convert categorical features (features described with a string instead of a number) to numeric data. For example, you convert the names of the three types of penguins to the numerical values `0` , `1` , and `2` .

  - Remove any columns in the dataset that aren't used.

  - Remove any rows that cannot be used.

  - Split the data into two distinct sets of data. Each set of data is stored in a [pandas `DataFrame`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) object.
    
      - The `df_train` `DataFrame` contains data used to train your model.
    
      - the `df_for_prediction` `DataFrame` contains data used to generate predictions.

After processing the data, the code maps the three categorical columns' numerical values to their string values, then prints them so that you can see what the data looks like.

To download and process your data, run the following code in your notebook:

    import numpy as np
    import pandas as pd
    
    LABEL_COLUMN = "species"
    
    # Define the BigQuery source dataset
    BQ_SOURCE = "bigquery-public-data.ml_datasets.penguins"
    
    # Define NA values
    NA_VALUES = ["NA", "."]
    
    # Download a table
    table = bq_client.get_table(BQ_SOURCE)
    df = bq_client.list_rows(table).to_dataframe()
    
    # Drop unusable rows
    df = df.replace(to_replace=NA_VALUES, value=np.NaN).dropna()
    
    # Convert categorical columns to numeric
    df["island"], island_values = pd.factorize(df["island"])
    df["species"], species_values = pd.factorize(df["species"])
    df["sex"], sex_values = pd.factorize(df["sex"])
    
    # Split into a training and holdout dataset
    df_train = df.sample(frac=0.8, random_state=100)
    df_for_prediction = df[~df.index.isin(df_train.index)]
    
    # Map numeric values to string values
    index_to_island = dict(enumerate(island_values))
    index_to_species = dict(enumerate(species_values))
    index_to_sex = dict(enumerate(sex_values))
    
    # View the mapped island, species, and sex data
    print(index_to_island)
    print(index_to_species)
    print(index_to_sex)

The following are the printed mapped values for characteristics that are not numeric:

    {0: 'Dream', 1: 'Biscoe', 2: 'Torgersen'}
    {0: 'Adelie Penguin (Pygoscelis adeliae)', 1: 'Chinstrap penguin (Pygoscelis antarctica)', 2: 'Gentoo penguin (Pygoscelis papua)'}
    {0: 'FEMALE', 1: 'MALE'}

The first three values are the islands a penguin might inhabit. The second three values are important because they map to the predictions you receive at the end of this tutorial. The third row shows the `FEMALE` sex characteristic maps to `0` and the `MALE` the sex characteristic maps to `1` .

## Create a tabular dataset for training your model

In the previous step you downloaded and processed your data. In this step, you load the data stored in your `df_train` `DataFrame` into a BigQuery dataset. Then, you use the BigQuery dataset to create a Gemini Enterprise Agent Platform tabular dataset. This tabular dataset is used to train your model. For more information, see [Use managed datasets](https://docs.cloud.google.com/vertex-ai/docs/training/using-managed-datasets) .

### Create a BigQuery dataset

To create your BigQuery dataset that's used to create a Gemini Enterprise Agent Platform dataset, run the following code. The [`create_dataset`](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_create_dataset) command returns a new BigQuery [`DataSet`](https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dataset.Dataset) .

    # Create a BigQuery dataset
    bq_dataset_id = f"{project_id}.dataset_id_unique"
    bq_dataset = bigquery.Dataset(bq_dataset_id)
    bq_client.create_dataset(bq_dataset, exists_ok=True)

### Create a Gemini Enterprise Agent Platform tabular dataset

To convert your BigQuery dataset a Gemini Enterprise Agent Platform tabular dataset, run the following code. You can ignore the warning about the required number of rows to train using tabular data. Because the purpose of this tutorial is to quickly show you how to get predictions, a relatively small set of data is used to show you how to generate predictions. In a real world scenario, you want at least 1000 rows in a tabular dataset. The [`create_from_dataframe`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset#google_cloud_aiplatform_TabularDataset_create_from_dataframe) command returns a Gemini Enterprise Agent Platform [`TabularDataset`](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset#google_cloud_aiplatform_TabularDataset) .

    # Create an Agent Platform tabular dataset
    dataset = aiplatform.TabularDataset.create_from_dataframe(
        df_source=df_train,
        staging_path=f"bq://{bq_dataset_id}.table-unique",
        display_name="sample-penguins",
    )

You now have the Gemini Enterprise Agent Platform tabular dataset used to train your model.

## (Optional) View the public dataset in BigQuery

If you want to view the public data used in this tutorial, you can open it in BigQuery.

1.  In **Search** in the Google Cloud, enter BigQuery, then press return.

2.  In the search results, click on BigQuery

3.  In the **Explorer** window, expand **bigquery-public-data** .

4.  Under **bigquery-public-data** , expand **ml\_datasets** , then click **penguins** .

5.  Click any of the names under **Field name** to view that field's data.

![View penguin public dataset.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/images/penguin-public-dataset.png)
