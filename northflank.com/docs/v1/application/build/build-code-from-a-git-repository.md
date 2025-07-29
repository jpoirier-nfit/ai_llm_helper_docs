---
source_url: https://northflank.com/docs/v1/application/build/build-code-from-a-git-repository
title: Build code from a Git repository | Build | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.251995
watsonmd_version: 0.1.0
---

Build / 

# Build code from a Git repository

Northflank offers different methods for building code from a Git repository:

  * You can manually or automatically build commits on specified branches or pull requests from a linked Git repository using a build service
  * You can build and deploy commits on a branch from a linked Git repository with continuous integration and delivery in a combined service
  * You can build commits on a branch from a linked Git repository manually or on a regular schedule using a job



Enabling CI will allow you to automatically build code when a new commit is pushed to a linked branch from your repository, or specific branches and/or pull requests. Built code can then be continuously deployed and added to a pipeline to create complex workflows.

You'll need an account on a Git provider that is [linked to Northflank](../getting-started/link-your-git-account) to get started.

[Click here ](https://app.northflank.com/s/project/create/service) to create a build or combined service.

Build from a repository

To build and run code from one branch on a repository you can use:

  * a combined service
  * a build service linked to a deployment service
  * a cron or manual job



Create a new service or job, select the repository you want to build from, then select the branch.

Once created your service will build an image for every new commit to the branches or pull requests it is monitoring, as long as CI is enabled.

Manually trigger a build

You can manually trigger a build by navigating to the branch or pull request to build from and selecting a commit to build.

You can find the list of branches and pull requests in the build service menu, or by clicking the build button `` in the build service header.

Northflank will begin building your commit, which may take several minutes. You can monitor the progress from the builds page and click through to view the logs for the build.

![Starting a new build in the Northflank application](https://assets.northflank.com/documentation/v1/application/build/build-code-from-a-git-repository/build-service-new-build.png)

Build specific branches or pull requests

You can use a build service to build and run code from specific branches and/or pull request branches by specifying build rules when creating a build service. You can edit the build rules of an existing build service on the build options page.

A build service will not build any branches or pull request branches without specified build rules. By default, a build service will build from all pull request branches (`*`) and the `master` branch.

Pull request rules match the name of a branch, and not the name of the pull request itself. For example, if you create a pull request rule for `patch/*`, a build will be triggered when a pull request is opened for any branch matching this regex. However, creating a pull request with a title that matches `patch/*` for a branch that does not match this regex will not trigger a build.

Example build rules:

Regex| Result  
---|---  
`*`| Builds every branch or pull request branch  
`master`| Builds the branch or pull request branch called _master_  
`feature/*`| Builds every branch or pull request branch starting with _release/_  
`feature/test`| Builds only the branch or pull request branch _feature/test_  
  
Build a specific repository directory

If you have a single repository with multiple microservices, or your repository is structured so that your build context is not the root, you can specify the build context when creating or editing your services.

By default, the build context is root (`/`), which makes all files in your repository available during the build. You can specify the set of files to be used in the build process by referring to a specific path relative to the root of your repository, such as `/app` or `/app/src`. If you change your build context to a non-root path, it will make all directories and files outside that path unavailable during the build. For example, setting your build context to `/app/src` will make both `/setup.sh` and `/app/config` unavailable in your builds.

You can combine the build context with path rules to create services that only build specific services or jobs in a monorepo.

![Build options in the Northflank application](https://assets.northflank.com/documentation/v1/application/build/build-code-from-a-git-repository/build-options.png)

Trigger a build on changes to specific files or directories

You can use path rules to either ignore or only monitor specified files or directories in a repository. This allows you to [trigger builds with CI](../release/manage-ci-cd) only when specific files within a repository are changed, or ignore changes to files that don't necessitate a new build. You can combine this with the build context to create services or jobs that only update when the relevant code is changed.

Path rules can be useful, for example, to stop changes to documentation files such as `README.md` from triggering a new build, or to only trigger a build when the required microservice or job code from a monorepo is modified.

You can add path rules to a service or job that builds from a repository. You can add or modify path rules in the build options section of a service or job, under advanced build settings.

### Ignore or allow

You can toggle the path rules to either `ignore` or `allow` the specified paths.

You can use an ignore list to stop commits that modify certain files or directories from triggering a new build.

You can use an allow list to trigger a build only when the specified files or directories are changed.

### Path rules syntax

Path rules are written the same way as a [.gitignore file ](https://git-scm.com/docs/gitignore), for example:
    
    
    README.md               # all README.md files
    node_modules/           # all files and subdirectories in the node_modules directory
    *.foo                   # all files ending in .foo
    **/bar                  # all directories in the repository named 'bar'
    !important/file.foo     # not important/file.foo
    

Skip CI with commit messages

You can enable and add commit message ignore flags in the build options section of a service or job under advanced build settings.

When enabled it will stop CI from being triggered if a commit message contains a matching flag even if it matches other build triggers.

  * If you push a commit with a message that contains one of the ignore flags you have added a build will not be triggered for that commit
  * If you push multiple commits at once a build will not be triggered if any of the commits contain an ignore flag in their commit message
  * If your service is configured to build from a pull request that PR will not be built if the HEAD commit contains an ignore flag in its commit message



Ignore flags can be added as strings, with each flag on a separate line. The default flags are enclosed in brackets to match the format of other common CI tools, but you can add flags without brackets.

#### Default ignore flags

The following ignore flags are automatically enabled, but you can remove them or add your own.
    
    
    [skip ci]
    [ci skip]
    [no ci]
    [skip nf]
    [nf skip]
    [northflank skip]
    [skip northflank]
    

Cache layers

You can enable layer caching with [Dockerfile](build-with-a-dockerfile#layer-caching) and [buildpack](build-with-buildpacks#layer-caching) builds to cache and reuse build images to speed up subsequent builds.

Next steps

[Run an image continuouslyDeploy a built image as a continuously-running service.](/docs/v1/application/run/run-an-image-continuously)[Run an image once or on a scheduleRun an image manually or on a cron schedule.](/docs/v1/application/run/run-an-image-once-or-on-a-schedule)[Inject build argumentsPass secrets and configuration settings to your builds.](/docs/v1/application/build/inject-build-arguments)[Build a repository using a DockerfileConfigure your application build process using a Dockerfile.](/docs/v1/application/build/build-with-a-dockerfile)[Build a repository using BuildpacksBuild your application automatically using Buildpack stacks.](/docs/v1/application/build/build-with-buildpacks)[Trigger a build on changes to specific files or directoriesAdd path rules to monitor or ignore specific files and directories in a repository for continuous integration build triggers.](/docs/v1/application/build/build-code-from-a-git-repository#trigger-a-build-on-changes-to-specific-files-or-directories)