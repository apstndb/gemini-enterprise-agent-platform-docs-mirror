---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-standalone
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-standalone
title: Create a secure Gemini Enterprise Agent Platform Workbench instance in a VPC network
description: This tutorial shows you how to secure a Gemini Enterprise Agent Platform Workbench instance by creating it in a standalone VPC network.
data_source: docs.cloud.google.com
---

This tutorial is intended for enterprise data scientists, researchers, and network administrators. It shows how to secure a Agent Platform Workbench instance by creating it in a Virtual Private Cloud (VPC) network.

A [*VPC network*](https://docs.cloud.google.com/vpc/docs/overview) is a virtual version of a physical network that is implemented inside of Google's production network. It is a private network, with its own private IP addresses, subnets, and network gateways. In the enterprise, VPC networks are used to protect data and instances by controlling access to them from other networks and from the internet.

The VPC network in this tutorial is a standalone network. However, you can share a VPC network from one project (called a host project) to other projects in your Google Cloud organization. To learn more about which type of VPC network to use, see [Single VPC network and Shared VPC](https://cloud.google.com/architecture/best-practices-vpc-design#single_vpc_network_and) .

Following network security best practices, the VPC network in this tutorial uses a combination of [Cloud Router](https://docs.cloud.google.com/network-connectivity/docs/router/concepts/overview) , [Cloud NAT](https://docs.cloud.google.com/nat/docs/overview) , and [Private Google Access](https://docs.cloud.google.com/vpc/docs/private-google-access) to secure the instance in the following ways:

  - The Agent Platform Workbench instance doesn't have an external IP address.
  - The instance has outbound internet access through a regional Cloud Router and Cloud NAT gateway so that you can install software packages or other dependencies. Cloud NAT allows outbound connections and the inbound responses to those connections. It does *not* permit unsolicited inbound requests from the internet.
  - The instance uses Private Google Access to reach the external IP addresses of Google APIs and services.

The tutorial also shows how to do the following:

  - Create a post-startup script to automatically clone a GitHub repo into the newly created Agent Platform Workbench instance.
  - Use [Cloud Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics) to monitor the Agent Platform Workbench instance.
  - Use the [Compute Engine](https://docs.cloud.google.com/compute/docs/instances/schedule-instance-start-stop) API to start and stop the instance automatically to optimize costs.

![Architectural diagram of a Agent Platform Workbench instance in a VPC network.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-netsec-codelab1.png)

## Objectives

  - Create a VPC network and add a subnet that has Private Google Access enabled.
  - Create a Cloud Router and Cloud NAT for the VPC network.
  - Create a Agent Platform Workbench instance in the subnet, using a post-startup script that clones the [Google Cloud Generative AI](https://github.com/GoogleCloudPlatform/generative-ai/) GitHub repository.
  - Enable Cloud Monitoring for the instance.
  - Create a VM instance schedule and attach it to the instance.

## Costs

In this document, you use the following billable components of Google Cloud:

  - [Cloud NAT](https://docs.cloud.google.com/nat/pricing)
  - [Compute Engine](https://cloud.google.com/compute/all-pricing)
  - [Cloud Storage](https://docs.cloud.google.com/storage/pricing)
  - [Gemini Enterprise Agent Platform](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing)
  - [Virtual Private Cloud](https://docs.cloud.google.com/vpc/pricing)

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-standalone#clean-up) .

## Before you begin

1.  In the Google Cloud console, go to the project selector page.

2.  Select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `roles/resourcemanager.projectCreator` ), which contains the `resourcemanager.projects.create` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

3.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  Open [Cloud Shell](https://docs.cloud.google.com/shell/docs/launching-cloud-shell-editor) to execute the commands listed in this tutorial. Cloud Shell is an interactive shell environment for Google Cloud that lets you manage your projects and resources from your web browser.

5.  In the Cloud Shell, set the current project to your Google Cloud project ID and store the same project ID into the `projectid` shell variable:
    
    ``` 
      projectid="PROJECT_ID"
      gcloud config set project ${projectid}
    ```
    
    Replace PROJECT\_ID with your project ID. If necessary, you can locate your project ID in the Google Cloud console. For more information, see [Find your project ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/prerequisites#find-project-id) .

6.  Enable the IAM, Compute Engine, Notebooks, Cloud Storage, and Agent Platform APIs:
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
        gcloud services enable iam.googleapis.com  compute.googleapis.com notebooks.googleapis.com storage.googleapis.com aiplatform.googleapis.com

7.  If you're not the project owner, ask the project owner to grant you the [Project IAM Admin (roles/resourcemanager.projectIamAdmin)](https://docs.cloud.google.com/resource-manager/docs/access-control-proj#resourcemanager.projectIamAdmin) role. You must have this role to grant IAM roles in the next step.

8.  Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/aiplatform.user, roles/compute.networkAdmin, roles/compute.securityAdmin, roles/compute.instanceAdmin, roles/monitoring.viewer, roles/notebooks.admin, roles/resourcemanager.projectIamAdmin, roles/iam.serviceAccountAdmin, roles/iam.serviceAccountUser, roles/storage.Admin`
    
        gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE
    
    Replace the following:
    
      - `  PROJECT_ID  ` : Your project ID.
      - `  USER_IDENTIFIER  ` : The identifier for your user account. For example, `myemail@example.com` .
      - `  ROLE  ` : The IAM role that you grant to your user account.

## Create and configure a standalone VPC

1.  Create a VPC network named `securevertex-vpc` :
    
        gcloud compute networks create securevertex-vpc --subnet-mode=custom

2.  Create a subnet named `securevertex-subnet-a` , with a primary IPv4 range of `10.10.10.0/29` :
    
        gcloud compute networks subnets create securevertex-subnet-a --range=10.10.10.0/29 --network=securevertex-vpc --region=us-central1 --enable-private-ip-google-access
    
    You can supply a different value for the `--range` parameter. However, the minimum prefix length for a single notebook is 29. For more information, see [IPv4 subnet ranges](https://docs.cloud.google.com/vpc/docs/subnets#ipv4-ranges) .

3.  Create a regional Cloud Router named `cloud-router-us-central1` :
    
        gcloud compute routers create cloud-router-us-central1 --network securevertex-vpc --region us-central1

4.  Create a regional Cloud NAT gateway named `cloud-nat-us-central1` :
    
        gcloud compute routers nats create cloud-nat-us-central1 --router=cloud-router-us-central1 --auto-allocate-nat-external-ips --nat-all-subnet-ip-ranges --region us-central1

## Create a Cloud Storage bucket

In this section, you create a Cloud Storage bucket to hold a post-startup script that you can run when you create a new Agent Platform Workbench instance.

1.  Create the Cloud Storage bucket:
    
        gcloud storage buckets create --location=us-central1 --uniform-bucket-level-access gs://BUCKET_NAME
    
    Replace BUCKET\_NAME with a unique bucket name.

2.  Set the `BUCKET_NAME` shell variable and verify that it was entered correctly:
    
        BUCKET_NAME=BUCKET_NAME
        echo $BUCKET_NAME

## Create and upload a post-startup script

In this section, you create a post-startup script to clone a GitHub repository into a new Agent Platform Workbench instance.

1.  To create the script, use a text editor such as [`vim`](https://www.cs.cmu.edu/%7E15131/f17/topics/vim/vim-cheatsheet.pdf) or [`nano`](https://www.nano-editor.org/dist/latest/cheatsheet.html) to create a `poststartup.sh` file. You need to prepend `sudo` in order to have permission to write to the file, for example:
    
        sudo vim poststartup.sh

2.  Paste the following shell script into the file:
    
        #! /bin/bash
        echo "Current user: id" >> /tmp/notebook_config.log 2>&1
        echo "Changing dir to /home/jupyter" >> /tmp/notebook_config.log 2>&1
        cd /home/jupyter
        echo "Cloning generative-ai from github" >> /tmp/notebook_config.log 2>&1
        su - jupyter -c "git clone https://github.com/GoogleCloudPlatform/generative-ai.git" >> /tmp/notebook_config.log 2>&1
        echo "Current user: id" >> /tmp/notebook_config.log 2>&1
        echo "Installing python packages" >> /tmp/notebook_config.log 2&1
        su - jupyter -c "pip install --upgrade --no-warn-conflicts --no-warn-script-location --user \
             google-cloud-bigquery \
             google-cloud-pipeline-components \
             google-cloud-aiplatform \
             seaborn \
             kfp" >> /tmp/notebook_config.log 2>&1

3.  Save the file as follows:
    
      - If you're using `vim` , press the `Esc` key, and then type `:wq` to save the file and exit.
      - If you're using `nano` , type `Control+O` and press `Enter` to save the file, and then type `Control+X` to exit.

4.  Upload the file to your Cloud Storage bucket:
    
        gcloud storage cp poststartup.sh gs://BUCKET_NAME

## Create a custom service account

When you create a Agent Platform Workbench instance, we strongly recommend that you clear the **Use Compute Engine default service account** checkbox and specify a custom service account. If your organization doesn't enforce the `iam.automaticIamGrantsForDefaultServiceAccounts` organization policy constraint, the Compute Engine default service account (and thus anyone you specify as an instance user) is granted the Editor role ( `roles/editor` ) on your project. To turn off this behavior, see [Disable automatic role grants to default service accounts](https://docs.cloud.google.com/resource-manager/docs/organization-policy/restricting-service-accounts#disable_service_account_default_grants) .

1.  Create a custom service account named `workbench-sa` :
    
        gcloud iam service-accounts create workbench-sa \
            --display-name="workbench-sa"

2.  Assign the Storage Object Viewer IAM role to the service account:
    
        gcloud projects add-iam-policy-binding $projectid \
            --member="serviceAccount:workbench-sa@$projectid.iam.gserviceaccount.com" \
            --role="roles/storage.objectViewer"

3.  Assign the Monitoring Metric Writer IAM role to the service account:
    
        gcloud projects add-iam-policy-binding $projectid \
            --member="serviceAccount:workbench-sa@$projectid.iam.gserviceaccount.com" \
            --role="roles/monitoring.metricWriter"

4.  Assign the Agent Platform User IAM role to the service account:
    
        gcloud projects add-iam-policy-binding $projectid \
            --member="serviceAccount:workbench-sa@$projectid.iam.gserviceaccount.com" \
            --role="roles/aiplatform.user"

## Create a Agent Platform Workbench instance

In this section, you create the Agent Platform Workbench instance. When the instance is created, the post-startup script you created is run automatically.

1.  In the Google Cloud console, go to the **Instances** tab in the **Agent Platform Workbench** page.

2.  Click add\_box **Create new** , and then click **Advanced options** .
    
    The **New instance** page opens.

3.  On the **New instance** page, in the **Details** section, provide the following information for your new instance and then click **Continue** :
    
      - **Name** : Provide a name for your new instance, or accept the default.
      - **Region** : Select **us-central1** .
      - **Zone** : Select **us-central1-a** .

4.  In the **Environment** section, provide the following and then click **Continue** :
    
      - **Post-startup script** : Click **Browse** , click navigate\_next **View child resources** next to the bucket name, click `poststartup.sh` , and then click **Select** .

5.  In the **Machine type** section, provide the following and then click **Continue** :
    
      - **Shielded VM** : Select the following checkboxes:
        
          - **Secure Boot**
          - **Virtual Trusted Platform Module (vTPM)**
          - **Integrity monitoring**

6.  In the **Disks** section, make sure that **Google-managed encryption key** is selected, and then click **Continue** :

7.  In the **Networking** section, provide the following and then click **Continue** :
    
      - **Networking** : Select **Network in this project** and complete the following steps:
        
        1.  In the **Network** field, select **securevertex-vpc** .
        
        2.  In the **Subnetwork** field, select **securevertex-subnet-a** .
        
        3.  Clear the **Assign external IP address** checkbox. Not assigning an external IP address prevents the instance from receiving unsolicited communication from the internet or other VPC networks.
        
        4.  Select the **Allow proxy access** checkbox.

8.  In the **IAM and security** section, provide the following and then click **Continue** :
    
      - **IAM and security** : To grant a single user access to the instance's JupyterLab interface, complete the following steps:
        
        1.  Select **Single user** .
        
        2.  In the **User email** field, enter the email address for a single user account. If you're creating the instance for someone else, the following conditions apply:
            
              - You (the instance creator) don't have access to the instance's JupyterLab interface. But you still control the instance, and you can start, stop, or delete it.
              - After you create the instance, you need to grant the user the Service Account User role ( `roles/iam.serviceAccountUser` ) on the instance's service account. See [Optional: Grant the Service Account User role to the instance user](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-standalone#grant-sa-user-role) .
        
        3.  Clear the **Use Compute Engine default service account** checkbox. This step is important, because the Compute Engine default service account (and thus the single user you just specified) could have the Editor role ( `roles/editor` ) on your project.
        
        4.  In the **Service account email** field, enter the following, replacing PROJECT\_ID with the project ID:
            
                workbench-sa@PROJECT_ID.iam.gserviceaccount.com
            
            (This is the custom service account email address that you created earlier.) This service account has limited permissions.
            
            To learn more about granting access, see [Manage access to a Agent Platform Workbench instance's JupyterLab interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab) .
    
      - **Security options** : Clear the following checkbox:
        
          - **Root access to the instance**
        
        Select the following checkbox:
        
          - **nbconvert** : [`nbconvert`](https://nbconvert.readthedocs.io/en/latest/) lets users export and download a notebook file as a different file type, such as HTML, PDF, or LaTeX. This setting is required by some of the notebooks in the [Google Cloud Generative AI](https://github.com/GoogleCloudPlatform/generative-ai/) GitHub repository.
        
        Clear the following checkbox:
        
          - **File downloading**
        
        Select the following checkbox, unless you're in a production environment:
        
          - **Terminal access** : This enables terminal access to your instance from within the JupyterLab user interface.

9.  In the **System health** section, select **Environment auto-upgrade** and provide the following:
    
      - In **Reporting** , select the following checkboxes:
        
          - **Report system health**
          - **Report custom metrics to Cloud Monitoring**
          - **Install Cloud Monitoring**
          - **Report DNS status for required Google domains**

10. Click **Create** and wait a few minutes for the Agent Platform Workbench instance to be created.

## Optional: Grant the Service Account User role to the instance user

If you're creating the Agent Platform Workbench instance for another user, you must grant them the [Service Account User role](https://docs.cloud.google.com/iam/docs/service-accounts#user-role) ( `roles/iam.serviceAccountUser` ) on the `workbench-sa` custom service account as follows:

    gcloud iam service-accounts add-iam-policy-binding \
        workbench-sa@PROJECT_ID.iam.gserviceaccount.com \
        --member="user:USER_EMAIL" \
        --role="roles/iam.serviceAccountUser"

Replace the following values:

  - PROJECT\_ID : the project ID
  - USER\_EMAIL : the email address for the user

## Verify that the Agent Platform Workbench instance was created

Agent Platform Workbench creates a Agent Platform Workbench instance based on your specified properties and automatically starts the instance.

When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link. This link is accessible only to the single user that you specified at instance creation time.

Open the instance in JupyterLab and verify that the cloned [Google Cloud Generative AI](https://github.com/GoogleCloudPlatform/generative-ai/) GitHub repository is present.

1.  In the Google Cloud console, go to the **Vertex AI Workbench** page.

2.  In the list of Agent Platform Workbench instances, click the **Open JupyterLab** link for the instance you created.
    
    In the folder list, you'll see a `generative-ai` folder. This folder contains the cloned GitHub repository.

## Monitor health status through Monitoring

You can monitor the system and application metrics for your Agent Platform Workbench instances by using the Google Cloud console. To learn more about instance monitoring and about creating custom metrics, see [Monitor health status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health) .

1.  In the Google Cloud console, go to the **Vertex AI Workbench** page.

2.  Click the name of the Agent Platform Workbench instance that you want to view the metrics for.

3.  On the **Instance details** page, click the **Monitoring** tab. Review the **CPU Utilization** and **Network Bytes** for your notebook instance. To learn how to interpret these metrics, see [Review resource metrics](https://docs.cloud.google.com/compute/docs/instances/observe-monitor-vms#review_resource_metrics) .
    
    If you just created the instance, you won't see any data right away. Wait a few minutes and refresh the console tab.

## Create a VM instance schedule for your Agent Platform Workbench instance

Because a Agent Platform Workbench instance is a Compute Engine VM instance, you can use Compute Engine APIs to create a VM instance schedule for it.

Use a VM instance schedule to start and stop your Agent Platform Workbench instance. During the hours when the instance is stopped, you pay only for Cloud Storage costs.

You can attach an instance schedule to any VM instance that's in the same region, so you can use the same instance schedule to control all your Agent Platform Workbench instances in the region.

To learn more about VM instance schedules, see [Scheduling a VM instance to start and stop](https://docs.cloud.google.com/compute/docs/instances/schedule-instance-start-stop) .

### Create a custom IAM role

As a security best practice, we recommend creating a custom IAM role that has only the following permissions and assigning it to the Compute Engine default service account:

  - `compute.instances.start`
  - `compute.instances.stop`

<!-- end list -->

1.  Inside Cloud Shell, create a custom role named `Vm_Scheduler` and include the necessary permissions:
    
        gcloud iam roles create Vm_Scheduler \
            --project=$projectid \
            --title=vm-scheduler-notebooks \
            --permissions="compute.instances.start,compute.instances.stop" --stage=ga

2.  Describe the custom role:
    
        gcloud iam roles describe Vm_Scheduler \
        --project=$projectid

### Assign the role to the Compute Engine default service account

To give the Compute Engine default service account permission to start and stop your Agent Platform Workbench instances, you need to assign the `Vm_Scheduler` custom role to it.

The Compute Engine default service account for your project has the following email address: `PROJECT_NUMBER-compute@developer.gserviceaccount.com` , where `PROJECT_NUMBER` is your project number.

1.  Identify your project number and store it in the `project_number` shell variable:
    
        project_number=$(gcloud projects describe $projectid --format 'get(projectNumber)')
        echo $project_number

2.  Assign the custom role to the default service account:
    
        gcloud projects add-iam-policy-binding $projectid \
            --member="serviceAccount:service-$project_number@compute-system.iam.gserviceaccount.com" \
            --role="projects/$projectid/roles/Vm_Scheduler"

### Create and attach the schedule

To create an instance schedule that starts your Agent Platform Workbench instance at 7 AM and stops it at 6 PM:

1.  Create a start and stop schedule named `optimize-notebooks` :
    
        gcloud compute resource-policies create instance-schedule optimize-notebooks \
            --region=us-central1 \
            --vm-start-schedule='0 7 * * *' \
            --vm-stop-schedule='0 18 * * *' \
            --timezone=TIME_ZONE
    
    Replace TIME\_ZONE with the location-based IANA time zone for this instance schedule, for example, `America/Chicago` . If omitted, the default value `UTC` is used. For more information, see [time zone](https://docs.cloud.google.com/compute/docs/instances/schedule-instance-start-stop#time_zone) .

2.  Identify the name of your Agent Platform Workbench instance by running the following command and noting the `NAME` value that it returns:
    
        gcloud compute instances list

3.  Store the name in the `notebook_vm` shell variable:
    
        notebook_vm=NOTEBOOK_VM_NAME
        echo $notebook_vm
    
    Replace NOTEBOOK\_VM\_NAME with your Agent Platform Workbench instance name.

4.  Attach the instance schedule to your Agent Platform Workbench instance:
    
        gcloud compute instances add-resource-policies $notebook_vm \
            --resource-policies=optimize-notebooks \
            --zone=us-central1-a

5.  Describe the instance schedule:
    
        gcloud compute resource-policies describe optimize-notebooks \
            --region=us-central1

You can verify if the instance schedule runs successfully by checking the [Compute Engine audit logs](https://docs.cloud.google.com/compute/docs/logging/audit-logging) for the instance schedule resource policy and the attached VM instance. You might need to wait for up to 15 minutes after the scheduled time for each operation.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either [delete the project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects) that contains the resources, or keep the project and delete the individual resources.

You can delete the individual resources in the project as follows by executing the following commands in the Cloud Shell:

1.  Remove the schedule from the instance:
    
        gcloud compute instances remove-resource-policies $notebook_vm \
            --resource-policies=optimize-notebooks \
            --zone=us-central1-a --quiet

2.  Delete the instance schedule:
    
        gcloud compute resource-policies delete optimize-notebooks --region=us-central1 --quiet

3.  Delete the `Vm_Scheduler` role:
    
        gcloud iam roles delete Vm_Scheduler --project=$projectid

4.  Delete the Agent Platform Workbench instance:
    
        gcloud workbench instances delete $notebook_vm \
            --location=us-central1-a \
            --quiet

5.  Delete the service account:
    
        gcloud iam service-accounts delete workbench-sa@$projectid.iam.gserviceaccount.com --quiet

6.  Delete the Cloud Storage bucket:
    
        gcloud storage rm -r gs://BUCKET_NAME

7.  Delete the regional Cloud NAT gateway:
    
        gcloud compute routers nats delete cloud-nat-us-central1 \
            --region=us-central1 \
            --router=cloud-router-us-central1 \
            --quiet

8.  Delete the regional Cloud Router:
    
        gcloud compute routers delete cloud-router-us-central1 \
            --region=us-central1 \
            --quiet

9.  Delete the VPC subnet:
    
        gcloud compute networks subnets delete securevertex-subnet-a \
            --region=us-central1 \
            --quiet

10. Delete the VPC network:
    
        gcloud compute networks delete securevertex-vpc --quiet

## What's next

\- Learn about [Gemini Enterprise Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) . - Learn how to [manage access to an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access) . - Learn how to [use an instance within a service perimeter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter) .
