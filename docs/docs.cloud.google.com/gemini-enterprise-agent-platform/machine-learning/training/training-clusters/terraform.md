---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/terraform
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/terraform
title: Provision Managed Training Clusters resources with Terraform
description: Learn how to provision Slurm clusters in Managed Training Clusters with Terraform.
data_source: docs.cloud.google.com
---

If you're interested in Managed Training Clusters on Gemini Enterprise Agent Platform, contact your sales representative for access.

You can use Terraform to create, update, import, and delete Slurm clusters in Managed Training Clusters. The `google_vertex_ai_model_development_cluster` resource is available in the `google-beta` provider, version 8.11.0 or later.

HashiCorp Terraform is an infrastructure-as-code (IaC) tool that lets you provision and manage cloud infrastructure. Terraform provides plugins called *providers* that let you interact with cloud providers and other APIs. You can use the *Terraform provider for Google Cloud* to provision and manage Google Cloud resources, including Managed Training Clusters.

This page introduces you to using Terraform with Managed Training Clusters, including an introduction to how Terraform works and some resources to help you get started using Terraform with Google Cloud. You'll also find links to Terraform reference docs for Managed Training Clusters, code examples, and guides for using Terraform to provision Managed Training Clusters resources.

For instructions on how to get started with Terraform for Google Cloud, see [Install and configure Terraform](https://docs.cloud.google.com/docs/terraform/install-configure-terraform) or the [Terraform for Google Cloud quickstart](https://docs.cloud.google.com/docs/terraform/create-vm-instance) .

## How Terraform works

Terraform has a declarative and configuration-oriented syntax, which you can use to describe the infrastructure that you want to provision in your Google Cloud project. After you author this configuration in one or more Terraform configuration files, you can use the Terraform CLI to apply this configuration to your Managed Training Clusters resources.

The following steps explain how Terraform works:

1.  You describe the infrastructure you want to provision in a *Terraform configuration file* . You don't need to write code describing how to provision the infrastructure. Terraform provisions the infrastructure for you.

2.  You run the `terraform plan` command, which evaluates your configuration and generates an execution plan. You can review the plan and make changes as needed.

3.  You run the `terraform apply` command, which performs the following actions:

    1.  It provisions your infrastructure based on your execution plan by invoking the corresponding Managed Training Clusters APIs in the background.

    2.  It creates a *Terraform state file* , which is a JSON file that maps the resources in your configuration file to the resources in the real-world infrastructure. Terraform uses this file to keep a record of the most recent state of your infrastructure, and to determine when to create, update, and destroy resources.

    3.  When you run `terraform apply` , Terraform uses the mapping in the state file to compare the existing infrastructure to the code, and make updates as necessary:

        - If a resource object is defined in the configuration file, but doesn't exist in the state file, Terraform creates it.
        - If a resource object exists in the state file, but has a different configuration from your configuration file, Terraform updates the resource to match your configuration file.
        - If a resource object in the state file matches your configuration file, Terraform leaves the resource unchanged.

## Terraform resources for Managed Training Clusters

*Resources* are the fundamental elements in the Terraform language. Each resource block describes one or more infrastructure objects, such as virtual networks or compute instances.

The following table lists the Terraform resources available for Managed Training Clusters:

| Service                                    | Terraform resources                                                                                                                                                     | Data sources |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Managed Training Clusters (Slurm clusters) | [`google_vertex_ai_model_development_cluster`](https://registry.terraform.io/providers/hashicorp/google-beta/latest/docs/resources/vertex_ai_model_development_cluster) | None         |

## What's next

- [Terraform on Google Cloud documentation](https://docs.cloud.google.com/docs/terraform)
- [Google Cloud provider documentation in HashiCorp](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
- [Infrastructure as code for Google Cloud](https://docs.cloud.google.com/docs/terraform/iac-overview)
