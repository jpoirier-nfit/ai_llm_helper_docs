---
source_url: https://northflank.com/docs/v1/application/run/run-an-image-continuously
title: Run an image continuously | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.326564
watsonmd_version: 0.1.0
---

Run / 

# Run an image continuously

You can run an image built on Northflank from your linked Git repositories as a continuous service.

Enabling continuous integration and continuous delivery ([CI/CD](../release/manage-ci-cd)) will allow you to automatically run your latest code when a new commit is pushed to your repository's branches and/or pull requests.

Deployment services can be added to a pipeline to create complex workflows.

Alternatively you can build and run from one repository branch in a single combined service.

[Click here ](https://app.northflank.com/s/project/create/service) to create a deployment or combined service.

Run an image built on Northflank

You can run an image built on Northflank continuously using a deployment service.

### Create a new deployment

Create a new deployment service, and select Northflank as the deployment source. Expand `link build service` and choose the service and branch to deploy builds from. You can also create a deployment service with no build and link a build service later.

![Creating a deployment service in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/run-an-image-continuously/create-deployment-service.png)

### Edit an existing deployment

Navigate to an existing deployment service and select `configure deployment` from the service overview. Select `Northflank` as the deployment source, and choose a build service and branch to deploy builds from. `Update` to restart the service with the selected build.

### Deploy builds using a pipeline and release flow

You can also [create a pipeline](../release/create-a-pipeline-and-release-flow) with a [release flow](../release/create-a-pipeline-and-release-flow#create-a-release-flow) to deploy builds when the release flow is run. You can configure the release flow to deploy either specific images, such as promoting a build deployed in a previous stage of the pipeline, or the latest image from a build service or container registry.

Build and run an image in one service

You can build and run an image from a Git provider in a single service using a combined service. This is a self-contained CI/CD pipeline, and so cannot be used in pipelines like build and deployment services.

You can select a branch from a linked repository to build from, but cannot specify build rules to build from multiple branches or from pull request branches. With CI enabled, the service will automatically build the latest commit to your linked branch.

You can enable CD for your combined service to automatically deploy the latest build from your linked repository. Alternatively you can select commits to manually build and deploy from the builds page.

You can choose whether to build using a [Dockerfile or a buildpack](../build/build-code-from-a-git-repository#choose-a-build-type).

Read the [getting started guide](../getting-started/build-and-deploy-your-code) for more detail on combined services.

Next steps

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Networking on NorthflankConfigure ports and security for your deployments.](/docs/v1/application/network/networking-on-northflank)[Scale your servicesIncrease the resources available to your services, and the number of instances to deploy.](/docs/v1/application/scale/scale-on-northflank)[Add databases and persistent storageCreate and use databases and other types of persistent storage in your project's applications and services.](/docs/v1/application/databases-and-persistence/stateful-workloads-on-northflank)