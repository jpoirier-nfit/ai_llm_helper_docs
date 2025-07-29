---
source_url: https://northflank.com/docs/v1/application/scale/scale-instances
title: Scale instances | Scale | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.207248
watsonmd_version: 0.1.0
---

Scale / 

# Scale instances

You can increase or decrease the number of running instances of your deployed services to meet demand.

The Northflank load-balancer will automatically ensure an even distribution of traffic to each running instance, avoiding containers that are initialising, terminating, or failing.

Each instance created will have the same resources (compute power, memory and storage) as configured in the service.

Scaling a database or addon will create additional replicas of the database or storage to increase availability, however this works differently depending on the type of database/addon.

![Scaling the number of instances for a deployment service in the Northflank application](https://assets.northflank.com/documentation/v1/application/scale/scale-replicas-instances/scale-instances.png)

Scale a service

You can increase or decrease the number of instances from the service overview using the `` scaling button in the header, or from the resources page.

Each instance will have the same resources as is configured for the service and Northflank will begin sending traffic to the new containers when they enter a healthy state.

Scaling a service to 0 instances will make it unavailable. If you leave [CI](../release/manage-ci-cd) enabled the service will still build the latest commit to the linked repository, if you leave [CD](../release/manage-ci-cd) enabled it will also deploy that latest build when scaled up again.

Set the grace period for containers

You can set the grace period (in seconds) allowed for a container to complete its shutdown phase in combined services, deployment services, and jobs. The grace period defines the maximum amount of time between a container receiving a SIGKILL after being sent a SIGTERM. By default, the grace period is 30 seconds.

You may want to increase this if your application includes processes which require being shutdown gracefully, and are terminated prematurely by SIGKILL.

The container may terminate earlier if the workload finishes executing before the grace period expires.

Next steps

[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)[Increase CPU and memoryPower-up your services by adding memory and moving from shared to dedicated CPU usage.](/docs/v1/application/scale/scale-cpu-and-memory)[Increase storageIncrease the persistent storage available for your replicas.](/docs/v1/application/scale/increase-storage)[Enable autoscalingIncrease availability and reduce cost by automatically responding to changes in usage of your deployments.](/docs/v1/application/scale/autoscale-deployments)