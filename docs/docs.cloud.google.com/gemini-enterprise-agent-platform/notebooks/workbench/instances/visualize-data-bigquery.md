---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/visualize-data-bigquery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/visualize-data-bigquery
title: Explore and visualize data in BigQuery from within JupyterLab
description: Explore and visualize data that is stored in BigQuery from within the JupyterLab interface of a Agent Platform Workbench instance
data_source: docs.cloud.google.com
---

# Explore and visualize data in BigQuery from within JupyterLab

This page shows you some examples of how to explore and visualize data that is stored in BigQuery from within the JupyterLab interface of your Gemini Enterprise Agent Platform Workbench instance.

## Before you begin

If you haven't already, [create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart) .

### Required roles

To ensure that your instance's service account has the necessary permissions to query data in BigQuery, ask your administrator to grant the Service Usage Consumer ( [`roles/serviceusage.serviceUsageConsumer`](https://docs.cloud.google.com/service-usage/docs/access-control#predefined_roles) ) IAM role to your instance's service account on the project.

> **Important:** You must grant this role to your instance's service account, *not* to your user account. Failure to grant the role to the correct principal might result in permission errors.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give your instance's service account the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Open JupyterLab

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your Agent Platform Workbench instance's name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

## Read data from BigQuery

In the next two sections, you read data from BigQuery that you will use to visualize later. These steps are identical to those in [Query data in BigQuery from within JupyterLab](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/bigquery) , so if you've completed them already, you can skip to [Get a summary of data in a BigQuery table](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/visualize-data-bigquery#summary) .

### Query data by using the %%bigquery magic command

In this section, you write SQL directly in notebook cells and read data from BigQuery into the Python notebook.

Magic commands that use a single or double percentage character ( `%` or `%%` ) let you use minimal syntax to interact with BigQuery within the notebook. The BigQuery client library for Python is automatically installed in a Agent Platform Workbench instance. Behind the scenes, the `%%bigquery` magic command uses the BigQuery client library for Python to run the given query, convert the results to a pandas DataFrame, optionally save the results to a variable, and then display the results.

**Note** : As of version 1.26.0 of the `google-cloud-bigquery` Python package, the [BigQuery Storage API](https://docs.cloud.google.com/bigquery/docs/reference/storage) is used by default to download results from the `%%bigquery` magics.

1.  To open a notebook file, select **File \> New \> Notebook** .

2.  In the **Select Kernel** dialog, select **Python 3** , and then click **Select** .
    
    Your new IPYNB file opens.

3.  To get the number of regions by country in the `international_top_terms` dataset, enter the following statement:
    
        %%bigquery
        SELECT
          country_code,
          country_name,
          COUNT(DISTINCT region_code) AS num_regions
        FROM
          `bigquery-public-data.google_trends.international_top_terms`
        WHERE
          refresh_date = DATE_SUB(CURRENT_DATE, INTERVAL 1 DAY)
        GROUP BY
          country_code,
          country_name
        ORDER BY
          num_regions DESC;

4.  Click play\_circle\_filled **Run cell** .
    
    The output is similar to the following:
    
    ```console
    Query complete after 0.07s: 100%|██████████| 4/4 [00:00<00:00, 1440.60query/s]
    Downloading: 100%|██████████| 41/41 [00:02<00:00, 20.21rows/s]
    country_code      country_name    num_regions
    0   TR  Turkey         81
    1   TH  Thailand       77
    2   VN  Vietnam        63
    3   JP  Japan          47
    4   RO  Romania        42
    5   NG  Nigeria        37
    6   IN  India          36
    7   ID  Indonesia      34
    8   CO  Colombia       33
    9   MX  Mexico         32
    10  BR  Brazil         27
    11  EG  Egypt          27
    12  UA  Ukraine        27
    13  CH  Switzerland    26
    14  AR  Argentina      24
    15  FR  France         22
    16  SE  Sweden         21
    17  HU  Hungary        20
    18  IT  Italy          20
    19  PT  Portugal       20
    20  NO  Norway         19
    21  FI  Finland        18
    22  NZ  New Zealand    17
    23  PH  Philippines    17
    ...
    ```
    
    > **Note:** Your results might differ from what is above as the `google_trends` dataset being queried is refreshed with new data on an ongoing basis.

5.  In the next cell (below the output from the previous cell), enter the following command to run the same query, but this time save the results to a new pandas DataFrame that's named `regions_by_country` . You provide that name by using an argument with the `%%bigquery` magic command.
    
        %%bigquery regions_by_country
        SELECT
          country_code,
          country_name,
          COUNT(DISTINCT region_code) AS num_regions
        FROM
          `bigquery-public-data.google_trends.international_top_terms`
        WHERE
          refresh_date = DATE_SUB(CURRENT_DATE, INTERVAL 1 DAY)
        GROUP BY
          country_code, country_name
        ORDER BY
          num_regions DESC;
    
    **Note:** For more information about available arguments for the `%%bigquery` command, see the [client library magics documentation](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/magics) .

6.  Click play\_circle\_filled **Run cell** .

7.  In the next cell, enter the following command to look at the first few rows of the query results that you just read in:
    
        regions_by_country.head()

8.  Click play\_circle\_filled **Run cell** .
    
    The pandas DataFrame `regions_by_country` is ready to plot.

### Query data by using the BigQuery client library directly

In this section, you use the BigQuery client library for Python directly to read data into the Python notebook.

The client library gives you more control over your queries and lets you use more complex configurations for queries and jobs. The library's integrations with pandas enable you to combine the power of declarative SQL with imperative code (Python) to help you analyze, visualize, and transform your data.

**Note:** You can use a number of Python data analysis, data wrangling, and visualization libraries, such as `numpy` , `pandas` , `matplotlib` , and many others. Several of these libraries are built on top of a DataFrame object.

1.  In the next cell, enter the following Python code to import the BigQuery client library for Python and initialize a client:
    
        from google.cloud import bigquery
        
        client = bigquery.Client()
    
    The BigQuery client is used to send and receive messages from the BigQuery API.

2.  Click play\_circle\_filled **Run cell** .

3.  In the next cell, enter the following code to retrieve the percentage of daily top terms in the US [`top_terms`](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_trends&t=top_terms&page=table) that overlap across time by number of days apart. The idea here is to look at each day's top terms and see what percentage of them overlap with the top terms from the day before, 2 days prior, 3 days prior, and so on (for all pairs of dates over about a month span).
    
        sql = """
        WITH
          TopTermsByDate AS (
            SELECT DISTINCT refresh_date AS date, term
            FROM `bigquery-public-data.google_trends.top_terms`
          ),
          DistinctDates AS (
            SELECT DISTINCT date
            FROM TopTermsByDate
          )
        SELECT
          DATE_DIFF(Dates2.date, Date1Terms.date, DAY)
            AS days_apart,
          COUNT(DISTINCT (Dates2.date || Date1Terms.date))
            AS num_date_pairs,
          COUNT(Date1Terms.term) AS num_date1_terms,
          SUM(IF(Date2Terms.term IS NOT NULL, 1, 0))
            AS overlap_terms,
          SAFE_DIVIDE(
            SUM(IF(Date2Terms.term IS NOT NULL, 1, 0)),
            COUNT(Date1Terms.term)
            ) AS pct_overlap_terms
        FROM
          TopTermsByDate AS Date1Terms
        CROSS JOIN
          DistinctDates AS Dates2
        LEFT JOIN
          TopTermsByDate AS Date2Terms
          ON
            Dates2.date = Date2Terms.date
            AND Date1Terms.term = Date2Terms.term
        WHERE
          Date1Terms.date <= Dates2.date
        GROUP BY
          days_apart
        
        ORDER BY
          days_apart;
        """
        pct_overlap_terms_by_days_apart = client.query(sql).to_dataframe()
        
        pct_overlap_terms_by_days_apart.head()
    
    The SQL being used is encapsulated in a Python string and then passed to the [`query()` method](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client#google_cloud_bigquery_client_Client_query) to run a query. The [`to_dataframe` method](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJob#google_cloud_bigquery_job_QueryJob_to_dataframe) waits for the query to finish and downloads the results to a pandas DataFrame by using the BigQuery Storage API.

4.  Click play\_circle\_filled **Run cell** .
    
    The first few rows of query results appear below the code cell.
    
    ```console
       days_apart   num_date_pairs  num_date1_terms overlap_terms   pct_overlap_terms
     0          0             32               800            800            1.000000
     1          1             31               775            203            0.261935
     2          2             30               750             73            0.097333
     3          3             29               725             31            0.042759
     4          4             28               700             23            0.032857
    ```
    
    > **Note:** Your results might differ from what is above as the `google_trends` dataset being queried is refreshed with new data on an ongoing basis.

For more information about using BigQuery client libraries, see the quickstart [Using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) .

## Get a summary of data in a BigQuery table

In this section, you use a notebook shortcut to get summary statistics and visualizations for all fields of a BigQuery table. This can be a fast way to profile your data before exploring further.

The BigQuery client library provides a magic command, `%bigquery_stats` , that you can call with a specific table name to provide an overview of the table and detailed statistics on each of the table's columns.

1.  In the next cell, enter the following code to run that analysis on the US [`top_terms` table](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_trends&t=top_terms&page=table) :
    
        %bigquery_stats bigquery-public-data.google_trends.top_terms

2.  Click play\_circle\_filled **Run cell** .
    
    After running for some time, an image appears with various statistics on each of the 7 variables in the `top_terms` table. The following image shows part of some example output:
    
    ![International top terms overview of statistics.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/jupyter-overview-of-statistics.png)

> **Note:** Your results might differ from what is above as the `google_trends` dataset being queried is refreshed with new data on an ongoing basis.

## Visualize BigQuery data

In this section, you use plotting capabilities to visualize the results from the queries that you previously ran in your Jupyter notebook.

1.  In the next cell, enter the following code to use the pandas `DataFrame.plot()` method to create a bar chart that visualizes the results of the query that returns the number of regions by country:
    
        regions_by_country.plot(kind="bar", x="country_name", y="num_regions", figsize=(15, 10))

2.  Click play\_circle\_filled **Run cell** .
    
    The chart is similar to the following:
    
    ![International top terms country results](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/jupyter-trends-country-name.png)

3.  In the next cell, enter the following code to use the pandas `DataFrame.plot()` method to create a scatter plot that visualizes the results from the query for the percentage of overlap in the top search terms by days apart:
    
        pct_overlap_terms_by_days_apart.plot(
          kind="scatter",
          x="days_apart",
          y="pct_overlap_terms",
          s=len(pct_overlap_terms_by_days_apart["num_date_pairs"]) * 20,
          figsize=(15, 10)
          )

4.  Click play\_circle\_filled **Run cell** .
    
    The chart is similar to the following. The size of each point reflects the number of date pairs that are that many days apart in the data. For example, there are more pairs that are 1 day apart than 30 days apart because the top search terms are surfaced daily over about a month's time.
    
    ![International top terms days apart chart.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/jupyter-chart-of-terms-v-days.png)

For more information about data visualization, see the [pandas documentation](https://pandas.pydata.org/pandas-docs/stable/visualization.html) .

## What's next

> To see an example of exploring and visualizing BigQuery data as part of a comprehensive workflow in Agent Platform Workbench, run the "Interactive exploratory analysis of BigQuery data in a notebook" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/exploratory_data_analysis/explore_data_in_bigquery_with_workbench.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fexploratory_data_analysis%2Fexplore_data_in_bigquery_with_workbench.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fexploratory_data_analysis%2Fexplore_data_in_bigquery_with_workbench.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/exploratory_data_analysis/explore_data_in_bigquery_with_workbench.ipynb)
