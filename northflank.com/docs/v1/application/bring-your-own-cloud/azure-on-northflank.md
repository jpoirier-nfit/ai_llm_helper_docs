---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/azure-on-northflank
title: Microsoft Azure on Northflank | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.931898
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Microsoft Azure on Northflank

You can integrate your Microsoft Azure account to create and manage clusters using Northflank.

To add your Azure account navigate to the clusters page in your account settings and create a new integration.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/azure) to create a new Azure integration.

After integrating your account, you can create a new cluster.

Add your Azure account

It is recommended that you create a new Azure Active Directory application to integrate with Northflank:

  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/azure) and select Azure as the provider
  3. Open [Azure Portal ](https://portal.azure.com/) and navigate to [Azure Entra ID ](https://portal.azure.com/#view/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/~/Overview)
  4. [Register a new application ](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) with Azure AD from the `add` menu, or from the `app registrations` page. Copy the directory (tenant) ID and the application (client) ID to the Northflank form.
  5. In your new application click the link for `managed application in local directory` (your application's name) and copy the application's object ID from properties to Northflank.
  6. Go back to your application overview and open the `certificates and secrets` page. Create a new client secret, and copy the secret value (not the secret ID) to Northflank.
  7. Navigate to [subscriptions ](https://portal.azure.com/#view/Microsoft_Azure_Billing/SubscriptionsBlade) and select an existing subscription, or create a new one. For security, the subscription you use with Northflank should have only the necessary permissions allocated to it.
  8. Open `access control (IAM)` and add a new role assignment to the subscription. Select the [contributor role ](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#contributor) from `privileged administrator roles`.
  9. Open the members page in the new role and assign access to `user, group, or service principle`. `Select members` and add your Active Directory application. You may need to start typing the name of your application for it to appear in the member selection menu.
  10. Open `resource providers` in your subscription, search for and select the provider `Microsoft.ContainerService`. Click `register` to add the provider to the subscription.
  11. Copy the subscription ID to Northflank and `create` the integration



You can now configure and deploy new clusters in your Azure account.

You can edit the integration at any time to update the secrets, if required. If the new secrets do not have permission to manage existing clusters, you will be unable to edit those clusters and deleting them via Azure Active Directory may leave orphaned resources.

Check your quotas

To successfully deploy a cluster on Azure using Northflank you must have the required resources available to your account for your desired region.

[Check the node types](deploy-and-scale-node-pools#select-node-type) you wish to deploy and ensure your cluster has access to the relevant resources. The specific quotas for each provider may differ, you will need to ensure you have sufficient quotas for your required node type, vCPU, and disk type for your desired regions.

Check and edit your [Azure subscription quotas ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits) from the `usage + quotas` page of the relevant subscription. You can filter the quotas by provider as well as region.

For example, to increase the number of node pools you can deploy on Azure using the `Standard_D2ds_v5` node type you should select the resource provider `compute`, filter quotas by your cluster's region, select `Standard DDSv5 Family vCPUs` from the list, and request a quota increase. This will also automatically increase your `Total Regional vCPUs` quota, if the request is successful.

Create a cluster

To add a new cluster, navigate to the clusters page in your account settings and click `create cluster`.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/new/azure) to create a new Azure cluster.

![Create a new cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/create-a-kubernetes-cluster-with-Northflank/create-cluster.png)

Enter a name for the cluster and select Azure as the cloud provider. Choose your integration credentials and select the region to deploy in.

### Configure node pools

You can now configure the node pools for your cluster. Node pools can also be added, deleted, and updated after creating your cluster. Click `add node pool` to add another pool.

Azure system node pool

Each cluster requires at least one node pool, and a combined minimum of 4 vCPU and 8GB memory across all node pools.  
One node pool must be assigned as the system node pool to schedule non-user workloads. For best performance you should assign it more than one node and disable autoscaling.

Each node can schedule up to 250 pods (minus system pods). The actual number of pods per node will usually be limited by resource requests and [request modifiers](configure-your-cluster#configure-resources) for smaller nodes.

#### Cluster networking limits

The number of workloads that can be deployed to an AKS cluster is limited by the available number of pod and service IP addresses, allocated by CIDR block.

AKS clusters allocate a CIDR block of `/16` for pods and services, which means you can deploy thousands of services and pods to your cluster without facing networking constraints.

See [deploy and scale node pools](deploy-and-scale-node-pools) for more information on configuring nodes and node pools.

### Configure advanced options

After adding your initial node pools you can configure advanced options for the cluster, such as build infrastructure and resource request modifiers.

When you create the cluster Northflank will begin installing system components in node pools according to their capacity. This may take up to 20 minutes.

Deploy to private nodes

On Azure AKS nodes are private by default, and will not allow public ingress requests.

Northflank installs a load balancer to provide public ingress only via the ports you configure on the Northflank platform.

Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)