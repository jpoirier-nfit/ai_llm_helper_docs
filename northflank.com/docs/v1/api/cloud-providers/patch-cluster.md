---
source_url: https://northflank.com/docs/v1/api/cloud-providers/patch-cluster
title: Patch cluster | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:53.641482
watsonmd_version: 0.1.0
---

Cloud Providers / 

# Patch cluster

Updates a cluster.

Required permission

Account > Cloud > Clusters > Update

Path parameters

    * clusterId

string required

ID of the cluster




Request body

  * {object}

    * name

string

The name of the cluster.

min length

3

max length

20

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

    * description

string

The description of the cluster.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

    * kubernetesVersion

string

Deprecated: This field is no longer used, the version is now set by the platform.

    * nodePools

(multiple options: oneOf)

An array of node pools for BYOC or BYOK.

      * [array]

An array of node pools for BYOC.

        * {object}

Node pool configuration for BYOC clusters

          * id

string required

ID of existing node pool. Must be passed when modifying existing node pools. Not relevant for new node pools

min length

3

max length

63

pattern

(^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$)|(^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-4[0-9a-fA-F]{3}-[89ABab][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$)

          * nodeType

string required

Machine type to be used by the node pool.

          * oci

{object}

OCI instance specific settings. Must respect ratios as determined by the selected node type.

            * ocpu

integer required

min

1

            * memory

integer required

min

1

          * gcp

{object}

GCP specific settings.

            * enablePrivateNodes

boolean

Set this flag to disable public IP assignment for nodes in this node pool.

          * azure

{object}

Azure specific settings.

            * systemPool

boolean

When 'provider' is 'azure', at least one system node pool is required per cluster.

            * enablePublicNodeIp

boolean

When 'provider' is 'azure', set this flag to use public node IPs.

            * vnetSubnetId

string

ID of the vnet subnet to use.

          * aws

{object}

AWS specific node pool settings.

            * launchTemplate

{object}

Specify a launch template to use for this node pool. When using a launch template, the disk size selection on the node pool level will be ignored.

              * id

string required

ID of the launch template to use.

              * version

integer required

Version of the launch template that should be used.

min

1

          * nodeCount

integer required

Number of nodes to the node pool should be provisioned with.

min

0

max

250

          * autoscaling

{object}

Auto scaling settings to use for the node pool. Requires that the cloud provider supports this feature.

            * enabled

boolean

            * min

integer

min

0

max

249

            * max

integer

min

1

max

250

          * computeResources

{object}

            * gpu

{object}

              * timeslicing

{object}

Time-slicing configuration object.

                * enabled

boolean

Whether or not to enable time-slicing on the GPU.

                * numSlices

number

Sets the amount of slices per GPU, e.g. how many pods may be scheduled concurrently on each GPU.

min

1

          * preemptible

boolean

Configures node pool with preemptible / spot instances if enabled.

          * diskType

string

The disk type to use.

          * diskSize

integer required

Disk size in GB

min

1

          * availabilityZones

[array] required

Zones in which the node pool should be provisioned.

            * string

          * subnets

[array]

Subnets in which the node pool should be provisioned. Required if provider is `oci`.

            * string

          * scheduling

{object}

Define basic workload scheduling restrictions for this node pool

            * allowJobs

boolean

Allow jobs to schedule to this node pool

            * onlyGpuJobs

boolean

Restrict job scheduling to jobs which have GPU resources configured. Only relevant for GPU node pools.

            * allowServices

boolean

Allow services to schedule to this node pool

            * onlyGpuServices

boolean

Restrict service scheduling to services which have GPU resources configured. Only relevant for GPU node pools.

            * allowAddons

boolean

Allow addons to schedule to this node pool

            * allowBuilds

boolean

Allow builds to schedule to this node pool

            * onlyGpuBuilds

boolean

Restrict build scheduling to builds which have GPU resources configured. Only relevant for GPU node pools.

            * allowCeph

boolean

Allow the placement of Ceph pods

          * labels

{object}

Set of label keys and values that can be used for advanced scheduling in combination with resource tag scheduling rules.

OR

      * [array]

An array of node pools for BYOK.

        * {object}

Node pool configuration for BYOK clusters

          * id

string required

ID of the node pool. Must be passed when modifying existing node pools. Not relevant for new node pools

min length

3

max length

63

pattern

(^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$)|(^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-4[0-9a-fA-F]{3}-[89ABab][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$)

          * providerId

string required

ID which identifies kubernetes nodes as belonging to this pool.

min length

3

max length

63

pattern

(^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$)|(^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-4[0-9a-fA-F]{3}-[89ABab][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$)

          * computeResources

{object}

            * gpu

{object}

              * supported

boolean

Whether this node pool consists of GPU nodes .

              * type

string

GPU type associated with the node pool.

pattern

[a-z0-9]

              * resources

{object}

                * memoryInfo

{object}

                  * sizeInGiB

number

Memory amount of the GPU in Gib.

min

1

              * mig

{object}

Multi-Instance GPU (MIG). configuration object.

                * enabled

boolean

Whether or not to enable Multi-Instance GPU (MIG).

                * partitions

[array]

The partitions to configure on the GPU.

                  * string

              * timeslicing

{object}

Time-slicing configuration object.

                * enabled

boolean

Whether or not to enable time-slicing on the GPU.

                * numSlices

number

Sets the amount of slices per GPU, e.g. how many pods may be scheduled concurrently on each GPU.

min

1

              * count

integer

Number of GPUs per node.

min

1

          * defaultPool

boolean

Fallback pool to which nodes which do not match any defined node pool are assigned. Exactly one default pool is required.

          * preemptible

boolean

Configures node pool with preemptible / spot instances if enabled.

          * scheduling

{object}

Define basic workload scheduling restrictions for this node pool

            * allowJobs

boolean

Allow jobs to schedule to this node pool

            * onlyGpuJobs

boolean

Restrict job scheduling to jobs which have GPU resources configured. Only relevant for GPU node pools.

            * allowServices

boolean

Allow services to schedule to this node pool

            * onlyGpuServices

boolean

Restrict service scheduling to services which have GPU resources configured. Only relevant for GPU node pools.

            * allowAddons

boolean

Allow addons to schedule to this node pool

            * allowBuilds

boolean

Allow builds to schedule to this node pool

            * onlyGpuBuilds

boolean

Restrict build scheduling to builds which have GPU resources configured. Only relevant for GPU node pools.

            * allowCeph

boolean

Allow the placement of Ceph pods

          * labels

{object}

Set of label keys and values that can be used for advanced scheduling in combination with resource tag scheduling rules.

    * settings

{object}

      * builds

{object}

        * mode

string

one of

paas, internal, build-cluster

        * plan

string

Plan to use for builds if they are run on the cluster

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * clusterId

string

Cluster to use for scheduling builds

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * registry

{object}

        * mode

string

one of

paas, self-hosted

        * registryId

string

Credentials to use for storing of images.

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * logging

(multiple options: oneOf)

Logging settings

        * {object}

Logging via PaaS.

          * mode

string

one of

paas

OR

        * {object}

Logging via Loki (S3 storage).

          * mode

string required

one of

loki

          * loki

{object}

            * storageType

string required

one of

s3

            * s3BucketName

string required

            * s3AccessKey

string required

            * s3SecretKey

string required

            * s3Region

string required

OR

        * {object}

Logging via Loki (GCS storage).

          * mode

string required

one of

loki

          * loki

{object}

            * storageType

string required

one of

gcs

            * gcsBucketName

string required

            * gcpIntegrationId

string required

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * vanityDomains

{object}

        * apps

{object}

          * zoneName

string required

          * integrationId

string required

        * customDomains

{object}

          * zoneName

string required

          * integrationId

string required

        * loadBalancers

{object}

          * zoneName

string required

          * integrationId

string required

      * infrastructure

{object}

        * workloads

{object}

          * runtimeClass

string

one of

none, gvisor, kata-clh, kata-qemu, katars-clh

        * builds

{object}

          * runtimeClass

string

one of

none, gvisor, kata-clh, kata-qemu, katars-clh

        * installKata

boolean

        * installGvisor

boolean

        * cleanupVolumes

boolean

        * cleanupSnapshots

boolean

        * cephStorageProvider

{object}

          * enabled

boolean

          * resources

{object}

            * cpu

number

Configure the CPU resources per Ceph replica

min

1

max

20

            * memory

number

Configure the memory resources per Ceph replica

min

4096

max

40960

            * storage

number

Configure the data disk size per Ceph replica

min

102400

max

5242880

          * enableMultiReadWriteStorage

boolean

Configure Ceph to be enable use of multi read write storage for persistent volumes on the cluster.

          * enableSingleReadWriteStorage

boolean

Configure Ceph to be used as default storage class for single read write storage. This will replace the default storage of the cloud provider.

          * enableErasureCoding

boolean

Configure Ceph to be set up with erasure coding. This will be less fault tolerant but more cost effective.

          * enableTopologyAwareScheduling

boolean

Configure Ceph to be set up with topology aware scheduling, enforcing deployment across multiple zones.

      * requestModifiers

{object}

Allows customising request modifier values.

        * services

{object}

Request modifiers for services

          * cpu

number required

min

0.2

max

1

          * memory

number required

min

0.4

max

1

        * jobs

{object}

Request modifiers for jobs

          * cpu

number required

min

0.2

max

1

          * memory

number required

min

0.4

max

1

        * builds

{object}

Request modifiers for builds

          * cpu

number required

min

0.1

max

1

          * memory

number required

min

0.1

max

1

        * addons

{object}

Request modifiers for addons

          * cpu

number required

min

0.2

max

1

          * memory

number required

min

0.4

max

1

    * restrictions

{object}

BYOC restrictions configuration for controlling team access

      * enabled

boolean required

Enable or disable BYOC restrictions for this entity

      * teams

[array]

List of teams that have access to this BYOC cluster

        * {object}

          * teamId

string required

The ID of the team that has access to this BYOC cluster

min length

3

max length

45

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

    * gcp

{object}

GCP specific data. Required when `provider` is `gcp`

      * networking

{object}

        * network

string

        * subnetwork

string

      * enableAuthorizedIpRanges

boolean

      * authorizedIpRanges

[array]

        * string

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\/([0-9]|[1-2][0-9]|3[0-2]))$

      * projectId

string

GCP Project ID

pattern

^[a-z][a-z0-9-]{4,28}[a-z0-9]$

    * aws

{object}

AWS specific data. Required when `provider` is `aws`.

      * enablePublicAccessCidrs

boolean

      * publicAccessCidrs

[array]

        * string

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\/([0-9]|[1-2][0-9]|3[0-2]))$

      * subnetConfiguration

{object}

        * mode

string required

The mode of the AWS subnet configuration

one of

default-subnets-for-azs, explicit-subnets

        * vpcId

string

Id of the VPC

        * subnets

[array] required

List of subnets the cluster should be created for. At least 2 must be specified.

          * string

      * vpcEgress

boolean

If egress traffic from the cluster should come from a single static egress IP.

    * azure

{object}

Azure specific data. Required when `provider` is `azure`.

      * networking

{object}

        * vnetConfiguration

{object}

          * mode

string required

The vnet mode to use for this cluster. Use this to switch between creation of a new vnet per cluster or specifying a custom vnet.

one of

create-default, custom-vnet

          * vnetId

string

Azure vnetId that should be used for this cluster. By default a new vnet will be created.

        * networkPluginMode

string

Optional setting to configure overlay mode on Azure.

one of

overlay

      * enableAuthorizedIpRanges

boolean

      * authorizedIpRanges

[array]

        * string

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\/([0-9]|[1-2][0-9]|3[0-2]))$

    * byok

{object}

BYOK specific data. Required when `provider` is `byok`.

      * nodePoolProviderIdLabel

string required




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * name

string required

The name of the cluster.

min length

3

max length

20

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

      * description

string

The description of the cluster.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

      * provider

string required

Cloud provider to be used for the selected resource

one of

aws, azure, civo, gcp, oci, cloudflare, byok

      * region

string required

Region of the cluster.

      * kubernetesVersion

string

Deprecated: This field is no longer used, the version is now set by the platform.

      * integrationId

string

Existing integration to use for this cluster.

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * storage

{object}

        * storageEnabled

boolean

        * snapshotsEnabled

boolean

        * storageClasses

[array]

          * {object}

            * id

string required

            * name

string required

            * description

string

            * platformMapping

string required

one of

ssd, hdd

            * kubernetesName

string required

            * defaultSnapshotClass

string

        * snapshotClasses

[array]

          * {object}

            * id

string required

            * name

string required

            * description

string

            * kubernetesName

string required

      * nodePools

(multiple options: oneOf) required

An array of node pools for BYOC or BYOK.

        * [array]

An array of node pools for BYOC.

          * {object}

Node pool configuration for BYOC clusters

            * id

string required

ID of existing node pool. Must be passed when modifying existing node pools. Not relevant for new node pools

min length

3

max length

63

pattern

(^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$)|(^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-4[0-9a-fA-F]{3}-[89ABab][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$)

            * nodeType

string required

Machine type to be used by the node pool.

            * oci

{object}

OCI instance specific settings. Must respect ratios as determined by the selected node type.

              * ocpu

integer required

min

1

              * memory

integer required

min

1

            * gcp

{object}

GCP specific settings.

              * enablePrivateNodes

boolean

Set this flag to disable public IP assignment for nodes in this node pool.

            * azure

{object}

Azure specific settings.

              * systemPool

boolean

When 'provider' is 'azure', at least one system node pool is required per cluster.

              * enablePublicNodeIp

boolean

When 'provider' is 'azure', set this flag to use public node IPs.

              * vnetSubnetId

string

ID of the vnet subnet to use.

            * aws

{object}

AWS specific node pool settings.

              * launchTemplate

{object}

Specify a launch template to use for this node pool. When using a launch template, the disk size selection on the node pool level will be ignored.

                * id

string required

ID of the launch template to use.

                * version

integer required

Version of the launch template that should be used.

min

1

            * nodeCount

integer required

Number of nodes to the node pool should be provisioned with.

min

0

max

250

            * autoscaling

{object}

Auto scaling settings to use for the node pool. Requires that the cloud provider supports this feature.

              * enabled

boolean

              * min

integer

min

0

max

249

              * max

integer

min

1

max

250

            * computeResources

{object}

              * gpu

{object}

                * timeslicing

{object}

Time-slicing configuration object.

                  * enabled

boolean

Whether or not to enable time-slicing on the GPU.

                  * numSlices

number

Sets the amount of slices per GPU, e.g. how many pods may be scheduled concurrently on each GPU.

min

1

            * preemptible

boolean

Configures node pool with preemptible / spot instances if enabled.

            * diskType

string

The disk type to use.

            * diskSize

integer required

Disk size in GB

min

1

            * availabilityZones

[array] required

Zones in which the node pool should be provisioned.

              * string

            * subnets

[array]

Subnets in which the node pool should be provisioned. Required if provider is `oci`.

              * string

            * scheduling

{object}

Define basic workload scheduling restrictions for this node pool

              * allowJobs

boolean

Allow jobs to schedule to this node pool

              * onlyGpuJobs

boolean

Restrict job scheduling to jobs which have GPU resources configured. Only relevant for GPU node pools.

              * allowServices

boolean

Allow services to schedule to this node pool

              * onlyGpuServices

boolean

Restrict service scheduling to services which have GPU resources configured. Only relevant for GPU node pools.

              * allowAddons

boolean

Allow addons to schedule to this node pool

              * allowBuilds

boolean

Allow builds to schedule to this node pool

              * onlyGpuBuilds

boolean

Restrict build scheduling to builds which have GPU resources configured. Only relevant for GPU node pools.

              * allowCeph

boolean

Allow the placement of Ceph pods

            * labels

{object}

Set of label keys and values that can be used for advanced scheduling in combination with resource tag scheduling rules.

OR

        * [array]

An array of node pools for BYOK.

          * {object}

Node pool configuration for BYOK clusters

            * id

string required

ID of the node pool. Must be passed when modifying existing node pools. Not relevant for new node pools

min length

3

max length

63

pattern

(^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$)|(^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-4[0-9a-fA-F]{3}-[89ABab][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$)

            * providerId

string required

ID which identifies kubernetes nodes as belonging to this pool.

min length

3

max length

63

pattern

(^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$)|(^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-4[0-9a-fA-F]{3}-[89ABab][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$)

            * computeResources

{object}

              * gpu

{object}

                * supported

boolean

Whether this node pool consists of GPU nodes .

                * type

string

GPU type associated with the node pool.

pattern

[a-z0-9]

                * resources

{object}

                  * memoryInfo

{object}

                    * sizeInGiB

number

Memory amount of the GPU in Gib.

min

1

                * mig

{object}

Multi-Instance GPU (MIG). configuration object.

                  * enabled

boolean

Whether or not to enable Multi-Instance GPU (MIG).

                  * partitions

[array]

The partitions to configure on the GPU.

                    * string

                * timeslicing

{object}

Time-slicing configuration object.

                  * enabled

boolean

Whether or not to enable time-slicing on the GPU.

                  * numSlices

number

Sets the amount of slices per GPU, e.g. how many pods may be scheduled concurrently on each GPU.

min

1

                * count

integer

Number of GPUs per node.

min

1

            * defaultPool

boolean

Fallback pool to which nodes which do not match any defined node pool are assigned. Exactly one default pool is required.

            * preemptible

boolean

Configures node pool with preemptible / spot instances if enabled.

            * scheduling

{object}

Define basic workload scheduling restrictions for this node pool

              * allowJobs

boolean

Allow jobs to schedule to this node pool

              * onlyGpuJobs

boolean

Restrict job scheduling to jobs which have GPU resources configured. Only relevant for GPU node pools.

              * allowServices

boolean

Allow services to schedule to this node pool

              * onlyGpuServices

boolean

Restrict service scheduling to services which have GPU resources configured. Only relevant for GPU node pools.

              * allowAddons

boolean

Allow addons to schedule to this node pool

              * allowBuilds

boolean

Allow builds to schedule to this node pool

              * onlyGpuBuilds

boolean

Restrict build scheduling to builds which have GPU resources configured. Only relevant for GPU node pools.

              * allowCeph

boolean

Allow the placement of Ceph pods

            * labels

{object}

Set of label keys and values that can be used for advanced scheduling in combination with resource tag scheduling rules.

      * settings

{object}

        * builds

{object}

          * mode

string

one of

paas, internal, build-cluster

          * plan

string

Plan to use for builds if they are run on the cluster

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * clusterId

string

Cluster to use for scheduling builds

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * registry

{object}

          * mode

string

one of

paas, self-hosted

          * registryId

string

Credentials to use for storing of images.

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * logging

(multiple options: oneOf)

Logging settings

          * {object}

Logging via PaaS.

            * mode

string

one of

paas

OR

          * {object}

Logging via Loki (S3 storage).

            * mode

string required

one of

loki

            * loki

{object}

              * storageType

string required

one of

s3

              * s3BucketName

string required

              * s3AccessKey

string required

              * s3SecretKey

string required

              * s3Region

string required

OR

          * {object}

Logging via Loki (GCS storage).

            * mode

string required

one of

loki

            * loki

{object}

              * storageType

string required

one of

gcs

              * gcsBucketName

string required

              * gcpIntegrationId

string required

pattern

^((org|team)\/)?[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * vanityDomains

{object}

          * apps

{object}

            * zoneName

string required

            * integrationId

string required

          * customDomains

{object}

            * zoneName

string required

            * integrationId

string required

          * loadBalancers

{object}

            * zoneName

string required

            * integrationId

string required

        * infrastructure

{object}

          * workloads

{object}

            * runtimeClass

string

one of

none, gvisor, kata-clh, kata-qemu, katars-clh

          * builds

{object}

            * runtimeClass

string

one of

none, gvisor, kata-clh, kata-qemu, katars-clh

          * installKata

boolean

          * installGvisor

boolean

          * cleanupVolumes

boolean

          * cleanupSnapshots

boolean

          * cephStorageProvider

{object}

            * enabled

boolean

            * resources

{object}

              * cpu

number

Configure the CPU resources per Ceph replica

min

1

max

20

              * memory

number

Configure the memory resources per Ceph replica

min

4096

max

40960

              * storage

number

Configure the data disk size per Ceph replica

min

102400

max

5242880

            * enableMultiReadWriteStorage

boolean

Configure Ceph to be enable use of multi read write storage for persistent volumes on the cluster.

            * enableSingleReadWriteStorage

boolean

Configure Ceph to be used as default storage class for single read write storage. This will replace the default storage of the cloud provider.

            * enableErasureCoding

boolean

Configure Ceph to be set up with erasure coding. This will be less fault tolerant but more cost effective.

            * enableTopologyAwareScheduling

boolean

Configure Ceph to be set up with topology aware scheduling, enforcing deployment across multiple zones.

        * requestModifiers

{object}

Allows customising request modifier values.

          * services

{object}

Request modifiers for services

            * cpu

number required

min

0.2

max

1

            * memory

number required

min

0.4

max

1

          * jobs

{object}

Request modifiers for jobs

            * cpu

number required

min

0.2

max

1

            * memory

number required

min

0.4

max

1

          * builds

{object}

Request modifiers for builds

            * cpu

number required

min

0.1

max

1

            * memory

number required

min

0.1

max

1

          * addons

{object}

Request modifiers for addons

            * cpu

number required

min

0.2

max

1

            * memory

number required

min

0.4

max

1

      * restrictions

{object}

BYOC restrictions configuration for controlling team access

        * enabled

boolean required

Enable or disable BYOC restrictions for this entity

        * teams

[array]

List of teams that have access to this BYOC cluster

          * {object}

            * teamId

string required

The ID of the team that has access to this BYOC cluster

min length

3

max length

45

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * gcp

{object}

GCP specific data. Required when `provider` is `gcp`

        * networking

{object}

          * network

string

          * subnetwork

string

        * enableAuthorizedIpRanges

boolean

        * authorizedIpRanges

[array]

          * string

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\/([0-9]|[1-2][0-9]|3[0-2]))$

        * projectId

string

GCP Project ID

pattern

^[a-z][a-z0-9-]{4,28}[a-z0-9]$

      * aws

{object}

AWS specific data. Required when `provider` is `aws`.

        * enablePublicAccessCidrs

boolean

        * publicAccessCidrs

[array]

          * string

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\/([0-9]|[1-2][0-9]|3[0-2]))$

        * subnetConfiguration

{object}

          * mode

string required

The mode of the AWS subnet configuration

one of

default-subnets-for-azs, explicit-subnets

          * vpcId

string

Id of the VPC

          * subnets

[array] required

List of subnets the cluster should be created for. At least 2 must be specified.

            * string

        * vpcEgress

boolean

If egress traffic from the cluster should come from a single static egress IP.

      * oci

{object}

OCI specific data. Required when `provider` is `oci`.

        * vcnConfiguration

{object} required

          * vcnId

string required

          * subnetIdForKubernetesApi

string required

          * subnetIdsForServiceLBs

[array] required

            * string

      * azure

{object}

Azure specific data. Required when `provider` is `azure`.

        * networking

{object}

          * vnetConfiguration

{object}

            * mode

string required

The vnet mode to use for this cluster. Use this to switch between creation of a new vnet per cluster or specifying a custom vnet.

one of

create-default, custom-vnet

            * vnetId

string

Azure vnetId that should be used for this cluster. By default a new vnet will be created.

          * networkPluginMode

string

Optional setting to configure overlay mode on Azure.

one of

overlay

        * enableAuthorizedIpRanges

boolean

        * authorizedIpRanges

[array]

          * string

pattern

^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\/([0-9]|[1-2][0-9]|3[0-2]))$

      * byok

{object}

BYOK specific data. Required when `provider` is `byok`.

        * nodePoolProviderIdLabel

string required

      * id

string required

The ID of cluster

      * status

{object}

        * state

{object}

          * state

string

          * transitionTime

string

        * nextUpdateAfter

string

      * dns

string

Auto-generated dns identifier for this cluster.

      * updatedAt

string required

The time the cluster was last updated.

      * createdAt

string required

The time the cluster was created.

      * deletionRequested

boolean required

Indicates if provider resource deletion has been requested.




API

CLI

JS Client

PATCH /v1/cloud-providers/clusters/{clusterId}

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request PATCH \
      --data '{"name":"GCP Cluster 1","description":"This is a new cluster.","kubernetesVersion":"1.30","nodePools":[{"id":"6aa96121-0345-43ad-bade-af36d540c222","nodeType":"n2-standard-8","nodeCount":3,"autoscaling":{"enabled":true,"min":0,"max":10},"preemptible":false,"diskSize":100}],"settings":{"builds":{"plan":"nf-compute-200"},"registry":{"registryId":"my-registry-credentials"},"requestModifiers":{"services":{"cpu":0.5,"memory":0.8},"jobs":{"cpu":0.5,"memory":0.8},"builds":{"cpu":0.2,"memory":0.5},"addons":{"cpu":0.5,"memory":0.8}}},"aws":{"subnetConfiguration":{"subnets":["eu-west-1a"]}}}' \
      https://api.northflank.com/v1/cloud-providers/clusters/{clusterId}

Example response

200 OK

Details about the updated cluster.

JSON
    
    
    {
      "data": {
        "name": "GCP Cluster 1",
        "description": "This is a new cluster.",
        "provider": "gcp",
        "region": "europe-west2",
        "kubernetesVersion": "1.30",
        "integrationId": "gcp-integration",
        "nodePools": [
          {
            "id": "6aa96121-0345-43ad-bade-af36d540c222",
            "nodeType": "n2-standard-8",
            "nodeCount": 3,
            "autoscaling": {
              "enabled": true,
              "min": 0,
              "max": 10
            },
            "preemptible": false,
            "diskSize": 100
          }
        ],
        "settings": {
          "builds": {
            "plan": "nf-compute-200"
          },
          "registry": {
            "registryId": "my-registry-credentials"
          },
          "requestModifiers": {
            "services": {
              "cpu": 0.5,
              "memory": 0.8
            },
            "jobs": {
              "cpu": 0.5,
              "memory": 0.8
            },
            "builds": {
              "cpu": 0.2,
              "memory": 0.5
            },
            "addons": {
              "cpu": 0.5,
              "memory": 0.8
            }
          }
        },
        "aws": {
          "subnetConfiguration": {
            "subnets": [
              "eu-west-1a"
            ]
          }
        },
        "id": "gcp-cluster-1",
        "status": {
          "state": {
            "state": "initial",
            "transitionTime": "2024-05-03T16:40:38.198Z"
          }
        },
        "dns": "xxxxxxxxxx",
        "updatedAt": "2021-01-20T11:19:53.175Z",
        "createdAt": "2021-01-20T11:19:53.175Z",
        "deletionRequested": false
      }
    }