---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/networking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/networking
title: Networking
description: Deploy Gemini Enterprise Agent Platform clusters. Configure IAM, enable APIs, define environment variables, and provision VPC, Filestore, and Lustre storage.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Gemini Enterprise Agent Platform training clusters is a managed Google Cloud service that is provisioned as a [Compute Engine instance](https://docs.cloud.google.com/vertex-ai/docs/glossary#compute_engine_instance) within your VPC. This deployment model allows the service to connect securely to other workloads within your VPC, Google-managed services, or multi-cloud networks.

## Network MTU requirement

To achieve optimal network performance for the training infrastructure, you must configure the Maximum Transmission Unit (MTU) of your VPC network.

### Recommended MTU settings

The recommended MTU value depends on the GPU machine type in your cluster:

  - For A3 Ultra and A4 nodes: Use an MTU of 8896.
  - For A3 Mega nodes: Use an MTU of 8244.

> **Important:** The MTU is a network-wide setting. The value you select applies to all VM instances within that VPC, which can impact existing workloads. For guidance on applying this setting, see [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) .

You may either create a new VPC or use an existing VPC.

## Deploying training clusters in a new VPC (recommended)

The recommended approach is to deploy the training cluster into a new, pre-configured VPC network. This ensures the correct MTU setting is applied automatically and avoids impacting existing workloads.

There are two main steps for deploying training clusters in a new VPC:

1.  Create the VPC network: [Create a new VPC network](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/networking#new-vpc) . To enable jumbo frames, set its MTU to 8896.

2.  Deploy the cluster: Deploy the training cluster into this newly configured network.

Following this order, the cluster's VM instances will automatically inherit the correct MTU setting upon their initial boot.

> **Note:** If you change the VPC's MTU after the cluster is already running, the new setting won't take effect automatically. You must reboot the cluster's VM instances to force them to adopt the new network MTU.

### Create and set up a new VPC

1.  Create the VPC network. To enable jumbo frames, set NETWORK\_MTU to 8896.
    
    ``` 
        # create VPC network
        gcloud compute networks create NETWORK \
          --project=PROJECT_ID \
          --subnet-mode=custom \
          --mtu=NETWORK_MTU
        
    ```

2.  Create the subnet used to deploy the training cluster, and update the range based on your environment's requirements. In this example, the subnet 192.168.0.0/19 is used for the training cluster deployment.
    
    ``` 
        # create VPC subnet
        gcloud compute networks subnets create SUBNETWORK \
          --project=PROJECT_ID \
          --network=NETWORK \
          --region=REGION \
          --enable-private-ip-google-access \
          --range=192.168.0.0/19
        
    ```

3.  Create an IAP firewall rule that allows SSH connectivity to the training cluster.
    
    ``` 
        gcloud compute firewall-rules create allow-ssh-ingress-from-iap \
        --direction=INGRESS   --action=allow   --rules=tcp:22 \
        --source-ranges=35.235.240.0/20 --network NETWORK
        
    ```

4.  Create an ingress firewall rule that allows all ports and protocols to the training cluster subnet.
    
    ``` 
       gcloud compute --project=PROJECT_ID firewall-rules create allow-internal \
       --direction=INGRESS --priority=1000 --network=NETWORK \
       --action=ALLOW --rules=tcp:1-65535,udp:1-65535,icmp \
       --source-ranges=192.168.0.0/19 --enable-logging
       
    ```

## Deploying training clusters in an existing VPC

If you're deploying the training cluster into an existing network with Cloud Storage instances, it's highly recommended that you use jumbo frames (MTU 8896) to ensure optimal performance. Before you begin, verify that the operating systems and applications on [your existing VMs can support this change](https://docs.cloud.google.com/vpc/docs/mtu#vms-and-mtu-settings) .

Implementing jumbo frames requires updating your VPC's MTU, which must be done during a planned maintenance window to prevent network instability.

The only safe procedure is to first stop all running VM instances in that network. Changing the MTU while VMs are active results in mismatched settings and unreliable connectivity.

Once all VMs are stopped, you can proceed with these steps:

1.  Change the network's MTU to your selected setting (for example, 8896).
2.  Restart all the VMs after the network update is complete.
3.  Manually update non-Linux VMs. Be aware that this restart isn't enough for all operating systems. While VMs from public Linux images automatically adopt the new MTU, you must manually update the MTU setting inside the OS for all Windows VMs and any custom-image VMs that don't use DHCP for MTU configuration.

Further requirements:

  - Enable Private Google Access in the subnet used to deploy the cluster.
  - Create an ingress firewall rule to grant IAP access to the cluster.
  - Create an ingress firewall rule to permit all traffic to the cluster.

## What's next

After preparing the VPC network with the correct MTU settings and firewall rules, the next steps are to create and secure the training cluster.

  - Verify your network configuration: Before creating your cluster, run a [Connectivity Test](https://docs.cloud.google.com/network-intelligence-center/docs/connectivity-tests/how-to/running-connectivity-tests) to verify your VPC network and MTU settings, especially if you modified an existing VPC.
  - Secure your cluster with a service perimeter: For enhanced data security, use VPC Service Controls to create a service perimeter around your Vertex AI resources. This helps prevent data exfiltration.
      - [Learn about VPC Service Controls with Vertex AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls)
  - Connect from a hybrid or multi-cloud environment: To access your training cluster from an on-premises data center or a public cloud, use Google Cloud's options for hybrid connectivity.
      - [Learn about Cloud VPN](https://docs.cloud.google.com/network-connectivity/docs/vpn/concepts/overview)
      - [Learn about Cloud Interconnect](https://docs.cloud.google.com/network-connectivity/docs/interconnect/concepts/overview)
