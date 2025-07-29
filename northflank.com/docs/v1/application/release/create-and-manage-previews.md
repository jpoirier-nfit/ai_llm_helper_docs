---
source_url: https://northflank.com/docs/v1/application/release/create-and-manage-previews
title: Create and manage previews | Release | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.579894
watsonmd_version: 0.1.0
---

Release / 

# Create and manage previews

Northflank will automatically create new preview environments for branches that match your branch and pull request Git trigger rules.

If you have configured a webhook trigger, a new preview environment will be created when you send a request to the webhook URL.

Updating preview environment templates

If you update your preview environment template while there are existing environments, please note that when the preview is next triggered:

  * Resources with the same ID (name) will be updated with the new values in the template
  * If the new template changes values that cannot be patched the template run will fail and the existing preview environment will not be updated
  * Existing resources will not be automatically deleted and if you have changed resource names in the template, the new resources will be created alongside the existing ones



All resources created by the preview environment will be tagged with the environment name. You are unable to assign or manage tags created by a preview environment, and they will be deleted when the environment is deleted.

You can see a list of preview environments created in your pipeline, with the repository, branch, and status for each environment. Click through to a preview environment to see the status of the template run and resources associated with the environment.

### Resources

Resources for a preview environment, including services, jobs, addons, and secret groups, will be added to the list as they are created by the template. You can view the status of resources created by the preview environment, pause and resume them, and click through to manage them where required.

### View runs

You can view a list of template runs for the preview environment, and click through to see the status and results of specific nodes in the template. A new template run for a preview environment will be triggered if a new commit is pushed to the same branch.

### Settings

You can delete your preview environment from the settings page.

Create a preview environment using a webhook

You can use a webhook trigger to create and update preview environments. Enable the webhook trigger in the template settings and trigger it by making either a `GET` or `POST` request.

You can include query parameters at the end of the webhook URL to pass values directly to your template as arguments.

### Git trigger parameters

You can override the values for Git triggers configured in your preview environment using a webhook. For example, you may have configured a template to build from multiple repositories, or to build from specific directories in a single repository, and need to override the default branch and commit for each trigger.

To set the values for specific triggers, use the name of the Git trigger followed by the field name in dot notation:

Parameter| Value  
---|---  
`<git-trigger>.branch`| The branch name  
`<git-trigger>.sha`| The commit SHA  
`<git-trigger>.pullRequestId`| The ID of the pull request, if triggered by PR  
`<git-trigger>.repoUrl`| The repository URL  
  
For example, the following endpoint would create a preview environment and set the branch for the trigger `frontend` to `feature/example` and the branch for the trigger `backend` to `develop`: `https://webhooks.northflank.com/previews/<TOKEN>?frontend.branch=feature%2Fexample&backend.branch=develop` (the character `/` has been encoded as `%2F`).

### Preview environment name and description

You can pass in optional query parameters to set the `name` and `description` for a preview environment. If you do not pass in `name`, the preview environment will use a generated name if it has the data required for your [selected naming convention](set-up-a-preview-environment#choose-a-naming-convention). Otherwise, it will use a random name which is returned in the response body.

Triggering a preview environment run with the name of an existing preview environment will update that environment.

### Other values

You can also add whatever other URL query parameters you require. For example, the triggering a preview environment with the following parameters: `https://webhooks.northflank.com/previews/<TOKEN>?foo=bar` would make `${args.foo}` available in the template, resolving to the value `bar`.

You can use this to pass in secrets or configuration details for your preview environment, or set the branch and commit in build nodes that don't have any Git triggers configured.

Create a preview environment manually

You can click ` create preview` in your pipeline to run your preview environment template manually.

You will be prompted to select the branches and commits to use from the repository for each Git trigger. You can also override any arguments for the template. Manually-created preview environments will be given a random name.

CI/CD is disabled for any manually-created environments, meaning it will not be updated when commits are pushed to the previewed branch. You can update the preview environment by creating a new preview with the same branch, which will run the preview template again.

Pause preview environment triggers

You can pause triggers for a preview environment in the header of the preview environment settings. While paused, Git triggers will be inactive and requests to the webhook will return the HTTP status `202`, with a message explaining the trigger is paused. Preview environments can still be created manually while triggers are paused.

This will suspend all Git and webhook triggers, and preview environments will not be automatically provisioned until you enable the triggers again.

Delete a preview environment

If the preview environment has been created by a pull request trigger, the environment will be deleted when the pull request is closed or merged. A preview environment created by a branch trigger will be deleted if the branch is deleted. You can manually delete a preview environment from its settings page.

Deleting a preview environment will remove all the resources generated by the template and remove the preview environment entirely from your pipeline. If a new commit is pushed that matches the Git trigger, a new preview environment will be created for the branch.

Preview environment tags will only be deleted when a preview environment is automatically or manually deleted.

Next steps

[Create and manage previewsManage your preview environments, pause triggers, and generate previews manually.](/docs/v1/application/release/create-and-manage-previews)[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Write a templateLearn how to structure a Northflank template, define workflows, create resources, and perform actions.](/docs/v1/application/infrastructure-as-code/write-a-template)[Run migrationsRun database migrations and update your deployments simultaneously when you update your schema.](/docs/v1/application/release/run-migrations)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)