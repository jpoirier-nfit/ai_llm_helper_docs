---
source_url: https://northflank.com/docs/v1/api/services/get-service-metrics
title: Get service metrics | Services | Northflank API docs
crawl_date: 2025-07-29T10:04:44.040874
watsonmd_version: 0.1.0
---

Services / 

# Get service metrics

Get metrics for a service

Required permission

Project > Services > Deployment > View Instance Metrics

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Query parameters

    * queryType

string

Selects metrics for specified timestamp.

one of

range, single

    * metricTypes

string

Type of metric. Multiple metric types can be selected by specifying the query parameter repeatedly.

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

    * startTime

string

Fetch metrics generated after this timestamp. Only valid for queryType: `range`.

    * endTime

string

Fetch metrics generated before this timestamp. Only valid for queryType: `range`.

    * duration

integer

Range duration in seconds. If set, only one of `startTime` or `endTime` can be set.

    * containerName

string

Limits metrics to a specific container.

    * deploymentId

string

Limits metrics to a specific deployment

    * time

string

Fetch metrics at this timestamp. If not provided will use current time. Only valid for queryType: `single`.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * cpu

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * memory

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * networkIngress

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * networkEgress

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * tcpConnectionsOpen

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * diskUsage

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * requests

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * http4xxResponses

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * http5xxResponses

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * bandwidth

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required

      * bandwidthVolume

{object}

        * metricInfo

{object}

          * metricId

string required

Type of metric to fetch

one of

cpu, memory, networkIngress, networkEgress, tcpConnectionsOpen, diskUsage, requests, http4xxResponses, http5xxResponses, bandwidth, bandwidthVolume

          * metricUnit

string required

one of

pct, vCPU, mb, kbps, rps, count

          * metricResolution

number

        * values

[array] required

          * {object}

            * metadata

{object}

              * containerId

string required

              * volumeId

string

            * data

[array] required

              * {object}

                * value

number required

                * ts

string required




API

CLI

JS Client

GET /v1/projects/{projectId}/services/{serviceId}/metrics

Example response

200 OK

List of metrics values

JSON
    
    
    {
      "data": {
        "cpu": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "memory": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "networkIngress": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "networkEgress": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "tcpConnectionsOpen": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "diskUsage": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "requests": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "http4xxResponses": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "http5xxResponses": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "bandwidth": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        },
        "bandwidthVolume": {
          "metricInfo": {
            "metricUnit": "pct",
            "metricResolution": 10
          },
          "values": [
            {
              "metadata": {
                "containerId": "nginx-669cc865b7-5458n",
                "volumeId": "data-volume-1"
              },
              "data": [
                {
                  "value": 0.5,
                  "ts": "2023-03-21T15:01:17.310Z"
                }
              ]
            }
          ]
        }
      }
    }