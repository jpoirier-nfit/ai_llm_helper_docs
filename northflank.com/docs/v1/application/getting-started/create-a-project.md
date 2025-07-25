---
source_url: https://northflank.com/docs/v1/application/getting-started/create-a-project
title: Create a project | Getting Started | Northflank Application docs
crawl_date: 2025-07-25T12:06:48.998345
watsonmd_version: 0.1.0
---

Getting Started / 

# Create a project

Projects allow you to group together different resources within Northflank.

Projects on Northflank contain services to build and deploy your code, databases, storage volumes, and secret groups which can create isolated networks with each other in the same project and can communicate without the need for public endpoints.

You can select the region for each of your projects, which determines where your services and data are hosted.

Select a billing plan

When creating your Northflank account you will be asked to select a billing plan. Your plan determines the resources available to you on Northflank’s managed cloud, as well as your own cloud providers.

You can select the Developer Sandbox to try the Northflank platform for free. You’ll be able to create one project with some services, jobs, and addons, as well as deploy one BYOC cluster. You can upgrade your plan at any time, keeping your existing resources.

Alternatively, you can start with the pay as you go plan to start using Northflank without restrictions straight away.

[See our pricing page for a detailed description of account plans. ](https://northflank.com/pricing)

Create a project

Projects are specific to geographic regions, which determine where resources will be provisioned.

To create a new project:

  1. [Click here ](https://app.northflank.com/s/account/projects/new), or select `project` from the create new drop-down menu in the top right corner of the screen
  2. Enter a project name (optional: choose a colour to help identify different projects)
  3. Choose your project region, this will determine where your project is hosted
  4. Create your new project



![Creating a new project in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/create-a-project/create-project.png)

note

  * The region cannot be changed after your project has been created
  * A project cannot be transferred to other teams



Once your project has been created, you can start building and running your code, managing workflows in pipelines, and more.

![Creating a new project in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/create-a-project/empty-project-overview.png)

Project region

You can deploy your code to a specific region by [creating a project](../getting-started/create-a-project) in that region. This allows jobs or services to be run closer to customers, your development team, or external service for better connectivity.

You cannot change the region of a project after it is created, and all resources deployed in that project will be deployed in that region. [Builds](../build/build-your-code-on-northflank), unless [configured to run on your own cluster](../bring-your-own-cloud/configure-your-cluster#select-build-infrastructure), are performed on Northflank build infrastructure outside your project.

Northflank currently supports the following regions:

Region| API reference| Global region  
---|---|---  
Asia Southeast| `asia-southeast`| Asia Pacific  
Europe West| `europe-west`| EMEA  
Europe West Netherlands| `europe-west-netherlands`| EMEA  
US Central| `us-central`| Americas  
US East1| `us-east1`| Americas  
US West| `us-west`| Americas  
  
Contact [[support@northflank.com](mailto:support@northflank.com)](mailto:support@northflank.com) to register your interest for regions not listed above.

You can also [integrate with other cloud providers](../bring-your-own-cloud/use-other-cloud-providers-with-northflank) to deploy your own clusters, which will allow you to create projects hosted on your chosen cloud provider, in the regions they support.

Delete a project

You can delete a project from the project `` menu in the header of your project, or from the ` project settings` page.

Deleting a project will trigger the deletion of all resources contained within it, including builds, deployments, jobs, addons, as well as configurations such as secret groups and release flows. The process is irreversible, so please ensure you have backed up any databases and configuration files you want to keep.

You will still be billed for all resources consumed up to the project's deletion.

Next steps

[Build and deploy your codeQuickly and easily build and run code from a Git repository using a Dockerfile or buildpack.](/docs/v1/application/getting-started/build-and-deploy-your-code)[Set up a pipelineManage your workflow and release your code in an intuitive pipeline.](/docs/v1/application/getting-started/set-up-a-pipeline)[Add and verify domainAdd your domain name to your Northflank account and link it to a public port.](/docs/v1/application/getting-started/add-a-and-verify-domain)