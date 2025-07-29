---
source_url: https://northflank.com/docs/v1/application/release/manage-ci-cd
title: Manage CI/CD | Release | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.449020
watsonmd_version: 0.1.0
---

Release / 

# Manage CI/CD

You can configure continuous integration (CI) and continuous deployment (CD) for individual services and jobs, or create combinations of build services with deployment services and jobs depending on your requirements.

Your service or job must build from a Git repository or deploy from a Northflank build service to configure CI/CD.

Continuous integration can be configured to build each commit, or you can build from specific branches or pull requests. You can also configure advanced settings to only build when specific files or directories are updated, or to skip builds with certain commit messages.

Continuous deployment can be enabled to always roll out or run the latest build.

Using CI/CD with [path rules](../build/build-code-from-a-git-repository#trigger-a-build-on-changes-to-specific-files-or-directories) and [ignore flags](../build/build-code-from-a-git-repository#skip-ci-with-commit-messages) allows you to manage your build and deployment workflow from development to production, automatically building and deploying only where desired and retaining manual control where needed.

For example, you could configure a build service with path rules, linked to a CD-enabled deployment service, to automatically build and deploy your frontend to preview changes immediately. You can then manually build and deploy your backend only when required. Add commit message ignore flags to skip building minor changes, and automatically build and deploy all your microservices when you want to test the pull request for your next release.

![Overview of a combined service with CI/CD settings in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/manage-ci-cd/combined_service_overview.png)

Use continuous integration

Continuous integration can be enabled on combined services, build services, and jobs that build from a repository as a source.

You can enable and disable CI using the toggle in the header of the service or job.

Trigger builds in templates

You may want to disable CI if you prefer to start builds in [templates](../infrastructure-as-code/infrastructure-as-code) or [release flows](./configure-a-release-flow). The build service will then only build commits specified by a start build node when the template is run.

### CI on a combined service

You can enable CI on a combined service so that any new commits to the linked repository branch will be built automatically. If you also enable CD, every new commit to the branch will be automatically built and deployed.

### CI on a build service

You can enable CI on a build service to build any [new commits to branches or pull requests](../build/build-code-from-a-git-repository#build-specific-branches-or-pull-requests) that the service is configured to monitor.

You can combine this build service with one or more deployment services to create an effective workflow. For example, your build service could build both your development and production branches, and a deployment service with CD enabled could automatically deploy the latest development build. Another deployment service with CD disabled could then be used to manually deploy stable production builds when you are ready to release. You can also use the build service as a source for jobs.

### CI on a job

If you create a job that has version control as the image source, you can configure CI and other build settings within the job. If you enable CI on a job, it will always build the latest commit to the linked branch. If you also enable CD, the job will use the latest build when a run is triggered.

Trigger builds with commits to specific files or directories

You can use [path rules](../build/build-code-from-a-git-repository#trigger-a-build-on-changes-to-specific-files-or-directories) to trigger a build only when specific parts of your repository have been modified. You can either ignore directories or files containing code that you don't want to build in a specific job or service, or allow only the directories or files containing code that you want to build for a particular service or job.

Path rules can be configured from the build options page of a job or service, in `advanced build settings` under build type.

![Advanced build options in the Northflank application](https://assets.northflank.com/documentation/v1/application/release/manage-ci-cd/advanced-build-options.png)

Skip builds with commit messages

You can use [commit message ignore flags](../build/build-code-from-a-git-repository#skip-ci-with-commit-messages) to stop builds being triggered if the commit message contains a specific string.

Commit message ignore flags can be configured from the build options page of a job or service, in `advanced build settings` under build type.

Use continuous deployment

Continuous deployment can be enabled on combined services, deployment services, and jobs.

You can enable and disable CD using the toggle in the header of the service or job.

CD override

CD will be automatically disabled if a build is deployed manually, or via a [template](../infrastructure-as-code/infrastructure-as-code) or [release flow](./configure-a-release-flow).

### CD on a combined service

You can enable CD on a combined service so that it will always use the latest build from the service. If you have CI enabled, any commits that trigger a build will then be automatically deployed.

### CD on a deployment service

You can enable CD on a deployment service to always use the latest available image from the source. If you're using a build service as source, this will trigger a redeployment with the latest build when one is completed successfully.

If you're deploying an image from a container registry, this will always deploy the image tagged `latest` when a container is started. This means you must roll out a restart of your service to redeploy the latest container image.

### CD on a job

You can enable CD on a job so that it will always run using the latest available build or the container image tagged `latest`.

Run a job on image change

You can configure a job to run automatically when the source image is changed, if the job uses version control or a Northflank build service as the source. You can set this when creating the job, and change it from the job settings page. The following options are available:

  * Never: the job will not automatically run when the image changes. The job will continue to run on a schedule, or when run manually, and the image deployed will be according to the CI/CD configuration
  * CD & pipeline promotion: the job will be triggered to run if a build finishes and CD is enabled, or if an image is promoted to the job [via a pipeline](../release/create-a-pipeline-and-release-flow)
  * Always: the job will run every time the image is deployed via the UI, if a build finishes and CD is enabled, or if an image is promoted via a pipeline



Next steps

[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Configure a release flowLearn how to use the visual editor or code to configure a release flow.](/docs/v1/application/release/configure-a-release-flow)