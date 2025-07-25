---
source_url: https://northflank.com/docs/v1/application/build/pull-images-from-Northflank
title: Pull images from Northflank | Build | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.300300
watsonmd_version: 0.1.0
---

Build / 

# Pull images from Northflank

Whenever you build a repository on Northflank the resulting image is stored in the Northflank container repository, ready to be deployed.

You can log in to the Northflank container registry to pull and run images locally, or use built images as the [base image ](https://docs.docker.com/engine/reference/builder/#from) in your Dockerfile. This can be useful if, for example, you are building from a monorepo and want to share a base image to reduce build times for different projects within it.

A reference to an image in the Northflank CR takes the format:

`registry.northflank.com/<projectId>/<serviceId>:<buildId>`

  * `projectId` is ID of the project your image was built in
  * `serviceId` is the service or job used to build your image
  * `buildId` can either be the Northflank-generated name for the build, the Git commit SHA, or `latest` to use the most recent build



Pull and run an image from Northflank

You can pull Docker images that have been built on Northflank using the [Docker CLI ](https://docs.docker.com/engine/reference/commandline/cli/).

Create an [API token](../secure/manage-api-tokens) or copy an existing one, and log in to the Northflank registry using Docker:

`docker login -u [USERNAME] -p [API_TOKEN] https://registry.northflank.com/`

You can find the relevant commands to pull and run the Docker image for a build by navigating to the builds page on a build service, combined service, or a job that builds from a git repository. Find the successful build in the list and click on it to open the logs and metrics view. In the top-right corner click the `pull docker image` button to view instructions and commands for that specific build.

You can then use this Docker pull command to pull your image from the Northflank registry:

`docker pull registry.northflank.com/<projectId>/<serviceId>:<buildId>`

The image can be run with the command:

`docker run -it registry.northflank.com/<projectId>/<serviceId>:<buildId>`

![A build log in the Northflank application showing the pull Docker image button](https://assets.northflank.com/documentation/v1/application/build/pull-images-from-northflank/build-logs-pull-image.png)

Use a built image as a base image

You can use an image built on Northflank as your base image for a [multi-stage build ](https://docs.docker.com/build/building/multi-stage/).

Find the URL for your image by following the steps to [pull an image](pull-images-from-Northflank#pull-and-run-an-image-from-northflank).

You can then use the image in your Dockerfile to build on Northflank, and also locally as long as you have pulled the image using Docker. You can supply the URL directly, or by using [build arguments](inject-build-arguments) (recommended).
    
    
    ARG PROJECT_ID
    ARG SERVICE_ID
    ARG BUILD_ID
    
    # method one
    FROM registry.northflank.com/${PROJECT_ID}/${SERVICE_ID}:${BUILD_ID}
    
    # method two: named build image
    FROM registry.northflank.com/${PROJECT_ID}/${SERVICE_ID}:${BUILD_ID} as builder
    

Next steps

[Build from a Git repositoryStart building from your linked Git repositories in minutes.](/docs/v1/application/build/build-code-from-a-git-repository)[Build a repository using a DockerfileConfigure your application build process using a Dockerfile.](/docs/v1/application/build/build-with-a-dockerfile)[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)[Upload a secret fileAdd secret files that will be mounted in your container.](/docs/v1/application/secure/upload-secret-files)