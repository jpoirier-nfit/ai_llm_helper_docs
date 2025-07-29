---
source_url: https://northflank.com/docs/v1/api/domains/get-subdomain
title: Get subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.393540
watsonmd_version: 0.1.0
---

Domains / 

# Get subdomain

Gets details about the given subdomain

Required permission

Account > Subdomains > General > Read

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

      * recordType

string required

The record type to use for the DNS record to verify the subdomain - always CNAME for subdomains.

      * name

string required

The subdomain.

      * fullName

string required

The full domain name with subdomain

      * content

string required

The content to set the DNS record to

      * verified

boolean required

Whether the subdomain has been verified successfully and can be used.

      * certificate

{object}

        * inProgress

boolean

Whether a certificate is in the process of being generated

        * expiryDate

string

Expiry date of the current certificate

        * refreshDare

string

Refresh date of the current certificate

      * cdn

{object}

        * cloudfront

{object}

          * enabled

boolean

          * status

string

          * deployedAt

string

        * fastly

{object}

          * enabled

boolean

          * status

string

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

          * deployedAt

string




API

CLI

JS Client

GET /v1/domains/{domain}/subdomains/{subdomain}

Example response

200 OK

Details about the subdomain.

JSON
    
    
    {
      "data": {
        "recordType": "CNAME",
        "name": "site",
        "fullName": "site.example.com",
        "content": "site.example.com.user-1234.dns.northflank.app",
        "verified": true
      }
    }