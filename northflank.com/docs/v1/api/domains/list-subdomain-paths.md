---
source_url: https://northflank.com/docs/v1/api/domains/list-subdomain-paths
title: List subdomain paths | Domains | Northflank API docs
crawl_date: 2025-07-29T10:02:17.438746
watsonmd_version: 0.1.0
---

Domains / 

# List subdomain paths

List paths for a given subdomain.

Required permission

Account > SubdomainPaths > General > Read

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * paths

[array] required

A list of paths created for the given subdomain.

        * {object}

Details about a subdomain path.

          * subdomain

string required

The domain the path should be created for.

pattern

^\\*|^@$|^([0-9a-z]([0-9a-z\\-]*[0-9a-z])?\\.)*[0-9a-z]([0-9a-z\\-]*[0-9a-z])?$

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

    * pagination

{object} required

Data about the endpoint pagination.

      * hasNextPage

boolean required

Is there another page of results available?

      * cursor

string

The cursor to access the next page of results.

      * count

number required

The number of results returned by this request.




API

CLI

JS Client

GET /v1/domains/{domain}/subdomains/{subdomain}/paths

Example response

200 OK

A list of paths for the given subdomain.

JSON
    
    
    {
      "data": {
        "paths": [
          {
            "subdomain": "site.example.com",
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
            }
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }