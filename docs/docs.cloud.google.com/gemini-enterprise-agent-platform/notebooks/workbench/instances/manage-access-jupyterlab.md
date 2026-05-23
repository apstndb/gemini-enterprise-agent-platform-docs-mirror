---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab
title: Manage access to a Agent Platform Workbench instance's JupyterLab interface
description: Grant a principal access to the JupyterLab interface of a Agent Platform Workbench instance
data_source: docs.cloud.google.com
---

# Manage access to an instance's JupyterLab interface

This page describes how to grant access to the JupyterLab interface of a Gemini Enterprise Agent Platform Workbench instance.

You control access to a Agent Platform Workbench instance's JupyterLab interface through the instance's access mode. You set a JupyterLab access mode when you create a Agent Platform Workbench instance. The access mode can't be changed after the notebook is created.

The JupyterLab access mode determines who can use the instance's JupyterLab interface. The access mode also determines which credentials are used when your instance interacts with other Google Cloud services.

## Access limitations

Granting a principal access to a Agent Platform Workbench instance's JupyterLab interface doesn't grant access to the instance itself. For example, to start, stop, or reset an instance, you must grant the principal access to perform those operations by setting an [IAM policy](https://docs.cloud.google.com/iam/docs/policies) on the instance. To grant access to the Agent Platform Workbench instance, see [Manage access to a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access) .

> **Caution:** When you revoke a user's IAM permissions for a Agent Platform Workbench instance, the user might still be able to access the JupyterLab web interface for up to five days using an existing browser session. To immediately prevent access, stop or reset the Agent Platform Workbench instance.

## JupyterLab access modes

Agent Platform Workbench instances support the following access modes:

  - [Single user only](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab#single-user-only) : The **Single user only** access mode grants access only to the user that you specify.

  - [Service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab#service-account) : The **Service account** access mode grants access to a service account. You can grant access to one or more users through this service account.

> **Note:** To grant access to the instance through the single user option or the service account, you must use an individual's user account email address. Group access is not supported.

## Single user only

When you create a Agent Platform Workbench instance with **Single user only** access, you specify a user account. The specified user account is the only user with access to the JupyterLab interface. If the specified user is not the creator of the instance, you must grant the specified user the [Service Account User role](https://docs.cloud.google.com/iam/docs/service-accounts#user-role) ( `roles/iam.serviceAccountUser` ) on the instance's service account. If the instance needs to access other Google Cloud resources, this service account must also have access to those Google Cloud resources.

> **Note:** When you create a Agent Platform Workbench instance with **Single user only** access, your instance completes the boot process using the Compute Engine default service account. Your specified user account can access the instance after the boot process is finished.

### Grant access to a single user

To grant access to a single user, complete the following steps.

1.  [Create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart) with the following specifications:
    
    1.  In the **Create instance** dialog, in the **IAM and security** section, select the **Single user only** access mode.
    
    2.  In the **User email** field, enter the user account that you want to grant access.

2.  Complete the rest of the dialog, and then click **Create** .

## Service account

When you create a Agent Platform Workbench instance with **Service account** access, you specify a service account. If the instance needs to access other Google resources, this service account must have access to those Google resources also.

When you specify a service account, choose one of the following:

  - Select the Compute Engine default service account.
  - Specify a custom service account. The custom service account must be in the same project as your Agent Platform Workbench instance. To create the instance, you must have the `iam.serviceAccounts.actAs` permission on the service account.

To grant access to users through a service account, you grant the `iam.serviceAccounts.actAs` permission on the specified service account for each user who needs to access JupyterLab.

### Grant access to multiple users through a service account

1.  [Create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart) with the following specifications:
    
    1.  In the **Create instance** dialog, in the **IAM and security** section, select the **Service account** access mode.
    
    2.  Choose the Compute Engine default service account or a [custom service account](https://docs.cloud.google.com/iam/docs/creating-managing-service-accounts) .
        
          - To use the Compute Engine default service account, select **Use Compute Engine default service account** .
        
          - To use a custom service account, clear **Use Compute Engine default service account** , and then, in the **Service account email** field, enter your custom service account email address.

2.  Complete the rest of the dialog, and then click **Create** .

3.  For each user who needs to access JupyterLab, [grant the `iam.serviceAccounts.actAs` permission on your service account](https://docs.cloud.google.com/iam/docs/manage-access-service-accounts) .

## Access mode metadata

The access mode that you configure during Agent Platform Workbench instance creation is stored in the notebook metadata.

When you select the **Single user only** access mode, Agent Platform Workbench stores a value for `proxy-mode` and `proxy-user-mail` . The following are examples of single user access metadata entries:

  - `proxy-mode=mail`
  - `proxy-user-mail=user@example.com`

When you select the **Service account** access mode, Agent Platform Workbench stores a `proxy-mode=service_account` metadata entry.

> **Caution:** Changing the access mode metadata is not supported and can make the JupyterLab interface inaccessible.

## What's next

  - [Grant a principal access to a Agent Platform Workbench instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access)

  - To learn how to grant access to other Google resources, see [Manage access to other resources](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
