---
source_url: https://northflank.com/docs/v1/api/domains/get-subdomain-path
title: Get subdomain path | Domains | Northflank API docs
crawl_date: 2025-07-29T09:24:14.668992
watsonmd_version: 0.1.0
---

Domains / 

# Get subdomain path

Get subdomain path details.

Required permission

Account > SubdomainPaths > General > Read

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain

    * subdomainPath

string required

Name of the path




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * mode

string required

Mode of the path, determining how the URI will be interpreted.

one of

prefix, exact, regex

      * uri

string required

URI of the subdomain path. Interpreted according to the selected path mode

      * options

{object}

        * priority

integer

In case of uri conflicts, the route with the higher priority will take precedence

min

0

max

100

        * ignoreUriCase

boolean

Allows case insensitive matching for 'prefix' and 'exact' modes

        * rewrite

(multiple options: oneOf)

Settings determining if a path should be rewritten. Either a uri or regex have to be specified.

          * {object}

Rewrite with URI

            * uri

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

OR

          * {object}

Rewrite with regex

            * regex

{object}

              * match

string required

Regex match for the given path

              * rewrite

string required

Regex rewrite for the given matched path

        * timeout

string

Customised request timeout for the given path. By default no timeout is set.

pattern

^[1-9][0-9]*(s|ms)$

        * headers

{object}

Settings allowing addition, re-write and removal of request as well as response headers.

          * request

{object}

            * set

{object}

            * add

{object}

            * remove

[array]

              * string

pattern

^[a-zA-Z0-9_\\-%$+]+$

          * response

{object}

            * set

{object}

            * add

{object}

            * remove

[array]

              * string

pattern

^[a-zA-Z0-9_\\-%$+]+$

        * corsPolicy

{object}

Settings allowing for customization of CORS policies.

          * enabled

boolean required

          * allowOrigins

[array]

            * {object}

              * mode

string required

Mode of the path, determining how the URI will be interpreted.

one of

prefix, exact, regex

              * origin

string

Origin definition.

          * allowMethods

[array]

            * string

one of

GET, POST, PUT, PATCH, DELETE, OPTIONS, TRACE, CONNECT, HEAD

          * allowCredentials

boolean

          * allowHeaders

[array]

            * string

          * maxAge

string

pattern

^[1-9][0-9]*(s|m|h)$

        * retries

{object}

Settings allowing for customization of retries.

          * enabled

boolean required

          * attempts

integer required

min

1

max

3

          * perTryTimeout

string

Timeout per attempt. By default uses the path level timeout.

pattern

^[1-9][0-9]*(s|ms)$

          * retryOn

[array]

Configure the cases in which the retry should be triggered.

            * string

one of

5xx, gateway-error, reset, connect-failure, envoy-ratelimited, retriable-4xx, refused-stream, retriable-status-codes, retriable-headers, cancelled, deadline-exceeded, internal, resource-exhausted, unavailable

      * name

string

The full URL including subdomain and path URI.

      * createdAt

string

time of creation

      * assignment

{object}

Data about the subdomain path assignment.

        * project

string required

The ID of the service to assign the subdomain path to.

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * service

string required

The ID of the project the service belongs to.

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * port

string required

The name of the port that will be assigned to the subdomain path.




API

CLI

JS Client

GET /v1/domains/{domain}/subdomains/{subdomain}/paths/{subdomainPath}

Example response

200 OK

Details about subdomain path.

JSON
    
    
    {
      "data": {
        "mode": "prefix",
        "uri": "/",
        "options": {
          "priority": 0,
          "corsPolicy": {
            "allowOrigins": [
              {
                "mode": "prefix",
                "origin": "https://example.com"
              }
            ]
          }
        },
        "assignment": {
          "project": "default-project",
          "service": "example-service",
          "port": "p01"
        }
      }
    }

Example response

404 Not Found

Path not found.