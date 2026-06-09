---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata
title: Manage features through metadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to manage some Vertex AI Workbench instance features by modifying the instance's metadata key-value pairs.

## Metadata keys

For information about features and their respective metadata keys, see the following table.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Description</th>
<th>Metadata key</th>
<th>Accepted values and defaults</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Enables Cloud Storage FUSE on a container image</td>
<td><p>Mounts <code dir="ltr" translate="no">/dev/fuse</code> onto the container and enables <code dir="ltr" translate="no">gcsfuse</code> for use on the container.</p></td>
<td><code dir="ltr" translate="no">container-allow-fuse</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Enables Cloud Storage FUSE.</li>
<li><code dir="ltr" translate="no">false</code> (default): Doesn't enable Cloud Storage FUSE.</li>
</ul></td>
</tr>
<tr class="even">
<td>nbconvert</td>
<td><p>Lets you export and download notebooks as a different file type.</p></td>
<td><code dir="ltr" translate="no">notebook-disable-nbconvert</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Turns off nbconvert.</li>
<li><code dir="ltr" translate="no">false</code> (default): Enables nbconvert.</li>
</ul></td>
</tr>
<tr class="odd">
<td>Delete to trash</td>
<td><p>Uses the operating system's trash behavior when deleting from JupyterLab.</p></td>
<td><code dir="ltr" translate="no">notebook-enable-delete-to-trash</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Enables deleting to the trash.</li>
<li><code dir="ltr" translate="no">false</code> (default): Uses the default JupyterLab behavior.</li>
</ul></td>
</tr>
<tr class="even">
<td>Managed Service for Apache Spark</td>
<td><p>Enables access to Managed Service for Apache Spark kernels.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-dataproc-enabled">Create a Managed Service for Apache Spark-enabled instance</a> .</p></td>
<td><code dir="ltr" translate="no">disable-mixer</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Turns off access to Managed Service for Apache Spark kernels.</li>
<li><code dir="ltr" translate="no">false</code> (default): Enables access to Managed Service for Apache Spark kernels.</li>
</ul></td>
</tr>
<tr class="odd">
<td>Idle shutdown</td>
<td><p>Enables idle shutdown.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown">Idle shutdown</a> .</p></td>
<td><code dir="ltr" translate="no">idle-timeout-seconds</code></td>
<td>An integer representing the idle time in seconds. The default value is <code dir="ltr" translate="no">10800</code> seconds (180 minutes).</td>
</tr>
<tr class="even">
<td>Guest attributes</td>
<td><p>Enables guest attributes. Required for running idle shutdown.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown#requirements">Requirements for running idle shutdown</a> .</p></td>
<td><code dir="ltr" translate="no">enable-guest-attributes</code></td>
<td><code dir="ltr" translate="no">true</code> (default): Enables guest attributes.
<code dir="ltr" translate="no">false</code> : Turns off guest attributes.</td>
</tr>
<tr class="odd">
<td>Scheduled OS patches</td>
<td><p>Schedules automatic OS updates of the instance. This enables Debian's <a href="https://wiki.debian.org/UnattendedUpgrades">unattended upgrade service</a> and only applies to VM-based images.</p></td>
<td><code dir="ltr" translate="no">install-unattended-upgrades</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Turns on automatic OS updates.</li>
<li><code dir="ltr" translate="no">false</code> (default): Turns off automatic OS updates.</li>
</ul></td>
</tr>
<tr class="even">
<td>Custom Jupyter user</td>
<td><p>Specifies the name of the default Jupyter user. This setting determines the name of the folder for your notebooks. For example, instead of the default <code dir="ltr" translate="no">/home/jupyter/</code> directory, you can change the directory to <code dir="ltr" translate="no">/home/          CUSTOM_NAME        </code> . This metadata key doesn't affect access to the instance.</p></td>
<td><code dir="ltr" translate="no">jupyter-user</code></td>
<td>A string. The default value is <code dir="ltr" translate="no">jupyter</code> .</td>
</tr>
<tr class="odd">
<td>File downloading</td>
<td><p>Lets you download files from JupyterLab.</p></td>
<td><code dir="ltr" translate="no">notebook-disable-downloads</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Turns off file downloading.</li>
<li><code dir="ltr" translate="no">false</code> (default): Enables file downloading.</li>
</ul></td>
</tr>
<tr class="even">
<td>Root access</td>
<td><p>Enables root access.</p></td>
<td><code dir="ltr" translate="no">notebook-disable-root</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Turns off root access.</li>
<li><code dir="ltr" translate="no">false</code> (default): Enables root access.</li>
</ul></td>
</tr>
<tr class="odd">
<td>Terminal access</td>
<td><p>Enables terminal access.</p></td>
<td><code dir="ltr" translate="no">notebook-disable-terminal</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> : Turns off terminal access.</li>
<li><code dir="ltr" translate="no">false</code> (default): Enables terminal access.</li>
</ul></td>
</tr>
<tr class="even">
<td>Scheduled upgrades</td>
<td><p>Schedules automatic upgrades of the instance.</p></td>
<td><code dir="ltr" translate="no">notebook-upgrade-schedule</code></td>
<td>The weekly or monthly schedule that you set, in <a href="https://man7.org/linux/man-pages/man5/crontab.5.html">unix-cron format</a> , for example, <code dir="ltr" translate="no">00 19 * * MON</code> means weekly on Monday, at 1900 hours Greenwich Mean Time (GMT). This feature is off by default.</td>
</tr>
<tr class="odd">
<td>Post-startup script</td>
<td><p>Runs a custom script after other startup scripts have completed. For details on the execution order, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata#startup-script-order">Startup script execution order</a> .</p></td>
<td><code dir="ltr" translate="no">post-startup-script</code></td>
<td>The URI of a post-startup script in Cloud Storage, for example: <code dir="ltr" translate="no">gs://bucket/hello.sh</code> . This feature is off by default.</td>
</tr>
<tr class="even">
<td>Post-startup script behavior</td>
<td><p>Defines when and how the post-startup script runs.</p></td>
<td><code dir="ltr" translate="no">post-startup-script-behavior</code></td>
<td><ul>
<li><code dir="ltr" translate="no">run_once</code> (default): Runs the post-startup script once after instance creation or upgrade.</li>
<li><code dir="ltr" translate="no">run_every_start</code> : Runs the post-startup script after every start.</li>
<li><code dir="ltr" translate="no">download_and_run_every_start</code> : Redownloads the post-startup script from its source then runs the script after every start.</li>
</ul></td>
</tr>
<tr class="odd">
<td>Report event health</td>
<td><p>Checks health every 30 seconds for VM metrics.</p></td>
<td><code dir="ltr" translate="no">report-event-health</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> (default): Enables event health reporting.</li>
<li><code dir="ltr" translate="no">false</code> : Turns off event health reporting.</li>
</ul></td>
</tr>
<tr class="even">
<td>Enable JupyterLab 4 or switch to JupyterLab 3</td>
<td><p>Enable JupyterLab 3. JupyterLab 4 is enabled, by default.</p></td>
<td><code dir="ltr" translate="no">enable-jupyterlab4</code></td>
<td><ul>
<li><code dir="ltr" translate="no">true</code> (default): Enables JupyterLab 4.</li>
<li><code dir="ltr" translate="no">false</code> : Enables JupyterLab 3.</li>
</ul></td>
</tr>
</tbody>
</table>

## Startup script execution order

If you use multiple startup scripts for your Vertex AI Workbench instance, they run in the following order:

1.  `startup-script` : Runs first during each boot after the initial boot.
2.  `startup-script-url` : Runs second during each boot after the initial boot.
3.  `workbench-startup-scripts` : Runs after the Compute Engine boot scripts ( `startup-script` and `startup-script-url` ) complete.
4.  `post-startup-script` : Runs after the `workbench-startup-scripts` complete.

Note that for the `post-startup-script` metadata key, you must provide the script as a Cloud Storage URI. You cannot provide the script content directly as the value.

## Metadata managed by Compute Engine

Some of the metadata keys are predefined by Compute Engine. For more information, see [Predefined metadata keys](https://docs.cloud.google.com/compute/docs/metadata/predefined-metadata-keys) .

## Protected metadata keys

Some metadata keys are reserved for system use only. If you assign values to these metadata keys, the new values will be overwritten by the system values.

Reserved metadata keys include and are not limited to:

  - `agent-health-check-interval-seconds`
  - `agent-health-check-path`
  - `cos-update-strategy`
  - `custom-container-image`
  - `custom-container-payload`
  - `data-disk-uri`
  - `dataproc-allow-custom-clusters`
  - `dataproc-cluster-name`
  - `dataproc-configs`
  - `dataproc-default-subnet`
  - `dataproc-locations-list`
  - `dataproc-machine-types-list`
  - `dataproc-notebooks-url`
  - `dataproc-region`
  - `dataproc-service-account`
  - `disable-check-xsrf`
  - `euc-enabled`
  - `framework`
  - `generate-diagnostics-bucket`
  - `generate-diagnostics-file`
  - `generate-diagnostics-options`
  - `google-logging-enabled`
  - `image-url`
  - `install-monitoring-agent`
  - `install-nvidia-driver`
  - `installed-extensions`
  - `last_updated_diagnostic`
  - `last_updated_diagnostics`
  - `notebooks-api`
  - `notebooks-api-version`
  - `notebooks-examples-location`
  - `notebooks-location`
  - `proxy-backend-id`
  - `proxy-byoid-url`
  - `proxy-mode`
  - `proxy-status`
  - `proxy-url`
  - `proxy-user-mail`
  - `report-container-health`
  - `report-event-url`
  - `report-notebook-metrics`
  - `report-system-health`
  - `report-system-status`
  - `resource-url`
  - `restriction`
  - `serial-port-logging-enable`
  - `service-account-mode`
  - `shutdown-script`
  - `title`
  - `use-collaborative`
  - `user-data`
  - `version`

## Create an instance with specific metadata

You can create a Vertex AI Workbench instance with specific metadata by using the Google Cloud console, the Google Cloud CLI, Terraform, or the Notebooks API.

### Console

When you create a Vertex AI Workbench instance, you can add metadata in the **Environment** section of **Advanced options** .

![The Add metadata button in the Environment section](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/metadata-during-create.png)

### gcloud

When you create a Vertex AI Workbench instance, you can add metadata by using the following command:

    gcloud workbench instances create INSTANCE_NAME --metadata=KEY=VALUE

### Terraform

To add metadata, create the resource with metadata key-value pairs.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

```terraform
resource "google_workbench_instance" "default" {
  name     = "workbench-instance-example"
  location = "us-central1-a"

  gce_setup {
    machine_type = "n1-standard-1"
    vm_image {
      project = "cloud-notebooks-managed"
      family  = "workbench-instances"
    }
    metadata = {
      key = "value"
    }
  }
}
```

### Notebooks API

Use the [`instances.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create) method with metadata values to manage the corresponding features.

## Update an instance's metadata

You can update the metadata of a Vertex AI Workbench instance by using the Google Cloud console, the Google Cloud CLI, Terraform, or the Notebooks API.

### Console

To update the metadata of a Vertex AI Workbench instance, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  In the list of instances, click the name of the instance that you want to update.

3.  On the **Instance details** page, click **Software and security** .

4.  In the **Metadata** section, update the metadata key-value pairs that you want to change.

5.  Click **Submit** .

### gcloud

You can update the metadata on a Vertex AI Workbench instance by using the following command:

    gcloud workbench instances update INSTANCE_NAME --metadata=KEY=VALUE

### Terraform

You can change the metadata key-value pairs to manage the corresponding features on Vertex AI Workbench instances.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

```terraform
resource "google_workbench_instance" "default" {
  name     = "workbench-instance-example"
  location = "us-central1-a"

  gce_setup {
    machine_type = "n1-standard-1"
    vm_image {
      project = "cloud-notebooks-managed"
      family  = "workbench-instances"
    }
    metadata = {
      key = "updated_value"
    }
  }
}
```

### Notebooks API

Use the [`instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method with metadata values and `gce_setup.metadata` in the `updateMask` to manage the corresponding features.

## Remove metadata from an instance

You can remove metadata from a Vertex AI Workbench instance by using the Google Cloud console, the Google Cloud CLI, Terraform, or the Notebooks API.

### Console

To remove metadata from a Vertex AI Workbench instance, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  In the list of instances, click the name of the instance that you want to modify.

3.  On the **Instance details** page, click **Software and security** .

4.  In the **Metadata** section, to the right of a key-value pair that you want to delete, click delete **Delete** .

5.  Click **Submit** .

### gcloud

You can remove metadata from a Vertex AI Workbench instance by using the following command:

    gcloud workbench instances update INSTANCE_NAME --metadata=KEY

### Terraform

You can remove metadata key-value pairs to manage the corresponding features of a Vertex AI Workbench instance.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

```terraform
resource "google_workbench_instance" "default" {
  name     = "workbench-instance-example"
  location = "us-central1-a"

  gce_setup {
    machine_type = "n1-standard-1"
    vm_image {
      project = "cloud-notebooks-managed"
      family  = "workbench-instances"
    }
    metadata = {
    }
  }
}
```

### Notebooks API

Use the [`instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method with the metadata value set to an empty string and `gce_setup.metadata` in the `updateMask` to remove the corresponding feature.
