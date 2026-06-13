---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpcsc-public-endpoint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpcsc-public-endpoint
title: Allow public endpoint access to protected resources from outside a VPC Service Controls perimeter
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to allow traffic from internal IP addresses in a VPC network to service perimeters using ingress and egress rules.

## Reference architecture

In the following reference architecture, a Shared VPC is deployed with a Gemini model in the service project, `ph-fm-svc-project` (foundation model service project) with the following service policy attributes allowing known public access to the Gemini Enterprise API for Generative AI on Gemini Enterprise Agent Platform:

  - A single VPC Service Controls perimeter
  - Access level - Known external public endpoint CIDR range
  - Project-defined user identity

![Architectural diagram of using VPC Service Controls to create a service perimeter.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-vpcsc-cuj1.png)

## Create the access level

Access Context Manager allows Google Cloud organization administrators to define fine-grained, attribute-based access control for projects and resources in Google Cloud. Administrators first define an [access policy](https://docs.cloud.google.com/access-context-manager/docs/overview#access-policies) , which is an organization-wide container for [access levels](https://docs.cloud.google.com/access-context-manager/docs/overview#access-levels) and service perimeters.

Access levels describe the requirements for requests to be honored. Examples include:

  - Device type and operating system (requires [Chrome Enterprise Premium](https://docs.cloud.google.com/chrome-enterprise-premium/docs/overview) license)
  - IP address
  - User identity

In this reference architecture, a public IP subnetwork access level is used to build the VPC Service Controls access policy.

1.  In the project selector at the top of the Google Cloud console, click the **All** tab, and then select your organization.

2.  Create a basic access level by following the directions in the [Create a basic access level](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level) page. Specify the following options:
    
    1.  Under **Create conditions in** , choose **Basic mode** .
    2.  In the **Access level title** field, enter `corp-public-block` .
    3.  In the **Conditions** section, for the **When condition is met, return** option, choose **TRUE** .
    4.  Under **IP Subnetworks** , choose **Public IP** .
    5.  For the IP address range, specify your external CIDR range that requires access into the VPC Service Controls perimeter.

## Build the VPC Service Controls service perimeter

When you [create a service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters#external-access) , allow access to protected services from outside the perimeter by specifying access level (IP address) when creating the VPC Service Controls perimeter in addition to the protected projects. When using VPC Service Controls with Shared VPC, best practice dictates creating one large perimeter that includes the host and service projects; solely selecting service projects in a perimeter would mean that network endpoints belonging to service projects appear to be outside the perimeter, because the subnets are associated with the host project.

### Select the configuration type for the new perimeter

In this section, you create a VPC Service Controls service perimeter in [dry run mode](https://docs.cloud.google.com/vpc-service-controls/docs/service-perimeters#dry-run-mode) . In dry run mode, the perimeter logs violations as though the perimeters are enforced but don't prevent access to restricted services. Using dry run mode before [switching to enforced mode](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations#enforce-configuration) is recommended as a best practice.

1.  In the Google Cloud console navigation menu, click **Security** , and then click **VPC Service Controls** .

2.  If you're prompted, select your organization, folder, or project.

3.  On the **VPC Service Controls** page, click **Dry run mode** .

4.  Click **New perimeter** .

5.  On the **New VPC Service Perimeter** tab, in the **Perimeter Name** box, type a name for the perimeter. Otherwise, accept the default values.
    
    A perimeter name can have a maximum length of 50 characters, must start with a letter, and can contain only ASCII Latin letters (a-z, A-Z), numbers (0-9), or underscores (\_). The perimeter name is case-sensitive and must be unique within an access policy.

### Select the resources to protect

1.  Click **Resources to protect** .

2.  To add projects or VPC networks that you want to secure within the perimeter, do the following:
    
    1.  Click **Add Resources** .
    
    2.  To add projects to the perimeter, in the **Add resources** pane, click **Add project** .
        
        1.  To select a project, in the **Add projects** dialog, select that project's checkbox. Select the checkboxes for the following projects:
            
              - `aiml-host-project`
              - `ph-fm-svc-project`
        
        2.  Click **Add selected resources** . The added projects appear in the **Projects** section.

### Select the restricted services

In this reference architecture, the scope of restricted APIs is limited, enabling only the necessary APIs required for Gemini. However, as a best practice, we recommend that you restrict all services when you create a perimeter to mitigate the risk of data exfiltration from Google Cloud services.

> **Note:** This example shows a pattern for a basic Agent Platform implementation. If you're using additional services, add those services to the list of restricted services.

To select the services to secure within the perimeter, do the following:

1.  Click **Restricted Services** .

2.  In the **Restricted Services** pane, click **Add services** .

3.  In the **Specify services to restrict** dialog, select **Agent Platform API** .

4.  Click **Add Agent Platform API** .

### Optional: Select the VPC accessible services

The [VPC accessible services](https://docs.cloud.google.com/vpc-service-controls/docs/vpc-accessible-services) setting limits the set of services that are accessible from network endpoints inside your service perimeter. In this reference architecture, we're keeping the default setting of **All Services** .

1.  Click **VPC accessible services** .

2.  In the **VPC accessible services** pane, select **All services** .

### Select the access level

Allow access to protected resources from outside the perimeter by doing the following:

1.  Click **Access Levels** .

2.  Click the **Choose Access Level** box.
    
    You can also [add access levels](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters#add-access-level) after a perimeter has been created.

3.  Select the checkbox corresponding to the `corp-public-block` access level.

### Ingress and egress policies

In this reference architecture, there's no need to specify any settings in the **Ingress Policy** or **Egress Policy** panes.

### Create the perimeter

Once you have completed the preceding configuration steps, create the perimeter by clicking **Create perimeter** .

## Validate your perimeter in dry run mode

In this reference architecture, the service perimeter is configured in dry run mode, letting you test the effect of access policy without enforcement. This means that you can see how your policies would impact your environment if they were active, but without the risk of disrupting legitimate traffic.

After validating your perimeter in dry run mode, [switch it to enforced mode](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations#enforce-configuration) .

To learn how to validate your perimeter in dry run mode, see [VPC Service Controls dry run logging](https://www.youtube.com/watch?v=_l-ei3ZlgWc) .
