---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/run-a-template
title: Run a template | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.805884
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Run a template

You can run a template manually from either your account templates page or a project templates page. You can see all of your team's templates in the team templates page, while the project templates page will only contain templates that have created that project or affected project resources.

Open the template you want to use and click ` run` to start a template run.

You can add or edit [argument overrides](create-a-template#provide-secrets-securely-to-a-template) to change values and secrets for the template run. You can also provide arguments for a template run [using the API](../../api/templates/run-template). This allows you to use one template and provide different configuration and secret values on each run simply by passing the required arguments.

View run status and history

When you run a template it will be scheduled to run, and enter the `pending` state.

It will shortly enter the `running` state, where it will begin running through the workflows defined in the template. You can see the status of each template, as well as the repository and file if [GitOps is enabled](gitops-on-northflank).

Each of your individual templates contains a list of template runs, the status of the template run, the commit hash (if the template run was triggered by a commit to a repository), and the time the template run was triggered.

### View template run

You can click on a template run to view the status of the components of your template, including creating/updating the project, overall workflows, and resources within individual workflows. Each node will indicate the state it is in, which can help you debug templates that are taking longer than expected to complete, or failing.

Each node can be expanded to view the template JSON for `running` nodes, and `successful` or `failed` nodes will also contain a `response` object from the Northflank API. Nodes can also receive a `retries` object, detailing the number of attempts and the time of the next attempt.

![The response for a node from a template run in the Northflank application](https://assets.northflank.com/documentation/v1/application/infrastructure-as-code/run-a-template/template-run-response.png)

### Template node states

Workflows and nodes can have the following states:

Pending: the node or workflow will run when previous steps are executed successfully

Running: the node or workflow is currently being executed

Waiting: the node is waiting for an action to be completed, will eventually timeout unless it receives a successful response

Retrying: the node has failed on previous runs, but is being executed again (up to 3 attempts)

Success: the node or workflow has completed successfully

Failed: the node or workflow has failed to execute, or exceeded 3 retries

Run a template automatically

You can enable `run a template automatically` so that any changes made to the template will trigger a template run, whether it's updated in the Northflank UI, via the API, or changed in the Git repository (if [GitOps is enabled](gitops-on-northflank)).

This is convenient if you want to manage your resources via templates, as triggering a run automatically will mean your resources will be updated to reflect the template specifications on change.

warning

As your modified template will run as soon as it's updated, make sure your changes are as intended before saving or pushing to the repository, especially if the template affects your production environment. Any other templates linked via GitOps will also run automatically, if this option is enabled for those templates.

Update a template

Templates can create new resources and update existing resources in your projects. If you update a template that uses one or more existing [projects as context](create-a-template#set-project-context) in the template, the next time it is run it will update resources with the same name (ID) with the new values in the template.

If the new template changes values that cannot be patched the template run will fail and the rest of the template will not be executed.

Existing resources in the projects, created manually or by previous template runs, will not be deleted by the template. If you have changed the names of resource in the template, new resources will be created alongside the existing ones, which may lead to unintended duplication of resources.

If you have enabled run a template automatically the template will be run immediately with any changes when you save the updated template. If you have also [enabled GitOps](create-a-template#enable-gitops-for-your-template) the template will be run as soon as your changes are committed.

Next steps

[Share a templateShare templates with your team or the public.](/docs/v1/application/infrastructure-as-code/share-a-template)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)