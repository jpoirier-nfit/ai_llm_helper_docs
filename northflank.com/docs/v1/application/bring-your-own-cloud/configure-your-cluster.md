---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/configure-your-cluster
title: Configure your cluster | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.979815
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Configure your cluster

You can configure how Northflank will manage volume deletion, builds, and resources requests for your cluster.

[Click here ](https://app.northflank.com/s/account/cloud/clusters) to view your clusters.

Select build infrastructure

You can configure the build infrastructure for the clusters you create, which allows you to define where all builds in projects on that cluster will take place, and what compute resources will be granted to builds (build plans).

This option can be found under `advanced` when creating a cluster, or in `settings` on the details page for existing clusters.

### Select a build cluster

You can select another cluster that you have provisioned specifically for builds, and the cluster you are currently configuring will then deploy all build workloads to the build cluster. All builds will use the build plan configured on the target build cluster.

This gives you the flexibility to:

  * ensure build workloads have capacity to be scheduled and completed by using a pooled build cluster, separate from your deployment clusters
  * ensure your deployments and jobs are not delayed by build workloads
  * select spot instances to reduce costs
  * use another cloud provider and different node types, if required



### Build using the Northflank platform as a service

You can select this option to build using Northflank's platform as a service, [paying only for the usage](../billing/pricing-on-northflank#usage-based-billing-paas) of compute resources. Specific build plans can be selected in each service or job.

### Build on the same cluster

You can choose to build and deploy on the same cluster, and select the specific build plan for all builds to use. The selected build plan will override build plans selected by users in their services and jobs created on that cluster. You should ensure that your node pools have sufficient resources and nodes to provision both deployments and build workloads.

Configure resources

You can configure the minimum resources requested by pods on a cluster by changing the `request modifiers` under `advanced` when creating a cluster, or in `settings` on the details page for existing clusters.

A pod's main runtime container requests resources from a node according to the selected compute or build plan for a service, job, or addon. The request modifiers reduce the resources specified in the plan by a percentage, so a request modifier of `0.7` will request 70% of the resource defined in the plan. This defines the minimum resources that will be requested by a po from a node, but the pod can use the full amount of resources specified in the plan if there is available capacity on a node. The resources available to the pod will be throttled to the minimum request, as calculated by the pod's plan and the request modifiers, if the available resources are reduced by other pods deployed to the node. Sidecar containers will consume resources within the same pod as the main runtime container, and system pods will reduce resources available on the node.

Reducing the request modifiers allows you to over-provision a node with containers, which can optimise your costs if your workload's average requirements are expected to be smaller than the resources of the selected plan. For example, you could provision a node with 10 vCPUs and use compute plans that request 2 vCPUs for deployment services, which would mean that 5 containers could be deployed on a node (ignoring overheads). By setting the service CPU request modifier to `0.5` the same node could now deploy up to 10 containers for the deployment service, with each container throttled to less than 2 vCPU as more workloads are deployed on the node, until they reach a minimum of 1 vCPU for each container.

  * Workloads will be increasingly throttled as the node reaches full CPU utilisation and as additional pods are deployed. Consider how much CPU and memory your workloads will require when configuring request modifiers to avoid situations where nodes become oversaturated.
  * An excessively aggressive memory request modifier can lead to memory usage exceeding the node memory. This will cause the node to experience out of memory (OOM) errors and workloads will become unavailable. This can also potentially cause cascading failures across nodes.



Request modifiers affect all container deployments on the cluster, and will reduce the resources requested by all compute and build plans by the same percentage. Changing the request modifiers for addons on an existing cluster will restart any addons on the cluster.

Custom resource plans

You can create [resource plans](./create-custom-resource-plans) for your team to deploy workloads with custom vCPU and memory requests and limits.

Set volume deletion preferences

By default, Northflank will delete all volumes and volume snapshots (from addon backups) when you delete a cluster.

If you want to retain these volumes you can expand the `advanced` menu and uncheck them, or uncheck them in the settings on an existing cluster, on the cluster details page.

Please note that you will still be billed by your cloud provider for any volumes left after cluster deletion. You should always delete your Northflank-created clusters through the Northflank interface to avoid orphaned resources.

Next steps

[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Manage your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/manage-your-cluster)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Create custom resource plansCreate custom plans for your team to deploy workloads and build code on your own clusters.](/docs/v1/application/bring-your-own-cloud/create-custom-resource-plans)