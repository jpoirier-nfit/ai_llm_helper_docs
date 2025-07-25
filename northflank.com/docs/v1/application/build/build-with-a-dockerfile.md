---
source_url: https://northflank.com/docs/v1/application/build/build-with-a-dockerfile
title: Build with a Dockerfile | Build | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.278203
watsonmd_version: 0.1.0
---

Build / 

# Build with a Dockerfile

You can build your projects on Northflank by supplying a Dockerfile in your repository.

A custom Dockerfile gives you full control over each step of the build process, including things like build arguments and custom base images. You must specify the location of the Dockerfile in your repository and the build context (root by default).

Select `Dockerfile` as the build type when creating your service, or change an existing service from the build options page.

See Docker's guide on [writing Dockerfiles ](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) and the [Dockerfile reference ](https://docs.docker.com/engine/reference/builder/) for more information.

![Docker build options in the Northflank application](https://assets.northflank.com/documentation/v1/application/build/build-with-a-dockerfile/build-options-dockerfile.png)

Dockerfile location

If you have a single repository with multiple services, or your repository is structured so that your Dockerfile is not in the root, you can specify its location when creating or editing your services.

You can specify the location of the Dockerfile relative to the root of the repository. For example root: `/Dockerfile`, or in a subdirectory: `/directory/subdirectory/Dockerfile`.

You can use a Dockerfile outside the build context, but commands in your Dockerfile are relative to the build context. If your build context is set to `/app/src`, the Docker command `COPY . /src` will copy all files from `/app/src` to the `/src` directory in your container.

Learn more about the [Dockerfile ](https://docs.docker.com/engine/reference/builder/).

Build engine

Choose between Kaniko (default) or BuildKit under advanced build settings. You may want to choose another build engine if you experience any issues with reliability.

Docker ignore

You should always include a `.dockerignore` file in your repository, in order to reduce the final image size by excluding everything unnecessary.

For example to ignore the git folder and `.env` files you would add the following to `.dockerignore`:
    
    
    .git
    *.env
    

Layer caching

You can create a more efficient Dockerfile that will build faster on subsequent builds by taking advantage of layer caching.

For this example, we'll look at the build stage from Northflank's [AngularJS template Dockerfile ](https://github.com/northflank-examples/angular-js-example/blob/master/Dockerfile).

The first time the image is built Northflank will run all the build steps in the Dockerfile and write each layer to the image registry. For each subsequent build it checks whether the files for that layer have changed. If there are no changes, the existing layers will be used to complete the build.

In this example the build step `COPY package*.json ./` is nearer the start of the Dockerfile as its files are likely to change less frequently. This means it can be cached and used for future builds where the contents of `package*.json` remain unchanged:
    
    
    FROM node:lts-alpine as build-stage     # layer unchanged, use cache
    WORKDIR /app                            # layer unchanged, use cache
    COPY package*.json ./                   # layer unchanged, use cache
    RUN npm install                         # layer unchanged, use cache
    COPY . .                                # layer changed, run again
    RUN npm run build                       # previous layer changed, run again
    

If you add another dependency to `package.json`, all layers after it must be rebuilt:
    
    
    FROM node:lts-alpine as build-stage     # layer unchanged, use cache
    WORKDIR /app                            # layer unchanged, use cache
    COPY package*.json ./                   # layer changed, run again
    RUN npm install                         # previous layer changed, run again
    COPY . .                                # previous layer changed, run again
    RUN npm run build                       # previous layer changed, run again
    

The above example covers the Dockerfile-based build engines (Kaniko and Buildkit). The buildpack build backend can also benefit from caching. If caching is enabled, the build engine will try to cache and reuse build dependencies from previous builds.

Learn more in the [Docker documentation ](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#leverage-build-cache).

Target build stage

If your Dockerfile contains multiple build stages you can specify the target stage by entering its name here.

For example, for a Dockerfile with the following stages:
    
    
    FROM debian AS build-env
    # ...
    
    FROM alpine AS production-env
    # ...
    

Specifying the target stage as `build-env` will build an image using the commands up until, but not including the `production-env` stage.

Learn more in the [Docker documentation ](https://docs.docker.com/engine/reference/commandline/build/#specifying-target-build-stage---target).

Docker build credentials

You can access private images from external container registries in your Docker build process by applying the relevant [registry credentials](../run/save-registry-credentials#root) in the build settings. You can add or update build credentials for any resource that builds from a Git repository and uses a Dockerfile, under the advanced build setting section in build options.

You can use multiple container registries, but only one credential per container registry can be selected.

After applying the credentials you can use private images in the Dockerfile for the build, in the format `FROM <container-registry>/<account>/<image>:<tag>`.

Clone git folder or full repository

When you build an image Northflank performs a shallow clone of your git repository by default, as only the most recent commit is required in the build process. The `.git` folder is also excluded by default.

If you require the `.git` folder in your build, you can include it in the build environment by selecting `include .git folder` in the build options section of a service or job, under advanced build settings.

If you require the entire git history to be available, you can also enable `full clone`. This may significantly increase the time it takes to build larger repositories with extensive histories.

Next steps

[Build from a Git repositoryStart building from your linked Git repositories in minutes.](/docs/v1/application/build/build-code-from-a-git-repository)[Inject build argumentsPass secrets and configuration settings to your builds.](/docs/v1/application/build/inject-build-arguments)[Run an image continuouslyDeploy a built image as a continuously-running service.](/docs/v1/application/run/run-an-image-continuously)[Run an image once or on a scheduleRun an image manually or on a cron schedule.](/docs/v1/application/run/run-an-image-once-or-on-a-schedule)