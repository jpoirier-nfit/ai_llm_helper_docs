---
source_url: https://northflank.com/docs/v1/api/services/patch-build-service
title: Patch build service | Services | Northflank API docs
crawl_date: 2025-07-29T09:24:10.993261
watsonmd_version: 0.1.0
---

Services / 

# Patch build service

Updates a build service.

Required permission

Project > Services > General > Update

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Request body

  * {object}

    * description

string

A description of the service.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

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

{object}

      * deploymentPlan

string

The ID of the deployment plan to use. (Deprecated - use buildPlan for build resources instead.).

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

      * buildPlan

string

The ID of the build plan to use.

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

string

          * gpuCount

integer

          * timesliced

boolean

    * disabledCI

boolean

Whether CI (continuous integration) should be disabled.

    * buildSource

string

Defines the build source for this resource

one of

git, bundle

    * vcsData

{object}

      * projectUrl

string

URL of the Git repo to build.

pattern

^(https:\/\/)?((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+(\/([a-zA-Z0-9\\-._]{2,}))+?$

      * projectType

string

The VCS provider to use.

one of

bitbucket, gitlab, github, self-hosted, azure

      * selfHostedVcsId

string

If projectType is self-hosted, the ID of the self-hosted vcs to use.

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

    * buildSettings

{object}

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

{object}

        * buildEngine

string

Build engine to use. Defaults to recommended build engine `buildkit`

one of

buildkit, kaniko

        * dockerFilePath

string

The file path of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

        * dockerWorkDir

string

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

      * buildpack

{object}

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

    * buildConfiguration

{object}

      * prRestrictions

[array]

An array of pull request build rules. Only supported for build services. Each commit belonging to a pull request on a branch that matches one of the provided build rules will be built automatically.

        * string

A pull request build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from pull requests from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

      * branchRestrictions

[array]

An array of branch build rules. Only supported for build services. Each commit belonging to a branch that matches one of the provided build rules will be built automatically.

        * string

A branch build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

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

    * buildArguments

{object}

An object containing the build arguments to set for the service

    * buildFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

    * dockerSecretMounts

{object}

Docker secret mount contents as JSON object, encrypted at rest. Must be a valid Docker secret mount identifier




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * name

string required

The name of the service.

min length

3

max length

54

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

      * description

string

A description of the service.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

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

        * deploymentPlan

string

The ID of the deployment plan to use. (Deprecated - use buildPlan for build resources instead.).

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

        * buildPlan

string

The ID of the build plan to use.

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

      * infrastructure

{object}

        * architecture

string

one of

x86, arm

      * disabledCI

boolean

Whether CI (continuous integration) should be disabled.

      * buildSource

string

Defines the build source for this resource

one of

git, bundle

      * vcsData

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

      * buildSettings

(multiple options: oneOf) required

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

      * buildConfiguration

{object}

        * prRestrictions

[array]

An array of pull request build rules. Only supported for build services. Each commit belonging to a pull request on a branch that matches one of the provided build rules will be built automatically.

          * string

A pull request build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from pull requests from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

        * branchRestrictions

[array]

An array of branch build rules. Only supported for build services. Each commit belonging to a branch that matches one of the provided build rules will be built automatically.

          * string

A branch build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

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

      * buildArguments

{object}

An object containing the build arguments to set for the service

      * buildFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

      * dockerSecretMounts

{object}

Docker secret mount contents as JSON object, encrypted at rest. Must be a valid Docker secret mount identifier

      * serviceType

string required

Type of the service (combined, build or deployment)

one of

build

      * id

string required

Identifier for the service

      * appId

string required

Full identifier used for service deployment

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

      * status

{object} required

Details about the current service status.

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




API

CLI

JS Client

PATCH /v1/projects/{projectId}/services/build/{serviceId}

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request PATCH \
      --data '{"description":"A service description","billing":{"deploymentPlan":"nf-compute-20","buildPlan":"nf-compute-200-8"},"buildSource":"git","vcsData":{"projectUrl":"https://github.com/northflank/gatsby-with-northflank","projectType":"github","accountLogin":"github-user"},"buildSettings":{"storage":{"ephemeralStorage":{"storageSize":16384}},"dockerfile":{"buildEngine":"buildkit","dockerFilePath":"/Dockerfile","dockerWorkDir":"/","buildkit":{"useCache":true,"cacheStorageSize":32768}},"buildpack":{"builder":"HEROKU_24","buildpackLocators":["https://buildpack-registry.heroku.com/cnb/mars/create-react-app"],"buildContext":"/","useCache":false}},"buildConfiguration":{"prRestrictions":["feature/*"],"branchRestrictions":["feature/*"],"pathIgnoreRules":["README.md"],"isAllowList":false,"ciIgnoreFlags":["[skip ci]"],"dockerCredentials":["example-docker-credential"],"storage":{"ephemeralStorage":{"storageSize":16384}}},"buildArguments":{"ARGUMENT_1":"abcdef","ARGUMENT_2":"12345"},"buildFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"dockerSecretMounts":{"example-secret-mount_1":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/build/{serviceId}

Example response

200 OK

Details about the updated service.

JSON
    
    
    {
      "data": {
        "name": "Example Service",
        "description": "A service description",
        "billing": {
          "deploymentPlan": "nf-compute-20",
          "buildPlan": "nf-compute-200-8"
        },
        "buildSource": "git",
        "vcsData": {
          "projectUrl": "https://github.com/northflank/gatsby-with-northflank",
          "projectType": "github",
          "accountLogin": "github-user"
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
        "buildConfiguration": {
          "prRestrictions": [
            "feature/*"
          ],
          "branchRestrictions": [
            "feature/*"
          ],
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
        "buildArguments": {
          "ARGUMENT_1": "abcdef",
          "ARGUMENT_2": "12345"
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
        "serviceType": "build",
        "id": "example-service",
        "appId": "/example-user/default-project/example-service",
        "cluster": {
          "id": "nf-europe-west",
          "name": "nf-europe-west",
          "namespace": "ns-8zy2mcjh9zn2",
          "loadBalancers": [
            "lb.659200800000000000000000.northflank.com"
          ]
        },
        "status": {
          "build": {
            "status": "SUCCESS",
            "lastTransitionTime": "2021-11-29T11:47:16.624Z"
          }
        }
      }
    }