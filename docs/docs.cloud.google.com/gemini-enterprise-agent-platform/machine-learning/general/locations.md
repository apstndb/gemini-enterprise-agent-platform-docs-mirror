---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations
title: Locations for machine learning services
description: Learn about the available locations and accelerators for Agent Platform machine learning services.
data_source: docs.cloud.google.com
---

Support for Gemini Enterprise Agent Platform machine learning features varies by region. This page lists the availability of specific features across different [regions](https://cloud.google.com/about/locations) . Google stores and processes your data only in the region that you specify for all features of Agent Platform except for data labeling tasks and any feature in [experimental or preview launch status](https://cloud.google.com/products#product-launch-stages) .

To see where Google and partner models and generative AI features are supported, see [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .

To see supported locations for agents, see [Supported locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .

## Choosing your location

You can choose any supported location when you [create a dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview) , [train a custom-trained model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) that doesn't use a managed dataset, or when you [import an existing model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) . You should typically use the region closest to your physical location or the physical location of your intended users, but check that the Agent Platform feature you want to use is [supported in your region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) . Agent Platform doesn't support a global location.

For operations other than creating a dataset or importing a model, you must use the location of the resources you are operating on. For example, when you create a training pipeline that uses a managed dataset, you must use the region where the dataset is located.

### Specifying the location using Google Cloud console

When you use Google Cloud console, you specify the location by using the location drop-down menu:

![locations drop-down menu](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/general/images/location-dropdown.png)

### Specifying the location using the Agent Platform API

You specify the location for a Agent Platform API request by using the appropriate locational endpoint.

For example, to make a request in the `europe-west4` region, use the following endpoint:

    https://europe-west4-aiplatform.googleapis.com

To make a request in the `us-central1` region, use the following endpoint:

    https://us-central1-aiplatform.googleapis.com

When you specify a resource, you use the name of the resource's region as the location. For example, a dataset in the `us-central1` region would be specified using the following path:

` projects/ PROJECT /locations/ us-central1 /datasets/ DATASET_ID  `

See the [list of supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#service-endpoint) .

## Available locations for machine learning services

Agent Platform machine learning services are available in the following regions:

### United States

  - Columbus, Ohio ( `us-east5` )
  - Dallas, Texas ( `us-south1` )
  - Iowa ( `us-central1` )
  - Las Vegas, Nevada ( `us-west4` )
  - Los Angeles, California ( `us-west2` )
  - Moncks Corner, South Carolina ( `us-east1` )
  - Northern Virginia ( `us-east4` )
  - Oregon ( `us-west1` )
  - Salt Lake City, Utah ( `us-west3` )

### Canada

  - Montréal ( `northamerica-northeast1` )
  - Toronto ( `northamerica-northeast2` )

### South America

  - Santiago, Chile ( `southamerica-west1` )
  - São Paulo, Brazil ( `southamerica-east1` )

### Africa

  - Johannesburg, South Africa ( `africa-south1` )

### Europe

  - Belgium ( `europe-west1` )
  - Finland ( `europe-north1` )
  - Frankfurt, Germany ( `europe-west3` )
  - London, United Kingdom ( `europe-west2` )
  - Madrid, Spain ( `europe-southwest1` )
  - Milan, Italy ( `europe-west8` )
  - Netherlands ( `europe-west4` )
  - Paris, France ( `europe-west9` )
  - Turin, Italy ( `europe-west12` )
  - Warsaw, Poland ( `europe-central2` )
  - Zürich, Switzerland ( `europe-west6` )

### Asia Pacific

  - Hong Kong, China ( `asia-east2` )
  - Jakarta, Indonesia ( `asia-southeast2` )
  - Melbourne, Australia ( `australia-southeast2` )
  - Mumbai, India ( `asia-south1` )
  - Delhi, India ( `asia-south2` )
  - Osaka, Japan ( `asia-northeast2` )
  - Seoul, Korea ( `asia-northeast3` )
  - Singapore ( `asia-southeast1` )
  - Sydney, Australia ( `australia-southeast1` )
  - Taiwan ( `asia-east1` )
  - Tokyo, Japan ( `asia-northeast1` )

### Middle East

  - Dammam, Saudi Arabia ( `me-central2` )
  - Doha, Qatar ( `me-central1` )
  - Tel Aviv ( `me-west1` )

Google Cloud also provides [additional regions](https://cloud.google.com/about/locations) for products other than Agent Platform.

### Feature availability

Some Agent Platform features aren't available in all regions. The following table lists the features that are available in each region.

> Locations for some Agent Platform components are listed separately. See the following:
> 
>   - [Colab Enterprise locations](https://docs.cloud.google.com/colab/docs/locations)
>   - [Agent Platform Workbench locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#workbench-locations)

The following sortable table lets you select different options to see where Agent Platform features are available. For example, to see a list of regions where Agent Platform Feature Store is available in Europe, you can select **Europe** from the **Select a location** drop-down menu, and **Agent Platform Feature Store** from the **Select a feature** drop-down menu.

Africa Asia Pacific Europe Middle East North America South America AutoML for image data AutoML for tabular data AutoML Forecasting Custom model batch inference Custom model online inference Custom model training Data labeling Model Monitoring Model Registry Agent Platform Neural Architecture Search Ray on Agent Platform Vector Search Agent Runtime Gemini Enterprise Agent Platform Experiments Agent Platform Feature Store Gemini Enterprise Agent Platform Pipelines Vertex AI TensorBoard Agent Platform Vizier Vertex Explainable AI Agent Platform ML Metadata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Region</th>
<th>Location</th>
<th>Features</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-east1</code><br />
</td>
<td>Changhua County, Taiwan, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Data labeling</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">africa-south1</code><br />
</td>
<td>Johannesburg, South Africa, Africa</td>
<td><ul>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-east2</code><br />
</td>
<td>Hong Kong, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-northeast1</code><br />
</td>
<td>Tokyo, Japan, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-northeast2</code><br />
</td>
<td>Osaka, Japan, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-northeast3</code><br />
</td>
<td>Seoul, South Korea, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-south1</code><br />
</td>
<td>Mumbai, India, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-southeast1</code><br />
</td>
<td>Jurong West, Singapore, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-southeast2</code><br />
</td>
<td>Jakarta, Indonesia, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">australia-southeast1</code><br />
</td>
<td>Sydney, Australia, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">australia-southeast2</code><br />
</td>
<td>Melbourne, Australia, Asia Pacific</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-central2</code><br />
</td>
<td>Warsaw, Poland, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-north1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Hamina, Finland, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-southwest1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Madrid, Spain, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>St. Ghislain, Belgium, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west2</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>London, England, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Data labeling</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west3</code><br />
</td>
<td>Frankfurt, Germany, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Data labeling</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west4</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Eemshaven, Netherlands, Europe</td>
<td><ul>
<li>AutoML for image data</li>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Data labeling</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west6</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Zürich, Switzerland, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west8</code><br />
</td>
<td>Milan, Italy, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west9</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Paris, France, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west12</code><br />
</td>
<td>Turin, Italy, Europe</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">me-central1</code><br />
</td>
<td>Doha, Qatar, Middle East</td>
<td><ul>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">me-central2</code><br />
</td>
<td>Damman, Saudi Arabia, Middle East</td>
<td><ul>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">me-west1</code><br />
</td>
<td>Tel Aviv, Israel, Middle East</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">northamerica-northeast1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Montréal, Québec, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">northamerica-northeast2</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Toronto, Ontario, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">southamerica-east1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Osasco, São Paulo, Brazil, South America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">southamerica-west1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Santiago, Chile, South America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-central1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Council Bluffs, Iowa, North America</td>
<td><ul>
<li>AutoML for image data</li>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Data labeling</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-east1</code><br />
</td>
<td>Moncks Corner, South Carolina, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-east4</code><br />
</td>
<td>Ashburn, Virginia, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-east5</code><br />
</td>
<td>Columbus, Ohio, North America</td>
<td><ul>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-south1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Dallas, Texas, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-west1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>The Dalles, Oregon, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Neural Architecture Search</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-west2</code><br />
</td>
<td>Los Angeles, California, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-west3</code><br />
</td>
<td>Salt Lake City, Utah, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>AutoML Forecasting</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-west4</code><br />
</td>
<td>Las Vegas, Nevada, North America</td>
<td><ul>
<li>AutoML for tabular data</li>
<li>Custom model batch inference</li>
<li>Custom model online inference</li>
<li>Custom model training</li>
<li>Model Monitoring</li>
<li>Model Registry</li>
<li>Vector Search</li>
<li>Gemini Enterprise Agent Platform Experiments</li>
<li>Gemini Enterprise Agent Platform Pipelines</li>
<li>Vertex AI TensorBoard</li>
<li>Agent Platform Vizier</li>
<li>Vertex Explainable AI</li>
</ul></td>
</tr>
</tbody>
</table>

\* Cells marked with asterisks represent regions where the service is available through the Agent Platform API but not in the Google Cloud console.

### Agent Platform Workbench locations

Agent Platform Workbench instances are available in the following zones.

Asia Pacific Europe Middle East North America South America

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Region</th>
<th>Location</th>
<th>Zones</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-east1</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Changhua County, Taiwan, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-east1-a</code><br />
<code dir="ltr" translate="no">asia-east1-b</code><br />
<code dir="ltr" translate="no">asia-east1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-east2</code><br />
</td>
<td>Hong Kong, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-east2-a</code><br />
<code dir="ltr" translate="no">asia-east2-b</code><br />
<code dir="ltr" translate="no">asia-east2-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-northeast1</code><br />
</td>
<td>Tokyo, Japan, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-northeast1-a</code><br />
<code dir="ltr" translate="no">asia-northeast1-b</code><br />
<code dir="ltr" translate="no">asia-northeast1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-northeast3</code><br />
</td>
<td>Seoul, South Korea, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-northeast3-a</code><br />
<code dir="ltr" translate="no">asia-northeast3-b</code><br />
<code dir="ltr" translate="no">asia-northeast3-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-south1</code><br />
</td>
<td>Mumbai, India, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-south1-a</code><br />
<code dir="ltr" translate="no">asia-south1-b</code><br />
<code dir="ltr" translate="no">asia-south1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-south2</code><br />
</td>
<td>Delhi, India, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-south2-a</code><br />
<code dir="ltr" translate="no">asia-south2-b</code><br />
<code dir="ltr" translate="no">asia-south2-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">asia-southeast1</code><br />
</td>
<td>Jurong West, Singapore, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-southeast1-a</code><br />
<code dir="ltr" translate="no">asia-southeast1-b</code><br />
<code dir="ltr" translate="no">asia-southeast1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">asia-southeast2</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Jakarta, Indonesia, Asia Pacific</td>
<td><code dir="ltr" translate="no">asia-southeast2-a</code><br />
<code dir="ltr" translate="no">asia-southeast2-b</code><br />
<code dir="ltr" translate="no">asia-southeast2-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">australia-southeast1</code><br />
</td>
<td>Sydney, Australia, Asia Pacific</td>
<td><code dir="ltr" translate="no">australia-southeast1-a</code><br />
<code dir="ltr" translate="no">australia-southeast1-b</code><br />
<code dir="ltr" translate="no">australia-southeast1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-central2</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Warsaw, Poland, Europe</td>
<td><code dir="ltr" translate="no">europe-central2-a</code><br />
<code dir="ltr" translate="no">europe-central2-b</code><br />
<code dir="ltr" translate="no">europe-central2-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>St. Ghislain, Belgium, Europe</td>
<td><code dir="ltr" translate="no">europe-west1-b</code><br />
<code dir="ltr" translate="no">europe-west1-c</code><br />
<code dir="ltr" translate="no">europe-west1-d</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west2</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>London, England, Europe</td>
<td><code dir="ltr" translate="no">europe-west2-a</code><br />
<code dir="ltr" translate="no">europe-west2-b</code><br />
<code dir="ltr" translate="no">europe-west2-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west3</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Frankfurt, Germany, Europe</td>
<td><code dir="ltr" translate="no">europe-west3-a</code><br />
<code dir="ltr" translate="no">europe-west3-b</code><br />
<code dir="ltr" translate="no">europe-west3-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west4</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-second-footnote">†</a><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Eemshaven, Netherlands, Europe</td>
<td><code dir="ltr" translate="no">europe-west4-a</code><br />
<code dir="ltr" translate="no">europe-west4-b</code><br />
<code dir="ltr" translate="no">europe-west4-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">europe-west6</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Zürich, Switzerland, Europe</td>
<td><code dir="ltr" translate="no">europe-west6-a</code><br />
<code dir="ltr" translate="no">europe-west6-b</code><br />
<code dir="ltr" translate="no">europe-west6-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">europe-west12</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Turin, Italy, Europe</td>
<td><code dir="ltr" translate="no">europe-west12-a</code><br />
<code dir="ltr" translate="no">europe-west12-b</code><br />
<code dir="ltr" translate="no">europe-west12-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">me-central1</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Doha, Qatar, Middle East</td>
<td><code dir="ltr" translate="no">me-central1-a</code><br />
<code dir="ltr" translate="no">me-central1-b</code><br />
<code dir="ltr" translate="no">me-central1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">me-central2</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Dammam, Saudi Arabia, Middle East</td>
<td><code dir="ltr" translate="no">me-central2-a</code><br />
<code dir="ltr" translate="no">me-central2-b</code><br />
<code dir="ltr" translate="no">me-central2-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">me-west1</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Tel Aviv, Israel, Middle East</td>
<td><code dir="ltr" translate="no">me-west1-a</code><br />
<code dir="ltr" translate="no">me-west1-b</code><br />
<code dir="ltr" translate="no">me-west1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">northamerica-northeast1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Montréal, Québec, North America</td>
<td><code dir="ltr" translate="no">northamerica-northeast1-a</code><br />
<code dir="ltr" translate="no">northamerica-northeast1-b</code><br />
<code dir="ltr" translate="no">northamerica-northeast1-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">northamerica-northeast2</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Toronto, Ontario, North America</td>
<td><code dir="ltr" translate="no">northamerica-northeast2-a</code><br />
<code dir="ltr" translate="no">northamerica-northeast2-b</code><br />
<code dir="ltr" translate="no">northamerica-northeast2-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">southamerica-east1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Osasco, São Paulo, Brazil, South America</td>
<td><code dir="ltr" translate="no">southamerica-east1-a</code><br />
<code dir="ltr" translate="no">southamerica-east1-b</code><br />
<code dir="ltr" translate="no">southamerica-east1-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-central1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Council Bluffs, Iowa, North America</td>
<td><code dir="ltr" translate="no">us-central1-a</code><br />
<code dir="ltr" translate="no">us-central1-b</code><br />
<code dir="ltr" translate="no">us-central1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-east1</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Moncks Corner, South Carolina, North America</td>
<td><code dir="ltr" translate="no">us-east1-b</code><br />
<code dir="ltr" translate="no">us-east1-c</code><br />
<code dir="ltr" translate="no">us-east1-d</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-east4</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Ashburn, Virginia, North America</td>
<td><code dir="ltr" translate="no">us-east4-a</code><br />
<code dir="ltr" translate="no">us-east4-b</code><br />
<code dir="ltr" translate="no">us-east4-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-east5</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Columbus, Ohio, North America</td>
<td><code dir="ltr" translate="no">us-east5-a</code><br />
<code dir="ltr" translate="no">us-east5-b</code><br />
<code dir="ltr" translate="no">us-east5-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-south1</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>Dallas, Texas, North America</td>
<td><code dir="ltr" translate="no">us-south1-a</code><br />
<code dir="ltr" translate="no">us-south1-b</code><br />
<code dir="ltr" translate="no">us-south1-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-west1</code><br />
<img src="https://cloud.google.com/sustainability/region-carbon/gleaf.svg" width="18" alt="leaf icon" /> <a href="https://cloud.google.com/sustainability/region-carbon#region-picker">Low CO <sub>2</sub></a></td>
<td>The Dalles, Oregon, North America</td>
<td><code dir="ltr" translate="no">us-west1-a</code><br />
<code dir="ltr" translate="no">us-west1-b</code><br />
<code dir="ltr" translate="no">us-west1-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-west2</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Los Angeles, California, North America</td>
<td><code dir="ltr" translate="no">us-west2-a</code><br />
<code dir="ltr" translate="no">us-west2-b</code><br />
<code dir="ltr" translate="no">us-west2-c</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">us-west3</code> <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#instances-footnote">*</a><br />
</td>
<td>Salt Lake City, Utah, North America</td>
<td><code dir="ltr" translate="no">us-west3-a</code><br />
<code dir="ltr" translate="no">us-west3-b</code><br />
<code dir="ltr" translate="no">us-west3-c</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">us-west4</code><br />
</td>
<td>Las Vegas, Nevada, North America</td>
<td><code dir="ltr" translate="no">us-west4-a</code><br />
<code dir="ltr" translate="no">us-west4-b</code><br />
<code dir="ltr" translate="no">us-west4-c</code></td>
</tr>
</tbody>
</table>

\* Regions marked with asterisks don't support [running or scheduling notebooks by using the Agent Platform Workbench executor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart) .

† Regions marked with daggers don't support the ability to schedule a notebook run, but all other abilities of the Agent Platform Workbench executor are supported.

## Region considerations

### Using accelerators

Accelerators are available on a region basis. The following table lists all the available accelerators for each region.

You can search either by location or GPU model, or a combination of both.

As a best practice, consider using only GPU accelerator types that are available in multiple zones. That way, if a zonal outage occurs, the accelerator's workload will try to fail over, capacity permitting.

Asia Pacific Europe North America South America A100 40GB A100 80GB B200 GB200 RTX PRO 6000 H100 H100 Mega H200 L4 P4 P100 T4 TPU v2 TPU v2 Pod TPU v3 TPU v3 Pod TPU v5e TPU v6e TPU7x V100

| Region                    | Location                                     | Accelerators                                                                                                                                                                                                                                              |
| ------------------------- | -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `asia-east1`              | Changhua County, Taiwan, Asia Pacific        | L4 <sup>†</sup> , P100, T4, TPU v2 <sup>\*</sup> , V100, H100 Mega <sup>\*</sup>                                                                                                                                                                          |
| `asia-east2`              | Hong Kong, Asia Pacific                      | T4                                                                                                                                                                                                                                                        |
| `asia-northeast1`         | Tokyo, Japan, Asia Pacific                   | A100 40GB <sup>†</sup> , H100, H100 Mega, B200 <sup>\*</sup> , L4 <sup>†</sup> , T4, TPU v6e                                                                                                                                                              |
| `asia-northeast3`         | Seoul, South Korea, Asia Pacific             | A100 40GB, H100, L4, T4                                                                                                                                                                                                                                   |
| `asia-south1`             | Mumbai, India, Asia Pacific                  | H100, L4, T4, H200                                                                                                                                                                                                                                        |
| `asia-south2`             | Delhi, India, APAC                           | H200, RTX PRO 6000                                                                                                                                                                                                                                        |
| `asia-southeast1`         | Jurong West, Singapore, Asia Pacific         | A100 40GB, A100 80GB, B200, H100, H100 Mega, L4, P4, T4, RTX PRO 6000                                                                                                                                                                                     |
| `asia-southeast2`         | Jakarta, Indonesia, Asia Pacific             | T4                                                                                                                                                                                                                                                        |
| `australia-southeast1`    | Sydney, Australia, Asia Pacific              | H100 Mega, P4, T4                                                                                                                                                                                                                                         |
| `europe-central2`         | Warsaw, Poland, Europe                       | T4                                                                                                                                                                                                                                                        |
| `europe-north1`           | Hamina, Finland, Europe                      | H100 Mega <sup>\*</sup>                                                                                                                                                                                                                                   |
| `europe-west1`            | St. Ghislain, Belgium, Europe                | H100, H100 Mega, H200, L4 <sup>†</sup> , P100, T4                                                                                                                                                                                                         |
| `europe-west2`            | London, England, Europe                      | H100, L4, T4                                                                                                                                                                                                                                              |
| `europe-west3`            | Frankfurt, Germany, Europe                   | H100, H100 Mega <sup>\*</sup> , L4 <sup>†</sup> , T4                                                                                                                                                                                                      |
| `europe-west4`            | Eemshaven, Netherlands, Europe               | A100 40GB, A100 80GB, H100, H100 Mega, H200, B200 <sup>\*</sup> , L4, P4, T4, V100, P100 <sup>\*</sup> , RTX PRO 6000, TPU v2 <sup>\*</sup> , TPU v2 Pod <sup>\*</sup> , TPU v3 <sup>\*</sup> , TPU v3 Pod <sup>\*</sup> , TPU v5e <sup>†</sup> , TPU v6e |
| `europe-west6`            | Zurich, Switzerland, Europe                  | L4 <sup>†</sup>                                                                                                                                                                                                                                           |
| `me-central2`             | Dammam, Saudi Arabia, Middle East            | L4                                                                                                                                                                                                                                                        |
| `me-west1`                | Tel Aviv, Israel, Middle East                | A100 40GB, A100 80GB <sup>†</sup> , T4 <sup>†</sup>                                                                                                                                                                                                       |
| `northamerica-northeast1` | Montréal, Québec, North America              | P4, T4                                                                                                                                                                                                                                                    |
| `northamerica-northeast2` | Toronto, Ontario, North America              | H100, L4                                                                                                                                                                                                                                                  |
| `southamerica-east1`      | Osasco, São Paulo, Brazil, South America     | T4                                                                                                                                                                                                                                                        |
| `southamerica-west1`      | Osasco, São Paulo, Brazil, South America     | T4 <sup>†</sup> ,TPU v6e <sup>\*</sup>                                                                                                                                                                                                                    |
| `us-central1`             | Council Bluffs, Iowa, North America          | A100 40GB, A100 80GB, B200, H100, H100 Mega, GB200, H200, L4, P4, P100, T4, RTX PRO 6000, TPU v2 <sup>\*</sup> , TPU v2 Pod <sup>\*</sup> , TPU v3 <sup>\*</sup> , TPU v5e <sup>\*</sup> , TPU v6e, TPU7x, V100                                           |
| `us-east1`                | Moncks Corner, South Carolina, North America | A100 40GB <sup>\*</sup> , B200 <sup>\*</sup> , L4, P100, T4, RTX PRO 6000, TPU v5e <sup>\*</sup> , TPU v6e <sup>+</sup> , V100                                                                                                                            |
| `us-east4`                | Ashburn, Virginia, North America             | A100 80GB, H100, H100 Mega, H200, B200 <sup>\*</sup> , GB200 <sup>\*</sup> , L4, P4, T4, RTX PRO 6000                                                                                                                                                     |
| `us-east5`                | Columbus, Ohio, North America                | A100 80GB, H100, H100 Mega, H200 <sup>\*</sup> , TPU v6e                                                                                                                                                                                                  |
| `us-south1`               | Dallas, Texas, North America                 | TPU v5e <sup>†</sup> , TPU v6e <sup>\*</sup> , B200 <sup>\*</sup> , H200                                                                                                                                                                                  |
| `us-west1`                | The Dalles, Oregon, North America            | H100 Mega, H200, L4, P100, T4, H100, TPU v5e, V100                                                                                                                                                                                                        |
| `us-west2`                | Los Angeles, California, North America       | P4, T4, B200                                                                                                                                                                                                                                              |
| `us-west3`                | Salt Lake City, Utah, North America          | A100 40GB, B200 <sup>\*</sup>                                                                                                                                                                                                                             |
| `us-west4`                | Las Vegas, Nevada, North America             | A100 40GB <sup>\*</sup> , H100, H100 Mega, L4 <sup>†</sup> , T4, TPU v5e                                                                                                                                                                                  |

<sup>\*</sup> The specified accelerator isn't available for [serving batch or online inferences](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) .

<sup>+</sup> The specified accelerator is available on an allowlist-only basis for [serving batch or online inferences](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) .

<sup>†</sup> The specified accelerator isn't available for [training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .

If your job uses multiple types of GPUs, they must all be available in a single zone in your region. For example, you can't run a job in `australia-southeast1` using NVIDIA Tesla P4 GPUs, NVIDIA Tesla T4 GPUs, and NVIDIA Tesla P100 GPUs. While all of these GPUs are available for jobs in `australia-southeast1` , no single zone in that region provides all three types of GPU. To learn more about the zone availability of GPUs, see [GPU locations](https://docs.cloud.google.com/compute/docs/regions-zones/gpu-regions-zones) .

### BigQuery location requirements

When you use a BigQuery table as a source for a managed tabular dataset or tabular inference data, it must conform to the following location requirements:

### Americas

  - BigQuery tables can be either multi-regional ( `US` ) or regional ( `us-central1` ).

  - BigQuery views must be regional ( `us-central1` ).

  - If the table or view is not in the same project that the Agent Platform job is running in, make sure that Agent Platform has [the correct roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#bq-roles) .

### Europe

  - BigQuery tables and views must be regional ( `europe-west4` ).

  - Location: The region that your Agent Platform job runs in, such as `us-central1` , `europe-west4` , or `asia-east1` .

  - If the table or view is not in the same project that the Agent Platform job is running in, make sure that Agent Platform has [the correct roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#bq-roles) .

### Cloud Storage bucket requirements

Some Agent Platform tasks, such as importing data, use a [Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .

  - For best performance, we recommend that you use the following settings when creating a Cloud Storage bucket to use with Agent Platform:
    
      - Location type: [`Region`](https://docs.cloud.google.com/storage/docs/locations) .
      - Location: The region where you are using Agent Platform; for example, `us-central1` , `europe-west4` , or `asia-east1` .
      - Storage class: [`Standard`](https://docs.cloud.google.com/storage/docs/storage-classes) .
    
    For Agent Platform training jobs, buckets must be regional.

  - If the bucket is not in the same project that the Agent Platform job is running in, make sure Agent Platform has [the correct roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#storage-roles) .

## Restricting resource locations

Organization policy administrators can restrict the regions available where you can use Agent Platform by [creating a resource locations constraint](https://docs.cloud.google.com/resource-manager/docs/organization-policy/defining-locations) . Read about [how a resource locations constraint applies to Agent Platform](https://docs.cloud.google.com/resource-manager/docs/organization-policy/defining-locations-supported-services#ai-platform-unified)

## What's next

  - Learn about [Google Cloud regions](https://docs.cloud.google.com/docs/geography-and-regions) .
  - Learn about [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for Google and partner models and generative AI features.
  - Learn about [Supported locations for agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
