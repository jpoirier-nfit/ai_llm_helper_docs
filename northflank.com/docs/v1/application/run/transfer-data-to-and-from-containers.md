---
source_url: https://northflank.com/docs/v1/application/run/transfer-data-to-and-from-containers
title: Transfer data to and from containers | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.415188
watsonmd_version: 0.1.0
---

Run / 

# Transfer data to and from containers

You can transfer data to and from a container's ephemeral storage, or migrate data to and from a persistent volume.

If you want to transfer on a persistent volume and your service does not support the methods below, you can temporarily detach the volume from the existing service and attach it to one that does to transfer the data.

You can compress directories or groups of files to make downloading or uploading them quicker and simpler, especially if you have a large number of files to transfer. Compressing and uncompressing archives may require increased [compute resources](../scale/scale-cpu-and-memory).

Transfer data using Northflank

You can use the [Northflank CLI](/docs/v1/api/use-the-cli) or [JavaScript client](/docs/v1/api/use-the-javascript-client) to transfer data between your local machine and running jobs or services.

For guidance on uploading or downloading files and directories with the CLI or JavaScript client, see [this documentation](/docs/v1/api/copy-files).

Transfer data using curl or wget

You can use [curl ](https://curl.se/docs/manpage.html) or [wget ](https://www.gnu.org/software/wget/manual/wget.html) to download data from an external host to your containers and persistent volumes on Northflank. Similarly, you can transfer data from your containers or persistent volumes to external destinations.

You can execute a curl or wget command in a running container either via the [shell in the Northflank application](access-running-containers-locally#execute-commands-in-a-container), using the [CLI, API, or JavaScript Client](../../api/execute-command), or [in a template](access-running-containers-locally#execute-commands-in-an-action-node).

### Download data using curl or wget

You can run a curl or wget command in your container to retrieve data from an external source:
    
    
    curl -O https://example.com/path/data.zip
    
    
    
    wget https://example.com/path/data.zip
    

You can also recursively download directories with wget: `wget -r http://example.com/files/`

You can upload files to S3 storage or other file-hosting services, or run a HTTP server locally to serve files from your machine (when combined with forwarding).

Similarly, you can serve files from your container using a HTTP server, and retrieve them using curl or wget. You can either configure your application to serve files over HTTP, or attach your volume to another service that does.

### Send data using curl or wget

You can also send data from your container using curl to an endpoint that accepts file uploads.
    
    
    curl -X POST -F "file=@/path/data.zip" https://example.com/upload`
    
    
    
    wget --method=POST --body-file=/path/data.zip https://example.com/upload
    

#### Example simple HTTP server

You can create a quick HTTP file server simply by running `python3 -m http.server`.

To deploy this on Northflank, create a deployment service with the external image `python:latest`, expose port `8000`, and set the command override to `python3 -m http.server` to serve the entire filesystem, or set the entrypoint to `/bin/sh -c` and the command to `"cd /your/path && python3 -m http.server` to serve a specific directory.

Transfer data using rsync

You can connect to a container running an [rsync daemon ](https://man7.org/linux/man-pages/man1/rsync.1.html) from your local machine to download and upload files from the container's filesystem or an attached volume.

You can create a deployment service with [an rsyncd image ](https://hub.docker.com/r/alpinelinux/rsyncd) and attach the volume you want to access to it, or install and run rsyncd inside a running container using the [shell](access-running-containers-locally#execute-commands-in-a-container) if your image supports it.

You will need to have installed rsync on your local machine, as well as the [Northflank CLI](../../api/use-the-cli) to securely forward the deployment.

### Deploy an rsyncd image

To deploy rsyncd on Northflank, create a deployment service, choose external image and set the path to `alpinelinux/rsyncd:latest`, or another rsyncd image. Add `873` as a TCP port in networking.

In the service's runtime variables, expand `advanced` and create two secret files, mounted to `/etc/rsyncd.conf` and `/etc/rsyncd.secrets`.

#### rsyncd.conf

You can [specify a configuration ](https://www.man7.org/linux/man-pages/man5/rsyncd.conf.5.html) for each path you want to make accessible via rsync, and provide rules for that configuration. In the example below, the rsync configuration `data` makes the `/data` path and its contents available to the user `username`.
    
    
    [default]
    path = /data
    comment = Northflank volume access
    read only = no
    write only = no
    list = yes
    uid = root
    gid = root
    auth users = username
    secrets file = /etc/rsyncd.secrets
    

#### rsyncd.secrets

The secrets file contains login details for you to access the container using rsync. The file is line-based and contains one `username:password` pair per line.
    
    
    username:password
    

After deploying rsyncd, attach one or more volumes that you want to access to it, with the corresponding mount paths.

### Connect to rsyncd

[Forward](../../api/forwarding) the rsyncd service to your local machine using the Northflank CLI to make it available at `<service-name>:873`. The full rsync address for commands takes the format `<username>@<service-name>::<config_name>`, for example `northflank@rsync::default`.

You can now run rsync commands against the Northflank rsync deployment. For example:

  * `rsync -avz username@rsync::default ./data` recursively downloads all files from the path specified in the configuration `default` to the local directory `data`
  * `rsync -rltv ./data/ username@rsync::default` recursively uploads all files from the local directory `data` to the path specified in the configuration `default`



Transfer data securely

You can securely [forward your service](../../api/forwarding) to your local machine. This will allow you to send and receive data without making it available on the internet. You will need to run a HTTP server locally to use wget and curl.

### Securely transfer data with wget and curl

Both wget and curl support [basic authentication and bearer tokens](../network/create-path-based-security-policies#require-credentials) to secure transfers.

#### Basic authentication

    
    
    curl -u username:password -O https://example.com/path/data.zip
    
    
    
    wget --user=username --password=password https://example.com/path/data.zip
    

#### Bearer token

    
    
    curl -H "Authorization: Bearer <your-token>" -O https://example.com/path/data.zip
    
    
    
    wget --header="Authorization: Bearer <your-token>" https://example.com/path/data.zip
    

Next steps

[Override command or entrypointOverride the default command or entrypoint instructions for your application.](/docs/v1/application/run/override-command-entrypoint)[Add a persistent volumeAdd persistent volumes to your deployments.](/docs/v1/application/databases-and-persistence/add-a-volume)[Upload a secret fileAdd secret files that will be mounted in your container.](/docs/v1/application/secure/upload-secret-files)[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)