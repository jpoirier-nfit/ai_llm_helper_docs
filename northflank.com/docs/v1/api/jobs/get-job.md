---
source_url: https://northflank.com/docs/v1/api/jobs/get-job
title: Get job | Jobs | Northflank API docs
crawl_date: 2025-07-29T10:04:45.790517
watsonmd_version: 0.1.0
---

Jobs / 

# Get job

Gets information about the given job

Required permission

Project > Jobs > General > Read

Path parameters

    * projectId

string required

ID of the project

    * jobId

string required

ID of the job




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * id

string required

Identifier for the job

      * appId

string required

Full identifier used for job deployment

      * name

string required

Job name

      * tags

[array] required

An array of previously defined tags to help identify and group the resource.

        * string

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

      * description

string

A short description of the job

      * projectId

string required

ID of the project that the job belongs to

      * jobType

string required

Type of the job (manual or cron)

one of

manual, cron

      * createdAt

string required

The time the job was created.

      * vcsData

{object}

        * projectUrl

string required

URL of the repository being built

        * projectType

string required

VCS provider for the repo being built

one of

bitbucket, gitlab, github, self-hosted, azure

        * selfHostedVcsId

string

ID of the self-hosted VCS, if applicable.

        * projectBranch

string

Branch of the repo being built

        * publicRepo

boolean

Whether the repo is being accessed without authentication.

        * dockerWorkDir

string required

Working directory used by the dockerfile

        * dockerFilePath

string required

File path of the Dockerfile

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

      * buildEngineConfiguration

{object}

        * buildEngine

string

The build engine used.

one of

buildpack, buildkit, kaniko

        * buildpack

{object}

Details about Buildpack settings.

          * builder

string

The Buildpack stack used.

one of

HEROKU_24, HEROKU_22, HEROKU_22_CLASSIC, HEROKU_20, HEROKU_18, GOOGLE_22, GOOGLE_V1, CNB_ALPINE, CNB_BIONIC, PAKETO_JAMMY_TINY, PAKETO_JAMMY_BASE, PAKETO_JAMMY_FULL, PAKETO_TINY, PAKETO_BASE, PAKETO_FULL

          * buildpackLocators

[array]

Array of custom Buildpacks used.

            * string

Url or registry identifier of custom Buildpack.

          * useCache

boolean

Should build dependencies be cached?

        * buildkit

{object}

Details about Buildkit settings.

          * useCache

boolean

Should intermediate image layers be cached?

          * useInternalCache

boolean

Should use persistent storage to store all layers?

          * internalCacheStorage

boolean

Storage size to use for internal cache

        * kaniko

{object}

Details about Kaniko settings.

          * useCache

boolean

Should intermediate image layers be cached?

      * disabledCI

boolean required

Whether Continuous Integration is disabled

      * disabledCD

boolean required

Whether Continuous Deployment is disabled

      * deployment

{object}

        * region

string

Region where this job is deployed and built

        * buildpack

{object}

Details about the Buildpack overrides for this deployment.

          * configType

string required

Type of buildpack run configuration.

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run.

          * customEntrypoint

string

Custom entrypoint which should be run.

          * customCommand

string

Custom command which should be run.

        * docker

{object}

Details about the Docker overrides for this deployment.

          * configType

string required

Override configuration which is used at runtime.

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

The CMD to run instead of the default if entrypoint override is enabled.

          * customCommand

string

The CMD to run instead of the default if CMD override is enabled.

        * storage

{object}

Details about storage settings for this deployment.

          * ephemeralStorage

{object}

Details about ephemeral storage settings for this deployment.

            * storageSize

number required

Ephemeral storage per container in MB

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

      * billing

{object} required

        * deploymentPlan

string required

ID of the billing plan used by this job

      * suspended

boolean

Cron specific. Whether or not the job's automatic scheduling is suspended

      * settings

{object} required

Job settings

        * cron

{object}

Cron job specific settings

          * schedule

string

The cron timer scheduling when to run the job.

          * concurrencyPolicy

string

Whether this job should run when another instance of the job is already running.

one of

Allow, Forbid, Replace

        * backoffLimit

integer required

The number of attempts to rerun a job before it is marked as failed.

        * activeDeadlineSeconds

integer required

The maximum amount of time, in seconds, for a job to run before it is marked as failed.

min

1

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




API

CLI

JS Client

GET /v1/projects/{projectId}/jobs/{jobId}

Example response

200 OK

Details about the job.

JSON
    
    
    {
      "data": {
        "id": "example-job",
        "appId": "/example-user/default-project/example-job",
        "name": "Example Job",
        "description": "This is the job description",
        "projectId": "default-project",
        "jobType": "cron",
        "createdAt": "2021-01-20T11:19:53.175Z",
        "vcsData": {
          "projectUrl": "https://github.com/northflank/gatsby-with-northflank",
          "projectType": "github",
          "selfHostedVcsId": "example-team/self-hosted-vcs",
          "projectBranch": "master",
          "publicRepo": false,
          "dockerWorkDir": "/",
          "dockerFilePath": "/Dockerfile"
        },
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
        "buildEngineConfiguration": {
          "buildEngine": "buildpack",
          "buildpack": {
            "builder": "HEROKU_24",
            "buildpackLocators": [
              "https://buildpack-registry.heroku.com/cnb/mars/create-react-app"
            ]
          }
        },
        "disabledCI": false,
        "disabledCD": false,
        "deployment": {
          "region": "europe-west",
          "buildpack": {
            "configType": "default"
          },
          "docker": {
            "configType": "default"
          },
          "storage": {
            "ephemeralStorage": {
              "storageSize": 1024
            }
          }
        },
        "billing": {
          "deploymentPlan": "nf-compute-20"
        },
        "suspended": false,
        "settings": {
          "cron": {
            "schedule": "30 8 * * *",
            "concurrencyPolicy": "Allow"
          },
          "backoffLimit": 0,
          "activeDeadlineSeconds": 600
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