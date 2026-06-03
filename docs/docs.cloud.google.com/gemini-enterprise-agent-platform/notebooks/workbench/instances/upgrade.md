---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade
title: Upgrade the environment of a Agent Platform Workbench instance
description: Upgrade the environment of a Agent Platform Workbench instance
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform Workbench instances are [Deep Learning VM Images](https://docs.cloud.google.com/ai-platform/deep-learning-vm/docs/introduction) instances with JupyterLab notebook environments enabled and ready for use. This page describes how to upgrade the environment of a Agent Platform Workbench instance.

## Reasons to upgrade

You might want to upgrade the environment of your Agent Platform Workbench instance for any of the following reasons:

  - To use new capabilities that are only available in a newer version of your environment.

  - To benefit from framework updates, package updates, and bug fixes that have been implemented in a newer version of your environment.

## Upgrade methods

There are two ways to upgrade a Agent Platform Workbench instance:

  - **Automatic upgrade** : Enable auto upgrade when you create a Agent Platform Workbench instance. During a recurring time period that you specify, Agent Platform Workbench checks whether your instance can be upgraded, and if so, Agent Platform Workbench upgrades your instance.

  - **Manual upgrade** : If an existing Agent Platform Workbench instance meets the [requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade#requirements) for upgrading, you can upgrade the instance manually.

## Requirements and limitations

Backward compatibility with your Agent Platform Workbench isn't guaranteed. [Make a copy of your data](https://docs.cloud.google.com/vertex-ai/docs/general/troubleshooting-workbench#copy-user-data) before upgrading a Agent Platform Workbench instance.

To determine whether you can upgrade a specific Agent Platform Workbench instance, see the following requirements and limitations:

  - The Notebooks API must be [enabled in the instance's Google Cloud project](https://console.cloud.google.com/apis/library/notebooks.googleapis.com) . For more information, see [List enabled services](https://docs.cloud.google.com/service-usage/docs/list-services#enabled) and [Enable an API](https://docs.cloud.google.com/endpoints/docs/openapi/enable-api#enabling_an_api) .

  - If your Agent Platform Workbench instance is container-based, Agent Platform Workbench upgrades the OS. The image version depends on the specific image pulled by your Dockerfile.
    
    To help make sure the upgrade uses the most recent version of the image, consider using the `latest` tag in your Dockerfile.

If upgrading your instance is not an option for you, consider [migrating your data to a new Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/migrate) .

## How the upgrade works

Agent Platform Workbench instances that can be upgraded are dual-disk, with one boot disk and one data disk. The upgrade process upgrades the boot disk to a new image while preserving your data on the data disk.

### Which components are upgraded or preserved?

The following table shows which components of your Agent Platform Workbench instance are upgraded and which are preserved.

| Component                                    | Upgrade result                                                                                                                                                                                   |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Machine learning frameworks                  | Upgraded                                                                                                                                                                                         |
| Machine learning data                        | Preserved                                                                                                                                                                                        |
| Preinstalled dependencies                    | Upgraded                                                                                                                                                                                         |
| User-installed libraries                     | By default, must be reinstalled (see [User-installed libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade#user-installed-libraries) ) |
| Local files in the `/home/jupyter` directory | Preserved                                                                                                                                                                                        |
| Local files in any other `/home/` directory  | Not preserved                                                                                                                                                                                    |
| Preinstalled operating system packages       | Upgraded                                                                                                                                                                                         |
| User-installed operating system packages     | Not preserved                                                                                                                                                                                    |
| GPU drivers                                  | Upgraded                                                                                                                                                                                         |
| Notebooks                                    | Preserved                                                                                                                                                                                        |
| User configurations                          | Preserved                                                                                                                                                                                        |

#### User-installed libraries

By default, Agent Platform Workbench instances store pip and Conda libraries in the boot disk, which is replaced during an upgrade. When you install pip libraries, you can include the `--user` flag to install them in the `/home/jupyter/` directory, where they are preserved during an upgrade.

By default, if you install pip or Conda libraries in a kernel created from a custom container, the libraries only persist while the kernel is running. Each time the kernel is restarted, those libraries will need to be reinstalled. To install persistent libraries in a custom container, include the library installations in your Dockerfile. When installing pip libraries in a kernel created from a custom container, you can include the `--user` flag so that the libraries will persist until instance restart.

### Environment versions

Your Agent Platform Workbench instance has an environment version number that you can verify:

1.  In the Google Cloud console, go to the **Instances** page.

2.  In the list of instances, find the version number of your instance's environment in the **Version** column.

Agent Platform Workbench updates environments regularly (see the [Release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) ), but with each released version, not all of the environments are updated. Agent Platform Workbench only upgrades an instance if there is a newer environment version for the VM image that your instance is based on.

For information about how to use a specific version to create a Agent Platform Workbench instance, see [Create a specific version of a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version) .

## Before you begin

Before you upgrade, complete the following steps.

1.  Check the [release notes](https://docs.cloud.google.com/vertex-ai/docs/release-notes) to learn about updates to newer versions.

2.  [Make a copy of your data](https://docs.cloud.google.com/vertex-ai/docs/general/troubleshooting-workbench#copy-user-data) as a backup.

## Automatic upgrade

Agent Platform Workbench can automatically upgrade instances that are running. If your instance is stopped, it doesn't automatically upgrade your instance, even if you enabled auto upgrade when you created it.

When you enable automatic environment upgrades, you specify a recurring time period in which Agent Platform Workbench checks whether the instance can be upgraded, and if it can be, upgrades the instance.

The time period you specify is stored as a `notebook-upgrade-schedule` metadata entry, in [unix-cron format](https://man7.org/linux/man-pages/man5/crontab.5.html) , Greenwich Mean Time (GMT).

To check whether an instance can be upgraded, Agent Platform Workbench uses the API method [`checkUpgradability`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/checkUpgradability) . This method checks for a newer version of the image on the instance's boot disk.

If the instance can be upgraded, Agent Platform Workbench uses an internal upgrade method to upgrade the instance.

### Create a Agent Platform Workbench instance with auto upgrade enabled

To create a Agent Platform Workbench instance with auto upgrade enabled, select the **Enable environment auto-upgrade** checkbox and set a schedule when you create the instance.

You can specify auto-upgrade by using the Google Cloud console.

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Details** section, provide the following information for your new instance:
    
      - **Name** : Provide a name for your new instance.
      - **Region** and **Zone** : Select a region and zone for the new instance. For best network performance, select the region that is geographically closest to you. See the available [Agent Platform Workbench locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations#instances) .

5.  In the **System health** section, select **Environment auto-upgrade** .

6.  Choose whether to upgrade your notebook **Weekly** or **Monthly** .

7.  In the **Weekday** field, select the option that you want.

8.  In the **Hour** field, choose an hour of the day.

9.  Complete the rest of the instance creation dialog, and then click **Create** .

### Edit the auto upgrade schedule

To edit the auto upgrade schedule after you have created your Agent Platform Workbench instance, complete the following steps:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click the instance name that needs the schedule change.

3.  On the **Instance details** page, in the **Environment auto-upgrade** section, edit the schedule.

4.  Click **Submit** to save your changes.

## Manual upgrade

You can manually upgrade Agent Platform Workbench instances that meet the [requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade#requirements) .

### Check for a newer version of your instance's environment

To check whether a newer version of your instance's environment is available, access your instance from the Google Cloud console.

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click the instance name that you want to check for availability of a newer environment version.

3.  On the **Instance details** page, next to **VM details** , click **View in Compute Engine** .
    
    If a newer version of the environment is available, a "This instance needs to be upgraded" message appears.

### Upgrade your instance's environment to a newer version

You can manually upgrade a Agent Platform Workbench instance in the Google Cloud console.

> **Note:** Upgrades can affect user operations that are running.

1.  In the Google Cloud console, go to the **Instances** page.

2.  If your instance isn't running, [start the instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart#start_your_instance) . Agent Platform Workbench can only upgrade instances when they're running.

3.  Click the instance name that you want to upgrade.

4.  On the **Instance details** page, click ![](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/upgrade.png) **Upgrade** .

5.  Make sure you have [made a copy of the data on your instance](https://docs.cloud.google.com/vertex-ai/docs/general/troubleshooting-workbench#copy-user-data) before continuing.

6.  After your data is backed up, click **Upgrade** . Agent Platform Workbench upgrades and starts your instance.

## Roll back an upgrade

To roll back an upgrade, complete the following steps:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click the instance name that you would like to roll back.

3.  On the **Instance details** page, under **Upgrade history** , click **Rollback** .

4.  Agent Platform Workbench rolls your instance back to the previous version.
