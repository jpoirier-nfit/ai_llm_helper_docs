---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/infrastructure-as-code
title: Infrastructure as code on Northflank | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.591674
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Infrastructure as code on Northflank

Northflank templates give you the ability to codify your workflow to create and update resources on Northflank. Everything you can do in the Northflank UI or API can be achieved in repeatable, programmatic templates.

Enable bidirectional GitOps on your templates to automatically update resource configurations and scale infrastructure on Git push.

You can create templates with dynamic variables to deploy different environments, across multiple regions and cloud providers, and provide other users the ability to quickly deploy your stack with their desired configuration.

### Types of template

  * Templates are created in your team. You create and update team-level integrations and infrastructure, projects and resources. You can include pipelines with release flow and preview environment templates within these templates.
  * Release flow templates can be defined for each stage of a pipeline. They automate your workflow to run a release for the specific stage.
  * Preview environment templates are also defined within a pipeline. They specify resources and secrets to create for ephemeral environments.



![An example of a successfully run template in the Northflank application](https://assets.northflank.com/documentation/v1/application/infrastructure-as-code/infrastructure-as-code-on-northflank/template-success.png)

Create integrations, infrastructure, and resources in templates

Templates allow you to create reproducible specifications for setting up team integrations, infrastructure, and resources to deploy in any region or [cloud provider](../bring-your-own-cloud/use-other-cloud-providers-with-northflank).

You can reproduce any workflow you would use to create integrations and deploy resources using the Northflank UI or API in a template, such as:

  * Automate the process to deploy a single service, or multiple projects
  * Manage your infrastructure and deployments using GitOps
  * Add [integrations with cloud providers](../bring-your-own-cloud/use-other-cloud-providers-with-northflank) and deploy clusters into your own cloud accounts
  * Define pipelines with release flows and preview environments
  * Create shareable one-click deployments for your project so users can get up and running immediately



Templates can be created using the visual editor in the Northflank application, or edited directly as JSON.

[Create a templateLearn how to create and configure a Northflank template.](/docs/v1/application/infrastructure-as-code/create-a-template)[Write a templateLearn how to structure a Northflank template, define workflows, create resources, and perform actions.](/docs/v1/application/infrastructure-as-code/write-a-template)[Template nodesLearn about different types of template nodes, their behaviour, and their specifications.](/docs/v1/application/infrastructure-as-code/template-nodes)[Run a templateRun templates manually or automatically.](/docs/v1/application/infrastructure-as-code/run-a-template)[Share a templateShare templates with your team or the public.](/docs/v1/application/infrastructure-as-code/share-a-template)

Write dynamic templates

You can write templates in a programmatic manner so that they can be easily run with different configurations, or use dynamic values based on variables. Hardcoded values can be replaced by template arguments, references to the output from a previous template node, and functions that are evaluated when the template is run.

This allows you to use a single generalised template to deploy the same project in different regions, as different staging environments, or share a template where team members or the public can enter their own arguments to configure a deployment.

[Use values from a template nodeUse the values output from a node executed in a template.](/docs/v1/application/infrastructure-as-code/make-a-template-dynamic#get-node-outputs-from-references)[Use arguments in your templateUse variables to make your template dynamic, and override the values on individual template runs.](/docs/v1/application/infrastructure-as-code/make-a-template-dynamic#add-arguments)[Use functions in templatesUse Northflank functions in your templates to change and evaluate values based on arguments and node outputs.](/docs/v1/application/infrastructure-as-code/make-a-template-dynamic#use-northflank-functions)[Manage multiple templates with GitOpsUse a single source of truth for your infrastructure and projects across regions and cloud providers, or deploy the same project with different configuration values.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank#create-multiple-northflank-templates-from-one-source)

Manage infrastructure with GitOps

Northflank's bidirectional GitOps helps you maintain a single source of truth for your infrastructure and resource configuration. Any changes to your template code committed to your repository will automatically update the template on Northflank, and any changes to your template in Northflank will be committed to your repository. You can use one source template to manage multiple Northflank templates. Combined with arguments and overrides you can update multiple projects with separate configurations.

You can also set your template to run automatically when it is updated, meaning you can manage your infrastructure and configuration using Git.

[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)[Use Git Actions on NorthflankCreate workflows and publish GitHub Actions that interact with Northflank.](/docs/v1/application/infrastructure-as-code/use-github-actions-with-northflank)

Define release flows and preview environments

Release flows are templates for specific pipeline stages that can automate release tasks, such as backing up databases, triggering and deploying builds, running jobs, and promoting images from one stage to another.

You can create a release flow either in an existing project's pipeline, or by configuring it in a pipeline node in a Northflank template. You can add Git or webhook triggers to run a release automatically.

[Release flows and preview environments within templatesCreate and manage pipelines with release flow and preview environment templates within Northflank templates.](/docs/v1/application/infrastructure-as-code/write-a-template#include-release-flows-and-preview-environment-templates)[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Configure a release flowLearn how to use the visual editor or code to configure a release flow.](/docs/v1/application/release/configure-a-release-flow)[Set up a preview environmentCreate templates in your pipelines to automatically generate temporary preview environments to view pull requests and branches.](/docs/v1/application/release/set-up-a-preview-environment)

Versioning and history for templates

You can use GitOps with your Northflank templates to track and manage changes in your Git repository.

All templates have a run history, detailing the status and output of each template run, which you can use to review and troubleshoot templates. Release flows allow you to roll back to a previous release with a single click.

Enterprise customers can use the template drafts feature to review proposed changes to a template directly in Northflank, and track template changes and runs using [audit logs](../observe/audit-logs).

[Manage template versions on NorthflankUse the template drafts system to review, accept, or reject proposed changes to your team's Northflank templates.](/docs/v1/application/infrastructure-as-code/manage-template-versions)[Roll back a releaseRoll back a release to a previous version.](/docs/v1/application/release/run-and-manage-releases#roll-back-a-release)