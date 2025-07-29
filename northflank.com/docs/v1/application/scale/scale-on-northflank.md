---
source_url: https://northflank.com/docs/v1/application/scale/scale-on-northflank
title: Scale on Northflank | Scale | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.200644
watsonmd_version: 0.1.0
---

Scale / 

# Scale on Northflank

You can scale your resources on Northflank horizontally and vertically. Increase the resources available to individual instances, or increase the amount of instances for your deployments.

Check the [metrics](../observe/view-metrics) for your addon replicas, builds, and deployments in order to identify bottlenecks which may be impacting your resources.

See [Northflank pricing plans ](https://northflank.com/pricing) for compute plans available on Northflank's managed cloud, as well as storage and network egress costs.

Scale instances

You can increase the available vCPU and memory allocated to each instance of a service.

[Scale instancesEasily increase or decrease the amount of instances to run depending on demand for your service.](/docs/v1/application/scale/scale-instances)

Scale compute

You can scale vertically by increasing the available vCPU and memory allocated to each instance of a deployment.

You can select a compute plan for Northflank services, builds, jobs, databases, and other addons.

[Increase CPU and memoryPower-up your services by adding memory and moving from shared to dedicated CPU usage.](/docs/v1/application/scale/scale-cpu-and-memory)

Scale storage

You can scale horizontally and vertically on Northflank with no unexpected spend.

You can increase the number of instances running each deployment, or replicas of your databases, and increase the available computing power, memory, and storage space allocated to each instance.

You can also configure autoscaling to handle spikes in activity - never suffer from a loss of service from high traffic or intense workloads, while avoiding the cost of permanently running the number of instances required at your peak usage.

You can check the [metrics](../observe/view-metrics) for your builds or running instances in order to identify bottlenecks which may be impacting your service.

[Increase storageIncrease the persistent storage available for your replicas.](/docs/v1/application/scale/increase-storage)

Use autoscaling

You can configure autoscaling to handle spikes in activity for your continuous deployments.

This can help you avoid a loss of service from high traffic or unexpected spikes in usage, without the cost of permanently running the number of instances required at peak usage.

[Enable autoscalingIncrease availability and reduce cost by automatically responding to changes in usage of your deployments.](/docs/v1/application/scale/autoscale-deployments)

Scale using infrastructure as code

You can configure service and addon resources within a template, and update your infrastructure by running a template or pushing to git.

[Infrastructure as codeAutomate workflows, share deployments, and automate complex tasks using Northflank templates.](/docs/v1/application/infrastructure-as-code/infrastructure-as-code)

Scale your own cloud

You can add and scale node pools of different node types, and enable autoscaling for clusters deployed in your own cloud account. You can also create custom plans for your team to deploy workloads with vCPU and memory resources that you specify.

[Bring your own cloud to NorthflankUse all the features of the Northflank platform on other cloud hosting providers, with control over your own infrastructure.](/docs/v1/application/bring-your-own-cloud/use-other-cloud-providers-with-northflank)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Create custom resource plansCreate custom plans for your team to deploy workloads and build code on your own clusters.](/docs/v1/application/bring-your-own-cloud/create-custom-resource-plans)