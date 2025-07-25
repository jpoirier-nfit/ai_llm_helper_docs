---
source_url: https://northflank.com/docs/v1/application/build/build-your-code-on-northflank
title: Build your code on Northflank | Build | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.236741
watsonmd_version: 0.1.0
---

Build / 

# Build your code on Northflank

At the heart of Northflank is your ability to build your code from Git repositories with a Dockerfile.

Northflank builds Docker container images from your repositories, which can then be easily deployed and scaled on our platform.

When building from Git you can enable continuous integration (CI) to automatically build new commits to the repository, or to specific branches or pull requests.

To build and run an image in one self-contained service you can use [a combined service](../run/run-an-image-continuously#build-and-run-an-image-in-one-service).

[Build from a Git repositoryStart building from your linked Git repositories in minutes.](/docs/v1/application/build/build-code-from-a-git-repository)[Add a self-hosted VCSAdd your own self-hosted Git provider and build from its repositories.](/docs/v1/application/collaborate/manage-git-integrations#add-a-self-hosted-vcs)[Build a repository using a DockerfileConfigure your application build process using a Dockerfile.](/docs/v1/application/build/build-with-a-dockerfile)[Build a repository using BuildpacksBuild your application automatically using Buildpack stacks.](/docs/v1/application/build/build-with-buildpacks)[Build a specific directorySpecify the build context to build only specific directories from your repository.](/docs/v1/application/build/build-code-from-a-git-repository#build-a-specific-repository-directory)[Trigger a build on changes to specific files or directoriesAdd path rules to monitor or ignore specific files and directories in a repository for continuous integration build triggers.](/docs/v1/application/build/build-code-from-a-git-repository#trigger-a-build-on-changes-to-specific-files-or-directories)[Skip CI builds with commit messagesAdd strings to your commit messages that will stop Northflank CI from automatically building commits pushed to your repository.](/docs/v1/application/build/build-code-from-a-git-repository#skip-ci-with-commit-messages)[Inject build argumentsPass secrets and configuration settings to your builds.](/docs/v1/application/build/inject-build-arguments)[Pull an image from NorthflankPull images built on Northflank locally, or use built images as the base image in your Dockerfile.](/docs/v1/application/build/pull-images-from-Northflank)