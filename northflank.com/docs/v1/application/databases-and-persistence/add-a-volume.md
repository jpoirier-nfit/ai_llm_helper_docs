---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/add-a-volume
title: Add a persistent volume | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.336745
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Add a persistent volume

Volumes can be added to your deployment services to persist data across restarts. This can be useful if you require a storage solution other than the available [databases](./deploy-a-database). Volumes are highly configurable and can be moved between services.

Adding a volume to a deployment will limit that service to 1 instance, and during restarts the running container will always be terminated before the new one starts (regardless of any health check settings).

Persistent volumes use SSDs for best performance.

Create a persistent volume

You can create a volume on the volumes page of a [combined or deployment service](../run/run-containers-and-micro-services). Select `add volume`, choose a name, and select the size of the volume to create. Volume storage cannot be scaled down after creation.

You must add at least one container mount path, and optionally a volume mount path.

You can attach multiple volumes to the same service.

![Configuring a persistent volume in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/add-a-volume/edit-volume.png)

Volume mount configuration

You can add multiple mount rules for each volume to determine how the volume is mounted and accessed.

#### Container mount path

The container mount path allows you to specify where to make the volume available in the running container for a service. Anything your application reads and writes to the path will be written or read from the volume.

For example, using the path `/data` means any files in `/data` or subdirectories of `/data` will be written to or read from the volume. The container mount path is absolute, and must start from the container root (`/`).

#### Volume mount path

The volume mount path is optional and allows you to specify a directory on the volume to mount, rather than the volume root. The volume mount path is relative, and cannot start from root (`/`).

You can use this to persist data in multiple directories in a service on the same volume. Any data written or read from the container mount path will be written or read to the volume mount path.

Container mount path| Volume mount path| Volume directory used| Result  
---|---|---|---  
`/data`| -| `/`| The whole volume is mounted to the container path `/data`  
`/data/config`| `config`| `config`| The volume directory `config` is mounted to the container path `/data/config`  
`/data/logs`| `logs`| `logs`| The volume directory `logs` is mounted to the container path `/data/logs`  
  
Permissions

Ownership of persistent volumes will be given to the group specified in the Docker image, determined at build time. This may cause issues if your application attempts to read, write, or execute with a different user. You can designate the user and group the image will use in your Dockerfile with the command `USER <user>:<group>`.

To avoid permissions issues and to not overwrite any existing data from the image you should mount the volume only to the specific path(s) you require. For example if you mount a volume to `/app/data` your application may try to write data to that path and encounter permission errors, which may crash your application. If, in this case, you only need to persist data written to `/app/data/logs`, you should mount to that specific path instead. You can use volume mount paths to mount to multiple paths using the same volume.

If you are experiencing application issues with permissions, you can include a script as part of your application startup to run the `chown` command and change the directory to the required ownership and permissions: `chown -R <user>:<group> /<container-mount-path>`.

Alternatively you can set a [custom entrypoint and command](../run/override-command-entrypoint) for the deployment, with the entrypoint as `bash -c` and the command as `"chown -R <user>:<group> /<container-mount-path> && <default startup command>"`

Scale a volume

To scale an attached volume, navigate to the volumes page of the service that has the volume attached. To scale a detached volume, navigate to any service's volumes page.

Select edit volume `` and open the `storage` dropdown to resize the volume. Volume storage cannot be scaled down.

Move or delete a volume

Volumes can be detached `` on the volumes page of the service they are currently linked to. Detaching a volume will redeploy any running containers in the service.

A volume must be detached from its current service before being attached to another. Attach a volume to another service by navigating to the detached section on the volumes page of the service you want to link it to and select `` on the volume to attach. Attaching a volume will redeploy any running containers in the service.

Volumes can be deleted by first detaching them, and then selecting delete ``.

Transfer data to and from a volume

You can transfer data to and from a persistent volume when it is mounted to a running service using commands like curl or wget. See [transfer data to and from containers](../run/transfer-data-to-and-from-containers) for more detail.

Next steps

[Deploy a databaseCreate a database to use with your Northflank deployments.](/docs/v1/application/databases-and-persistence/deploy-a-database)[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)[Transfer data to and from containersDownload data from, or to, ephemeral or persistent storage in your running containers.](/docs/v1/application/run/transfer-data-to-and-from-containers)