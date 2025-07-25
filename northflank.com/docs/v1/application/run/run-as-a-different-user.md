---
source_url: https://northflank.com/docs/v1/application/run/run-as-a-different-user
title: Run as a different user | Run | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.408183
watsonmd_version: 0.1.0
---

Run / 

# Run as a different user

Docker images have their own filesystem and user management system, with their own user and group IDs. You may need to run commands in a container as a different user, or build your image with permission changes to run your application successfully.

Most base images will use `root` as the default user, and any commands in the Dockerfile will run as the default user. Some images may set another user with reduced permissions as default for extra security.

Run a command as a different user

You can change the user that runs your Docker command (`CMD`) when your container deploys, either in the Dockerfile or by using Northflank's [CMD override](override-command-entrypoint). You may need to [invoke a shell](override-command-entrypoint#execute-shell-commands) depending on your image's configured entrypoint, and the user needs to exist in the built image (or must be created).

For example, the Dockerfile below creates the user `notRoot`, but the default command will still execute as `root`.
    
    
    FROM ubuntu:24.04
    RUN useradd -m -s /bin/bash notRoot
    CMD ["bin/bash", "-c", "whoami"]
    

To run the command as a different user, you can include a `USER` command in your Dockerfile:
    
    
    FROM ubuntu:24.04
    RUN useradd -m -s /bin/bash notRoot
    USER notRoot
    CMD ["bin/bash", "-c", "whoami"]
    

The container will start with the user `notRoot`, and this user will be used to execute any future commands in the container.

Alternatively, you can supply a [custom entrypoint and command](override-command-entrypoint) which specifies the user `notRoot` to execute the command. This is useful if you cannot, or do not want to, modify the Dockerfile.

Entrypoint| Command  
---|---  
`bin/bash -c`| `"su - notRoot -c "whoami"`  
  
### Execute a command in the shell as a different user

You can execute a command in a running container either via the [shell in the Northflank application](access-running-containers-locally#execute-commands-in-a-container), using the [CLI, API, or JavaScript Client](../../api/execute-command), or [in a template](access-running-containers-locally#execute-commands-in-an-action-node).

The shell invoked for a container will be the default shell for the user, and the user will be the default for the image. You can switch user, or open another shell, before executing your commands. Some shell scripts may only work with specific shells, for example a script may work when executed with `bash` but not `sh`.

note

You will not be able to switch from a non-root user to root. You will have to modify the Dockerfile to use root, or switch to a different user with the necessary permissions.

Change file ownership and permissions

The ownership of files in your built Docker image is determined by the commands in your Dockerfile and the permissions depend on the original source files copied during the build process.

For example, the following Dockerfile command will copy `setup.sh` from the source (the cloned repository). The command is executed by the default user `root` and the copied file is owned by the same user (`root`).
    
    
    FROM ubuntu:24.04
    COPY /init/setup.sh /scripts/
    CMD ["/bin/bash", "-c", "/scripts/setup.sh"]
    

Git only tracks whether a file is executable or not. If the source file is not created or modified to be executable, then this permission will persist into the build image. You will not be able to execute a file until it is made executable (`chmod +x`).

note

You can change the user for subsequent commands in your Dockerfile with `USER`, however Docker will always copy files as the root user. Ownership must be changed after the files are copied.

Learn more about the [USER ](https://docs.docker.com/reference/dockerfile/#user), [COPY ](https://docs.docker.com/reference/dockerfile/#copy), and [ADD ](https://docs.docker.com/reference/dockerfile/#copy) commands.

You can the ownership or permissions of files using the `RUN` command in your Dockerfile, as long as the current user has sufficient permissions. For example, the following commands are executed by the default user `root` to change ownership of `setup.sh` and make it executable. The default user is then set to `notRoot`, which will start the container with the `CMD`.
    
    
    FROM ubuntu:24.04
    
    COPY /init/setup.sh /scripts/
    RUN useradd -m -s /bin/bash notRoot
    
    RUN chown notRoot:notRoot /scripts/setup.sh
    RUN chmod +x /scripts/setup.sh
    
    USER notRoot
    CMD ["/bin/bash", "-c", "/scripts/setup.sh"]
    

### Change permissions in a running container

You can also execute commands to change file ownership and permissions in a running container, either via the [shell in the Northflank application](access-running-containers-locally#execute-commands-in-a-container), using the [CLI, API, or JavaScript Client](../../api/execute-command), or [in a template](access-running-containers-locally#execute-commands-in-an-action-node).

### Change permissions and ownership in a shell script

You may need to make a file executable, or change the ownership of a [volume mount path](../databases-and-persistence/add-a-volume#permissions). To achieve this you can add a shell script that runs on container startup, before executing your normal application startup command. You can also include the shell script as a [secret file](../secure/upload-secret-files) and call it using a command override.

For example, the following changes the ownership of the directory `/path` to `notRoot` and then runs the normal startup command for the application. To execute these commands the user should be root, either from the image default user or specified in the Dockerfile.
    
    
    #!/bin/bash
    
    chown -R notRoot:notRoot /path
    <application start command>
    

Alternatively you can set a [custom entrypoint and command](override-command-entrypoint) for the deployment.

Entrypoint| Command  
---|---  
`bin/bash -c`| `"chown -R notRoot:notRoot /path && <application start command>"`  
  
Next steps

[Override command or entrypointOverride the default command or entrypoint instructions for your application.](/docs/v1/application/run/override-command-entrypoint)[Add a persistent volumeAdd persistent volumes to your deployments.](/docs/v1/application/databases-and-persistence/add-a-volume)[Upload a secret fileAdd secret files that will be mounted in your container.](/docs/v1/application/secure/upload-secret-files)[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)