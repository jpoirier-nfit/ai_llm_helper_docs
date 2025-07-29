---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/gcp-on-northflank
title: Google Cloud Platform on Northflank | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.903669
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Google Cloud Platform on Northflank

You can integrate your Google Cloud Platform account to create and manage clusters using Northflank.

To add your GCP account navigate to the clusters page in your account settings and create a new integration.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/gcp) to create a new GCP integration.

You can create an integration using a cross-project service account (recommended), or using a service key (legacy method).

After integrating your account, you can create a new cluster.

Select or create your GCP project

You can use Northflank with an existing Google Cloud Platform project, or create a new one.

### New GCP project setup

  1. Open your [GCP console ](https://console.cloud.google.com/) and create a new project, or select an existing one.
  2. Ensure [billing is enabled ](https://cloud.google.com/billing/docs/how-to/modify-project)
  3. Enable the [Kubernetes Engine API ](https://console.cloud.google.com/marketplace/product/google/container.googleapis.com) and [Cloud Resource Manager API ](https://console.cloud.google.com/marketplace/product/google/cloudresourcemanager.googleapis.com)



Required permissions

The standard Google roles [`roles/iam.serviceAccountUser` (Service Account User) ](https://cloud.google.com/iam/docs/understanding-roles#service-accounts-roles) and [`roles/container.admin` (Kubernetes Engine Admin) ](https://cloud.google.com/iam/docs/understanding-roles#kubernetes-engine-roles) contain all the required permissions to integrate your GCP account.

Required GCP permissions

  * `iam.serviceAccounts.actAs`
  * `iam.serviceAccounts.get`
  * `container.clusterRoleBindings.create`
  * `container.clusterRoleBindings.delete`
  * `container.clusterRoleBindings.get`
  * `container.clusterRoleBindings.list`
  * `container.clusterRoleBindings.update`
  * `container.clusterRoles.bind`
  * `container.clusterRoles.create`
  * `container.clusterRoles.escalate`
  * `container.clusterRoles.get`
  * `container.clusterRoles.list`
  * `container.clusterRoles.update`
  * `container.clusters.create`
  * `container.clusters.delete`
  * `container.clusters.get`
  * `container.clusters.getCredentials`
  * `container.clusters.list`
  * `container.clusters.update`
  * `container.configMaps.create`
  * `container.configMaps.get`
  * `container.configMaps.list`
  * `container.configMaps.update`
  * `container.customResourceDefinitions.create`
  * `container.customResourceDefinitions.get`
  * `container.customResourceDefinitions.update`
  * `container.daemonSets.create`
  * `container.daemonSets.delete`
  * `container.daemonSets.get`
  * `container.daemonSets.list`
  * `container.daemonSets.update`
  * `container.deployments.create`
  * `container.deployments.get`
  * `container.deployments.list`
  * `container.deployments.update`
  * `container.horizontalPodAutoscalers.create`
  * `container.horizontalPodAutoscalers.list`
  * `container.horizontalPodAutoscalers.update`
  * `container.mutatingWebhookConfigurations.create`
  * `container.mutatingWebhookConfigurations.list`
  * `container.mutatingWebhookConfigurations.update`
  * `container.namespaces.create`
  * `container.namespaces.get`
  * `container.namespaces.update`
  * `container.networkPolicies.create`
  * `container.networkPolicies.get`
  * `container.networkPolicies.update`
  * `container.nodes.list`
  * `container.operations.list`
  * `container.persistentVolumeClaims.list`
  * `container.podDisruptionBudgets.create`
  * `container.podDisruptionBudgets.list`
  * `container.podDisruptionBudgets.update`
  * `container.pods.list`
  * `container.pods.proxy`
  * `container.podSecurityPolicies.create`
  * `container.podSecurityPolicies.get`
  * `container.podSecurityPolicies.update`
  * `container.replicaSets.list`
  * `container.resourceQuotas.create`
  * `container.resourceQuotas.get`
  * `container.resourceQuotas.update`
  * `container.roleBindings.create`
  * `container.roleBindings.get`
  * `container.roleBindings.list`
  * `container.roleBindings.update`
  * `container.roles.bind`
  * `container.roles.create`
  * `container.roles.escalate`
  * `container.roles.get`
  * `container.roles.list`
  * `container.roles.update`
  * `container.runtimeClasses.list`
  * `container.secrets.create`
  * `container.secrets.get`
  * `container.secrets.list`
  * `container.secrets.update`
  * `container.serviceAccounts.create`
  * `container.serviceAccounts.delete`
  * `container.serviceAccounts.get`
  * `container.serviceAccounts.list`
  * `container.serviceAccounts.update`
  * `container.services.create`
  * `container.services.get`
  * `container.services.list`
  * `container.services.update`
  * `container.statefulSets.create`
  * `container.statefulSets.get`
  * `container.storageClasses.create`
  * `container.storageClasses.get`
  * `container.storageClasses.update`
  * `container.thirdPartyObjects.create`
  * `container.thirdPartyObjects.get`
  * `container.thirdPartyObjects.list`
  * `container.thirdPartyObjects.update`
  * `container.validatingWebhookConfigurations.create`
  * `container.validatingWebhookConfigurations.get`
  * `container.validatingWebhookConfigurations.list`
  * `container.validatingWebhookConfigurations.update`
  * `container.volumeSnapshotClasses.create`
  * `container.volumeSnapshotClasses.get`
  * `container.volumeSnapshotClasses.update`



Add your account with a cross-project service account

You can integrate your Google Cloud Platform account using a cross-project service account. Northflank will create a new service account in Google Cloud Platform which you can then grant access to your GCP project.

Requirements

You will need the following to get started:

  * a GCP project
  * access to roles with the necessary permissions for your account
  * sufficient quotas to deploy your cluster



  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/gcp) and select Google Cloud Platform as the provider
  3. Name the integration, enter your [Google Project ID ](https://cloud.google.com/resource-manager/docs/creating-managing-projects), and click `create`
  4. Copy the Northflank service account email from the credentials section
  5. Go to the [IAM page ](https://console.cloud.google.com/iam-admin/iam) in your GCP console
  6. Click `Grant Access` and add the Northflank service account email as a principal
  7. Select `Service Account User` and `Kubernetes Engine Admin` as roles, or add roles with the equivalent permissions
  8. Save and return to Northflank to verify the permissions



Add your account with a service key

You can add your account to Northflank by providing the service key for an IAM user. This is a legacy method, it is recommended that you instead integrate using a cross-project service account.

Requirements

You will need the following to get started:

  * a GCP project
  * access to roles with the necessary permissions for your account
  * sufficient quotas to deploy your cluster



You should create a new service account to integrate with Northflank using a service key.

  1. Navigate to the service accounts page in `IAM and admin` in your Google Cloud Platform project
  2. Create a new service account:
     1. Add a name and description, click `create and continue`
     2. Add roles with the required permissions
     3. Select the new service account and go to the keys page. Create a new key and download the key file with the type `JSON`
  3. Navigate to your Northflank account settings and open the clusters page
  4. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/gcp) and select Google Cloud Platform as the provider
  5. Copy and paste the contents of your `keyfile.json` and `create` the integration



You can now configure and deploy new clusters in your GCP account.

You can edit the integration at any time to update the `keyfile.json` and Google project ID, if required. If you change the Google project while there are still Northflank clusters on it, you will be unable to manage those clusters and deleting them via Google may leave orphaned resources.

note

If you have recently added or changed permissions for your service user account they may take some time to propagate throughout Google.

Check your quotas

To successfully deploy a cluster on GCP using Northflank you must have the required resources available to your account for your desired region.

[Check the node types](deploy-and-scale-node-pools#select-node-type) you wish to deploy and ensure your account has sufficient quotas for your required node type, vCPU, and disk type for your desired regions.

You can manage your [Google quota settings ](https://cloud.google.com/docs/quota_detail/view_manage) from your [quotas page ](https://console.cloud.google.com/iam-admin/quotas) on the `IAM and admin` page of your Google Cloud project. You can filter the list by resource and region.

For example, to increase the number of node pools you can deploy on Google Cloud using the `n2-standard-4` node type in the region `europe-west2`, filter the quota list with `region:europe-west2` and `n2_cpus`, select the quota from the list, and click `edit quotas`.

Create a cluster

To add a new cluster, navigate to the clusters page in your account settings and click `create cluster`.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/new/gcp) to create a new GCP cluster.

![Create a new cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/create-a-kubernetes-cluster-with-Northflank/create-cluster.png)

Enter a name for the cluster and select GCP as the cloud provider. Choose your integration credentials and select the region to deploy in.

The Google project ID field will be automatically filled based on the provided credentials.

### Configure node pools

You can now configure the node pools for your cluster. Node pools can also be added, deleted, and updated after creating your cluster. Click `add node pool` to add another pool.

Minimum cluster requirements

Each cluster requires at least one node pool, and a combined minimum of 4 vCPU and 8GB memory across all node pools.

Each node can schedule up to 256 pods (minus system pods). The actual number of pods per node will usually be limited by resource requests and [request modifiers](configure-your-cluster#configure-resources) for smaller nodes.

#### Cluster networking limits

The number of workloads that can be deployed to a GCP cluster is limited by the available number of pod and service IP addresses, allocated by CIDR block.

Northflank configures GCP clusters with a CIDR block of `/14` for pods and a CIDR block of `/20` for services, which means you will be able to deploy up to 4000 services, jobs, and addons to your cluster before facing networking constraints.

See [deploy and scale node pools](deploy-and-scale-node-pools) for more information on configuring nodes and node pools.

### Configure advanced options

After adding your initial node pools you can configure advanced options for the cluster, such as build infrastructure and resource request modifiers.

When you create the cluster Northflank will begin installing system components in node pools according to their capacity. This may take up to 20 minutes.

Deploy to private nodes

GCP currently provides no way to provision private nodes. All nodes on GCP clusters will have public internet ingress and egress available.

Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)