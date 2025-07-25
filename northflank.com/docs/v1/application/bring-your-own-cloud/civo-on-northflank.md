---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/civo-on-northflank
title: Civo on Northflank | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.943285
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Civo on Northflank

To add your Civo account to Northflank, navigate to the clusters page in your account settings and create a new integration.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/civo) to create a new Civo integration.

You must have sufficient resource quotas available in your Civo account to deploy a cluster using Northflank.

Add your Civo account to Northflank

  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/civo) and select Civo as the provider
  3. Open your Civo dashboard and navigate to the [security page ](https://dashboard.civo.com/security) in your profile, under settings
  4. Copy your [Civo API key ](https://www.civo.com/docs/account/api-keys) into the Northflank integration form and `create` the integration



You can now configure and deploy new clusters in your Civo account.

You can edit the integration at any time to update the API key, if required. You should not install any applications from the Civo marketplace to Northflank-managed clusters.

note

  * Disk snapshots for addon backups are not currently available on Civo clusters.
  * Spot instances are not available on Civo clusters.



Check your quotas

To successfully deploy a cluster on Civo using Northflank you must have the required resources available to your account. Civo quotas are account-wide rather than region-specific.

You can view your account quota in your Civo settings on the [quota page ](https://dashboard.civo.com/quota), and request quota increases from this page. Provisioning Northflank clusters will require sufficient quotas for `instances`, `CPUs`, `RAM`, `Disk`, and `Volumes`.

Learn more on the [Civo documentation on quotas ](https://www.civo.com/docs/account/quota).

Create a cluster

To add a new cluster, navigate to the clusters page in your account settings and click `create cluster`.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/new/civo) to create a new Civo cluster.

![Create a new cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/create-a-kubernetes-cluster-with-Northflank/create-cluster.png)

Enter a name for the cluster and select Civo as the cloud provider. Choose your integration credentials and select the region to deploy in.

### Configure node pools

You can now configure the node pools for your cluster. Node pools can also be added, deleted, and updated after creating your cluster. Click `add node pool` to add another pool.

Minimum cluster requirements

Each cluster requires at least one node pool, and a combined minimum of 4 vCPU and 8GB memory across all node pools.

Each node can schedule up to 256 pods (minus system pods). The actual number of pods per node will usually be limited by resource requests and [request modifiers](configure-your-cluster#configure-resources) for smaller nodes.

See [deploy and scale node pools](deploy-and-scale-node-pools) for more information on configuring nodes and node pools.

Spot instances are not available on Civo.

### Configure advanced options

After adding your initial node pools you can configure advanced options for the cluster, such as build infrastructure and resource request modifiers.

When you create the cluster Northflank will begin installing system components in node pools according to their capacity. This may take up to 20 minutes.

Deploy to private nodes

Northflank deploys your Civo cluster using the default network and firewall. All nodes on Civo clusters will have public internet ingress and egress available.

Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)