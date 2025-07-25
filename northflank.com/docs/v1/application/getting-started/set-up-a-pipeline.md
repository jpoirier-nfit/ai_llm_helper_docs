---
source_url: https://northflank.com/docs/v1/application/getting-started/set-up-a-pipeline
title: Set up a pipeline | Getting Started | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.030858
watsonmd_version: 0.1.0
---

Getting Started / 

# Set up a pipeline

Pipelines on Northflank allow you to create and manage complex continuous integration and continuous delivery (CI/CD) workflows.

By adding your project's resources to a pipeline and creating release flows for each stage, you can automate your releases from development through to production.

Pipelines and release flows allow you to manage building and deploying your code, backing up data and running migrations, promoting deployed images from one stage to the next, and more.

This guide will take you through creating a pipeline, a build service, and a deployment service, and then populating a pipeline stage and configuring a simple release flow to deploy code built on Northflank.

Create a pipeline

To create a pipeline:

  1. [Click here ](https://app.northflank.com/s/project/create/pipeline), or choose `pipeline` from the create new drop-down menu in the top right corner of the dashboard
  2. Enter a name
  3. Click `create pipeline`



Create a build service

You can configure most aspects of a build service after it is created - except the name.

  1. [Click here ](https://app.northflank.com/s/project/create/service), or open the `create new` menu in the top right corner of the dashboard and select `service`
  2. Select `build`
  3. Basic information: enter a name for your service
  4. Repository: select the repository from the drop-down list and choose the branch you want to build from
  5. Repository: enter your pull request and branch build rules, or leave blank to build all new commits. You can set multiple rules, and you can add rules for both pull requests and branches.
  6. Build options: choose Dockerfile if you have a custom Dockerfile in your registry, or buildpack to automatically build your application. If your Dockerfile and/or build context are not root, specify the relative paths.
  7. Environment variables (optional): you can set runtime variables and build arguments here, if required
  8. Resources: set the compute plan to suit your build
  9. Click `create service`



Create deployment services

You can configure most aspects of a deployment service after it is created - except the name.

  1. [Click here ](https://app.northflank.com/s/project/create/service), or open the `create new` menu in the top right corner of the dashboard and select `service`
  2. Select `deployment`
  3. Basic information: enter a name for your service
  4. Deployment: select Northflank as the source, but do not link the build service
  5. Environment variables (optional): you can set runtime variables and build arguments here, if required
  6. Networking (optional): add any required public or private ports
  7. Resources: set the compute plan and number of instances to suit your deployment
  8. Advanced (optional): you can configure health checks and a Docker CMD override, if required
  9. Click `create service`



Add resources to your pipeline

  1. Select the pipeline you want to use from the project pipelines page
  2. Click ` add items to development`
  3. Find your deployment service, select it, and click `add 1 item` to add it to the stage. This will make it available in your release flow when you configure one.



![A pipeline in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/set-up-a-pipeline/pipeline.png)

You can add multiple deployment services, jobs, and addons to a pipeline stage.

Removing a deployment service from a pipeline will not unlink its build service or external image, nor pause the deployment service. You can edit or disable the deployment service itself from its own dashboard.

Add a release flow

Now you can create a release flow for the development stage of your pipeline, which you have populated with your deployment service.

  1. Click ` add release flow` in the header for the development stage
  2. Select ` get started with visual editor`
  3. Click and drag a `start build` node into the sequential workflow
  4. Click on the `start build` node to edit it. Select your build service for `service / job`, the `branch` you want to build, and leave the `commit` field blank to build the latest commit to the branch, or select a specific commit to build.
  5. Enable `wait for completion` for the node. This option means that the next node will not run until this one has completed, in this instance the release flow will wait for the build to finish before running the next node. `Save node` to finish configuring the node.
  6. Click and drag a `deploy build` node and drop it below the `start build` node. Click on it to configure the node.
  7. Select the same `build service` as you used in the `start build` node, select the `build` by selecting the branch or PR you want to deploy from, and either `latest` or a specific build. Select your deployment service as the `target` and `save node`.
  8. Exit the release flow editor by clicking the `` close button in the top-right corner



![Editing a node in a release flow in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/set-up-a-pipeline/release-flow-edit-node.png)

Run a release flow

After you have configured a release flow for your pipeline stage, you can now run it and Northflank will execute the workflow as you have specified it.

  1. Click ` run` in the header for the development stage
  2. Add a name for the release and a description. This can be useful to track your releases, so you can quickly identify what is deployed to an environment and to roll back to a previous release if you need to.
  3. Ignore the expandable menu with the name of your deployment service. In future, you can use this to override the default release flow configuration for one run only, so you can quickly run a release without needing to edit the whole template.
  4. Click `run` and watch the release flow



![A release flow run in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/set-up-a-pipeline/release-flow-run-success.png)

Promote a deployed image

You can configure a release flow to promote images deployed in the preceding stage to the stage that contains the release flow. You can promote any image deployed to a deployment service or job, whether they are built on Northflank or deployed from an external container registry.

You can only select images from the previous pipeline stage to promote.

To deploy images from a previous stage:

  1. Add your required deployment services and jobs to your staging or production stage
  2. Open the release flow editor and add a `promote deployment` node
  3. Edit the node and select the `origin`, which is a deployment service or job from the previous stage
  4. Select `target`, which is the deployment service or job in the current stage that you want to deploy the image
  5. `Save release flow` and ` run` it, the image(s) in your previous stage will be promoted to the current stage



![A release flow node to promote a deployment in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/set-up-a-pipeline/release-flow-promote-deployment.png)

Learn more about using pipelines and release flows on Northflank

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Configure a release flowLearn how to use the visual editor or code to configure a release flow.](/docs/v1/application/release/configure-a-release-flow)[Run a release flowRun a release flow and manage releases for your different environments.](/docs/v1/application/release/run-and-manage-releases)[Set up a preview environmentCreate templates in your pipelines to automatically generate temporary preview environments to view pull requests and branches.](/docs/v1/application/release/set-up-a-preview-environment)[Roll back a releaseRoll back a release to a previous version.](/docs/v1/application/release/run-and-manage-releases#roll-back-a-release)[Manage CI/CDConfigure continuous integration and continuous delivery on your Northflank services.](/docs/v1/application/release/manage-ci-cd)[Run migrationsRun database migrations and update your deployments simultaneously when you update your schema.](/docs/v1/application/release/run-migrations)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)