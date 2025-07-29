---
source_url: https://northflank.com/docs/v1/application/observe/configure-health-checks
title: Configure health checks | Observe | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.119776
watsonmd_version: 0.1.0
---

Observe / 

# Configure health checks

Health checks allow you to configure tests to ensure maximum availability of your services. These health checks can be configured so that incoming traffic is only routed to available and healthy containers, and that containers which fail health checks are automatically terminated and restarted.

Without configured health checks Northflank will still try to warn about containers with failing processes, but as long as the container is able to run it will not be automatically restarted if there is an issue. You must ensure that your health checks are correctly configured for the code you are deploying, as incorrectly configured health checks may stop containers from receiving traffic, or terminate containers before they have a chance to become healthy, rendering your service unavailable.

The code deployed to your service or job must be configured to respond on the path, or successfully run the given command, set in the health check.

Health checks can be viewed and added on the health checks page of any service or job, excluding build services. Addons have pre-configured health checks.

![Creating a readiness probe for a deployment service in the Northflank application](https://assets.northflank.com/documentation/v1/application/observe/configure-health-checks/readiness-probe.png)

Types of health check

You can configure up to three health checks for a service or job, one of each probe type. You may only require one probe, or you may need to configure a combination of probes to ensure your containers are tested properly.

#### Liveness probe

A liveness probe will regularly test a given endpoint of a service, or run the specified command, to make sure a container is available and healthy. If the check fails the container will be marked for termination and a new container will be initialised.

#### Readiness probe

You can add a readiness probe to test if a container is ready to receive traffic. Network requests will not be sent to the container until the check passes and the probe will continue to run throughout the life of the container. If it fails at any point, the container will be removed from the load balancer and no longer serve traffic, avoiding dropped requests.

#### Startup probe

Startup probes delay any configured readiness and liveness probes until the startup probe succeeds. You can configure a startup probe for applications that take a long time to become ready after the container is started, or that have a varying startup time. Startup probes enable you to use a different endpoint or command, and different initial delays from your other probes, and can help you create efficient health checks to test your containers at the right times, so failing containers can be replaced as soon as possible. If the check fails the container will be marked for termination and a new container will be initialised.

Health check protocols

Probes can either check a HTTP endpoint, a TCP endpoint, or run a command in the container.

The protocol you should use depends on the service or application you want to test. For example, you may want to configure a HTTP probe for a web application, and a TCP or CMD probe for a microservice that doesn't serve HTTP requests.

#### HTTP

HTTP probes will send a GET request which passes if the response has a status code greater than or equal to 200 and less than 400. The path should be defined relative to the root of the service, for example `/healthz` to check the endpoint `localhost:[port]/healthz`.

#### TCP

TCP probes will test whether a connection can be made and gracefully terminated at the specified port.

#### CMD

CMD probes will execute the specified command inside the container which passes if command exits with a status code of 0. The CMD is executed in the container and passes if the command succeeds, for example `/bin/sh -c "cat /tmp/healthz"`.

Create a health check

You can create a new health check from the health checks page of a combined or deployment service, or any job. You can also add a health check when creating a service or job in the advanced section.

Click `add health check` and select the type of health check you want to create. Only one of each type of health check can be added per service.

Choose which protocol to test the container by: HTTP, TCP, or CMD. If using HTTP, enter the endpoint to test, if using CMD, enter the command to run.

Use the dropdown menu to select the port to test (for HTTP and TCP), or enter it manually. The port must be exposed by your application, but does not need to be exposed in Northflank port configuration, as the request is made inside the container.

Click `save changes` to create or update the health checks, or `add health check` to add another.

Advanced configuration

You can also configure the following options by expanding the advanced menu in a health check:

  * Initial delay: set the time (in seconds) to wait from container initialization before making the first check
  * Interval: set the time (in seconds) to wait between checks
  * Timeout: set the time (in seconds) to wait for a response from the container
  * Max failures: specify the maximum number of attempts to check the container before failing.
  * Success threshold: set the number of successful checks required for a readiness probe to pass



Set up a probe endpoint

Health check probes can be as simple as testing a HTTP endpoint that is configured to return a 200 OK response. This could be a designated path (for example `/healthz`), or the site root (`/`).

For example, a healthcheck endpoint in Express.js could look something like this:
    
    
    app.get('/healthz', (req, res) => {
      res.status(200).send('OK');
    });
    

A more complex readiness probe might test a connection to a database before returning an OK response. The example below uses a hypothetical`testConnection` method on a database module (`db`) that would check your database is accessible.
    
    
    app.get('/healthz', (req, res) => {
      const database = db.testConnection();
      if (database === 'OK') {
        res.status(200).send('OK');
      } else {
          res.status(500).send('Database connection failed');
      }
    });
    

Probes using a command to test for healthiness execute the given command inside the container, and pass if the exit code is ok (returns `0`). For example, you could configure your application to create a file by running a shell script when it initialises (`touch /tmp/healthz`). Your startup probe can then check this file exists to confirm your application has initialised (`cat /tmp/healthz`).

TCP probes only require a port to be exposed by your container.

Below is an example of three configured health checks, from a [Northflank template]().
    
    
        "healthChecks": [
          {
            "protocol": "HTTP",
            "type": "livenessProbe",
            "port": 80,
            "path": "/healthz",
            "initialDelaySeconds": 10,
            "periodSeconds": 60,
            "timeoutSeconds": 3,
            "failureThreshold": 2,
            "successThreshold": 1
          },
          {
            "protocol": "TCP",
            "type": "readinessProbe",
            "port": 80,
            "initialDelaySeconds": 10,
            "periodSeconds": 10,
            "timeoutSeconds": 3,
            "failureThreshold": 2,
            "successThreshold": 1
          },
          {
            "protocol": "CMD",
            "type": "startupProbe",
            "cmd": "cat /tmp/healthy",
            "initialDelaySeconds": 5,
            "periodSeconds": 30,
            "timeoutSeconds": 10,
            "failureThreshold": 3,
            "successThreshold": 1
          }
        ],
    

Monitor a health check

Individual container health checks can be viewed in:

  * a combined or deployment service by selecting an entry from the [list of containers for a deployment](./monitor-containers#observe-deployments), on the observe page
  * an addon by selecting an entry from the containers list
  * a job by selecting an entry from the list of containers for a job run



The health check page displays each configured health check sorted by type, with the details of the result (such as latency and response), and the last time the status of the health check changed.

You can only view health checks for individual containers. Health checks for builds simply show the build status.

The list of containers will also include a column with the number of passing health checks.

Learn more

[More about health checksHealth checks use Kubernetes probes to test containers. Learn more about them here.](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)