---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/manage-your-cluster
title: Manage your cluster | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.005575
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Manage your cluster

You can monitor and manage your cluster from the clusters page in your account settings. The total number of clusters and resources provisioned in your cloud provider accounts is displayed at the top of your clusters page.

[Click here ](https://app.northflank.com/s/account/cloud/clusters) to view your clusters.

![Viewing the details of a cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/manage-and-use-your-kubernetes-cluster-with-Northflank/cluster-details.png)

warning

You should not edit or delete Northflank nodes or clusters via your cloud provider's interface. Doing so may leave orphaned resources which you could still be billed for by your cloud provider.

Deploy on your cluster

To begin using your chosen cloud provider on Northflank [create a new project](../getting-started/create-a-project) and select your cluster as the provider. Learn more in [deploy workloads to your cluster](deploy-workloads-to-your-cluster) and [run GPU workloads in your cluster](../run/run-gpu-workloads).

Monitor your cluster

You can view the status of each cluster in your team on Northflank. Click through to a cluster for the following observability and management tools:

  * `Details`: see details of the cluster such as region, Kubernetes version, and subnets, as well as cluster configuration options including build infrastructure and resource request modifiers
  * `Observe`: contains metrics for the cluster, with breakdowns by node pool and node
  * `Node pools`: view and edit your node pool configurations
  * `Components`: see the status of the Northflank platform components
  * `Cluster history`: review the history of the cluster state, for example to check when an update took place and how long it took
  * `Projects`: a list of projects deployed on the cluster



### Observe cluster usage

The observe page of a cluster shows an overview of all cluster resources with combined usage metrics for vCPU, memory, number of pods, and network usage.

You can see each node pool deployed to the cluster, with the node pool ID and node type. Each node pool also lists the nodes deployed in it, and the used resources (`vCPU`, `Memory`) compared to the requested resources (`rCPU`, `rMem`) for each node.

You can also show deleted node pools, and cordon and drain node pools.

![Viewing the metrics and deployed nodes of a cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/manage-and-use-your-kubernetes-cluster-with-Northflank/cluster-observe.png)

### Configure alerts

You can configure [infrastructure alerts](../observe/set-infrastructure-alerts) to send notifications to your [integrated channels](../observe/configure-notification-integrations). These can alert you to problems with your cluster, node pools, or scheduling pods.

View cluster deployments

You can view workloads deployed on your cluster from the cluster's project page, which will list all projects deployed to your cluster.

You can also open a team's project view and sort by provider.

[Click here ](https://app.northflank.com/s/account/projects) to view your team's projects.

Scale nodes and node pools

You can add, scale, and delete node pools on the `node pools` page in your cluster overview.

See [deploy and scale node pools](deploy-and-scale-node-pools) for more information on configuring nodes and node pools.

Cordon and drain node pools

You can cordon, drain, and uncordon node pools on your cluster's observe page by opening the menu `` on a node pool. You can use these to gracefully migrate workloads to another node pool, for example to upgrade node type or move availability zone, or if you are experiencing issues with a node pool you can prevent workloads from being scheduled to it until the problem is resolved.

### Cordon

Cordoning a node pool will prevent new workloads from being scheduled to the nodes. Existing workloads will continue running until they are terminated, and will then be deployed to another node pool if they are rescheduled.

### Uncordon

Uncordon removes the cordon from the node pool and allows workloads to be scheduled to the nodes.

### Drain

Draining a node pool will send a signal to gracefully terminate all workloads on the node pool. Workloads will respect the [user-configured grace period](../scale/scale-instances#set-the-grace-period-for-containers) if one is set.

Migrating addons and volumes

If you are moving addons from one node pool to another, the new node pool must be in the same availability zone so that the workload can deploy where the disk is located. This also applies to services deployed with a persistent volume.

Upgrade Kubernetes

Kubernetes upgrades are managed by Northflank with no user intervention required, using our advanced upgrade system.

Upgrades to Kubernetes aim to minimise downtime, as workloads are redeployed according to your configuration for services and addons.

A Kubernetes upgrade follows the steps:

  1. The master control plane is upgraded
  2. Existing node pools are duplicated
  3. Workloads are redeployed onto the new node pools in accordance with your configured redeployment strategy
  4. Old node pools are terminated and the upgrade is complete



If you would like to discuss setting maintenance windows for your clusters, contact [[support@northflank.com](mailto:support@northflank.com)](mailto:support@northflank.com).

Delete a cluster

You can delete a cluster from the cluster's overview by using the `` delete button. This will remove the entire cluster and associated resources from your cloud provider account. You must delete all projects hosted on the cluster first.

Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Infrastructure alertsSet infrastructure alerts to let you and your team know when there is an issue with your applications or addons.](/docs/v1/application/observe/set-infrastructure-alerts)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)