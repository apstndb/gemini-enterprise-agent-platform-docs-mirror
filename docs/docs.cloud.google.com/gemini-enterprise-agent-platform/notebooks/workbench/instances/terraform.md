---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/terraform
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/terraform
description: Learn how to provision Terraform for Vertex AI Workbench resources
data_source: docs.cloud.google.com
---

Provision Vertex AI Workbench resources with Terraform

HashiCorp Terraform is an infrastructure-as-code (IaC) tool that lets you provision and manage cloud infrastructure. Terraform provides plugins called *providers* that let you interact with cloud providers and other APIs. You can use the *Terraform provider for Google Cloud* to provision and manage Google Cloud resources, including Vertex AI Workbench.

This page introduces you to using Terraform with Vertex AI Workbench, including an introduction to how Terraform works and some resources to help you get started using Terraform with Google Cloud. You'll also find links to Terraform reference docs for Vertex AI Workbench, code examples, and guides for using Terraform to provision Vertex AI Workbench resources.

For instructions on how to get started with Terraform for Google Cloud, see [Install and configure Terraform](https://docs.cloud.google.com/docs/terraform/install-configure-terraform) or the [Terraform for Google Cloud quickstart](https://docs.cloud.google.com/docs/terraform/create-vm-instance) .

## How Terraform works

Terraform has a declarative and configuration-oriented syntax, which you can use to describe the infrastructure that you want to provision in your Google Cloud project. After you author this configuration in one or more Terraform configuration files, you can use the Terraform CLI to apply this configuration to your Vertex AI Workbench resources.

The following steps explain how Terraform works:

1.  You describe the infrastructure you want to provision in a *Terraform configuration file* . You don't need to write code describing how to provision the infrastructure. Terraform provisions the infrastructure for you.

2.  You run the `terraform plan` command, which evaluates your configuration and generates an execution plan. You can review the plan and make changes as needed.

3.  You run the `terraform apply` command, which performs the following actions:
    
    1.  It provisions your infrastructure based on your execution plan by invoking the corresponding Vertex AI Workbench APIs in the background.
    
    2.  It creates a *Terraform state file* , which is a JSON file that maps the resources in your configuration file to the resources in the real-world infrastructure. Terraform uses this file to keep a record of the most recent state of your infrastructure, and to determine when to create, update, and destroy resources.
    
    3.  When you run `terraform apply` , Terraform uses the mapping in the state file to compare the existing infrastructure to the code, and make updates as necessary:
        
          - If a resource object is defined in the configuration file, but doesn't exist in the state file, Terraform creates it.
          - If a resource object exists in the state file, but has a different configuration from your configuration file, Terraform updates the resource to match your configuration file.
          - If a resource object in the state file matches your configuration file, Terraform leaves the resource unchanged.

## Terraform resources for Vertex AI Workbench

*Resources* are the fundamental elements in the Terraform language. Each resource block describes one or more infrastructure objects, such as virtual networks or compute instances.

The following table lists the Terraform resources available for Vertex AI Workbench:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Service</th>
<th>Terraform resources</th>
<th>Data sources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Vertex AI Workbench</td>
<td><ul>
<li><a href="https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/workbench_instance"><code dir="ltr" translate="no">google_workbench_instance</code></a></li>
<li><a href="https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/workbench_instance_iam"><code dir="ltr" translate="no">google_workbench_instance_iam</code></a></li>
</ul></td>
<td><a href="https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/workbench_instance_iam_policy"><code dir="ltr" translate="no">google_workbench_instance_iam_policy</code></a></td>
</tr>
</tbody>
</table>

## Terraform-based guides for Vertex AI Workbench

The following table lists Terraform-based how-to guides and tutorials for Vertex AI Workbench:

| **Guide**                                                                                                                                                            | **Details**                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [Create a Vertex AI Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#terraform)               | Create a Vertex AI Workbench instance with a basic configuration.                                  |
| [Manage idle shutdown on Terraform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown#terraform)            | Configure the idle shutdown settings on a Vertex AI Workbench instance.                            |
| [Upgrade a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#upgrade-container) | Change the `container_image` field in the Terraform configuration to update the container payload. |
| [Create an instance with specific metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata#terraform)  | Create a Vertex AI Workbench instance with specific metadata.                                      |

## Terraform modules and blueprints for Vertex AI Workbench

Modules and blueprints help you automate provisioning and managing of Google Cloud resources at scale. A *module* is a reusable set of Terraform configuration files that creates a logical abstraction of Terraform resources. A *blueprint* is a package of deployable and reusable modules, and a policy that implements and documents a specific solution.

The following table lists modules and blueprints related to Vertex AI Workbench:

| Module or blueprint                                                                  | Details                                                                                      |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| [`ai-notebook`](https://github.com/GoogleCloudPlatform/notebooks-blueprint-security) | This module demonstrates how to protect confidential data in a Vertex AI Workbench instance. |

## What's next

  - [Terraform code samples for Vertex AI Workbench](https://docs.cloud.google.com/docs/samples?language=terraform)
  - [Terraform on Google Cloud documentation](https://docs.cloud.google.com/docs/terraform)
  - [Google Cloud provider documentation in HashiCorp](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
  - [Infrastructure as code for Google Cloud](https://docs.cloud.google.com/docs/terraform/iac-overview)
