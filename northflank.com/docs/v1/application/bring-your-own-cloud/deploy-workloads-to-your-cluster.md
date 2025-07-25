---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster
title: Deploy workloads to your cluster | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.005657
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Deploy workloads to your cluster

You can deploy your workloads to your cluster by [creating a project](../getting-started/create-a-project), selecting `bring your own cloud`, and choosing a cluster from your team.

Any services, jobs, addons, and volumes created in this project will be deployed to the selected cluster. Workloads will be automatically scheduled to nodes based on type, load, and capacity.

[Click here ](https://app.northflank.com/s/account/projects/new) to create a new project.

When you deploy resources to a project on your cluster Northflank will attempt to schedule the workload to a node pool that meets the requirements of the workload. The node pool a workload will be scheduled to can depend on:

  * node capacity
  * spot/on-demand nodes
  * scheduling rules
  * node affinity rules
  * zonal redundancy requirements
  * GPU requirement



If you have configured a workload with conflicting rules, or your cluster lacks capacity in suitable node pools, your workloads will fail to deploy. To fix this you can [scale node pools](deploy-and-scale-node-pools#set-scheduling-rules), change the scheduling rules for a node pool, remove or update tags with conflicting affinity rules, or [change the requested resources](../scale/scale-on-northflank) for your workload.

Deploy workloads to specific node pools

You can use [tags](../release/tag-workloads-and-resources) to manage the deployment of workloads on your own cloud-hosted clusters.

You can mark workloads to prefer to be deployed using spot/preemptible instances, or create your own node pool affinities to deploy workloads on specific node pools.

Node pool labels and node pool affinities allow you to create deployment strategies based on the configured resources and availability zones for your node pools. For example, you may want to ensure that some workloads are deployed with more resources, or you may need to deploy workloads in a specific availability zone.

Use spot instances

You can [tag workloads](../release/tag-workloads-and-resources#provision-by-tag) to deploy them on spot (preemptible) nodes, which means they will first try to deploy on node pools that have [spot instances enabled](deploy-and-scale-node-pools#use-spot-instances).

If there is no capacity on your node pools that use spot instances then these workloads will deploy on on-demand node pools.

Workloads without a tag that enables deployment on spot instances will never be deployed on node pools that use spot instances.

Create node affinity rules

You can add labels to your node pools to [create tags](../release/tag-workloads-and-resources) with node affinity rules. Node affinity rules can be used in addition to spot node rules.

You can create multiple node affinity rules for a tag, each with multiple match expressions. This allows you to configure a combination of mandatory and preferential affinity rules for the same workloads.

If a workload's node affinity rules require it to be deployed on a node pool with no availability, it will not be deployed until there is availability on the required node pool. Availability can be increased by removing other workloads, [scaling up the number of nodes](deploy-and-scale-node-pools#set-node-count-and-autoscaling) in the pool, or adding a new node pool with matching labels.

warning

You can create conflicting rules that prevent the deployment of workloads. If you create mandatory match expression rules that do not correspond to any labels on your node pools, a workload with the tag will never be deployed. If an addon is created with rules that prevent it from being deployed, it must be deleted.

### Label a node pool

You can add labels when you create a node pool, node pool labels cannot be modified after creation.

Navigate to your cluster and add a new node pool with your desired configuration.

Expand the `advanced` section and enter as many labels as required, as name-value pairs. This allows you to create rules across different node pools and clusters by testing against values for a specific label.

You can create labels to make sure your workloads are deployed in specific availability zones, or to node pools with specific resources (for example `resourceType: highCpu` or `availabilityZone: 1a`).

Save your new cluster or click `update node pools` to deploy the new node pool(s) with your labels.

![Creating node pool labels in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/deploy-your-workloads-to-specific-node-pools/node-pool-label.png)

### Deploy workloads according to node affinity rules

To use your node pool labels to manage your deployments you must [tag your workloads](../release/tag-workloads-and-resources#provision-by-tag). You must have created appropriate affinity rules in the tag to match or disallow scheduling to the desired nodes.

Use zonal redundancy for high availability

You can enable zonal redundancy to ensure a resource is scheduled across multiple availability zones. In the event that one availability zone becomes unavailable, your resource will continue to run on node pools in other availability zones. You must have deployed [node pools](deploy-and-scale-node-pools#choose-availability-zone) in multiple availability zones to use zonal redundancy.

### Zonal redundancy for services

Zonal redundancy is configured in the advanced resources section in deployment and combined services. You can configure this during creation, and modify it for existing services.

You can select from the following types of redundancy:

Type| Description  
---|---  
Disabled (default)| The workload will be scheduled based on node pool capacity and any configured affinity rules  
Preferred| The workload will be scheduled in different availability zones if there is capacity. If there is only capacity in one availability zone, all instances for the workload will be scheduled there.  
Required| You can choose the number of zones that must be available for a workload to schedule on. If the specified number of zones is not available in your cluster, the workload will not schedule.  
  
Node pools must also meet the requirements for node type and any affinity rules for a workload to schedule. If a service is scaled to 1 instance, it will not be affected by zonal redundancy rules.

### Zonal redundancy for addons

You can configure [zonal redundancy](../databases-and-persistence/configure-addons-for-high-availability) for an addon during creation. This cannot be changed after creation as the persistent disk is tied to the availability zone, so zonal redundancy can only be disabled or enabled for addons:

Type| Description  
---|---  
Disabled (default)| The addon's replicas will be scheduled based on node pool capacity and any configured affinity rules  
Required| You can choose the number of zones that must be available for an addon to schedule replicas on. If the specified number of zones is not available in your cluster, the addon will not deploy until they become available.  
  
Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Create node pools with spot instancesUse spot instances to reduce costs for non-critical workloads.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools#use-spot-instances)[Tag your workloads and resourcesCreate tags to assign to your Northflank workloads and resources to help keep track of them.](/docs/v1/application/release/tag-workloads-and-resources)[Create a projectCreate a project to contain your services, persistent data, secrets, and more.](/docs/v1/application/getting-started/create-a-project)