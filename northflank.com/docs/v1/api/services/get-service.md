---
source_url: https://northflank.com/docs/v1/api/services/get-service
title: Get service | Services | Northflank API docs
crawl_date: 2025-07-29T10:44:52.215372
watsonmd_version: 0.1.0
---

Services / 

# Get service

Gets information about the given service.

Required permission

Project > Services > General > Read

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * id

string required

Identifier for the service

      * appId

string required

Full identifier used for service deployment

      * name

string required

Service name

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

A short description of the service

      * projectId

string required

ID of the project that the service belongs to

      * serviceType

string required

Type of the service (combined, build or deployment)

one of

combined, build, deployment

      * createdAt

string required

The time the service was created.

      * disabledCI

boolean required

Whether Continuous Integration is disabled

      * disabledCD

boolean required

Whether Continuous Deployment is disabled

      * billing

{object} required

        * deploymentPlan

string required

ID of the billing plan used by this service

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

        * deployment

{object}

Details about the current deployment status.

          * status

string required

The current status of the deployment.

one of

PENDING, IN_PROGRESS, COMPLETED, FAILED

          * reason

string required

The reason the current deployment was started.

one of

SCALING, DEPLOYING

          * lastTransitionTime

string

The timestamp of when the deployment reached this status.

      * servicePaused

boolean required

Is the service paused?

      * buildSource

string

Defines the build source for this resource

one of

git, bundle

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

      * bundleData

{object}

        * bundleUrl

string required

URL of the bundle to be built

        * projectBranch

string

Branch of the bundle being built

        * dockerWorkDir

string required

Working directory used by the dockerfile

        * dockerFilePath

string required

File path of the Dockerfile

      * deployment

{object}

        * region

string

Region where this service is deployed and/or built

        * instances

integer

Number of instances/replicas running

        * external

{object}

Data about a deployment from an external registry.

          * imagePath

string required

Path of the external image excluding the hostname

          * registryProvider

string required

Registry provider hosting the external image

one of

acr, ecr, gar, dockerhub, github, gitlab, custom, legacy

          * privateImage

boolean required

Does the image require authentication

        * internal

{object}

          * nfObjectId

string required

Database ID of deployed entity

          * nfObjectType

string required

Type of deployed entity

one of

service

          * repository

string required

URL of the repository being deployed

          * branch

string required

Branch of the repo being deployed

          * buildSHA

string required

Commit SHA to be deployed. `latest` means the latest commit is automatically being deployed.

          * deployedSHA

string

Currently deployed commit SHA. If buildSHA is set to `latest`, this will show the SHA of the latest commit.

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

        * strategy

{object}

Roll out strategy of the service

          * type

string

Configures the instance roll out strategy of your service. Currently only available via feature flag.

one of

recreate, rollout-steady, rollout-balanced, rollout-fast

        * zonalRedundancy

{object}

          * type

string

Defines scheduling behaviour across different zones within the same region.

one of

disabled, preferred, required

          * minZones

integer

Defines how many zones are required and will prevent containers from additional scheduling into existing zones. (Only relevant if type is set to "required")

min

1

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

        * imageUrl

string

URL at which the service's deployed image is located

      * loadBalancing

{object}

        * mode

string required

one of

leastConnection, consistentHash, roundRobin, consistentReplicaRouting

        * consistentHash

{object}

          * mode

string required

one of

ip, customHeader

          * header

string

        * consistentReplicaRouting

{object}

          * mode

string required

one of

path, header

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

      * autoscaling

{object}

Describes all autoscaling configurations

        * horizontal

{object}

Describes the horizontal autoscaling configuration

          * enabled

boolean required

Whether horizontal autoscaling should be enabled

          * minReplicas

number required

Minimum number of replicas which should be running at any time

min

1

          * maxReplicas

number required

Maximum number of replicas which can be running at any time

          * cpu

{object}

            * enabled

boolean required

Whether autoscaling should take into account cpu usage

            * thresholdPercentage

integer required

Threshold CPU usage percentage at which the workload will be scaled

min

10

max

100

          * memory

{object}

            * enabled

boolean required

Whether autoscaling should take into account memory usage

            * thresholdPercentage

integer required

Threshold memory usage percentage at which the workload will be scaled

min

10

max

100

          * rps

{object}

            * enabled

boolean required

Whether autoscaling should take into requests-per-second

            * thresholdValue

integer required

Threshold rps value on which the workload will be scaled

min

1

          * userMetrics

{object}

            * enabled

boolean required

Whether to enable handling for custom metrics in the autoscaling configuration

            * exposedMetricsPath

string required

Path on which the metrics will be exposed by the service..

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

            * exposedMetricsPort

integer required

Port on which the metrics will be exposed by the service.

            * metrics

[array] required

Array of custom metrics exposed by the service that will be used by the autoscaling configuration. At least one metric is required.

              * {object}

                * metricName

string required

Name of the custom metric

pattern

[a-zA-Z_:][a-zA-Z0-9_:]*$

                * metricType

string required

Type of metric exposed, this will affect how it'll be queried by the autoscaler component: Gauge will be used as is, Counter will be used with rate()

one of

gauge, counter

                * thresholdValue

number required

Threshold value on which the workload will be scaled. Represents the average value across all running pods.

      * ports

[array] required

An array of ports of the service.

        * {object}

          * id

string required

The id used to identify the port across requests.

pattern

^[a-z]-?[a-z0-9]+(-[a-z0-9]+)*$

          * name

string required

The name of the port used in the public url and UI.

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * internalPort

integer required

The port number.

          * protocol

string required

The protocol used by the port.

one of

HTTP, HTTP/2, TCP, UDP

          * public

boolean required

If true, the port is exposed publicly.

          * dns

string

DNS entry for this port.

          * domains

[array] required

An array of domains that redirect to this port.

            * {object}

              * name

string required

The custom domain redirecting to this port.

              * certificate

{object} required

Details about the TLS certificate generation for this domain.

                * inProgress

boolean

Is the certificate in the process of being generated?

                * expiryDate

string

The timestamp when the TLS certificate will expire.

                * refreshDate

string

The timestamp when a new TLS certificate will be generated.

          * security

{object}

Details about security settings for this port.

            * credentials

[array]

An array of credentials to access the service.

              * {object}

                * username

string required

The username to access the service

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

                * password

string required

The password to access the service with this username.

                * type

string required

The type of authentication used

one of

basic-auth

            * policies

[array]

An array of IP address policies.

              * {object}

                * addresses

[array] required

An array of IP addresses used for this rule

                  * string

An IP address used by this rule

                * action

string required

The action for this rule.

one of

ALLOW, DENY

            * sso

{object}

Configure SSO access control for this port.

              * organizationId

string

Organization ID of the work OS organization that should be validated.

              * directoryGroupIds

[array]

List of directory groupIds, one of which the user has to be a member of.

                * string

              * validateInternalTraffic

boolean

Enforce internal traffic through SSO authentication flow

              * setCookieOnRootDomain

boolean

Set SSO authentication cookie on root domain

              * allowInternalTrafficViaPublicDns

boolean

Allow internal traffic from same or shared projects via public DNS to skip SSO authentication flow

            * verificationMode

string

Mode used to verify multiple security features like ip policies and SSO authentication

one of

or, and

            * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

              * {object}

                * regexMode

boolean

                * name

(multiple options: oneOf)

                  * string

OR

                  * string

pattern

^[a-zA-Z0-9_\\-%$+]+$

                * value

string required

          * disableNfDomain

boolean

Disable routing on the default code.run domain for public HTTP ports with custom domains.

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

GET /v1/projects/{projectId}/services/{serviceId}

Example response

200 OK

Details about the service.

JSON
    
    
    {
      "data": {
        "id": "example-service",
        "appId": "/example-user/default-project/example-service",
        "name": "Example Service",
        "description": "This is the service description",
        "projectId": "default-project",
        "serviceType": "combined",
        "createdAt": "2021-01-20T11:19:53.175Z",
        "disabledCI": false,
        "disabledCD": false,
        "billing": {
          "deploymentPlan": "nf-compute-20"
        },
        "status": {
          "build": {
            "status": "SUCCESS",
            "lastTransitionTime": "2021-11-29T11:47:16.624Z"
          },
          "deployment": {
            "status": "COMPLETED",
            "reason": "DEPLOYING",
            "lastTransitionTime": "2021-11-29T11:47:16.624Z"
          }
        },
        "buildSource": "git",
        "vcsData": {
          "projectUrl": "https://github.com/northflank/gatsby-with-northflank",
          "projectType": "github",
          "selfHostedVcsId": "example-team/self-hosted-vcs",
          "projectBranch": "master",
          "publicRepo": false,
          "dockerWorkDir": "/",
          "dockerFilePath": "/Dockerfile"
        },
        "bundleData": {
          "bundleUrl": "https://example.com/archive.tar",
          "projectBranch": "main",
          "dockerWorkDir": "/",
          "dockerFilePath": "/Dockerfile"
        },
        "deployment": {
          "region": "europe-west",
          "instances": 1,
          "internal": {
            "nfObjectId": "example-service",
            "nfObjectType": "service",
            "repository": "https://github.com/northflank/gatsby-with-northflank",
            "branch": "master",
            "buildSHA": "latest",
            "deployedSHA": "262ed9817b3cad5142fbceabe0c9e371e390d616"
          },
          "docker": {
            "configType": "default"
          },
          "buildpack": {
            "configType": "default"
          },
          "storage": {
            "ephemeralStorage": {
              "storageSize": 1024
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
        "buildEngineConfiguration": {
          "buildEngine": "buildpack",
          "buildpack": {
            "builder": "HEROKU_24",
            "buildpackLocators": [
              "https://buildpack-registry.heroku.com/cnb/mars/create-react-app"
            ]
          }
        },
        "autoscaling": {
          "horizontal": {
            "userMetrics": {
              "exposedMetricsPath": "/metrics",
              "exposedMetricsPort": 8080
            }
          }
        },
        "ports": [
          {
            "id": "eonyui",
            "name": "p01",
            "internalPort": 8080,
            "protocol": "HTTP",
            "public": true,
            "dns": "p01--example-service--default-service--user-abc1.salvo.code.run",
            "domains": [
              {
                "name": "app.example.com",
                "certificate": {
                  "inProgress": false,
                  "expiryDate": "2022-04-26T09:25:02.000Z",
                  "refreshDate": "2022-03-27T09:25:02.000Z"
                }
              }
            ],
            "security": {
              "credentials": [
                {
                  "username": "admin",
                  "password": "password123",
                  "type": "basic-auth"
                }
              ],
              "policies": [
                {
                  "addresses": [
                    "127.0.0.1"
                  ],
                  "action": "DENY"
                }
              ],
              "sso": {
                "organizationId": "org_uniquestringidentifier",
                "directoryGroupIds": [
                  "directory_group_uniquestringidentifier"
                ]
              }
            },
            "disableNfDomain": false
          }
        ],
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