---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/glossary
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/glossary
title: Gemini Enterprise Agent Platform glossary
description: Provides a list of glossary terms relevant to Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

  - ##### annotation set
    
      - An annotation set contains the labels associated with the uploaded source files within a dataset. An annotation set is associated with both a data type and an objective (for example, video/classification).

  - ##### API endpoint
    
      - API Endpoints is a service config aspect that specifies the network addresses, also known as service endpoints (for example, aiplatform.googleapis.com).

  - ##### Application Default Credentials (ADC)
    
      - The Application Default Credentials (ADC) provide a simple way to get authorization credentials for use in calling Google APIs. They are best suited for cases when the call needs to have the same identity and authorization level for the application independent of the user. This is the recommended approach to authorize calls to Google Cloud APIs, particularly when you're building an application that is deployed to Google App Engine (GAE) or Compute Engine virtual machines. For more information, see [How Application Default Credentials works](https://cloud.google.com/docs/authentication/application-default-credentials) .

  - ##### Approximate Nearest Neighbor (ANN)
    
      - The Approximate Nearest Neighbor (ANN) service is a high scale, low latency solution, to find similar vectors (or more specifically, "embeddings") for a large corpus. For more information, see [How to use Vector Search for semantic matching](https://cloud.google.com/vertex-ai/docs/vector-search/overview#how_to_use_for_semantic_matching) .

  - ##### artifact
    
      - An artifact is a discrete entity or piece of data produced and consumed by a machine learning workflow. Examples of artifacts include datasets, models, input files, and training logs.

  - ##### Artifact Registry
    
      - Artifact Registry is a universal artifact management service. It is the recommended service for managing containers and other artifacts on Google Cloud. For more information, see [Artifact Registry](https://cloud.google.com/artifact-registry/docs/overview) .

  - ##### Artificial Intelligence (AI)
    
      - Artificial intelligence (or AI) is the study and design of machines that appear to be "intelligent", meaning one which mimics human or intellectual functions such as mechanical movement, reasoning or problem solving. One of the most popular subfields of AI is machine learning, which uses a statistical and data-driven approach to create AI. However, some people use these two terms interchangeably.

  - ##### authentication
    
      - The process of verifying the identity of a client (which might be a user or another process) for the purposes of gaining access to a secured system. A client that has proven its identity is said to be authenticated. For more information, see [Authentication methods at Google](https://cloud.google.com/docs/authentication) .

  - ##### Automatic side-by-side (AutoSxS)
    
      - Automatic side-by-side (AutoSxS) is a model-assisted evaluation tool that compares two large language models (LLMs) side by side. It can be used to evaluate the performance of either generative AI models in Vertex AI Model Registry or pregenerated inferences. AutoSxS uses an autorater to decide which model gives the better response to a prompt. AutoSxS is available on demand and evaluates language models with comparable performance to human raters.

  - ##### AutoML
    
      - Machine learning algorithms that "learn to learn" through black-box optimization. For more information, see [ML Glossary](https://developers.google.com/machine-learning/glossary#automl) .

  - ##### autologging
    
      - Autologging is a feature in machine learning platforms and libraries that automatically logs key metrics, parameters, and artifacts during the model training process without requiring explicit code instrumentation. It streamlines experiment tracking by automatically capturing information such as hyperparameters, evaluation metrics (for example, accuracy, loss), and model checkpoints, allowing developers to easily compare and reproduce experiments.

  - ##### autorater
    
      - An autorater is a language model that evaluates the quality of model responses given an original inference prompt. It's used in the AutoSxS pipeline to compare the inferences of two models and determine which model performed the best. For more information, see [The autorater](https://cloud.google.com/vertex-ai/generative-ai/docs/models/side-by-side-eval#autorater) .

  - ##### autoscaling
    
      - Autoscaling is the capability of a compute resource, like a Ray cluster's worker pool, to automatically adjust the number of nodes up or down based on the workload demands, optimizing resource utilization and cost. For more information, see [Scale Ray clusters on Vertex AI: Autoscaling](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/scale-clusters#autoscaling) .

  - ##### baseline
    
      - A model used as a reference point for comparing how well another model (typically, a more complex one) is performing. For example, a logistic regression model might serve as a good baseline for a deep model. For a particular problem, the baseline helps model developers quantify the minimal expected performance that a new model must achieve for the new model to be useful. For more information, see [Baseline and target datasets](https://cloud.google.com/vertex-ai/docs/model-monitoring/set-up-model-monitoring#baseline_and_target_datasets) .

  - ##### batch
    
      - The set of examples used in one training iteration. The batch size determines the number of examples in a batch.

  - ##### batch size
    
      - The number of examples in a batch. For example, the batch size of SGD is 1, while the batch size of a mini-batch is usually between 10 and 1000. Batch size is usually fixed during training and inference; however, TensorFlow does permit dynamic batch sizes.

  - ##### batch inference
    
      - Batch inference takes a group of inference requests and outputs the results in one file. For more information, see [Overview of getting inferences on Vertex AI](https://cloud.google.com/vertex-ai/docs/predictions/overview#batch-inference) .

  - ##### bias
    
      - 1\. Stereotyping, prejudice or favoritism towards some things, people, or groups over others. These biases can affect collection and interpretation of data, the design of a system, and how users interact with a system. 2. Systematic error introduced by a sampling or reporting procedure.

  - ##### bidrectional
    
      - A term used to describe a system that evaluates the text that both precedes and follows a target section of text. In contrast, a unidirectional system only evaluates the text that precedes a target section of text.

  - ##### Bidirectional Encoder Representations from Transformers (BERT)
    
      - BERT is a method of pre-training language representations, meaning that we train a general-purpose "language understanding" model on a large text corpus (like Wikipedia), and then use that model for downstream NLP tasks that we care about (like question answering). BERT outperforms previous methods because it is the first unsupervised, deeply bidirectional system for pre-training NLP.

  - ##### BigQuery
    
      - BigQuery is a fully managed, serverless, and highly scalable enterprise data warehouse provided by Google Cloud, designed for analyzing massive datasets using SQL queries at incredibly high speeds. BigQuery enables powerful business intelligence and analytics without requiring users to manage any infrastructure. For more information, see [From data warehouse to autonomous data and AI platform](https://cloud.google.com/bigquery/docs) .

  - ##### BigQuery ML
    
      - BigQuery ML is a feature within Google Cloud's BigQuery data warehouse that lets data analysts and data scientists create, train, and deploy machine learning models directly inside BigQuery using standard SQL queries. This eliminates the need to move data to separate ML platforms, simplifying the machine learning workflow and making ML more accessible to SQL users. For more information, see [Create machine learning models in BigQuery ML](https://cloud.google.com/bigquery/docs/create-machine-learning-model) .

  - ##### Bigtable
    
      - A fully managed, NoSQL database service, also recommended as a storage option for training data when using Vertex AI. For more information, see [Bigtable overview](https://cloud.google.com/bigtable/docs) .

  - ##### Bilingual Evaluation Understudy (BLEU)
    
      - A popular measure for evaluating the quality of a machine-translation algorithm by comparing its output to that of one or more human translations.

  - ##### bounding box
    
      - A bounding box for an object in the video frame can be specified in either of two ways (i) Using 2 vertices consisting of a set of x,y coordinates if they are diagonally opposite points of the rectangle. For example: x\_relative\_min, y\_relative\_min,,,x\_relative\_max,y\_relative\_max,, (ii) Use all 4 vertices. For more information, see [Prepare video data](https://cloud.google.com/vertex-ai/docs/video-data/object-tracking/prepare-data#csv) .

  - ##### bucket
    
      - Top-level folder for Cloud Storage. Bucket names must be unique across all users of Cloud Storage. Buckets contain files. For more information, see [Product overview of Cloud Storage](https://cloud.google.com/storage/docs/introduction) .

  - ##### chat
    
      - The contents of a back-and-forth dialogue with an ML system, typically a large language model. The previous interaction in a chat (what you typed and how the large language model responded) becomes the context for subsequent parts of the chat. A chatbot is an application of a large language model.

  - ##### checkpoint
    
      - Data that captures the state of a model's parameters either during training or after training is completed. For example, during training, you can: 1. Stop training, perhaps intentionally or perhaps as the result of certain errors. 2. Capture the checkpoint. 3. Later, reload the checkpoint, possibly on different hardware. 4. Restart training. Within Gemini, a checkpoint refers to a specific version of a Gemini model trained on a specific dataset.

  - ##### classification model
    
      - A model whose inference is a class. For example, the following are all classification models: A model that predicts an input sentence's language (French? Spanish? Italian?). A model that predicts tree species (Maple? Oak? Baobab?). A model that predicts the positive or negative class for a particular medical condition.

  - ##### classification metrics
    
      - Supported classification metrics in the Vertex AI SDK for Python are confusion matrix and ROC curve.

  - ##### Cloud Logging
    
      - Cloud Logging is a fully managed, real-time logging service provided by Google Cloud that lets you collect, store, analyze, and monitor logs from all your Google Cloud resources, on-premises applications, and even custom sources. Cloud Logging centralizes log management, which makes it easier to troubleshoot, audit, and understand the behavior and health of your applications and infrastructure. For more information, see [Cloud Logging overview](https://cloud.google.com/logging/docs/overview) .

  - ##### Cloud Monitoring
    
      - Cloud Monitoring is a comprehensive observability platform provided by Google Cloud that collects and visualizes metrics, logs, and events from Google Cloud services, on-premises infrastructure, and application components. It enables users to gain insights into the performance, availability, and overall health of their systems, allowing for proactive issue detection, troubleshooting, and alerting. For more information, see [Cloud Monitoring metrics for Vertex AI](https://cloud.google.com/vertex-ai/docs/general/monitoring-metrics) .

  - ##### Cloud Network Address Translation (Cloud NAT)
    
      - Cloud NAT (Network Address Translation) is a fully managed Google Cloud service that allows virtual machine instances and other resources without external IP addresses to connect to the internet. For more information, see [Cloud NAT documentation](https://cloud.google.com/nat/docs) .

  - ##### Cloud Profiler
    
      - Cloud Profiler is a continuous profiling service provided by Google Cloud that helps you identify and analyze CPU and memory consumption, as well as other resource usage (like heap, wall time, contention), in your applications. It automatically collects profiling data from your production applications with minimal overhead, allowing you to visualize and understand the performance bottlenecks across various services and optimize your code for better efficiency and reduced costs. For more information, see [Cloud Profiler overview](https://cloud.google.com/profiler/docs/about-profiler) .

  - ##### Cloud Router
    
      - Cloud Router is a distributed and fully managed offering that provides Border Gateway Protocol (BGP) speaker and responder capabilities. Cloud Router works with Cloud Interconnect, Cloud VPN, Cloud NAT, and Router appliances to create dynamic routes in VPC networks based on BGP-received and custom learned routes. For more information, see [Cloud Router Concepts Overview](https://cloud.google.com/network-connectivity/docs/router/concepts/overview) .

  - ##### Cloud Storage
    
      - Google Cloud's scalable and secure object storage service, recommended for storing large datasets used in training and verification with Vertex AI for optimal performance. For more information, see [Cloud Storage documentation](https://cloud.google.com/storage/docs) .

  - ##### Cloud Storage Fuse
    
      - An open-source FUSE adapter that lets you mount Cloud Storage buckets as a file system on Linux or macOS systems. For more information, see [Cloud Storage Fuse](https://cloud.google.com/storage/docs/cloud-storage-fuse/overview) .

  - ##### Cloud TPU
    
      - A specialized hardware accelerator designed to speed up machine learning workloads on Google Cloud.

  - ##### Colab Enterprise
    
      - Colab Enterprise is a collaborative, managed Jupyter notebook environment that brings the popular Google Colab user experience to Google Cloud, offering enterprise-level security and compliance capabilities. Colab Enterprise provides a notebook-centric, zero-configuration experience, with compute resources managed by Vertex AI, and integrates with other Google Cloud services like BigQuery. For more information, see [Introduction to Colab Enterprise](https://cloud.google.com/colab/docs/introduction) .

  - ##### consumer VPC
    
      - A consumer Virtual Private Cloud (VPC) network is used to privately access managed services from within their VPC network. For more information, see [Private Service Connect](https://cloud.google.com/vpc/docs/private-service-connect#interfaces) .

  - ##### container image
    
      - A container image is a package that includes the component's executable code and a definition of the environment that the code runs in. For more information, see [Vertex AI serverless training overview](https://cloud.google.com/vertex-ai/docs/training/overview) .

  - ##### context
    
      - A context is used to group artifacts and executions together under a single, queryable, and typed category. Contexts can be used to represent sets of metadata. An example of a Context would be a run of a machine learning pipeline.

  - ##### context cache
    
      - A context cache in Vertex AI is a large amount of data that can be used in multiple requests to a Gemini model. The cached content is stored in the region where the request to create the cache is made. It can be any MIME type supported by Gemini multimodal models, such as text, audio, or video. For more information, see [Context caching overview](https://cloud.google.com/vertex-ai/generative-ai/docs/context-cache/context-cache-overview) .

  - ##### context window
    
      - The number of tokens a model can process in a given prompt. The larger the context window, the more information the model can use to provide coherent and consistent responses to the prompt.

  - ##### Customer-managed encryption keys (cmek)
    
      - Customer-managed encryption keys (CMEK) are integrations that allow customers to encrypt data in existing Google services using a key they manage in Cloud KMS (also known as Storky). The key in Cloud KMS is the key encryption key protecting their data. For more information, see [Customer-managed encryption keys (CMEK)](https://cloud.google.com/vertex-ai/docs/general/cmek) .

  - ##### consumer VPC network
    
      - A consumer VPC network is a Google Cloud Virtual Private Cloud (VPC) that privately accesses a service hosted in another VPC (known as the producer VPC). For more information, see [Private Service Connect](https://cloud.google.com/vpc/docs/private-service-connect#producers-and-consumers) .

  - ##### CustomJob
    
      - A CustomJob is one of three Vertex AI resources a user can create to train custom models on Vertex AI. Serverless training jobs are the basic way to run custom machine learning (ML) training code in Vertex AI. For more information, see [Create a serverless training job](https://cloud.google.com/vertex-ai/docs/training/create-custom-job) .

  - ##### custom container image
    
      - A custom container image is a self-contained, executable package that includes the user's application code, its runtime, libraries, dependencies, and environment configuration. In the context of Google Cloud, particularly Vertex AI, it lets the user package their machine learning training code or serving application with its exact dependencies, ensuring reproducibility and enabling the user to run a workload on managed services using specific software versions or unique configurations not provided by standard environments. For more information, see [Custom container requirements for inference](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) .

  - ##### custom training
    
      - Vertex AI provides two primary modes for running your custom training code: a serverless, on-demand environment, or a dedicated, reserved cluster. For more information, see [Train and use your own models](https://cloud.google.com/vertex-ai/docs/training-overview#custom-training) .

  - ##### Dask
    
      - Dask is a distributed computing platform that is often used with TensorFlow, Pytorch, and other ML frameworks to manage distributed training jobs. For more information, see [Wikipedia](https://en.wikipedia.org/wiki/Dask_%28software%29) .

  - ##### data analysis
    
      - Obtaining an understanding of data by considering samples, measurement, and visualization. Data analysis can be particularly useful when a dataset is first received, before one builds the first model. It is also crucial in understanding experiments and debugging problems with the system.

  - ##### data augmentation
    
      - Artificially boosting the range and number of training examples by transforming existing examples to create additional examples. For example, suppose images are one of your features, but your dataset doesn't contain enough image examples for the model to learn useful associations. Ideally, you'd add enough labeled images to your dataset to enable your model to train properly. If that's not possible, data augmentation can rotate, stretch, and reflect each image to produce many variants of the original picture, possibly yielding enough labeled data to enable excellent training.

  - ##### Data Center GPU manager (DCGM )
    
      - A suite of tools from NVIDIA for managing and monitoring NVIDIA GPUs in a data center environment. For more information, see [NVIDIA Data Center GPU Manager (DCGM)](https://cloud.google.com/monitoring/agent/ops-agent/third-party-nvidia) .

  - ##### DataFrame
    
      - A popular pandas data type for representing datasets in memory. A DataFrame is analogous to a table or a spreadsheet. Each column of a DataFrame has a name (a header), and each row is identified by a unique number. Each column in a DataFrame is structured like a 2D array, except that each column can be assigned its own data type.

  - ##### dataset (data set)
    
      - A dataset is broadly defined as a collection of structured or unstructured data records. A collection of raw data, commonly (but not exclusively) organized in one of the following formats: a spreadsheet a file in CSV (comma-separated values) format. For more information, see [Create a dataset](https://cloud.google.com/vertex-ai/docs/samples/aiplatform-create-dataset-sample) .

  - ##### decoder
    
      - In general, any ML system that converts from a processed, dense, or internal representation to a more raw, sparse, or external representation. Decoders are often a component of a larger model, where they are frequently paired with an encoder. In sequence-to-sequence tasks, a decoder starts with the internal state generated by the encoder to predict the next sequence.

  - ##### deep neural network (DNN)
    
      - A neural network with multiple hidden layers, typically programmed through deep learning techniques.

  - ##### depth
    
      - The sum of the following in a neural network: 1. the number of hidden layers 2. the number of output layers, which is typically one 3. the number of any embedding layers. For example, a neural network with five hidden layers and one output layer has a depth of 6. Notice that the input layer doesn't influence depth.

  - ##### DevOps
    
      - DevOps is a suite of Google Cloud Platform products, for example, Artifact Registry, Cloud Deploy.

  - ##### early stopping
    
      - A method for regularization that involves ending training before training loss finishes decreasing. In early stopping, you intentionally stop training the model when the loss on a validation dataset starts to increase; that is, when generalization performance worsens.

  - ##### embedding
    
      - Numerical representations of words or pieces of text. These numbers capture the semantic meaning and context of the text. Similar or related words or text tend to have similar embeddings, which means they are closer together in the high-dimensional vector space.

  - ##### embedding space (latent space)
    
      - In Generative AI, embedding space refers to a numerical representation of text, images, or videos that captures relationships between inputs. Machine learning models, particularly generative AI models, are adept at creating these embeddings by identifying patterns within large datasets. Applications can utilize embeddings to process and generate language, recognizing complex meanings and semantic relationships specific to the content.

  - ##### embedding vector
    
      - A dense, often low-dimensional, vector representation of an item such that, if two items are semantically similar, their respective embeddings are located near each other in the embedding vector space.

  - ##### encoder
    
      - In general, any ML system that converts from a raw, sparse, or external representation into a more processed, denser, or more internal representation. Encoders are often a component of a larger model, where they are frequently paired with a decoder. Some transformers pair encoders with decoders, though other transformers use only the encoder or only the decoder. Some systems use the encoder's output as the input to a classification or regression network. In sequence-to-sequence tasks, an encoder takes an input sequence and returns an internal state (a vector). Then, the decoder uses that internal state to predict the next sequence.

  - ##### endpoint
    
      - Resources to which you can deploy trained models to serve inferences. For more information, see [Choose an endpoint type](https://cloud.google.com/vertex-ai/docs/predictions/choose-endpoint-type) .

  - ##### ensemble
    
      - A collection of models trained independently whose inferences are averaged or aggregated. In many cases, an ensemble produces better inferences than a single model. For example, a random forest is an ensemble built from multiple decision trees. Note that not all decision forests are ensembles.

  - ##### environment
    
      - In reinforcement learning, the world that contains the agent and allows the agent to observe that world's state. For example, the represented world can be a game like chess, or a physical world like a maze. When the agent applies an action to the environment, then the environment transitions between states.

  - ##### evaluation (eval)
    
      - An eval, short for "evaluation", is a type of experiment in which logged or synthetic queries are sent through two Search stacks--an experimental stack that includes your change and a base stack without your change. Evals produce diffs and metrics that let you evaluate the impact, quality, and other effects of your change on search results and other parts of the Google user experience. Evals are used during tuning, or iterations, on your change. They are also used as part of launching a change to live user traffic.

  - ##### event
    
      - An event describes the relationship between artifacts and executions. Each artifact can be produced by an execution and consumed by other executions. Events help you to determine the provenance of artifacts in their ML workflows by chaining together artifacts and executions.

  - ##### execution
    
      - An execution is a record of an individual machine learning workflow step, typically annotated with its runtime parameters. Examples of executions include data ingestion, data validation, model training, model evaluation, and model deployment.

  - ##### experiment
    
      - An experiment is a context that can contain a set of n experiment runs in addition to pipeline runs where a user can investigate, as a group, different configurations such as input artifacts or hyperparameters.

  - ##### experiment run
    
      - A specific, trackable execution within a Vertex AI Experiment, which logs inputs (like algorithm, parameters, and datasets) and outputs (like models, checkpoints, and metrics) to monitor and compare ML development iterations. For more information, see [Create and manage experiment runs](https://cloud.google.com/vertex-ai/docs/experiments/create-manage-exp-run) .

  - ##### Explainable AI
    
      - A feature of Vertex AI that provides tools and capabilities to understand and interpret inferences made by ML models, offering insights into feature importance and model behavior. For more information, see [Introduction to Vertex Explainable AI](https://cloud.google.com/vertex-ai/docs/explainable-ai/overview) .

  - ##### exploratory data analysis
    
      - In statistics, exploratory data analysis (EDA) is an approach to analyzing data sets to summarize their main characteristics, often with visual methods. A statistical model can be used or not, but primarily EDA is for seeing what the data can tell us beyond the formal modeling or hypothesis testing task.

  - ##### F1 Score
    
      - The F1 score is a metric used to evaluate the accuracy of a model's output. It's particularly useful for assessing the performance of models on tasks where both precision and recall are important, such as information extraction. For generative AI models, the F1 score can be used to compare the model's inferences with ground truth data to determine the model's accuracy. However, for generative tasks like summarization and text generation, other metrics like Rough-L score might be more appropriate.

  - ##### feature
    
      - In machine learning (ML), a feature is a characteristic or attribute of an instance or entity that's used as an input to train an ML model or to make inferences.

  - ##### feature engineering
    
      - Feature engineering is the process of transforming raw machine learning (ML) data into features that can be used to train ML models or to make inferences.

  - ##### feature group
    
      - A feature group is a feature registry resource that corresponds to a BigQuery source table or view containing feature data. A feature view might contain features and can be thought of as a logical grouping of feature columns in the data source.

  - ##### feature record
    
      - A feature record is an aggregation of all feature values that describe the attributes of a unique entity at a specific point in time.

  - ##### feature registry
    
      - A feature registry is a central interface for recording feature data sources that you want to serve for online inferences. For more information, see [Feature Registry setup](https://cloud.google.com/vertex-ai/docs/featurestore/latest/overview#feature_registry_setup) .

  - ##### feature serving
    
      - Feature serving is the process of exporting or fetching feature values for training or inference. In Vertex AI, there are two types of feature serving—online serving and offline serving. Online serving retrieves the latest feature values of a subset of the feature data source for online inferences. Offline or batch serving exports high volumes of feature data—including historical data—for offline processing, such as ML model training.

  - ##### feature timestamp
    
      - A feature timestamp indicates when the set of feature values in a specific feature record for an entity were generated.

  - ##### feature value
    
      - A feature value corresponds to the actual and measurable value of a feature (attribute) of an instance or entity. A collection of feature values for the unique entity represent the feature record corresponding to the entity.

  - ##### feature view
    
      - A feature view is a logical collection of features materialized from a BigQuery data source to an online store instance. A feature view stores and periodically refreshes the customer's feature data, which is refreshed periodically from the BigQuery source. A feature view is associated with the feature data storage either directly or through associations to feature registry resources.

  - ##### Filestore
    
      - A fully managed, high-performance file storage service from Google Cloud, often used for applications that require a shared file system. For more information, see [Filestore overview](https://cloud.google.com/filestore/docs/overview) .

  - ##### foundation model (FM)
    
      - Models trained on broad data such that they can be adapted (for example, fine-tuned) to a wide range of downstream tasks.

  - ##### Foundation Model Operations (FMOPs)
    
      - FMOps expands upon the capabilities of MLOps and focuses on the efficient productionization of pre-trained (trained from scratch) or customized (fine-tuned) FMs.

  - ##### Google Cloud pipeline components SDK
    
      - The Google Cloud pipeline components (GCPC) SDK provides a set of prebuilt Kubeflow Pipelines components that are production quality, performant, and easy to use. You can use Google Cloud Pipeline Components to define and run ML pipelines in Vertex AI Pipelines and other ML pipeline execution backends conformant with Kubeflow Pipelines. For more information, see [Introduction to Google Cloud Pipeline Components](https://cloud.google.com/vertex-ai/docs/pipelines/components-introduction) .

  - ##### Compute Engine
    
      - Compute Engine is a component of the Google Cloud Platform and is an Infrastructure as a Service (IaaS) offering that lets users run virtual machines on Google's infrastructure. For more information, see [Compute Engine overview](https://cloud.google.com/compute/docs/overview) .

  - ##### Compute Engine instance
    
      - A Compute Engine instance is a virtual machine (VM) that runs on Google's infrastructure. You can choose its specifications, run applications on it, and connect to it over the internet, but you don't have to manage the physical hardware. For more information, see [Virtual machines for any workload](https://cloud.google.com/products/compute) .

  - ##### Google Embedded Modem System (GEMS)
    
      - GEMS is an embedded software framework targeting modems, and an accompanying set of development workflows and infrastructure. The core vision of GEMS is to provide high quality modem system code with high reusability across many Google devices that contain modems. To achieve this broad vision, GEMS provides a comprehensive environment for developers, comprised of the major building blocks depicted below.

  - ##### gradient
    
      - The vector of partial derivatives with respect to all of the independent variables. In machine learning, the gradient is the vector of partial derivatives of the model function. The gradient points in the direction of steepest ascent.

  - ##### graph
    
      - In the context of Vertex AI, a graph refers to a data structure that represents the relationships between entities and their attributes. It is used to model and analyze complex data, such as knowledge graphs, social networks, and business processes. For more information, see [Introduction to Vertex ML Metadata](https://cloud.google.com/vertex-ai/docs/ml-metadata/introduction#overview_of) .

  - ##### ground truth (GT)
    
      - Ground truth is a term used in various fields to refer to the absolute truth of some decision or measurement problem, as opposed to some system's estimate. In machine learning, the term "ground truth" refers to the training set for supervised learning techniques.

  - ##### heuristic
    
      - A simple and quickly implemented solution to a problem. For example, "With a heuristic, we achieved 86% accuracy. When we switched to a deep neural network, accuracy went up to 98%".

  - ##### hidden layer
    
      - A layer in a neural network between the input layer (the features) and the output layer (the inference). Each hidden layer consists of one or more neurons. A deep neural network contains more than one hidden layer.

  - ##### histogram
    
      - A graphical display of the variation in a set of data using bars. A histogram visualizes patterns that are difficult to detect in a simple table of numbers.

  - ##### hyperparameter
    
      - A hyperparameter refers to a variable that governs the training process of a machine learning model. These variables can include learning rates, momentum values in the optimizer, and the number of units in the last hidden layer of a model. For more information, see [Hyperparameter tuning overview](https://cloud.google.com/vertex-ai/docs/training/hyperparameter-tuning-overview) .

  - ##### hyperparameter tuning
    
      - Hyperparameter tuning in Vertex AI involves running multiple trials of a training application with different values for the chosen hyperparameters, set within specified limits. The goal is to optimize the hyperparameter settings to maximize the model's predictive accuracy. For more information, see [Hyperparameter tuning overview](https://cloud.google.com/vertex-ai/docs/training/hyperparameter-tuning-overview) .

  - ##### Identity and Access Management permissions (IAM)
    
      - Identity and Access Management (IAM) permissions are specific granular capabilities that define who can do what on which Google Cloud resources. They are assigned to principals (like users, groups, or service accounts) through roles, allowing precise control over access to services and data within a Google Cloud project or organization. For more information, see [Access control with IAM](https://cloud.google.com/support/docs/access-control) .

  - ##### image recognition
    
      - Image recognition is the process of classifying objects, patterns, or concepts in an image. It is also known as image classification. Image recognition is a subfield of machine learning and computer vision.

  - ##### index
    
      - A collection of vectors deployed together for similarity search. Vectors can be added to an index or removed from an index. Similarity search queries are issued to a specific index and will search over the vectors in that index.

  - ##### inference
    
      - In the context of the Vertex AI platform, inference refers to the process of running data points through a machine learning model to calculate an output, such as a single numerical score. This process is also known as "operationalizing a machine learning model" or "putting a machine learning model into production." Inference is an important step in the machine learning workflow, since it enables models to be used to make inferences on new data. In Vertex AI, inference can be performed in various ways, including batch inference and online inference. Batch inference involves running a group of inference requests and outputting the results in one file, while online inference allows for real-time inferences on individual data points.

  - ##### information retrieval (IR)
    
      - Information retrieval (IR) is a key component of Vertex AI Search. It is the process of finding and retrieving relevant information from a large collection of data. In the context of Vertex AI, IR is used to retrieve documents from a corpus based on a user's query. Vertex AI offers a suite of APIs to help you build your own Retrieval Augmented Generation (RAG) applications or to build your own Search engine. For more information, see [Use Vertex AI Search as a retrieval backend using RAG Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/use-vertexai-search) .

  - ##### Infrastructure as Code (IaC)
    
      - Infrastructure as Code. An approach to manage IT infrastructure where teams can manage and provision services through code. With IaC, configuration files are created that contain the infrastructure specifications, which makes it easier to create and edit infrastructure at scale.

  - ##### Infrastructure as Code (IaC)
    
      - Infrastructure as Code. An approach to manage IT infrastructure where teams can manage and provision services through code. With IaC, configuration files are created that contain the infrastructure specifications, which makes it easier to create and edit infrastructure at scale.

  - ##### IP address exhaustion
    
      - IP address exhaustion occurs when the available IP addresses within a designated range are depleted. For more information, see [Best practices for Cloud Run networking](https://cloud.google.com/run/docs/configuring/networking-best-practices) .

  - ##### Location
    
      - A location is the physical place in the world where your cloud resources are hosted. This concept is broken down into two main parts: regions and zones For more information, see [Regions and zones](https://cloud.google.com/docs/geography-and-regions) .

  - ##### Location
    
      - A location is the physical place in the world where your cloud resources are hosted. This concept is broken down into two main parts: regions and zones. For more information, see [Regions and zones](https://cloud.google.com/docs/geography-and-regions) .

  - ##### login node
    
      - A login node is the main entry point for a user to access the cluster, submit jobs, and manage files. For more information, see [What is high performance computing?](https://cloud.google.com/discover/what-is-high-performance-computing) .

  - ##### Machine Learning Metadata
    
      - ML Metadata (MLMD) is a library for recording and retrieving metadata associated with ML developer and data scientist workflows. MLMD is an integral part of TensorFlow Extended (TFX), but is designed so that it can be used independently. As part of the broader TFX platform, most users only interact with MLMD when examining the results of pipeline components, for example in notebooks or in TensorBoard.

  - ##### managed dataset
    
      - A dataset object created in and hosted by Vertex AI.

  - ##### manual logging
    
      - The process of explicitly adding code (for example, using the Vertex AI SDK for Python) to a training script to track and log custom parameters, metrics, and artifacts to a Vertex AI Experiments run. For more information, see [Monitoring and logging overview](https://cloud.google.com/run/docs/monitoring-overview) .

  - ##### Managed Lustre
    
      - A parallel, distributed file system designed for high-performance computing. Google Cloud's Managed Lustre provides a high-throughput file system for demanding workloads. For more information, see [Managed Lustre overview](https://cloud.google.com/managed-lustre/docs/overview) .

  - ##### Managed Training on reserved clusters
    
      - Managed Training on reserved clusters is a Google Cloud service designed to simplify and accelerate the largest and most complex AI/ML workloads by providing a fully managed experience on dedicated, reserved hardware. It’s built to solve common large-scale training challenges, including complex cluster configuration, hardware failure recovery, and framework optimization. For more information, see [Managed Training on reserved clusters overview](https://docs.cloud.google.com/vertex-ai/docs/training/training-clusters/overview) .

  - ##### manual scaling
    
      - Manual scaling refers to the process of explicitly and deliberately adjusting the number of computational resources (such as virtual machines, containers, or servers) allocated to an application or service by a user or administrator. Unlike autoscaling, which adjusts resources automatically based on demand, manual scaling requires direct intervention to provision or de-provision resources, providing precise control but lacking the dynamic responsiveness of automated solutions. For more information, see [Scale Ray clusters on Vertex AI: Manual scaling](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/scale-clusters#manual_scaling) .

  - ##### manual scaling
    
      - Manual scaling refers to the process of explicitly and deliberately adjusting the number of computational resources (such as virtual machines, containers, or servers) allocated to an application or service by a user or administrator. Unlike autoscaling, which adjusts resources automatically based on demand, manual scaling requires direct intervention to provision or de-provision resources, providing precise control but lacking the dynamic responsiveness of automated solutions. For more information, see [Scale Ray clusters on Vertex AI: Manual scaling](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/scale-clusters#manual_scaling) .

  - ##### Maximum transmission unit (MTU)
    
      - The largest size of a data packet that a network-connected device can transmit. Larger MTU sizes (jumbo frames) can improve network performance for certain workloads. For more information, see [Maximum transmission unit](https://cloud.google.com/vpc/docs/mtu) .

  - ##### MetadataSchema
    
      - A MetadataSchema describes the schema for particular types of artifacts, executions, or contexts. MetadataSchemas are used to validate the key-value pairs during creation of the corresponding Metadata resources. Schema validation is only performed on matching fields between the resource and the MetadataSchema. Type schemas are represented using OpenAPI Schema Objects, which should be described using YAML.

  - ##### MetadataStore
    
      - A MetadataStore is the top-level container for metadata resources. MetadataStore is regionalized and associated with a specific Google Cloud project. Typically, an organization uses one shared MetadataStore for metadata resources within each project.

  - ##### ML pipelines
    
      - ML pipelines are portable and scalable ML workflows that are based on containers.

  - ##### model
    
      - Any model pre-trained or not. In general, any mathematical construct that processes input data and returns output. Phrased differently, a model is the set of parameters and structure needed for a system to make inferences.

  - ##### model distillation (knowledge distillation, teacher-student models)
    
      - Model distillation is a technique that allows a smaller student model to learn from a larger teacher model. The student model is trained to mimic the output of the teacher model, and it can then be used to generate new data or make inferences. Model distillation is often used to make large models more efficient or to make them more accessible to devices with limited resources. It can also be used to improve the generalization of models by reducing overfitting.

  - ##### Model Evaluation
    
      - Vertex AI Model Evaluation is a managed service within Google Cloud's Vertex AI platform that helps the user assess the performance and quality of their machine learning models. It provides tools to generate various evaluation metrics and visualizations, allowing the user to understand how well their models are performing, identify potential biases, and make informed decisions about model deployment and improvement. For more information, see [Model evaluation in Vertex AI](https://cloud.google.com/vertex-ai/docs/evaluation/introduction) .

  - ##### Model Monitoring
    
      - Vertex AI Model Monitoring is a service that continuously evaluates the performance of deployed models by detecting feature skew and drift in prediction requests, helping to maintain model quality over time. For more information, see [Introduction to Vertex AI Model Monitoring](https://cloud.google.com/vertex-ai/docs/model-monitoring/overview) .

  - ##### model resource name
    
      - The resource name for a [`model`](https://docs.cloud.google.com/vertex-ai/docs/reference/rest/v1/projects.locations.models) is as follows: `projects/<PROJECT_ID>/locations/<LOCATION_ID>/models/<MODEL_ID>` . You can find the model's ID in the Cloud console on the Model Registry page.

  - ##### Network File System (NFS)
    
      - A client/server system that lets users access files across a network and treat them as if they resided in a local file directory. For more information, see [Mount a Network File System share](https://cloud.google.com/vertex-ai/docs/training/train-nfs-share) .

  - ##### NVIDIA Collective Communications Library (NCCL)
    
      - A library that provides optimized inter-GPU communication primitives for deep learning frameworks, enabling high-performance multi-GPU training. For more information, see [NVIDIA Collective Communications Library (NCCL)](https://developer.nvidia.com/nccl) .

  - ##### node
    
      - A single virtual machine (Compute Engine instance) within a cluster. In the context of Managed Training on reserved clusters, a node refers to an individual virtual machine (VM) that serves as a single unit of computation within your cluster. Think of it as one of the dedicated worker machines that runs a portion of your overall training job. Each node is equipped with specific resources like CPU, memory, and accelerators (for example, A3 or A4 GPUs), and they all work together in a coordinated way to handle large-scale, distributed training tasks.

  - ##### offline store
    
      - The offline store is a storage facility storing recent and historical feature data, which is typically used for training ML models. An offline store also contains the latest feature values, which you can serve for online inferences.

  - ##### Online inference
    
      - Obtaining inferences on individual instances synchronously. For more information, see [Online inference](https://cloud.google.com/vertex-ai/docs/predictions/overview#online-inference) .

  - ##### Online prediction
    
      - Obtaining predictions on individual instances synchronously. For more information, see [Online prediction](https://cloud.google.com/vertex-ai/docs/predictions/overview#online-inference) .

  - ##### online store
    
      - In feature management, an online store is a storage facility for the latest feature values to be served for online inferences.

  - ##### parameter
    
      - Parameters are keyed input values that configure a run, regulate the behavior of the run, and affect the results of the run. Examples include learning rate, dropout rate, and number of training steps.

  - ##### partition
    
      - In Slurm, a logical grouping of nodes, often used to separate nodes with different hardware configurations.

  - ##### performance tier
    
      - A configuration setting for a Managed Lustre instance that defines its throughput speed (in MBps per TiB) and affects its minimum and maximum capacity.

  - ##### persistent resource
    
      - A type of Vertex AI compute resource, such as a Ray cluster, that remains allocated and available until explicitly deleted, which is beneficial for iterative development and reduces startup overhead between jobs. For more information, see [Get persistent resource information](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-get) .

  - ##### pipeline
    
      - ML pipelines are portable and scalable ML workflows that are based on containers. For more information, see [Introduction to Vertex AI Pipelines](https://cloud.google.com/vertex-ai/docs/pipelines/introduction) .

  - ##### pipeline component
    
      - A self-contained set of code that performs one step in a pipeline's workflow, such as data preprocessing, data transformation, and training a model.

  - ##### pipeline job
    
      - A pipeline job or a pipeline run corresponds to the PipelineJob resource in the Vertex AI API. It's an execution instance of your ML pipeline definition, which is defined as a set of ML tasks interconnected by input-output dependencies.

  - ##### pipeline run
    
      - One or more Vertex PipelineJobs can be associated with an experiment where each PipelineJob is represented as a single run. In this context, the parameters of the run are inferred by the parameters of the PipelineJob. The metrics are inferred from the system.Metric artifacts produced by that PipelineJob. The artifacts of the run are inferred from artifacts produced by that PipelineJob.

  - ##### pipeline template
    
      - An ML workflow definition that a single user or multiple users can reuse to create multiple pipeline runs.

  - ##### positive class
    
      - "Positive class" refers to the outcome or category that a model is trained to predict. For example, if a model is predicting whether a customer will purchase a jacket, the positive class would be "customer purchases a jacket". Similarly, in a model predicting customer signup for a term deposit, the positive class would be "customer signed up". The opposite is the "negative class".

  - ##### Prebuilt container
    
      - Container images provided by Vertex AI that come pre-installed with common ML frameworks and dependencies, simplifying the setup for training and inference jobs. For more information, see [Prebuilt containers for serverless training](https://cloud.google.com/vertex-ai/docs/training/pre-built-containers) .

  - ##### Private Google Access (PGA)
    
      - Private Google Access enables VM instances with only internal (private) IP addresses (no external IP addresses) to reach the public IP addresses of Google APIs and services. For more information, see [Configure Private Google Access](https://cloud.google.com/vpc/docs/configure-private-google-access) .

  - ##### private services access
    
      - Private services access is a private connection between your Virtual Private Cloud (VPC) network and networks owned by Google or third-party service providers. It allows virtual machine (VM) instances in your VPC network to communicate with these services using internal IP addresses, avoiding exposure to the public internet. For more information, see [Private services access](https://cloud.google.com/vpc/docs/private-services-access) .

  - ##### Private Service Connect (PSC)
    
      - Private Service Connect is a technology that allows Compute Engine customers to map private IPs in their network to either another VPC network or to Google APIs. For more information, see [Private Service Connect](https://cloud.google.com/vpc/docs/private-service-connect) .

  - ##### Private Service Connect interface (PSC-I)
    
      - Private Service Connect interface provides a way for producers to initiate connections to any network resources in consumer VPC privately.

  - ##### producer VPC
    
      - A producer VPC is a Virtual Private Cloud (VPC) network that hosts a managed service and makes it available to other VPC networks.

  - ##### quantization
    
      - Quantization is a model optimization technique used to reduce the precision of the numbers used to represent a model's parameters. This can lead to smaller models, lower power consumption, and reduced inference latency.

  - ##### Random Forest
    
      - Random Forest is a machine learning algorithm used for both classification and regression. It's not directly a generative AI model itself, but it's a component that can be used within a larger generative AI system. A random forest consists of multiple decision trees, and its inference is an aggregation of the inferences from these individual trees. For example, in a classification task, each tree "votes" for a class, and the final inference is the class with the most votes For more information, see [Decision forest](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-design-strategies) .

  - ##### Ray client API (Ray Client)
    
      - Ray client is an API that allows a local Python script or interactive shell (such as a Jupyter notebook) to connect to and interact with a remote Ray cluster. Essentially, Ray client enables users to develop and execute Ray code as if the code were running locally, while actually leveraging the distributed computing power of a remote cluster. For more information, see [Ray on Vertex AI overview](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) .

  - ##### Ray cluster on Vertex AI
    
      - A Ray cluster on Vertex AI is a managed cluster of compute nodes that can be used to run distributed machine learning (ML) and Python applications. It provides the infrastructure to perform distributed computing and parallel processing for your ML workflow. Ray clusters are built into Vertex AI to ensure capacity availability for critical ML workloads or during peak seasons. Unlike custom jobs, where the training service releases the resource after job completion, Ray clusters remain available until deleted. For more information, see [Ray on Vertex AI overview](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) .

  - ##### Ray on Vertex AI (RoV)
    
      - Ray on Vertex AI is designed so you can use the same open source Ray code to write programs and develop applications on Vertex AI with minimal changes. For more information, see [Ray on Vertex AI overview](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) .

  - ##### Ray on Vertex AI SDK for Python
    
      - Ray on Vertex AI SDK for Python is a version of the Vertex AI SDK for Python that includes the functionality of the Ray Client, Ray BigQuery connector, Ray cluster management on Vertex AI, and inferences on Vertex AI. For more information, see [Introduction to the Vertex AI SDK for Python](https://cloud.google.com/vertex-ai/docs/python-sdk/use-vertex-ai-python-sdk-ref) .

  - ##### recall
    
      - The percentage of true nearest neighbors returned by the index. For example, if a nearest neighbor query for 20 nearest neighbors returned 19 of the "ground truth" nearest neighbors, the recall is 19/20x100 = 95%.

  - ##### recipe
    
      - In the context of Managed Training, a recipe is a comprehensive and reusable package that contains everything needed to execute a specific large-scale training workload.

  - ##### Reduction Server
    
      - Reduction Server is a feature or component available within Vertex AI, specifically designed to optimize distributed GPU training. Reduction Server functions as an all-reduce algorithm that helps increase throughput and reduce latency for large-scale machine learning model training. For more information, see [Reduce training time with Reduction Server](https://cloud.google.com/vertex-ai/docs/training/distributed-training#reduce_training_time_with_reduction_server) .

  - ##### regularization
    
      - Regularization is a technique used to prevent overfitting in machine learning models. Overfitting occurs when a model learns the training data too well, resulting in poor performance on unseen data. One specific type of regularization mentioned is early stopping, where training is halted before the loss on a validation dataset begins to increase, indicating a decline in generalization performance. For more information, see [Overfitting: L2 regularization](https://developers.google.com/machine-learning/crash-course/overfitting/regularization) .

  - ##### Reinforcement Learning (RL)
    
      - A type of machine learning where an agent learns to make decisions by taking actions in an environment to maximize a cumulative reward. For more information, see [RLHF Tuning with Vertex AI](https://cloud.google.com/blog/products/ai-machine-learning/rlhf-on-google-cloud) .

  - ##### restricts
    
      - Functionality to "restrict" searches to a subset of the index by using Boolean rules. Restrict is also referred to as "filtering". With Vector Search, you can use numeric filtering and text attribute filtering.

  - ##### service account
    
      - Service accounts are special Google Cloud accounts used by applications or virtual machines to make authorized API calls to Google Cloud services. Unlike user accounts, they are not tied to an individual human but act as an identity for your code, enabling secure and programmatic access to resources without requiring human credentials. For more information, see [Service accounts overview](https://cloud.google.com/iam/docs/service-account-overview) .

  - ##### service agent
    
      - A service agent refers to a Google-managed service account. It's utilized when a service requires access to resources created by a different service. For instance, when Dataflow or Dataproc services need to create instances during runtime or when a Cloud Function wants to use the Key Management Service (KMS) to protect the Cloud Function. Service agents are created automatically by Google Cloud when a service requires them. They are typically used to manage access to resources and perform various tasks on behalf of the service. For more information, see [Service agents](https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) .

  - ##### Simple Linux Utility for Resource Management (SLURM)
    
      - Slurm is an open-source, powerful, and widely used workload manager and job scheduler for Linux and Unix-like kernels, especially in high-performance computing (HPC) environments. For more information, see [Slurm workload manager](https://slurm.schedmd.com/documentation.html) .

  - ##### Slurm cluster
    
      - A collection of Compute Engine instances, managed by Slurm, that includes a login node and multiple worker nodes configured for running training jobs. For more information, see [Slurm workload manager](https://slurm.schedmd.com/overview.html) .

  - ##### summary metrics
    
      - Summary metrics are a single value for each metric key in an experiment run. For example, the test accuracy of an experiment is the accuracy calculated against a test dataset at the end of training that can be captured as a single value summary metric.

  - ##### Supervised fine-tuning (SFT)
    
      - A machine learning technique where a pre-trained model is further trained on a smaller, labeled dataset to adapt it to a specific task.

  - ##### TensorBoard
    
      - TensorBoard is a suite of web applications for visualizing and understanding TensorFlow runs and models. For more information, see [TensorBoard](https://www.tensorflow.org/tensorboard/get_started) .

  - ##### TensorBoard instance
    
      - A TensorBoard instance is a regionalized resource that stores Vertex AI TensorBoard Experiments associated with a Project. You can create multiple TensorBoard instances in a project if, for example, you want multiple CMEK enabled instances. This is the same as the TensorBoard resource in the API.

  - ##### TensorBoard Resource name
    
      - A TensorBoard Resource name is used to fully identify a Vertex AI TensorBoard instance. The format is as follows: projects/PROJECT\_ID\_OR\_NUMBER/locations/REGION/tensorboards/TENSORBOARD\_INSTANCE\_ID.

  - ##### TensorFlow Extended (TFX)
    
      - TensorFlow extended (TFX) is an end-to-end platform for deploying production machine learning pipelines based on the TensorFlow platform.

  - ##### TensorFlow Serving container
    
      - A specialized container image designed to efficiently serve TensorFlow models for inferences, used when deploying custom tabular models with Vertex AI Model Monitoring.

  - ##### time offset
    
      - Time offset is relative to the beginning of a video.

  - ##### time segment
    
      - A time segment is identified by beginning and ending time offsets.

  - ##### time series metrics
    
      - Time series metrics are longitudinal metric values where each value represents a step in the training routine portion of a run. Time series metrics are stored in Vertex AI TensorBoard. Vertex AI Experiments stores a reference to the Vertex TensorBoard resource.

  - ##### token
    
      - A token in a language model is the atomic unit that the model is training and making inferences on, namely words, morphemes, and characters. In domains outside of language models, tokens can represent other kinds of atomic units. For example, in computer vision, a token might be a subset of an image. For more information, see [List and count tokens](https://cloud.google.com/vertex-ai/generative-ai/docs/multimodal/list-token) .

  - ##### training cluster
    
      - A training cluster is a group of interconnected computing resources (like virtual machines, GPUs, and associated storage) specifically configured and dedicated to executing machine learning model training workloads in a distributed manner. These clusters are designed to provide the computational power and scalability needed to train complex models efficiently, often leveraging parallel processing across multiple nodes. For more information, see [Structure of the training cluster](https://cloud.google.com/vertex-ai/docs/training/distributed-training.md#cluster-structure) .

  - ##### training set
    
      - In Vertex AI, the training set is the largest portion of your data (typically 80%) used to train a machine learning model. The model learns the patterns and relationships within this data to make inferences. The training set is distinct from the validation and test sets, which are used to evaluate the model's performance during and after training.

  - ##### trajectory
    
      - A "trajectory" refers to a sequence of steps or actions taken by an agent or model. It's often used in the evaluation of generative models, where the model's ability to generate text, code, or other content is assessed. There are several types of trajectory metrics that can be used to evaluate generative models, including trajectory exact match, trajectory in-order match, trajectory any order match, and trajectory precision. These metrics measure the similarity between the model's output and a set of human-generated reference outputs.

  - ##### Transformer
    
      - A "Transformer" is a neural network architecture that underlies most state-of-the-art generative models. It's used in various language model applications, including translation. Transformers consist of an encoder and a decoder; the encoder converts input text into an intermediate representation, and the decoder converts this into useful output. They utilize a self-attention mechanism to gather context from words surrounding the word being processed. While training a Transformer requires significant resources, fine-tuning a pre-trained Transformer for specific applications is more efficient.

  - ##### true positive
    
      - A "true positive" refers to an inference where the model correctly identifies a positive class. For example, if a model is trained to identify customers who will purchase a jacket, a true positive would be correctly predicting that a customer will make such a purchase.

  - ##### unmanaged artifacts
    
      - An artifact that exists outside of the Vertex AI context.

  - ##### vector
    
      - A vector refers to a numerical representation of text, images, or videos that captures relationships between inputs. Machine learning models are suited for creating embeddings by identifying patterns within large datasets. Applications can use embeddings to process and produce language, recognizing complex meanings and semantic relationships specific to the content. For more information, see [Embeddings APIs overview](https://cloud.google.com/vertex-ai/generative-ai/docs/embeddings) .

  - ##### Vertex AI Agent Engine
    
      - Vertex AI Agent Engine, a part of the Vertex AI Platform, is a set of services that enables developers to deploy, manage, and scale AI agents in production. Agent Engine handles the infrastructure to scale agents in production so you can focus on creating applications. For more information, see [Vertex AI Agent Engine overview](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview) .

  - ##### Vertex AI data type
    
      - Vertex AI data types are "image," "text," "tabular," and "video".

  - ##### Vertex AI Experiments
    
      - Vertex AI Experiments lets users track the following: 1. Steps of an experiment run (for example, preprocessing and training). 2. Inputs (for example, algorithm, parameters, and datasets). 3. Outputs of those steps (for example, models, checkpoints, and metrics).

  - ##### Vertex AI Feature Store
    
      - A managed service for storing, serving, and managing machine learning features. For more information, see [About Vertex AI Feature Store](https://cloud.google.com/vertex-ai/docs/featurestore/latest/overview) .

  - ##### Vertex AI Inference
    
      - A Vertex AI service that lets you use a trained machine learning (ML) model to make inferences from new, unseen data. Vertex AI provides services to deploy models for inference. For more information, see [Get inferences from a custom trained model](https://cloud.google.com/vertex-ai/docs/predictions/get-predictions) .

  - ##### Vertex ML Metadata
    
      - A system for tracking and analyzing metadata from machine learning workflows. For more information, see [Introduction to Vertex ML Metadata](https://cloud.google.com/vertex-ai/docs/ml-metadata/introduction) .

  - ##### Vertex AI Model Registry
    
      - The Vertex AI Model Registry is a central repository where you can manage the lifecycle of your ML models. From the Vertex AI Model Registry, you have an overview of your models so you can better organize, track, and train new versions. When you have a model version you would like to deploy, you can assign it to an endpoint directly from the registry, or using aliases, deploy models to an endpoint. For more information, see [Introduction to the Vertex AI Model Registry](https://cloud.google.com/vertex-ai/docs/model-registry/introduction) .

  - ##### Vertex AI SDK for Python
    
      - Vertex AI SDK for Python provides similar functionality as the Vertex AI Python client library, except the SDK is higher-level and less granular.

  - ##### Vertex AI TensorBoard
    
      - Vertex AI TensorBoard is a managed, scalable service on Google Cloud that enables data scientists and ML engineers to visualize their machine learning experiments, debug model training, and track performance metrics using the familiar open-source TensorBoard interface. It integrates seamlessly with Vertex AI Training and other services, providing persistent storage for experiment data and allowing collaborative analysis of model development. For more information, see [Introduction to Vertex AI TensorBoard](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-introduction) .

  - ##### Vertex AI Vizier
    
      - A black-box optimization service for tuning hyperparameters and other parameters. For more information, see [Vertex AI Vizier overview](https://cloud.google.com/vertex-ai/docs/vizier/overview) .

  - ##### Vertex AI Workbench
    
      - Vertex AI Workbench is a unified, Jupyter notebook-based development environment that supports the entire data science workflow, from data exploration and analysis to model development, training, and deployment. Vertex AI Workbench provides a managed and scalable infrastructure with built-in integrations to other Google Cloud services like BigQuery and Cloud Storage, enabling data scientists to perform their machine learning tasks efficiently without managing underlying infrastructure. For more information, see [Introduction to Vertex AI Workbench](https://cloud.google.com/vertex-ai/docs/workbench/introduction) .

  - ##### video segment
    
      - A video segment is identified by beginning and ending time offset of a video.

  - ##### Virtual Machine (VM)
    
      - A Virtual Machine (VM) is a complete computer system that is emulated entirely in software. It runs as a self-contained "guest" on a physical "host" machine. For more information, see [Compute Engine instances](https://cloud.google.com/compute/docs/instances) .

  - ##### Virtual Private Cloud (VPC)
    
      - A secure, isolated private cloud hosted within a public cloud, which lets you define a virtual network that is logically isolated from other virtual networks in Google Cloud. For more information, see [Virtual Private Cloud](https://cloud.google.com/vpc) .

  - ##### VPC Network Peering
    
      - A networking connection that allows two VPC networks to communicate privately. In the context of Managed Training on reserved clusters, VPC Network Peering is a critical component for integrating essential services. For instance, it is the required method for connecting your cluster's VPC to a Filestore instance, which provides the necessary shared \`/home\` directory for all the nodes in your cluster.

  - ##### VPC Service Controls
    
      - VPC Service Controls is a security feature within Google Cloud that lets organizations create secure perimeters around their sensitive data and resources to mitigate the risk of data exfiltration. VPC Service Controls achieves this by restricting access to specified Google Cloud services and data from unauthorized networks and preventing data from moving outside these defined perimeters, thereby providing a strong defense against insider threats and accidental data leakage. For more information, see [VPC Service Controls](https://cloud.google.com/vpc-service-controls/docs) .

  - ##### worker node
    
      - A worker node refers to an individual machine or computational instance within a cluster that's responsible for executing tasks or performing work. In systems like Kubernetes or Ray clusters, nodes are the fundamental units of compute. For more information, see [What is high performance computing (HPC)?](https://cloud.google.com/discover/what-is-high-performance-computing) .

  - ##### worker pool
    
      - Components of a Ray cluster that execute distributed tasks. Worker pools can be configured with specific machine types and support both autoscaling and manual scaling. For more information, see [Structure of the training cluster](https://cloud.google.com/vertex-ai/docs/training/distributed-training#cluster-structure) .

  - ##### zone
    
      - A specific deployment area within a Google Cloud region. In the context of Managed Training on reserved clusters, for best performance, all components of the service (the cluster, Filestore, and Managed Lustre instances) should be created in the same zone.
