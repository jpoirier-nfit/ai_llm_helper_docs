---
source_url: https://northflank.com/docs/v1/application/run/change-deployment-source
title: Change deployment source | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.363280
watsonmd_version: 0.1.0
---

Run / 

# Change deployment source

You can switch a deployment service from using an image built from your linked Git provider to an image hosted on a container registry at any time, and vice versa. You cannot change the image source for jobs.

## Change source via the deployment overview

You can open the edit deployment dialog from the service overview.

![Changing the deployment source in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/change-deployment-source/deployment-service-edit-deployment.png)

### Northflank

Change the source to an image built on Northflank from a Git repository. Select a build service and branch to deploy builds from, the deployment service will use the latest build from the branch.

### External image

Change the source to use an image from an external container registry. Enter the image path and your [registry credentials](run-an-image-from-a-container-registry#registry-credentials), if using a private image.

Next steps

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Networking on NorthflankConfigure ports and security for your deployments.](/docs/v1/application/network/networking-on-northflank)[Scale your servicesIncrease the resources available to your services, and the number of instances to deploy.](/docs/v1/application/scale/scale-on-northflank)[Add databases and persistent storageCreate and use databases and other types of persistent storage in your project's applications and services.](/docs/v1/application/databases-and-persistence/stateful-workloads-on-northflank)