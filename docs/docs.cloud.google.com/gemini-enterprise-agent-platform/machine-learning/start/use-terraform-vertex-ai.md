---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/use-terraform-vertex-ai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/use-terraform-vertex-ai
title: Terraform support for Gemini Enterprise Agent Platform
description: Use Terraform to provision Agent Platform resources.
data_source: docs.cloud.google.com
---

Terraform is an infrastructure as code (IaC) tool that you can use to provision resources and permissions for multiple Google Cloud services, including Gemini Enterprise Agent Platform.

Terraform has a declarative and configuration-oriented syntax, which you can use to describe the infrastructure that you want to provision in your Agent Platform project. After you author this configuration in one or more Terraform configuration files, you can use the Terraform CLI to apply this configuration to your Agent Platform resources.

Consider a scenario where you want to apply a standardized configuration to multiple Gemini Enterprise Agent Platform resources of a specific type. Using Terraform, you can streamline the entire process, as follows:

  - Describe the selected infrastructure in a Terraform configuration file. You don't need to author code describing how to provision this configuration using objects and methods from the Agent Platform API.

  - Use Terraform to evaluate your Terraform configuration and generate an execution plan. Based on this configuration, Terraform indicates what changes it plans to make to the Agent Platform infrastructure.

  - Use Terraform to apply the changes in the execution plan. Terraform invokes the Agent Platform API in the background to apply the planned changes.
    
      - If an Agent Platform resource or infrastructure object defined in the Terraform configuration does not exist, Terraform creates it.
    
      - If an Agent Platform resource or infrastructure object exists but has a different configuration, Terraform updates it to match your Terraform configuration.
    
      - If any Agent Platform resource or infrastructure object matches your Terraform configuration, Terraform leaves it unchanged.

## Terraform resources available for Agent Platform

[Terraform resources](https://developer.hashicorp.com/terraform/language/resources) represent infrastructure objects. The following table lists the Terraform resources that are available for Agent Platform products and services, along with links to Terraform configuration samples:

Agent Platform product or service

Terraform resource

Terraform configuration samples

[Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction)

[`google_workbench_instance`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/workbench_instance)

[View in GitHub](https://github.com/terraform-google-modules/terraform-docs-samples/blob/main/vertex_ai/workbench/main.tf)

[Agent Platform managed datasets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview)

[`google_vertex_ai_dataset`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_dataset)

[View in GitHub](https://github.com/terraform-google-modules/terraform-docs-samples/blob/main/vertex_ai/dataset/main.tf)

[Online inferences (AutoML and custom training)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions)

[`google_vertex_ai_endpoint`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_endpoint)

[View in GitHub](https://github.com/terraform-google-modules/terraform-docs-samples/blob/main/vertex_ai/endpoint/main.tf)

[Model Garden](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-garden/explore-models)

[`google_vertex_ai_endpoint_with_model_garden_deployment`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_endpoint_with_model_garden_deployment)

[Agent Platform Feature Store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/featurestore/latest/overview)

[`google_vertex_ai_feature_group`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_feature_group)

[`google_vertex_ai_feature_group_feature`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_feature_group_feature)

[`google_vertex_ai_feature_online_store`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_feature_online_store)

[`google_vertex_ai_feature_online_store_featureview`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_feature_online_store_featureview)

[Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/ml-metadata/introduction)

[`google_vertex_ai_metadata_store`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_metadata_store)

[View in GitHub](https://github.com/terraform-google-modules/terraform-docs-samples/blob/main/vertex_ai/metadata_store_cmek/main.tf)

[Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/matching-engine/overview)

[`google_vertex_ai_index`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_index)

[View in GitHub](https://github.com/terraform-google-modules/terraform-docs-samples/blob/main/vertex_ai/index/main.tf)

[`google_vertex_ai_index_endpoint`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_index_endpoint)

[`google_vertex_ai_index_endpoint_deployed_index`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_index_endpoint_deployed_index)

[Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/experiments/tensorboard-introduction)

[`google_vertex_ai_tensorboard`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_tensorboard)

[View in GitHub](https://github.com/terraform-google-modules/terraform-docs-samples/blob/main/vertex_ai/tensorboard/main.tf)

## Learn more about Terraform

  - [Terraform Developer website](https://developer.hashicorp.com/terraform/)

  - [What is Terraform?](https://developer.hashicorp.com/terraform/intro)

  - [Terraform Language Documentation](https://developer.hashicorp.com/terraform/language)

  - [Terraform CLI Documentation](https://developer.hashicorp.com/terraform/cli)

  - [Terraform registry](https://registry.terraform.io/providers/hashicorp/google/latest/docs/)
