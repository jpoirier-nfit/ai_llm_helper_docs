---
source_url: https://northflank.com/docs/v1/api/billing/list-invoices
title: List invoices | Billing | Northflank API docs
crawl_date: 2025-07-29T10:44:50.751464
watsonmd_version: 0.1.0
---

Billing / 

# List invoices

Get a list of past invoices

Required permission

Account > Billing > General > Read

Query parameters

    * per_page

integer

The number of results to display per request. Maximum of 100 results per page.

    * page

integer

The page number to access.

    * cursor

string

The cursor returned from the previous page of results, used to request the next page.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * invoices

{object}

        * period

{object} required

Information about the billing period of the invoice.

          * start

number required

Unix timestamp of the start of the billing period.

          * end

number required

Unix timestamp of the end of the billing period.

        * total

number required

Total cost of the invoice, in cents, including tax.

        * paid

boolean

If `timestamp` is passed in, whether the invoice has been paid.

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

GET /v1/billing/invoices

Example response

200 OK

Details about an invoice.

JSON
    
    
    {
      "data": {
        "invoices": {
          "period": {
            "start": 1655823815,
            "end": 1655910214
          },
          "total": 1200
        }
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }