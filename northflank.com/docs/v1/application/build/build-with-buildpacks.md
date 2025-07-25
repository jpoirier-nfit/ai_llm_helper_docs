---
source_url: https://northflank.com/docs/v1/application/build/build-with-buildpacks
title: Build with buildpacks | Build | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.292766
watsonmd_version: 0.1.0
---

Build / 

# Build with buildpacks

You can build your projects on Northflank using [buildpacks ](https://buildpacks.io/docs/). This does not require you to supply a Dockerfile as a buildpack will try to automatically determine how to build your project. You must specify the build context (root by default).

Select `buildpack` as the build type when creating your service, or change an existing service from the build options page.

You can select from a list of popular buildpacks under advanced build settings if you require support for other languages. Check the provider's documentation for more information on base images and language versions.

![Buildpack stack options in the Northflank application](https://assets.northflank.com/documentation/v1/application/build/build-with-buildpacks/build-options-buildpack.png)

Buildpack stacks on Northflank

Buildpack stack| Base image| Supported languages  
---|---|---  
[heroku/builder:24 ](https://github.com/heroku/builder) 1| Ubuntu 22.04| Go, Java, Node.js, PHP, Python, Ruby, Scala, .NET  
[heroku/builder:22 ](https://github.com/heroku/builder) 1| Ubuntu 22.04| Go, Java, Node.js, PHP, Python, Ruby, Scala, .NET  
[heroku/builder-classic:22 ](https://github.com/heroku/builder) 1 (deprecated)| Ubuntu 22.04| Go, Java, Node.js, PHP, Python, Ruby, Scala, Clojure  
[heroku/buildpacks:20 ](https://github.com/heroku/cnb-builder-images) (deprecated)| Ubuntu 20.04| Go, Java, Node.js, PHP, Python, Ruby, Scala  
[heroku/buildpacks:18 ](https://github.com/heroku/cnb-builder-images) (deprecated)| Ubuntu 18.04| Go, Java, Node.js, PHP, Python, Ruby, Scala  
[gcr.io/buildpacks/builder:v1 ](https://github.com/GoogleCloudPlatform/buildpacks)| Ubuntu 18.04| Node.js, Python, Go, Java, Ruby  
[cnbs/sample-builder:alpine ](https://github.com/buildpacks/samples/tree/master/builders/alpine) 2| Alpine 3.10| Java, Kotlin  
[cnbs/sample-builder:bionic ](https://github.com/buildpacks/samples/tree/master/builders/bionic) 2| Ubuntu 18.04| Java, Kotlin, Ruby  
[paketobuildpacks/builder:tiny ](https://paketo.io/docs/concepts/builders/#tiny)| Ubuntu 18.04| Java, Go  
[paketobuildpacks/builder:base ](https://paketo.io/docs/concepts/builders/#base)| Ubuntu 18.04| Java, Node.js, Go, .NET Core, Ruby, NGINX  
[paketobuildpacks/builder:full ](https://paketo.io/docs/concepts/builders/#full)| Ubuntu 18.04| PHP, Java, Node.js, Go, .NET Core, Ruby, NGINX, HTTPD  
  
  1. Heroku builder stacks are compatible with the [Cloud Native Buildpacks ](https://buildpacks.io/) specification
  2. Cloud Native Buildpack stack samples are not recommended for use in production.



Custom buildpack group

You can use multiple buildpacks together to provide support for more complex builds. For example, you might use one buildpack to install Java, and another buildpack to use Maven to build your application. The builder will run through all the buildpacks to identify the correct ones to use in the build.

You can specify buildpacks in one of the following formats:

Source| Format| Example| Notes  
---|---|---|---  
URL| `https://<host>/<path>`| `https://buildpack-registry.heroku.com/cnb/heroku/nodejs`| Needs to resolve to a tar.gz file  
Github URL| `https://<host>/<path>`| `https://github.com/heroku/heroku-buildpack-nodejs.git`| May further specify a tag, branch or commit ID using the format `https://<host>/<repo>#<tag/branch/commit-id>`  
Image| `[docker://][<host>]/<path>[:<tag>]`| `docker://docker.io/heroku/procfile-cnb:latest`| Can use `@digest` instead of `:<tag>`  
CNB registry resource| `urn:cnb:registry[:<id>[@<version>]]`| `urn:cnb:registry:heroku/nodejs`|   
  
If a string does not include a scheme prefix (ex. `docker://`) the buildpack type can be inferred from the format:

  * If it looks like a Docker ref, it will be treated as a `docker://` URI
  * If it looks like a buildpack Registry ID, it will be treated as a `urn:cnb:registry` URI



Layer caching

You can make buildpack builds more efficient and faster on subsequent builds by enabling caching. If enabled, the build engine will cache and reuse build dependencies from previous builds.

Learn more in the [buildpack documentation ](https://buildpacks.io/docs/buildpack-author-guide/create-buildpack/caching/).

Next steps

[Build from a Git repositoryStart building from your linked Git repositories in minutes.](/docs/v1/application/build/build-code-from-a-git-repository)[Inject build argumentsPass secrets and configuration settings to your builds.](/docs/v1/application/build/inject-build-arguments)[Run an image continuouslyDeploy a built image as a continuously-running service.](/docs/v1/application/run/run-an-image-continuously)[Run an image once or on a scheduleRun an image manually or on a cron schedule.](/docs/v1/application/run/run-an-image-once-or-on-a-schedule)