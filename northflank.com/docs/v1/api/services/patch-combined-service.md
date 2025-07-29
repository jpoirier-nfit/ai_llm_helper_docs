---
source_url: https://northflank.com/docs/v1/api/services/patch-combined-service
title: Patch combined service | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:22.119059
watsonmd_version: 0.1.0
---

Services / 

# Patch combined service

Updates a combined service.

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

The ID of the deployment plan to use.

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

    * deployment

{object}

      * instances

integer

The number of instances to run the service on.

      * buildpack

{object}

        * configType

string

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

        * configType

string

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

string

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

    * ports

[array]

      * {object}

        * name

string required

The name used to identify the port.

min length

1

max length

8

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * internalPort

integer required

The port number.

min

1

max

65535

        * public

boolean

If true, the port will be exposed publicly.

        * security

{object}

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

          * ip

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

Configure port authentication via SSO

            * organizationId

string

ID of the SSO organization that the user will have to be a member of

            * directoryGroupIds

[array]

Array of directory groups that will have access

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

          * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

            * (multiple options: anyOf)

              * {object}

Matches provided headers as strings.

                * regexMode

boolean

                * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                * value

string required

OR

              * {object}

Matches provided headers as regex.

                * regexMode

boolean

                * name

string required

                * value

string required

          * verificationMode

string

Mode used to verify multiple security features like ip policies and SSO authentication

one of

or, and

          * securePathConfiguration

{object}

            * enabled

boolean

Enable security policies on a path-level style

            * skipSecurityPoliciesForInternalTrafficViaPublicDns

boolean

Allow internal traffic from same or shared projects via public DNS to skip all security policies

            * rules

[array]

              * {object}

                * paths

[array] required

Array of path objects which represent the paths and their priority for which the security policies will be enforced

                  * (multiple options: oneOf)

Data about how the path should be handled.

                    * {object}

Route when the path starts with the provided prefix.

                      * path

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

                      * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

prefix

                      * priority

integer required

min

0

max

100

OR

                    * {object}

Route when the path is an exact match.

                      * path

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

                      * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

exact

                      * priority

integer required

min

0

max

100

OR

                    * {object}

Route when the path matches the provided regex.

                      * path

string required

                      * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

regex

                      * priority

integer required

min

0

max

100

                * accessMode

string required

Specify the way the path rule will behave when processing policies. This enables an allow-list/deny-list approach for access control on each path

one of

protected, unprotected

                * securityPolicies

{object}

                  * orPolicies

{object}

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

                    * ip

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

Configure port authentication via SSO

                      * organizationId

string

ID of the SSO organization that the user will have to be a member of

                      * directoryGroupIds

[array]

Array of directory groups that will have access

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

                    * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

                      * (multiple options: anyOf)

                        * {object}

Matches provided headers as strings.

                          * regexMode

boolean

                          * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                          * value

string required

OR

                        * {object}

Matches provided headers as regex.

                          * regexMode

boolean

                          * name

string required

                          * value

string required

                  * requiredPolicies

{object}

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

                    * ip

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

Configure port authentication via SSO

                      * organizationId

string

ID of the SSO organization that the user will have to be a member of

                      * directoryGroupIds

[array]

Array of directory groups that will have access

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

                    * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

                      * (multiple options: anyOf)

                        * {object}

Matches provided headers as strings.

                          * regexMode

boolean

                          * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                          * value

string required

OR

                        * {object}

Matches provided headers as regex.

                          * regexMode

boolean

                          * name

string required

                          * value

string required

        * domains

[array]

An array of domains to redirect to this port. Each domain must first be verified and registered to your account.

          * string

A domain to redirect to this port.

        * disableNfDomain

boolean

Disable routing on the default code.run domain for public HTTP ports with custom domains.

        * advancedOptions

{object}

          * enableTlsPassthrough

boolean

Whether this port should use pass through mode for TLS

        * protocol

string required

The protocol to use for the port.

one of

HTTP, HTTP/2, TCP, UDP

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

      * projectBranch

string

The name of the branch to use.

    * bundleData

{object}

      * bundleUrl

string

URL of the bundle to be built

      * branch

string

Branch identifier for the bundle.

pattern

^[A-Za-z0-9-]+$

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

An object containing the runtime environment to set for the service. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

    * runtimeFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

    * buildArguments

{object}

An object containing the build arguments to set for the service. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

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

    * loadBalancing

{object}

      * mode

string

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

    * autoscaling

{object}

      * horizontal

{object}

        * enabled

boolean

Whether horizontal autoscaling should be enabled

        * minReplicas

number

Minimum number of replicas which should be running at any time

min

1

        * maxReplicas

number

Maximum number of replicas which can be running at any time

        * cpu

{object}

          * enabled

boolean

Whether autoscaling should take into account cpu usage

          * thresholdPercentage

integer

Threshold CPU usage percentage at which the workload will be scaled

min

10

max

100

        * memory

{object}

          * enabled

boolean

Whether autoscaling should take into account memory usage

          * thresholdPercentage

integer

Threshold memory usage percentage at which the workload will be scaled

min

10

max

100

        * rps

{object}

          * enabled

boolean

Whether autoscaling should take into requests-per-second

          * thresholdValue

integer

Threshold rps value on which the workload will be scaled

min

1

        * userMetrics

{object}

          * enabled

boolean

Whether to enable handling for custom metrics in the autoscaling configuration

          * exposedMetricsPath

string

Path on which the metrics will be exposed by the service..

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

          * exposedMetricsPort

integer

Port on which the metrics will be exposed by the service.

          * metrics

[array]

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

string required

The ID of the deployment plan to use.

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

      * ports

[array]

        * {object}

          * name

string required

The name used to identify the port.

min length

1

max length

8

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * internalPort

integer required

The port number.

min

1

max

65535

          * public

boolean

If true, the port will be exposed publicly.

          * security

{object}

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

            * ip

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

Configure port authentication via SSO

              * organizationId

string

ID of the SSO organization that the user will have to be a member of

              * directoryGroupIds

[array]

Array of directory groups that will have access

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

            * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

              * (multiple options: anyOf)

                * {object}

Matches provided headers as strings.

                  * regexMode

boolean

                  * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                  * value

string required

OR

                * {object}

Matches provided headers as regex.

                  * regexMode

boolean

                  * name

string required

                  * value

string required

            * verificationMode

string

Mode used to verify multiple security features like ip policies and SSO authentication

one of

or, and

            * securePathConfiguration

{object}

              * enabled

boolean

Enable security policies on a path-level style

              * skipSecurityPoliciesForInternalTrafficViaPublicDns

boolean

Allow internal traffic from same or shared projects via public DNS to skip all security policies

              * rules

[array]

                * {object}

                  * paths

[array] required

Array of path objects which represent the paths and their priority for which the security policies will be enforced

                    * (multiple options: oneOf)

Data about how the path should be handled.

                      * {object}

Route when the path starts with the provided prefix.

                        * path

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

                        * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

prefix

                        * priority

integer required

min

0

max

100

OR

                      * {object}

Route when the path is an exact match.

                        * path

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

                        * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

exact

                        * priority

integer required

min

0

max

100

OR

                      * {object}

Route when the path matches the provided regex.

                        * path

string required

                        * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

regex

                        * priority

integer required

min

0

max

100

                  * accessMode

string required

Specify the way the path rule will behave when processing policies. This enables an allow-list/deny-list approach for access control on each path

one of

protected, unprotected

                  * securityPolicies

{object}

                    * orPolicies

{object}

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

                      * ip

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

Configure port authentication via SSO

                        * organizationId

string

ID of the SSO organization that the user will have to be a member of

                        * directoryGroupIds

[array]

Array of directory groups that will have access

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

                      * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

                        * (multiple options: anyOf)

                          * {object}

Matches provided headers as strings.

                            * regexMode

boolean

                            * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                            * value

string required

OR

                          * {object}

Matches provided headers as regex.

                            * regexMode

boolean

                            * name

string required

                            * value

string required

                    * requiredPolicies

{object}

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

                      * ip

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

Configure port authentication via SSO

                        * organizationId

string

ID of the SSO organization that the user will have to be a member of

                        * directoryGroupIds

[array]

Array of directory groups that will have access

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

                      * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

                        * (multiple options: anyOf)

                          * {object}

Matches provided headers as strings.

                            * regexMode

boolean

                            * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                            * value

string required

OR

                          * {object}

Matches provided headers as regex.

                            * regexMode

boolean

                            * name

string required

                            * value

string required

          * domains

[array]

An array of domains to redirect to this port. Each domain must first be verified and registered to your account.

            * string

A domain to redirect to this port.

          * disableNfDomain

boolean

Disable routing on the default code.run domain for public HTTP ports with custom domains.

          * advancedOptions

{object}

            * enableTlsPassthrough

boolean

Whether this port should use pass through mode for TLS

          * protocol

(multiple options: oneOf) required

The protocol to use for the port.

            * string

one of

HTTP, HTTP/2

OR

            * string

one of

HTTP, HTTP/2, TCP, UDP

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

        * projectBranch

string required

The name of the branch to use.

      * bundleData

{object}

        * bundleUrl

string required

URL of the bundle to be built

        * branch

string required

Branch identifier for the bundle.

pattern

^[A-Za-z0-9-]+$

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

An object containing the runtime environment to set for the service. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

      * runtimeFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

      * buildArguments

{object}

An object containing the build arguments to set for the service. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

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

      * deploymentSysctlSettings

{object}

        * vm.max_map_count

integer

min

1

max

1048576

      * serviceType

string required

Type of the service (combined, build or deployment)

one of

combined

      * deployment

{object} required

        * type

string

The way the service should be deployed. Either as a deployment (default), or as a stateful set.

one of

deployment, statefulSet

        * instances

integer required

The number of instances to run the service on.

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

Image registry url of the deployed image.

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

        * deployment

{object} required

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




API

CLI

JS Client

PATCH /v1/projects/{projectId}/services/combined/{serviceId}

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request PATCH \
      --data '{"description":"A service description","billing":{"deploymentPlan":"nf-compute-20","buildPlan":"nf-compute-200-8"},"deployment":{"instances":1,"docker":{"configType":"default"},"storage":{"ephemeralStorage":{"storageSize":1024}}},"ports":[{"name":"p01","internalPort":8080,"public":true,"security":{"credentials":[{"username":"admin","password":"password123","type":"basic-auth"}],"ip":[{"addresses":["127.0.0.1"],"action":"DENY"}],"policies":[{"addresses":["127.0.0.1"],"action":"DENY"}],"headers":[{"regexMode":false}],"securePathConfiguration":{"rules":[{"paths":[{"routingMode":"prefix"}],"securityPolicies":{"orPolicies":{"credentials":[{"username":"admin","password":"password123","type":"basic-auth"}],"ip":[{"addresses":["127.0.0.1"],"action":"DENY"}],"policies":[{"addresses":["127.0.0.1"],"action":"DENY"}],"headers":[{"regexMode":false}]},"requiredPolicies":{"credentials":[{"username":"admin","password":"password123","type":"basic-auth"}],"ip":[{"addresses":["127.0.0.1"],"action":"DENY"}],"policies":[{"addresses":["127.0.0.1"],"action":"DENY"}],"headers":[{"regexMode":false}]}}}]}},"domains":["app.example.com"],"protocol":"HTTP"}],"buildSource":"git","vcsData":{"projectUrl":"https://github.com/northflank/gatsby-with-northflank","projectType":"github","accountLogin":"github-user","projectBranch":"master"},"bundleData":{"bundleUrl":"https://example.com/archive.tar"},"buildSettings":{"storage":{"ephemeralStorage":{"storageSize":16384}},"dockerfile":{"buildEngine":"buildkit","dockerFilePath":"/Dockerfile","dockerWorkDir":"/","buildkit":{"useCache":true,"cacheStorageSize":32768}},"buildpack":{"builder":"HEROKU_24","buildpackLocators":["https://buildpack-registry.heroku.com/cnb/mars/create-react-app"],"buildContext":"/","useCache":false}},"buildConfiguration":{"pathIgnoreRules":["README.md"],"isAllowList":false,"ciIgnoreFlags":["[skip ci]"],"dockerCredentials":["example-docker-credential"],"storage":{"ephemeralStorage":{"storageSize":16384}}},"runtimeEnvironment":{"VARIABLE_1":"abcdef","VARIABLE_2":"12345"},"runtimeFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"buildArguments":{"ARGUMENT_1":"abcdef","ARGUMENT_2":"12345"},"buildFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"dockerSecretMounts":{"example-secret-mount_1":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"healthChecks":[{"protocol":"HTTP","type":"readinessProbe","path":"/health-check","port":8080,"initialDelaySeconds":10,"periodSeconds":60,"timeoutSeconds":1,"failureThreshold":3,"successThreshold":1}],"autoscaling":{"horizontal":{"userMetrics":{"exposedMetricsPath":"/metrics","exposedMetricsPort":8080}}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/combined/{serviceId}

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
        "ports": [
          {
            "name": "p01",
            "internalPort": 8080,
            "public": true,
            "security": {
              "credentials": [
                {
                  "username": "admin",
                  "password": "password123",
                  "type": "basic-auth"
                }
              ],
              "ip": [
                {
                  "addresses": [
                    "127.0.0.1"
                  ],
                  "action": "DENY"
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
              "headers": [
                {
                  "regexMode": false
                }
              ],
              "securePathConfiguration": {
                "rules": [
                  {
                    "paths": [
                      {
                        "routingMode": "prefix"
                      }
                    ],
                    "securityPolicies": {
                      "orPolicies": {
                        "credentials": [
                          {
                            "username": "admin",
                            "password": "password123",
                            "type": "basic-auth"
                          }
                        ],
                        "ip": [
                          {
                            "addresses": [
                              "127.0.0.1"
                            ],
                            "action": "DENY"
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
                        "headers": [
                          {
                            "regexMode": false
                          }
                        ]
                      },
                      "requiredPolicies": {
                        "credentials": [
                          {
                            "username": "admin",
                            "password": "password123",
                            "type": "basic-auth"
                          }
                        ],
                        "ip": [
                          {
                            "addresses": [
                              "127.0.0.1"
                            ],
                            "action": "DENY"
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
                        "headers": [
                          {
                            "regexMode": false
                          }
                        ]
                      }
                    }
                  }
                ]
              }
            },
            "domains": [
              "app.example.com"
            ]
          }
        ],
        "buildSource": "git",
        "vcsData": {
          "projectUrl": "https://github.com/northflank/gatsby-with-northflank",
          "projectType": "github",
          "accountLogin": "github-user",
          "projectBranch": "master"
        },
        "bundleData": {
          "bundleUrl": "https://example.com/archive.tar"
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
          "VARIABLE_1": "abcdef",
          "VARIABLE_2": "12345"
        },
        "runtimeFiles": {
          "/dir/fileName": {
            "data": "VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=",
            "encoding": "utf-8"
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
        "autoscaling": {
          "horizontal": {
            "userMetrics": {
              "exposedMetricsPath": "/metrics",
              "exposedMetricsPort": 8080
            }
          }
        },
        "serviceType": "combined",
        "deployment": {
          "instances": 1,
          "docker": {
            "configType": "default"
          },
          "storage": {
            "ephemeralStorage": {
              "storageSize": 1024
            }
          }
        },
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
          },
          "deployment": {
            "status": "COMPLETED",
            "reason": "DEPLOYING",
            "lastTransitionTime": "2021-11-29T11:47:16.624Z"
          }
        }
      }
    }