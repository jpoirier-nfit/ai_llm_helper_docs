---
source_url: https://northflank.com/docs/v1/application/scale/increase-storage
title: Increase storage | Scale | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.218264
watsonmd_version: 0.1.0
---

Scale / 

# Increase storage

Your runtime instances have access to 1GB of ephemeral storage by default to allow your workloads to download and process data.

Ephemeral storage will be erased when the container is restarted or terminated, and the data lost. Ephemeral storage is allocated to each running container, and cannot be shared between multiple containers.

Ephemeral storage is available in combined services, deployment services, and jobs.

Scale ephemeral storage

You can increase the ephemeral storage available to containers by expanding `advanced resource options` in the resources section. Ephemeral storage is available for builds, deployments, and jobs. Any data written to ephemeral storage will be lost when the container is terminated.

If a container attempts to create a file larger than the ephemeral storage assigned to it, it may be evicted. This will trigger a restart for deployments.

The ephemeral storage limits do not apply to paths where a persistent volume is mounted.

Running deployments will be restarted with the new amount of storage.

![Increasing the ephemeral storage available to a deployment service in the Northflank application](https://assets.northflank.com/documentation/v1/application/scale/increase-storage/add-ephemeral.png)

Add persistent storage

You can make persistent storage available to deployments with a wide range of managed [databases](../databases-and-persistence/deploy-a-database), which you can deploy easily and scale horizontally and vertically.

For other use cases you can also attach a [persistent volume](../databases-and-persistence/add-a-volume) to a runtime instance.

Next steps

[Deploy a databaseCreate a database to use with your Northflank deployments.](/docs/v1/application/databases-and-persistence/deploy-a-database)[Add a persistent volumeAdd persistent volumes to your deployments.](/docs/v1/application/databases-and-persistence/add-a-volume)[Scale instancesEasily increase or decrease the amount of instances to run depending on demand for your service.](/docs/v1/application/scale/scale-instances)[Increase CPU and memoryPower-up your services by adding memory and moving from shared to dedicated CPU usage.](/docs/v1/application/scale/scale-cpu-and-memory)