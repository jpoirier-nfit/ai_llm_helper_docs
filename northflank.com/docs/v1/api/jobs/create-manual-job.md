---
source_url: https://northflank.com/docs/v1/api/jobs/create-manual-job
title: Create manual job | Jobs | Northflank API docs
crawl_date: 2025-07-29T09:24:15.421052
watsonmd_version: 0.1.0
---

Jobs / 

# Create manual job

Creates a new manual job that only runs when initiated via the UI, CLI, API or JS client.

Required permission

Project > Jobs > General > Create

Path parameters

    * projectId

string required

ID of the project




Request body

  * {object}

    * name

string required

The name of the job.

min length

3

max length

52

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

    * description

string

A description of the job.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

    * infrastructure

{object}

      * architecture

string

one of

x86, arm

    * tags

[array]

An array of previously defined tags to help identify and group the resource.

      * string

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

    * billing

{object} required

      * buildPlan

string

The ID of the build plan to use.

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

      * deploymentPlan

string required

The ID of the deployment plan to use.

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

      * gpu

{object}

        * enabled

boolean

        * configuration

{object}

          * gpuType

string required

          * gpuCount

integer

          * timesliced

boolean

    * backoffLimit

integer required

The number of attempts to rerun a job before it is marked as failed.

    * runOnSourceChange

string

Configure when the job should be run if the source image changes.

one of

never, cd-promote, always

    * activeDeadlineSeconds

integer

The maximum amount of time, in seconds, for a job to run before it is marked as failed.

min

1

    * deployment

(multiple options: oneOf)

Where to deploy the job from.

      * {object}

Deploy from version control

        * buildpack

{object}

Allows for customization of buildpack runtime

          * configType

string required

Type of buildpack run configuration

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run. Required in case where `configType` is `customProcess`

          * customEntrypoint

string

Custom entrypoint which should be run. Required in case where `configType` is `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be run. Required in case where `configType` is `customCommand`, `customEntrypointCustomCommand` or `originalEntrypointCustomCommand`

        * docker

{object}

Allows for customization of docker runtime

          * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per container in MB

min

1024

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

        * gpu

{object}

          * enabled

boolean

          * configuration

{object}

            * gpuType

string required

            * gpuCount

integer

            * timesliced

boolean

        * gracePeriodSeconds

integer

The maximum amount of time the process has to shut down after receiving a SIGTERM signal before it is forcefully shut down SIGKILL by the system.

min

15

max

600

        * metadata

{object}

Allow setting custom labels and annotations for workloads.

          * labels

{object}

Specify custom labels for the workload.

          * annotations

{object}

Specify custom annotations for the workload as string or object.

        * vcs

{object} required

          * projectUrl

string required

URL of the Git repo to build.

pattern

^(https:\/\/)?((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+(\/([a-zA-Z0-9\\-._]{2,}))+?$

          * projectType

string required

The VCS provider to use.

one of

bitbucket, gitlab, github, self-hosted, azure

          * selfHostedVcsId

string

If projectType is self-hosted, the ID of the self-hosted vcs to use.

pattern

^([A-Za-z0-9-]+\/[A-Za-z0-9-]+)|([0-9a-f]{24})$

          * accountLogin

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `accountLogin` is provided, Northflank will instead use your linked account with that login name.

          * vcsLinkId

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `vcsLinkId` is provided, Northflank will instead use your linked account with that ID.

min length

24

max length

24

          * projectBranch

string required

The name of the branch to use.

OR

      * {object}

Deploy from an external image

        * buildpack

{object}

Allows for customization of buildpack runtime

          * configType

string required

Type of buildpack run configuration

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run. Required in case where `configType` is `customProcess`

          * customEntrypoint

string

Custom entrypoint which should be run. Required in case where `configType` is `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be run. Required in case where `configType` is `customCommand`, `customEntrypointCustomCommand` or `originalEntrypointCustomCommand`

        * docker

{object}

Allows for customization of docker runtime

          * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per container in MB

min

1024

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

        * gpu

{object}

          * enabled

boolean

          * configuration

{object}

            * gpuType

string required

            * gpuCount

integer

            * timesliced

boolean

        * gracePeriodSeconds

integer

The maximum amount of time the process has to shut down after receiving a SIGTERM signal before it is forcefully shut down SIGKILL by the system.

min

15

max

600

        * metadata

{object}

Allow setting custom labels and annotations for workloads.

          * labels

{object}

Specify custom labels for the workload.

          * annotations

{object}

Specify custom annotations for the workload as string or object.

        * external

{object} required

          * imagePath

string required

Image to be deployed. When not deploying from Dockerhub the URL must be specified.

pattern

^(?:(?:https?:\/\/)?([a-zA-Z0-9\\-]+\\.[a-zA-Z0-9\\.\\-]+)(\/v1)?)?(?:\/)?([a-zA-Z/-9\\.\\-_]+)(?:\:([a-zA-Z/-9\\.\\-_\:]+)|\@([a-zA-Z/-9\\.\\-_\:]+))$

          * credentials

string

ID of the saved credentials to use to access this external image.

pattern

^[A-Za-z0-9-]+$

OR

      * {object}

Deploy from a Northflank build service

        * buildpack

{object}

Allows for customization of buildpack runtime

          * configType

string required

Type of buildpack run configuration

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run. Required in case where `configType` is `customProcess`

          * customEntrypoint

string

Custom entrypoint which should be run. Required in case where `configType` is `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be run. Required in case where `configType` is `customCommand`, `customEntrypointCustomCommand` or `originalEntrypointCustomCommand`

        * docker

{object}

Allows for customization of docker runtime

          * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per container in MB

min

1024

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

        * gpu

{object}

          * enabled

boolean

          * configuration

{object}

            * gpuType

string required

            * gpuCount

integer

            * timesliced

boolean

        * gracePeriodSeconds

integer

The maximum amount of time the process has to shut down after receiving a SIGTERM signal before it is forcefully shut down SIGKILL by the system.

min

15

max

600

        * metadata

{object}

Allow setting custom labels and annotations for workloads.

          * labels

{object}

Specify custom labels for the workload.

          * annotations

{object}

Specify custom annotations for the workload as string or object.

        * internal

{object} required

          * id

string

ID of the build service to deploy

min length

3

max length

54

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * branch

string

Branch to deploy

          * buildSHA

(multiple options: oneOf)

Commit SHA to deploy, or 'latest' to deploy the most recent commit

            * string

A commit sha.

min length

40

max length

40

OR

            * string

Latest commit.

one of

latest

          * buildId

string

ID of the build that should be deployed

OR

      * {object}

Choose later

    * disabledCI

boolean

Whether CI should be disabled. Only relevant for jobs deploying directly from version control.

    * buildConfiguration

{object}

      * pathIgnoreRules

[array]

An array of path ignore rules. A commit will only be built if a file has been changed that does not match any of the ignore rules. Path ignore rules follow `.gitignore` syntax.

        * string

A path ignore rule, following `.gitignore` syntax. For example, `*.md` will ignore all files ending with `.md`.

max length

260

      * isAllowList

boolean

If `true`, the functionality of `pathIgnoreRules` will be inverted. A commit will only be built if a file has been changed that matches one or more of the rules in `pathIgnoreRules`.

      * ciIgnoreFlagsEnabled

boolean

If `true`, enables commit ignore flags. If a commit message contains one or more of the flags in `ciIgnoreFlags`, that commit will not be built.

      * ciIgnoreFlags

[array]

An array of commit ignore flags. If a commit message contains one or more of these flags, that commit will not be built. Defaults to `["[skip ci]", "[ci skip]", "[no ci]", "[skip nf]", "[nf skip]", "[northflank skip]", "[skip northflank]"]`

        * string

A commit ignore flag.

max length

72

      * dockerfileTarget

string

If your Dockerfile contains multiple build stages, you can specify the target stage by entering its name here.

      * dockerCredentials

[array]

        * string

The ID of the docker credentials to use.

pattern

^[A-Za-z0-9-]+$

      * includeGitFolder

boolean

Include .git folder inside the build context

      * fullGitClone

boolean

Include the entire git history as part of the .git folder. Only relevant if "includeGitFolder" is set.

      * storage

{object}

        * ephemeralStorage

{object}

          * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536

    * buildSettings

(multiple options: oneOf)

Build engine

      * {object}

Build from a Dockerfile

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536

        * dockerfile

{object} required

          * useCache

boolean

DEPRECATED: This field will be removed in the near future and currently has no effect.

          * buildEngine

string

Build engine to use. Defaults to recommended build engine `buildkit`

one of

buildkit, kaniko

          * dockerFilePath

string required

The file path of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

          * dockerWorkDir

string required

The working directory of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]*$

          * buildkit

{object}

            * useCache

boolean

Use persistent storage to cache build layers.

            * cacheStorageSize

integer

The amount of persistent storage available to each build in MB.

            * useInternalCache

boolean

DEPRECATED: This field will be removed in the near future.

            * internalCacheStorage

number

DEPRECATED: This field will be removed in the near future.

OR

      * {object}

Build from a Buildpack

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536

        * buildpack

{object} required

          * builder

string

Buildpack stack to use. Defaults to recommended stack `HEROKU_24`.

one of

HEROKU_24, HEROKU_22, HEROKU_22_CLASSIC, HEROKU_20, HEROKU_18, GOOGLE_22, GOOGLE_V1, CNB_ALPINE, CNB_BIONIC, PAKETO_JAMMY_TINY, PAKETO_JAMMY_BASE, PAKETO_JAMMY_FULL, PAKETO_TINY, PAKETO_BASE, PAKETO_FULL

          * buildpackLocators

[array]

Array of custom Buildpacks to use.

            * string

Url or registry identifier of custom Buildpack.

          * buildContext

string

The working directory to build in.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]*$

          * useCache

boolean

Should build dependencies be cached?

    * runtimeEnvironment

{object}

An object containing the runtime environment to set for the job. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

    * runtimeFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

    * buildArguments

{object}

An object containing the build arguments to set for the job. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

    * buildFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

    * dockerSecretMounts

{object}

Docker secret mount contents as JSON object, encrypted at rest. Must be a valid Docker secret mount identifier

    * healthChecks

[array]

An array of health checks.

      * {object}

A health check object.

        * protocol

string required

The protocol to access the health check with.

one of

HTTP, CMD, TCP

        * type

string required

The type of health check.

one of

livenessProbe, readinessProbe, startupProbe

        * path

string

The path of the health check endpoint. Required when protocol is HTTP.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

        * cmd

string

The command to run for the health check. Required when protocol is CMD

        * port

integer

Port number for the health check endpoint. Required when protocol is HTTP.

min

1

        * initialDelaySeconds

integer required

Initial delay, in seconds, before the health check is first run.

min

1

max

180

        * periodSeconds

integer required

The time between each check, in seconds.

min

10

max

600

        * timeoutSeconds

integer required

The time to wait for a response before marking the health check as a failure.

min

1

max

60

        * failureThreshold

integer required

The maximum number of allowed failures.

min

1

max

255

        * successThreshold

integer

The number of successes required to mark the health check as a success.

min

1

max

255




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * name

string required

The name of the job.

min length

3

max length

52

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

      * description

string

A description of the job.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

      * infrastructure

{object}

        * architecture

string

one of

x86, arm

      * tags

[array]

An array of previously defined tags to help identify and group the resource.

        * string

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

      * billing

{object} required

        * buildPlan

string

The ID of the build plan to use.

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

        * deploymentPlan

string required

The ID of the deployment plan to use.

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

        * gpu

{object}

          * enabled

boolean

          * configuration

{object}

            * gpuType

string required

            * gpuCount

integer

            * timesliced

boolean

      * backoffLimit

integer required

The number of attempts to rerun a job before it is marked as failed.

      * runOnSourceChange

string

Configure when the job should be run if the source image changes.

one of

never, cd-promote, always

      * activeDeadlineSeconds

integer

The maximum amount of time, in seconds, for a job to run before it is marked as failed.

min

1

      * disabledCI

boolean

Whether CI should be disabled. Only relevant for jobs deploying directly from version control.

      * buildConfiguration

{object}

        * pathIgnoreRules

[array]

An array of path ignore rules. A commit will only be built if a file has been changed that does not match any of the ignore rules. Path ignore rules follow `.gitignore` syntax.

          * string

A path ignore rule, following `.gitignore` syntax. For example, `*.md` will ignore all files ending with `.md`.

max length

260

        * isAllowList

boolean

If `true`, the functionality of `pathIgnoreRules` will be inverted. A commit will only be built if a file has been changed that matches one or more of the rules in `pathIgnoreRules`.

        * ciIgnoreFlagsEnabled

boolean

If `true`, enables commit ignore flags. If a commit message contains one or more of the flags in `ciIgnoreFlags`, that commit will not be built.

        * ciIgnoreFlags

[array]

An array of commit ignore flags. If a commit message contains one or more of these flags, that commit will not be built. Defaults to `["[skip ci]", "[ci skip]", "[no ci]", "[skip nf]", "[nf skip]", "[northflank skip]", "[skip northflank]"]`

          * string

A commit ignore flag.

max length

72

        * dockerfileTarget

string

If your Dockerfile contains multiple build stages, you can specify the target stage by entering its name here.

        * dockerCredentials

[array]

          * string

The ID of the docker credentials to use.

pattern

^[A-Za-z0-9-]+$

        * includeGitFolder

boolean

Include .git folder inside the build context

        * fullGitClone

boolean

Include the entire git history as part of the .git folder. Only relevant if "includeGitFolder" is set.

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536

      * runtimeEnvironment

{object}

An object containing the runtime environment to set for the job. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

      * runtimeFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

      * buildArguments

{object}

An object containing the build arguments to set for the job. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

      * buildFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

      * dockerSecretMounts

{object}

Docker secret mount contents as JSON object, encrypted at rest. Must be a valid Docker secret mount identifier

      * healthChecks

[array]

An array of health checks.

        * {object}

A health check object.

          * protocol

string required

The protocol to access the health check with.

one of

HTTP, CMD, TCP

          * type

string required

The type of health check.

one of

livenessProbe, readinessProbe, startupProbe

          * path

string

The path of the health check endpoint. Required when protocol is HTTP.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

          * cmd

string

The command to run for the health check. Required when protocol is CMD

          * port

integer

Port number for the health check endpoint. Required when protocol is HTTP.

min

1

          * initialDelaySeconds

integer required

Initial delay, in seconds, before the health check is first run.

min

1

max

180

          * periodSeconds

integer required

The time between each check, in seconds.

min

10

max

600

          * timeoutSeconds

integer required

The time to wait for a response before marking the health check as a failure.

min

1

max

60

          * failureThreshold

integer required

The maximum number of allowed failures.

min

1

max

255

          * successThreshold

integer

The number of successes required to mark the health check as a success.

min

1

max

255

      * jobType

string required

Type of the job (manual or manual)

one of

manual

      * id

string required

Identifier for the job

      * appId

string required

Full identifier used for job deployment

      * deployment

{object}

        * buildpack

{object}

Allows for customization of buildpack runtime

          * configType

string required

Type of buildpack run configuration

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run. Required in case where `configType` is `customProcess`

          * customEntrypoint

string

Custom entrypoint which should be run. Required in case where `configType` is `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be run. Required in case where `configType` is `customCommand`, `customEntrypointCustomCommand` or `originalEntrypointCustomCommand`

        * docker

{object}

Allows for customization of docker runtime

          * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

          * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`

        * storage

{object}

          * ephemeralStorage

{object}

            * storageSize

integer

Ephemeral storage per container in MB

min

1024

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

        * gpu

{object}

          * enabled

boolean

          * configuration

{object}

            * gpuType

string required

            * gpuCount

integer

            * timesliced

boolean

        * gracePeriodSeconds

integer

The maximum amount of time the process has to shut down after receiving a SIGTERM signal before it is forcefully shut down SIGKILL by the system.

min

15

max

600

        * metadata

{object}

Allow setting custom labels and annotations for workloads.

          * labels

{object}

Specify custom labels for the workload.

          * annotations

{object}

Specify custom annotations for the workload as string or object.

        * vcs

{object}

          * projectUrl

string required

URL of the Git repo to build.

pattern

^(https:\/\/)?((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+(\/([a-zA-Z0-9\\-._]{2,}))+?$

          * projectType

string required

The VCS provider to use.

one of

bitbucket, gitlab, github, self-hosted, azure

          * selfHostedVcsId

string

If projectType is self-hosted, the ID of the self-hosted vcs to use.

pattern

^([A-Za-z0-9-]+\/[A-Za-z0-9-]+)|([0-9a-f]{24})$

          * accountLogin

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `accountLogin` is provided, Northflank will instead use your linked account with that login name.

          * vcsLinkId

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `vcsLinkId` is provided, Northflank will instead use your linked account with that ID.

min length

24

max length

24

          * projectBranch

string required

The name of the branch to use.

        * external

{object}

          * imagePath

string required

Image to be deployed. When not deploying from Dockerhub the URL must be specified.

pattern

^(?:(?:https?:\/\/)?([a-zA-Z0-9\\-]+\\.[a-zA-Z0-9\\.\\-]+)(\/v1)?)?(?:\/)?([a-zA-Z/-9\\.\\-_]+)(?:\:([a-zA-Z/-9\\.\\-_\:]+)|\@([a-zA-Z/-9\\.\\-_\:]+))$

          * credentials

string

ID of the saved credentials to use to access this external image.

pattern

^[A-Za-z0-9-]+$

        * internal

{object}

          * id

string required

ID of the build service to deploy

min length

3

max length

54

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * branch

string

Branch to deploy

          * buildSHA

(multiple options: oneOf)

Commit SHA to deploy, or 'latest' to deploy the most recent commit

            * string

A commit sha.

min length

40

max length

40

OR

            * string

Latest commit.

one of

latest

          * buildId

string

ID of the build that should be deployed

        * imageUrl

string

Image registry url of the deployed image.

      * buildSettings

(multiple options: oneOf)

Build engine

        * {object}

Build from a Dockerfile

          * storage

{object}

            * ephemeralStorage

{object}

              * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536

          * dockerfile

{object} required

            * useCache

boolean

DEPRECATED: This field will be removed in the near future and currently has no effect.

            * buildEngine

string

Build engine to use. Defaults to recommended build engine `buildkit`

one of

buildkit, kaniko

            * dockerFilePath

string required

The file path of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

            * dockerWorkDir

string required

The working directory of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]*$

            * buildkit

{object}

              * useCache

boolean

Use persistent storage to cache build layers.

              * cacheStorageSize

integer

The amount of persistent storage available to each build in MB.

              * useInternalCache

boolean

DEPRECATED: This field will be removed in the near future.

              * internalCacheStorage

number

DEPRECATED: This field will be removed in the near future.

OR

        * {object}

Build from a Buildpack

          * storage

{object}

            * ephemeralStorage

{object}

              * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536

          * buildpack

{object} required

            * builder

string

Buildpack stack to use. Defaults to recommended stack `HEROKU_24`.

one of

HEROKU_24, HEROKU_22, HEROKU_22_CLASSIC, HEROKU_20, HEROKU_18, GOOGLE_22, GOOGLE_V1, CNB_ALPINE, CNB_BIONIC, PAKETO_JAMMY_TINY, PAKETO_JAMMY_BASE, PAKETO_JAMMY_FULL, PAKETO_TINY, PAKETO_BASE, PAKETO_FULL

            * buildpackLocators

[array]

Array of custom Buildpacks to use.

              * string

Url or registry identifier of custom Buildpack.

            * buildContext

string

The working directory to build in.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]*$

            * useCache

boolean

Should build dependencies be cached?

      * status

{object} required

Details about the current job status.

        * build

{object}

Details about the status of the most recent build.

          * status

string required

The current status of the build.

one of

QUEUED, PENDING, UNSCHEDULABLE, STARTING, CLONING, BUILDING, UPLOADING, ABORTED, FAILURE, SUBMISSION_FAILURE, SUCCESS, CRASHED, IN_PROGRESS

          * lastTransitionTime

string

The timestamp of when the build reached this status.

      * cluster

{object} required

Cluster information

        * id

string required

The id of the cluster associated with this project.

        * name

string required

The name of the cluster associated with this project.

        * namespace

string

Namespace this resource is located within on the cluster.

        * loadBalancers

[array]

Load balancer DNS for the cluster.

          * string

      * createdAt

string

time of creation

      * updatedAt

string

time of update




API

CLI

JS Client

POST /v1/projects/{projectId}/jobs/manual

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"name":"Example Job","description":"A job description","billing":{"buildPlan":"nf-compute-200-8","deploymentPlan":"nf-compute-20"},"backoffLimit":0,"runOnSourceChange":"never","activeDeadlineSeconds":600,"deployment":{"docker":{"configType":"default"},"storage":{"ephemeralStorage":{"storageSize":1024}},"vcs":{"projectUrl":"https://github.com/northflank/gatsby-with-northflank","projectType":"github","accountLogin":"github-user","projectBranch":"master"}},"buildConfiguration":{"pathIgnoreRules":["README.md"],"isAllowList":false,"ciIgnoreFlags":["[skip ci]"],"dockerCredentials":["example-docker-credential"],"storage":{"ephemeralStorage":{"storageSize":16384}}},"buildSettings":{"storage":{"ephemeralStorage":{"storageSize":16384}},"dockerfile":{"buildEngine":"buildkit","dockerFilePath":"/Dockerfile","dockerWorkDir":"/","buildkit":{"useCache":true,"cacheStorageSize":32768}}},"runtimeEnvironment":{"variable1":"abcdef","variable2":"12345"},"runtimeFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"buildArguments":{"variable1":"abcdef","variable2":"12345"},"buildFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"dockerSecretMounts":{"example-secret-mount_1":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"healthChecks":[{"protocol":"HTTP","type":"readinessProbe","path":"/health-check","port":8080,"initialDelaySeconds":10,"periodSeconds":60,"timeoutSeconds":1,"failureThreshold":3,"successThreshold":1}]}' \
      https://api.northflank.com/v1/projects/{projectId}/jobs/manual

Example response

200 OK

Details about the newly created job.

JSON
    
    
    {
      "data": {
        "name": "Example Job",
        "description": "A job description",
        "billing": {
          "buildPlan": "nf-compute-200-8",
          "deploymentPlan": "nf-compute-20"
        },
        "backoffLimit": 0,
        "runOnSourceChange": "never",
        "activeDeadlineSeconds": 600,
        "buildConfiguration": {
          "pathIgnoreRules": [
            "README.md"
          ],
          "isAllowList": false,
          "ciIgnoreFlags": [
            "[skip ci]"
          ],
          "dockerCredentials": [
            "example-docker-credential"
          ],
          "storage": {
            "ephemeralStorage": {
              "storageSize": 16384
            }
          }
        },
        "runtimeEnvironment": {
          "variable1": "abcdef",
          "variable2": "12345"
        },
        "runtimeFiles": {
          "/dir/fileName": {
            "data": "VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=",
            "encoding": "utf-8"
          }
        },
        "buildArguments": {
          "variable1": "abcdef",
          "variable2": "12345"
        },
        "buildFiles": {
          "/dir/fileName": {
            "data": "VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=",
            "encoding": "utf-8"
          }
        },
        "dockerSecretMounts": {
          "example-secret-mount_1": {
            "data": "VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=",
            "encoding": "utf-8"
          }
        },
        "healthChecks": [
          {
            "protocol": "HTTP",
            "type": "readinessProbe",
            "path": "/health-check",
            "port": 8080,
            "initialDelaySeconds": 10,
            "periodSeconds": 60,
            "timeoutSeconds": 1,
            "failureThreshold": 3,
            "successThreshold": 1
          }
        ],
        "jobType": "manual",
        "id": "example-job",
        "appId": "/example-user/default-project/example-job",
        "deployment": {
          "docker": {
            "configType": "default"
          },
          "storage": {
            "ephemeralStorage": {
              "storageSize": 1024
            }
          },
          "vcs": {
            "projectUrl": "https://github.com/northflank/gatsby-with-northflank",
            "projectType": "github",
            "accountLogin": "github-user",
            "projectBranch": "master"
          },
          "external": {
            "imagePath": "nginx:latest",
            "credentials": "example-credentials"
          },
          "internal": {
            "id": "example-build-service",
            "branch": "master",
            "buildId": "premium-guide-6393"
          }
        },
        "buildSettings": {
          "storage": {
            "ephemeralStorage": {
              "storageSize": 16384
            }
          },
          "dockerfile": {
            "buildEngine": "buildkit",
            "dockerFilePath": "/Dockerfile",
            "dockerWorkDir": "/",
            "buildkit": {
              "useCache": true,
              "cacheStorageSize": 32768
            }
          }
        },
        "status": {
          "build": {
            "status": "SUCCESS",
            "lastTransitionTime": "2021-11-29T11:47:16.624Z"
          }
        },
        "cluster": {
          "id": "nf-europe-west",
          "name": "nf-europe-west",
          "namespace": "ns-8zy2mcjh9zn2",
          "loadBalancers": [
            "lb.659200800000000000000000.northflank.com"
          ]
        }
      }
    }