---
source_url: https://northflank.com/docs/v1/application/release/run-and-manage-releases
title: Run and manage releases | Release | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.508396
watsonmd_version: 0.1.0
---

Release / 

# Run and manage releases

You can run and manage release flows from the pipeline you [created them in](create-a-pipeline-and-release-flow).

Select the pipeline that contains the release flows you want to manage from the pipelines list. You can ` run` a release flow for a stage, or click the options button `` to view runs or edit the release flow.

Run a release flow manually

You can run a release flow for a pipeline stage by clicking ` run` in the release header in the pipeline overview.

You can enter a display name and description for the release run to help you track releases, particularly useful if you need to roll back a release. If you do not enter a name for the run it will display the generated UUID, but you can edit the display name of a run afterwards.

If the release flow contains any build deployments from build services or container registries you will be able to override the configured build or image to deploy, if required.

Click `run` to begin the release flow run and the view of the release flow run will open, showing you the status of each workflow and node as they are executed.

![An example of a release flow run in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/run-and-manage-releases/release-run.png)

Use Git triggers to run a release flow

You can [add Git triggers on the settings page](create-a-pipeline-and-release-flow#automatically-run-a-release-flow) of a release flow.

A trigger will run the release flow whenever a change to the specified repository is committed.

You can include:

  * [branch and pull request rules](../build/build-code-from-a-git-repository#build-specific-branches-or-pull-requests) to only trigger on commits to specific branches or pull requests
  * [path rules](../build/build-code-from-a-git-repository#trigger-a-build-on-changes-to-specific-files-or-directories) to only trigger on changes to specific directories or files in a repository, or to ignore changes to specific directories or files
  * [commit message ignore flags](../build/build-code-from-a-git-repository#skip-ci-with-commit-messages) to skip runs for commits with messages that contain certain strings



You can [use references to obtain the values of Git triggers](configure-a-release-flow#use-git-triggers-in-a-release-flow) in your template.

Run a release flow using a webhook

You can trigger a release flow run by making a `GET` or `POST` request to a release flow's [webhook endpoint](configure-a-release-flow#enable-webhook-for-a-release-flow).

You can include query parameters at the end of the webhook URL to pass values directly to your template as arguments.

### Git trigger parameters

You can override the values for Git triggers configured in your release flow using a webhook. For example, you may have configured a template to build from multiple repositories, or to build from specific directories in a single repository, and need to override the default branch and commit for each trigger.

To set the values for specific triggers, use the name of the Git trigger followed by the field name in dot notation:

Parameter| Value  
---|---  
`<git-trigger>.branch`| The branch name  
`<git-trigger>.sha`| The commit SHA  
`<git-trigger>.pullRequestId`| The ID of the pull request  
`<git-trigger>.repoUrl`| The repository URL  
  
For example, the following endpoint would run a release and set the branch for the Git trigger `frontend` to `feature` and the branch for the trigger `backend` to `develop`:

`https://webhooks.northflank.com/release-flows/<TOKEN>?frontend%2Ebranch=feature&backend%2Ebranch=develop`

Note the characters `/` and `.` have been encoded as `%2F` and `%2E` respectively.

### Release flow name and description

You can pass in optional values to set the `name` and `description` for a release, otherwise the release flow will be given a random identifier as the name and no description.

### Other values

You can also add whatever other URL query parameters you require. For example, the triggering a release flow with the following parameters: `https://webhooks.northflank.com/release-flows/<TOKEN>?foo=bar` would make `${args.foo}` available in the template, resolving to the value `bar`.

You can use this to pass in secrets or configuration details for your release, or set the branch and commit in build nodes that don't have any Git triggers configured.

View runs

The state of the current or most recent release is indicated in the release header for each pipeline stage. This can be clicked on to view the currently running release, or the list of previous runs.

### Release flow run statuses

Pending: the release flow is scheduled to run

Running: the release flow is currently running

Success: all of the nodes within the release flow completed successfully

Failed: some or all of the nodes within the release flow failed to complete successfully

### Release flow runs

Click the options button `` and select ` view release flow runs`.

![A list of release flow runs and rollbacks in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/run-and-manage-releases/release-rollback.png)

This displays a list of previous and current release flow runs and their status. You can also see when the release flow was run, when it was completed, and whether it was a release or rollback.

Click on any run in the list to view the status of individual nodes. You can click on an individual node to view its code, as well as the `response` object which contains the response from the Northflank API and the `retries` object, which contains information about any attempted retries.

### Node statuses

Pending: the node or workflow will run when previous steps are executed successfully

Running: the node or workflow is currently being executed

Waiting: the node is waiting for an action to be completed, will eventually timeout unless it receives a successful response

Retrying: the node has failed on previous runs, but is being executed again (up to 3 attempts)

Success: the node or workflow has completed successfully

Failed: the node or workflow has failed to execute, or exceeded 3 retries

Roll back a release

You can roll back to a specific release by opening it from the list of past release flow runs.

Click ` roll back to this release` to return your pipeline stage to the state it was in after the selected release flow run.

Deployments to services, builds, etc, will be reverted to those deployed or promoted in the selected release flow run. This will not undo any changes such as a [database migration](handle-runtime-migrations), which you will need to restore manually.

You can also choose to `roll back release flow configuration`, which will restore your release flow configuration to the state it was in for the selected run.

Select `view rollbacks` to see a list of rollbacks to the selected release.

Next steps

[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)[Manage CI/CDConfigure continuous integration and continuous delivery on your Northflank services.](/docs/v1/application/release/manage-ci-cd)[Expose a deployment's portConfigure ports and security for your deployments.](/docs/v1/application/network/configure-ports)[Configure health checksMonitor the uptime and success of your deployed services and builds to ensure your code runs correctly and is always available.](/docs/v1/application/observe/configure-health-checks)[View logsView detailed, real-time logs from builds, deployments, and more.](/docs/v1/application/observe/view-logs)