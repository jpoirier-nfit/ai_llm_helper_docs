---
source_url: https://northflank.com/docs/v1/api/domains/enable-cdn-on-a-subdomain
title: Enable CDN on a subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:02:17.314494
watsonmd_version: 0.1.0
---

Domains / 

# Enable CDN on a subdomain

Enables a CDN integration on the given subdomain

Required permission

Account > Subdomains > General > Update

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain




Request body

  * {object}

Use Fastly as a CDN

    * provider

string required

Provider for which a CDN on the subdomain should be enabled.

    * options

{object}

      * service

{object}

        * forceTlsEnableHsts

boolean

        * hstsDuration

number

HSTS duration. Required when `forceTlsEnableHsts` is `true`.

min

300

        * staleIfError

boolean

        * staleIfErrorTtl

number

        * defaultTtl

number

      * logging

{object}

        * enabled

boolean

      * http3

{object}

        * enabled

boolean

      * websockets

{object}

        * enabled

boolean

      * compression

{object}

        * enabled

boolean

        * mode

string

Compression options. Required when `enabled` is `true`.

one of

gzip, brotli

      * vclSnippets

[array]

        * {object}

          * id

string

          * name

string required

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

          * type

string required

one of

init, recv, hash, hit, miss, pass, fetch, error, deliver, log, none

          * dynamic

string required

one of

0, 1

          * priority

number required

min

0

max

100

          * content

string required

      * cacheSettings

[array]

        * {object}

          * id

string

          * name

string required

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

          * action

string

one of

pass, cache, restart

          * cacheCondition

string

          * staleTtl

number required

          * ttl

number required




OR

  * {object}

Use Cloudfront as a CDN

    * provider

string required

Provider for which a CDN on the subdomain should be enabled.

    * options

{object}




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/domains/{domain}/subdomains/{subdomain}/cdn/enable

Example request

Request body

Use Fastly as a CDN

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"provider":"fastly"}' \
      https://api.northflank.com/v1/domains/{domain}/subdomains/{subdomain}/cdn/enable

OR

Use Cloudfront as a CDN

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"provider":"cloudfront"}' \
      https://api.northflank.com/v1/domains/{domain}/subdomains/{subdomain}/cdn/enable

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }