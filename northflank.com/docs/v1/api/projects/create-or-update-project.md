---
source_url: https://northflank.com/docs/v1/api/projects/create-or-update-project
title: Create or update project | Projects | Northflank API docs
crawl_date: 2025-07-29T09:24:10.592955
watsonmd_version: 0.1.0
---

Projects / 

# Create or update project

Creates or updates a project.

Required permission

Project > Projects > Manage > Create

Request body

  * {object}

Create a project in a Northflank region

    * name

string required

The name of the project.

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

    * description

string

The description of the project.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

    * color

string

The color of the project in the Northflank App.

pattern

^#([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$

    * region

string

The region the project will be hosted in.

    * networking

{object}

Advanced project networking settings.

      * allowedIngressProjects

[array]

Projects from which ingress request should be permitted.

        * string

pattern

^[A-Za-z0-9-]+$

      * tailscale

{object}

Defines this project's Tailscale sidecar settings

        * enabled

boolean

Whether or not to inject a Tailscale sidecar for this project's resources

        * authKeyTags

[array]

Tailscale tags to apply to generated auth keys, must match with the tags applied when creating the OAuth Client.

          * string

pattern

^tag:.+

        * restrictions

{object}

          * enabled

boolean required

Whether or not to restrict the settings to resources with specific tags

          * tags

[array]

The tags which determine the resources the settings should be applied to

            * string

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * tagMatchCondition

string

If all or any of the tags must be present on the target for it to match the condition.

one of

and, or

        * options

{object}

          * applyToAddons

boolean

Apply the Tailscale configuration to addons.

          * applyToAddonJobs

boolean

Apply the Tailscale configuration to addon jobs (backups, restores).

          * autoRedeployOnRegeneration

boolean

Automatically restart applicable services when the auth key is regenerated

        * tailscaleOptions

{object}

          * acceptRoutes

boolean

Accept advertised routes from the Tailscale network

        * secrets

{object}

Relevant Tailscale secrets

          * clientId

string required

Tailscale OAuth client ID (required for generating auth keys for Tailscale)

          * clientSecret

string required

Tailscale OAuth client secret (required for generating auth keys for Tailscale)

      * hostAliases

{object}

Defines the project host alias overrides to apply to /etc/hosts in resource containers

        * enabled

boolean

Enable support for adding /etc/hosts overrides for a container

        * hostEntries

[array]

Entries to add to /etc/hosts

          * {object}

            * ipAddress

string required

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$

            * hostnames

[array] required

              * string

pattern

^(([a-z0-9][a-z0-9\\-]*)|[a-z0-9]\\.)*([a-z]+|xn\\-\\-[a-z0-9]+)\\.?$

        * restrictions

{object}

          * enabled

boolean required

Whether or not to restrict the settings to resources with specific tags

          * tags

[array]

The tags which determine the resources the settings should be applied to

            * string

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * tagMatchCondition

string

If all or any of the tags must be present on the target for it to match the condition.

one of

and, or




OR

  * {object}

Create a project in a BYOC cluster

    * name

string required

The name of the project.

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

    * description

string

The description of the project.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

    * color

string

The color of the project in the Northflank App.

pattern

^#([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$

    * clusterId

string

The BYOC cluster this project will be hosted in.

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

    * networking

{object}

Advanced project networking settings.

      * allowedIngressProjects

[array]

Projects from which ingress request should be permitted.

        * string

pattern

^[A-Za-z0-9-]+$

      * tailscale

{object}

Defines this project's Tailscale sidecar settings

        * enabled

boolean

Whether or not to inject a Tailscale sidecar for this project's resources

        * authKeyTags

[array]

Tailscale tags to apply to generated auth keys, must match with the tags applied when creating the OAuth Client.

          * string

pattern

^tag:.+

        * restrictions

{object}

          * enabled

boolean required

Whether or not to restrict the settings to resources with specific tags

          * tags

[array]

The tags which determine the resources the settings should be applied to

            * string

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * tagMatchCondition

string

If all or any of the tags must be present on the target for it to match the condition.

one of

and, or

        * options

{object}

          * applyToAddons

boolean

Apply the Tailscale configuration to addons.

          * applyToAddonJobs

boolean

Apply the Tailscale configuration to addon jobs (backups, restores).

          * autoRedeployOnRegeneration

boolean

Automatically restart applicable services when the auth key is regenerated

        * tailscaleOptions

{object}

          * acceptRoutes

boolean

Accept advertised routes from the Tailscale network

        * secrets

{object}

Relevant Tailscale secrets

          * clientId

string required

Tailscale OAuth client ID (required for generating auth keys for Tailscale)

          * clientSecret

string required

Tailscale OAuth client secret (required for generating auth keys for Tailscale)

      * hostAliases

{object}

Defines the project host alias overrides to apply to /etc/hosts in resource containers

        * enabled

boolean

Enable support for adding /etc/hosts overrides for a container

        * hostEntries

[array]

Entries to add to /etc/hosts

          * {object}

            * ipAddress

string required

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$

            * hostnames

[array] required

              * string

pattern

^(([a-z0-9][a-z0-9\\-]*)|[a-z0-9]\\.)*([a-z]+|xn\\-\\-[a-z0-9]+)\\.?$

        * restrictions

{object}

          * enabled

boolean required

Whether or not to restrict the settings to resources with specific tags

          * tags

[array]

The tags which determine the resources the settings should be applied to

            * string

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * tagMatchCondition

string

If all or any of the tags must be present on the target for it to match the condition.

one of

and, or




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * id

string required

Identifier for the project

      * name

string required

The name of the project.

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

      * description

string

The description of the project.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

      * color

string

The color of the project in the Northflank App.

pattern

^#([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$

      * region

string

The region the project will be hosted in.

      * clusterId

string

The BYOC cluster this project will be hosted in.

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * networking

{object}

Advanced project networking settings.

        * allowedIngressProjects

[array]

Projects from which ingress request should be permitted.

          * string

pattern

^[A-Za-z0-9-]+$

        * tailscale

{object}

Defines this project's Tailscale sidecar settings

          * enabled

boolean

Whether or not to inject a Tailscale sidecar for this project's resources

          * authKeyTags

[array]

Tailscale tags to apply to generated auth keys, must match with the tags applied when creating the OAuth Client.

            * string

pattern

^tag:.+

          * restrictions

{object}

            * enabled

boolean required

Whether or not to restrict the settings to resources with specific tags

            * tags

[array]

The tags which determine the resources the settings should be applied to

              * string

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

            * tagMatchCondition

string

If all or any of the tags must be present on the target for it to match the condition.

one of

and, or

          * options

{object}

            * applyToAddons

boolean

Apply the Tailscale configuration to addons.

            * applyToAddonJobs

boolean

Apply the Tailscale configuration to addon jobs (backups, restores).

            * autoRedeployOnRegeneration

boolean

Automatically restart applicable services when the auth key is regenerated

          * tailscaleOptions

{object}

            * acceptRoutes

boolean

Accept advertised routes from the Tailscale network

          * secrets

{object}

Relevant Tailscale secrets

            * clientId

string required

Tailscale OAuth client ID (required for generating auth keys for Tailscale)

            * clientSecret

string required

Tailscale OAuth client secret (required for generating auth keys for Tailscale)

        * hostAliases

{object}

Defines the project host alias overrides to apply to /etc/hosts in resource containers

          * enabled

boolean

Enable support for adding /etc/hosts overrides for a container

          * hostEntries

[array]

Entries to add to /etc/hosts

            * {object}

              * ipAddress

string required

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$

              * hostnames

[array] required

                * string

pattern

^(([a-z0-9][a-z0-9\\-]*)|[a-z0-9]\\.)*([a-z]+|xn\\-\\-[a-z0-9]+)\\.?$

          * restrictions

{object}

            * enabled

boolean required

Whether or not to restrict the settings to resources with specific tags

            * tags

[array]

The tags which determine the resources the settings should be applied to

              * string

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

            * tagMatchCondition

string

If all or any of the tags must be present on the target for it to match the condition.

one of

and, or

      * createdAt

string

time of creation

      * updatedAt

string

time of update




API

CLI

JS Client

PUT /v1/projects

Example request

Request body

Create a project in a Northflank region

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request PUT \
      --data '{"name":"New Project","description":"This is a new project.","color":"#EF233C","region":"europe-west","networking":{"tailscale":{"restrictions":{"tagMatchCondition":"or"}},"hostAliases":{"restrictions":{"tagMatchCondition":"or"}}}}' \
      https://api.northflank.com/v1/projects

OR

Create a project in a BYOC cluster

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request PUT \
      --data '{"name":"New Project","description":"This is a new project.","color":"#EF233C","clusterId":"gcp-cluster-1","networking":{"tailscale":{"restrictions":{"tagMatchCondition":"or"}},"hostAliases":{"restrictions":{"tagMatchCondition":"or"}}}}' \
      https://api.northflank.com/v1/projects

Example response

200 OK

Details about the created or updated project.

JSON
    
    
    {
      "data": {
        "id": "example-project",
        "name": "New Project",
        "description": "This is a new project.",
        "color": "#EF233C",
        "region": "europe-west",
        "clusterId": "gcp-cluster-1",
        "networking": {
          "tailscale": {
            "restrictions": {
              "tagMatchCondition": "or"
            }
          },
          "hostAliases": {
            "restrictions": {
              "tagMatchCondition": "or"
            }
          }
        },
        "createdAt": "2000-01-01T12:00:00.000Z",
        "updatedAt": "2000-01-01T12:00:00.000Z"
      }
    }