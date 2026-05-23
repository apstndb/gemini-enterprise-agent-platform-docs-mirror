---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter
title: Use a Agent Platform Workbench instance within a service perimeter
description: Learn how to make a Agent Platform Workbench instance more secure by using a service perimeter
data_source: docs.cloud.google.com
---

# Use an instance within a service perimeter

This page describes how to use VPC Service Controls to set up a Gemini Enterprise Agent Platform Workbench instance within a service perimeter.

## Before you begin

1.  Read the [Overview of VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) .

2.  [Create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) . This instance is not within a service perimeter yet.

3.  [Create a service perimeter using VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters) . This service perimeter protects the Google-managed resources of services that you specify. While creating your service perimeter, do the following:
    
    1.  When it's time to add projects to your service perimeter, add the project that contains your Agent Platform Workbench instance.
    
    2.  When it's time to add services to your service perimeter, add the **Notebooks API** .
    
    If you have created your service perimeter without adding the projects and services you need, see [Managing service perimeters](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters) to learn how to update your service perimeter.

## Configure your DNS entries using Cloud DNS

Agent Platform Workbench instances use several domains that a Virtual Private Cloud network doesn't handle by default. To ensure that your VPC network correctly handles requests sent to those domains, use Cloud DNS to add DNS records. For more information about VPC routes, see [Routes](https://docs.cloud.google.com/vpc/docs/routes) .

To create a [managed zone](https://docs.cloud.google.com/dns/docs/zones#create_managed_zones) for a domain, add a DNS entry that will route the request, and execute the transaction, complete the following steps. Repeat these steps for each of [several domains](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter#domains) that you need to handle requests for, starting with `*.notebooks.googleapis.com` .

In [Cloud Shell](https://console.cloud.google.com/?cloudshell=true) or any environment where the [Google Cloud CLI](https://docs.cloud.google.com/sdk/docs) is installed, enter the following [Google Cloud CLI](https://docs.cloud.google.com/sdk/gcloud) commands.

1.  To create a private managed zone for one of the domains that your VPC network needs to handle:
    
    ``` 
        gcloud dns managed-zones create ZONE_NAME \
            --visibility=private \
            --networks=https://www.googleapis.com/compute/v1/projects/PROJECT_ID/global/networks/NETWORK_NAME \
            --dns-name=DNS_NAME \
            --description="Description of your managed zone"
        
    ```
    
    Replace the following:
    
      - `  ZONE_NAME  ` : a name for the zone to create. You must use a separate zone for each domain. This zone name is used in each of the following steps.
      - `  PROJECT_ID  ` : the ID of the project that hosts your VPC network
      - `  NETWORK_NAME  ` : the name of the VPC network that you created earlier
      - `  DNS_NAME  ` : the part of the domain name that comes after the `*.` , with a period on the end. For example, `*.notebooks.googleapis.com` has a `  DNS_NAME  ` of `notebooks.googleapis.com.`

2.  Start a transaction.
    
    ``` 
        gcloud dns record-sets transaction start --zone=ZONE_NAME
        
    ```

3.  Add the following DNS A record. This reroutes traffic to Google's restricted IP addresses.
    
    ``` 
        gcloud dns record-sets transaction add \
            --name=DNS_NAME. \
            --type=A 199.36.153.4 199.36.153.5 199.36.153.6 199.36.153.7 \
            --zone=ZONE_NAME \
            --ttl=300
        
    ```

4.  Add the following DNS CNAME record to point to the A record that you just added. This redirects all traffic matching the domain to the IP addresses listed in the previous step.
    
    ``` 
        gcloud dns record-sets transaction add \
            --name=\*.DNS_NAME. \
            --type=CNAME DNS_NAME. \
            --zone=ZONE_NAME \
            --ttl=300
        
    ```

5.  Execute the transaction.
    
    ``` 
        gcloud dns record-sets transaction execute --zone=ZONE_NAME
        
    ```

6.  Repeat these steps for each of the following domains. For each repetition, change ZONE\_NAME and DNS\_NAME to the appropriate values for that domain. Keep PROJECT\_ID and NETWORK\_NAME the same each time. You already completed these steps for `*.notebooks.googleapis.com` .
    
      - `*.notebooks.googleapis.com`
      - `*.notebooks.cloud.google.com`
      - `*.notebooks.googleusercontent.com`
      - `*.googleapis.com` to run code that interacts with other Google APIs and services

## Configure the service perimeter

After [configuring the DNS records](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter#configure-dns) , either [create a service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters) or [update an existing perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters#update) to add your project to the service perimeter.

In the VPC network, add a route for the `199.36.153.4/30` range with a next hop of `Default internet gateway` .

> **Note:** The `199.36.153.4/30` range is for `restricted.googleapis.com` to access APIs that are only VPC Service Controls compatible. If you aren't using VPC Service Controls, you can use the `199.36.153.8/30` range for `private.googleapis.com` . For more information about Private Google Access, see [Configure Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) .

## Use Artifact Registry within your service perimeter

If you want to use Artifact Registry in your service perimeter, see [Configure restricted access for GKE private clusters](https://docs.cloud.google.com/artifact-registry/docs/gke-private-clusters) .

## Use Shared VPC

If you are using [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) , you must add the host and the service projects to the service perimeter. In the host project, you must also grant the [Compute Network User ( `roles/compute.networkUser` )](https://docs.cloud.google.com/iam/docs/roles-permissions/compute#compute.networkUser) role to the [Notebooks Service Agent](https://docs.cloud.google.com/iam/docs/service-agents#cloud-ai-platform-notebooks-service-account) from the service project. For more information, see [Manage service perimeters](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters) .

## Access your Agent Platform Workbench instance

To open a Jupyter notebook on your new instance:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your instance's name, click **Open JupyterLab** .

3.  In JupyterLab, select **File \> New \> Notebook** .

4.  In the **Select kernel** dialog, choose a kernel, and then click **Select** .
    
    Your new notebook file opens.

## Limitations

The following limitations apply when using VPC Service Controls with Agent Platform Workbench:

### Identity type for ingress and egress policies

When you specify an ingress or egress policy for a service perimeter, you can't use `ANY_SERVICE_ACCOUNT` or `ANY_USER_ACCOUNT` as an identity type for all Agent Platform Workbench operations.

Instead, use `ANY_IDENTITY` as the identity type.

### Accessing the Agent Platform Workbench proxy from a workstation without internet

To access Agent Platform Workbench instances from a workstation with limited internet access, verify with your IT administrator that you can access the following domains:

  - `*.accounts.google.com`
  - `*.accounts.youtube.com`
  - `*.googleusercontent.com`
  - `*.kernels.googleusercontent.com`
  - `*.gstatic.com`
  - `*.notebooks.cloud.google.com`
  - `*.notebooks.googleapis.com`

You must have access to these domains for authentication to Google Cloud. See the previous section, [Configure your DNS entries using Cloud DNS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter#configure-dns) , for further configuration information.

### Public IP addresses

If you're using a Agent Platform Workbench instance within a service perimeter, ensure that your instance doesn't have a public IP address. Public IP addresses allow egress to the internet, which bypasses the service perimeter.

When you create a Agent Platform Workbench instance for use within a service perimeter, turn off the **Assign external IP address** option and use [Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) for the instance's subnet.
