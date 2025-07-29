---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/oci-on-northflank
title: Oracle Cloud Infrastructure on Northflank | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.970791
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Oracle Cloud Infrastructure on Northflank

To add your Oracle Cloud Infrastructure account to Northflank, navigate to the clusters page in your account settings and create a new integration. OCI integrations are on a regional basis, you will have to create a separate integration for each OCI region you want to deploy clusters in.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/oci) to create a new OCI integration.

Add your account to Northflank

Oracle Cloud Infrastructure resources

You may find it useful to refer to the following OCI documentation while following this guide:

  * [Set up a tenancy and compartment ](https://docs.oracle.com/en-us/iaas/Content/GSG/Concepts/settinguptenancy.htm)
  * [Add a user ](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/addingusers.htm)
  * [Find tenancy and user OCID, add a key pair ](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm)



To add your OCI account to Northflank:

  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/oci) and select Oracle as the provider
  3. Choose the region that the integration should provide access to
  4. Open your [OCI Console ](https://cloud.oracle.com), open your `profile` menu and click `tenancy`. Copy the OCID for your tenancy to Northflank.
  5. Create a new user or select an existing user. They must be in an IAM group that grants them the necessary permissions to create and manage OCI resources, and have access to the compartment that you will use with the integration.
  6. If you're using your own user, open your `profile` menu and click `my profile`. If you're using another (system) user open the `navigation menu`, select `identity & security` and click `users`, under identity. Select the user from the list.
  7. Copy the user's OCID into the Northflank form for the user ID
  8. You will need to generate an API signing key pair to use with your OCI user account and Northflank
     1. Generate a key pair in your OCI Console and download your private key, store this somewhere secure. Alternatively you can upload a key you have generated yourself.
     2. Copy the fingerprint of the key, displayed in the OCI Console, to Northflank
     3. Copy your private key to Northflank, or upload the `.pem` file containing your key
     4. Enter your passphrase (optional), if you generated the key with one (recommended)
  9. Enter the ID of the compartment that new clusters using this integration will be created in
  10. Click `create integration`



You can now configure and deploy new clusters in your OCI account, in the region specified in the integration.

You can edit the integration at any time to update the secrets, if required. If the new secrets do not have permission to manage existing clusters, you will be unable to edit those clusters and deleting them via OCI may leave orphaned resources.

Check your quotas

To successfully deploy a cluster on OCI using Northflank you must have the required resources available to your account.

Your OCI integration will have [Service Limits ](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/servicelimits.htm) set by Oracle and [Compartment Quotas ](https://docs.oracle.com/en-us/iaas/Content/Quotas/Concepts/resourcequotas.htm) set by account administrators. OCI Service Limits are regional.

You will only be able to see the [Compute Shapes ](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm) available to your account in the selected region for your cluster.

[Check the node types](deploy-and-scale-node-pools#select-node-type) you wish to deploy and ensure your account has the sufficient quotas.

Create a cluster

To add a new cluster, navigate to the clusters page in your account settings and click `create cluster`.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/new/oci) to create a new OCI cluster.

![Create a new cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/create-a-kubernetes-cluster-with-Northflank/create-cluster.png)

Enter a name for the cluster and select OCI as the cloud provider. Choose your integration credentials and select the region to deploy in.

### Select a VCN

You must select the [Virtual Cloud Network ](https://docs.oracle.com/en-us/iaas/Content/Network/Tasks/managingVCNs.htm) that your cluster will use. You can create a VCN with OCI's automatic configuration, or specify your own networking resources.

Select the subnets for the load balancer and the Kubernetes API you want to use for the cluster. These subnets will host the control plane components for your cluster and have no impact on the subnets that you can select for node pools.

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAEZSURBVHgB7ZXBDYIwFIbfa030YuIIuoEj6Ml4dALZQDdwBEdwCoPhghs4giuQSMCDoRYEUkqBB8GTfklDaN57//+nDQD8FOEFXbnubXoYtdC3wZKPhVzT4AJ7ah9SC1Pn06QJwRsGYoYb8Jr6SAmeDttlw2OEgEkwoqVoTBDacjCiqwokjcQUjQkYY1t9eAw1RW2C1H3lraGkqE+A7KC+jlZRsjIoKSoFEvcgLGiAM9x9alsK6O6riFPU1RoFqO4VGcs/w5wsQHWvwjkejaP0Dd+BOY/wBh14CbEcr+Gq7pUSyOFH6MgAsZS8IKB80Izo19TA4mEX+wsC3OCgLXqK/Axi91LgBD2gnkWeoA/3GQPFKPmH8+drvAGciFlVpRD4HQAAAABJRU5ErkJggg==)

important

You must select public subnets for the load balancer and Kubernetes API for Northflank to be able to manage your cluster.

### Configure node pools

You can now configure the node pools for your cluster. Node pools can also be added, deleted, and updated after creating your cluster. Click `add node pool` to add another pool.

Minimum cluster requirements

Each cluster requires at least one node pool, and a combined minimum of 4 vCPU and 8GB memory across all node pools.

Each node can schedule up to 256 pods (minus system pods). The actual number of pods per node will usually be limited by resource requests and [request modifiers](configure-your-cluster#configure-resources) for smaller nodes.

See [deploy and scale node pools](deploy-and-scale-node-pools) for more information on configuring nodes and node pools.

### Configure advanced options

After adding your initial node pools you can configure advanced options for the cluster, such as build infrastructure and resource request modifiers.

When you create the cluster Northflank will begin installing system components in node pools according to their capacity. This may take up to 20 minutes.

Deploy to private nodes

You can [create a Virtual Cloud Network ](https://docs.oracle.com/en-us/iaas/Content/Network/Tasks/create_vcn.htm) with [subnets ](https://docs.oracle.com/en-us/iaas/Content/Network/Tasks/create_subnet.htm) that have no public internet access. You must still create and use public subnets for your load balancer and Kubernetes API subnets.

You will need to create a cluster with a custom VCN that has private subnets configured on it, then select a private subnet when you create a new node pool.

You can then [create a project on your cluster](deploy-workloads-to-your-cluster), and use [node pool labels and Northflank tags](deploy-workloads-to-your-cluster#deploy-workloads-to-specific-node-pools) to schedule workloads to your private nodes.

Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)