---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/set-up-project
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/set-up-project
title: Set up a project for a team
description: Set up access control for a team's project.
data_source: docs.cloud.google.com
---

This page provides examples for how you might set up a project for a team working with Gemini Enterprise Agent Platform. This page assumes that you're already familiar with Identity and Access Management (IAM) concepts such as policies, roles, permissions, and principals as described in [Agent Platform access control with IAM](https://docs.cloud.google.com/vertex-ai/docs/general/access-control) and [Concepts related to access management](https://docs.cloud.google.com/iam/docs/overview#concepts_related_to_access_management) .

These examples are intended to be used generally. Consider the team's specific needs, and adjust how you set up the project accordingly.

## Overview

Agent Platform uses IAM to manage access to resources. When you plan access control for your resources, consider the following:

  - You can manage access at the project level or resource level. Project-level access applies to all of the resources in that project. Access to a specific resource only applies to that resource.

  - You grant access by assigning IAM roles to principals. Predefined roles are available to make it easier to set up access, but custom roles are recommended because you create them, so you can limit their access to only the permissions that are required.

To learn more about access control, see [Agent Platform access control with IAM](https://docs.cloud.google.com/vertex-ai/docs/general/access-control) .

## Single project with shared access to data and Agent Platform resources

In this example, a team shares a single project that contains their data and Agent Platform resources.

You might set up a project this way if the team's data, containers, and other Agent Platform resources can be shared among all users of the project.

Your project's IAM allow policy might look similar to the following:

```json
{
  "version": 1,
  "etag": "BwWKmjvelug=",
  "bindings": [
    {
      "role": "roles/aiplatform.user",
      "members": [
        "user:USER1_EMAIL_ADDRESS",
        "user:USER2_EMAIL_ADDRESS"
      ]
    },
    {
      "role": "roles/storage.admin",
      "members": [
        "user:USER1_EMAIL_ADDRESS",
        "user:USER2_EMAIL_ADDRESS"
      ]
    },
    {
      "role": "roles/aiplatform.serviceAgent",
      "members": [
        "user:service-PROJECT_NUMBER@gcp-sa-aiplatform-cc.iam.gserviceaccount.com"
      ]
    }
  ]
}
```

> **Note:** The project number is a unique identifier for your project. See [Find the project name, number, and ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Setting up a project this way makes it easier for a team to collaborate to train models, debug code, deploy models, and observe endpoints. All users see the same resources and can train with the same data. Agent Platform resources operate within a single project, so you don't need to grant access to resources outside of the project. Quota is shared across the team.

To set up access control for your team's project, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

## Separate data and Agent Platform resources

In this example, the team's data is located in a project separate from Agent Platform resources.

You might set up a project this way if:

  - The team's data is too difficult to move to the same project as your Agent Platform resources.

  - The team's data requires specific control over who can access it.

In these situations, we recommend creating a project for the data and a project for Agent Platform resources. The team's developers share the project that contains the Agent Platform resources. They use the Agent Platform resources to access and process the data stored in the other project. Data administrators grant the Agent Platform resources access through service agents or custom service accounts.

For example, you might grant the default Agent Platform service agents access to a Cloud Storage bucket with an allow policy that looks like the following:

```json
{
  "version": 1,
  "etag": "BwWKmjvelug=",
  "bindings": [
    {
      "role": "roles/storage.objectViewer",
      "members": [
        "user:service-PROJECT_NUMBER@gcp-sa-aiplatform-cc.iam.gserviceaccount.com",
        "user:service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com"
      ]
    }
  ]
}
```

When possible, specify a service account to use as the resource identity when you create Agent Platform resources, and use that service account to manage access control. This makes it easier to grant specific resources access to the data and manage permissions over time.

For example, you might grant a service account access to BigQuery with a policy that looks like the following:

```json
{
  "version": 1,
  "etag": "BwWKmjvelug=",
  "bindings": [
    {
      "role": "roles/bigquery.user",
      "members": [
        "user:SERVICE_ACCOUNT_NAME@PROJECT_NUMBER.iam.gserviceaccount.com"
      ]
    }
  ]
}
```

To set up access control for service accounts, see [Manage access to service accounts](https://docs.cloud.google.com/iam/docs/manage-access-service-accounts) .

In the project with the Agent Platform resources, administrators can grant users access to the data by granting the Service Account User role ( `roles/iam.serviceAccountUser` ) on the specified service accounts.

## Isolate less trusted code in additional separate projects

Models, prediction containers, and training containers are code. It's important to isolate less trusted code from sensitive models and data. Deploy endpoints and training stages in their own projects, use a dedicated service account with very limited permissions, and use VPC Service Controls to isolate them and reduce the impact of access granted to such containers and models.

## What's next

  - To learn more about endpoint access control, see [Control access to Agent Platform endpoints](https://docs.cloud.google.com/vertex-ai/docs/general/endpoint-access-control) .

  - To learn more about using a custom service account to control access to specific resources, see [Use a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .
