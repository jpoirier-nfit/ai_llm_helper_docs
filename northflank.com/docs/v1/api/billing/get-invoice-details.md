---
source_url: https://northflank.com/docs/v1/api/billing/get-invoice-details
title: Get invoice details | Billing | Northflank API docs
crawl_date: 2025-07-29T10:44:50.386418
watsonmd_version: 0.1.0
---

Billing / 

# Get invoice details

Get details about an invoice. If `timestamp` is passed in as a query parameter, this endpoint returns details about the invoice containing that timestamp. Otherwise, returns a preview invoice displaying billing data from after the most recent invoice.

Required permission

Account > Billing > General > Read

Query parameters

    * timestamp

integer

Timestamp of an invoice. If passed in, this endpoint will return details about the invoice that time belongs to.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * period

{object} required

Information about the billing period of the invoice.

        * start

number required

Unix timestamp of the start of the billing period.

        * end

number required

Unix timestamp of the end of the billing period.

      * paid

boolean

If `timestamp` is passed in, whether the invoice has been paid.

      * byocUsage

{object}

        * price

{object}

          * total

number

      * paasUsage

{object} required

        * price

{object}

          * total

number

          * cpu

number

          * memory

number

          * storage

number

        * teams

[array]

          * {object}

            * id

string

            * name

string

            * usage

{object}

              * price

{object}

                * total

number

                * cpu

number

                * memory

number

                * storage

number

              * projects

[array]

                * {object}

                  * id

string

                  * price

{object}

                    * total

number

                    * cpu

number

                    * memory

number

                    * storage

number

      * lineItems

[array]

        * {object}

          * title

string

          * total

number

      * subTotal

number

      * discount

number

      * tax

{object} required

Details about the tax on the invoice.

        * percent

number required

Percentage of subtotal to be applied as tax.

        * value

number required

Value of the tax on the invoice.

      * total

number




API

CLI

JS Client

GET /v1/billing/invoices/details

Example response

200 OK

Details about an invoice.

JSON
    
    
    {
      "data": {
        "period": {
          "start": 1655823815,
          "end": 1655910214
        },
        "tax": {
          "percent": 20,
          "value": 200
        }
      }
    }