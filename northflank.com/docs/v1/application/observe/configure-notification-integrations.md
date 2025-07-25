---
source_url: https://northflank.com/docs/v1/application/observe/configure-notification-integrations
title: Configure notification integrations | Observe | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.134072
watsonmd_version: 0.1.0
---

Observe / 

# Configure notification integrations

You can create integrations with external services like Slack and Discord to receive alerts when specified events, such as backups, job runs, or billing events occur on the Northflank platform.

You can also configure notifications to be sent to a webhook URL to create your own integrations and workflows.

[Click here ](https://app.northflank.com/s/account/integrations/notifications) to view your account notifications page.

### Infrastructure alerts

You can select [infrastructure alerts](set-infrastructure-alerts) to be sent to your notification integration. These alerts trigger notifications when certain your running containers crashes, have high CPU and memory usage, or when volumes have limited space available.

You can configure how often infrastructure alerts are generated on the alerts page in your account settings.

### Types of notification integrations

  * Slack: send formatted notifications to a Slack channel or user
  * Discord: send formatted notifications to a Discord channel
  * Teams: send formatted notifications to a Microsoft teams channel
  * Webhook: send notifications to a HTTP endpoint for processing



![Creating a webhook notification integration in the Northflank application](https://assets.northflank.com/documentation/v1/application/observe/configure-notification-integrations/create-webhook-notification-integration.png)

Filter events

You can filter events by type and by project.

Select the type of events you want to be notified about when creating or editing the integration. You can receive alerts for different events in various categories, such as a new build starting or a new job run beginning.

You can also receive notifications for specific projects. Enable the `handle events only from specific projects` and select one or more projects you want to receive notifications for.

Slack notifications

You can create or update a [Slack ](https://slack.com/) integration from the notifications page in your account/team settings. You may need to be an owner of the workspace to grant the Northflank notifications application access.

  1. Select the Slack integration type and the types of event you want to receive notifications about. Enable `handle events only from specific projects` if you want to restrict the integration to selected projects.
  2. Click `create notification integration` to be taken to the Slack integration page. Ensure the correct workspace is selected and select a channel, user, or group to send notifications to and click `allow`.



Your selected Slack channel should now receive the configured alerts whenever an event triggers them.

You can edit the events that will send a notification to your Slack channel, or restrict/unrestrict alerts to certain projects. If the integration is removed from your Slack channel, or you want to change the channel that will receive alerts, you can `reinstall` it.

Discord notifications

You can create or update a [Discord ](https://discord.com/) integration from the notifications page in your account/team settings. You need to have the `manage webhooks` permissions on the server that you want to send notifications.

  1. Select the Discord integration type and the types of event you want to receive notifications about. Enable `handle events only from specific projects` if you want to restrict the integration to selected projects.
  2. In Discord, either `edit channel` or select `integrations` and `view webhooks` from server settings. Select `new webhook` and give it a recognisable name, like `Northflank notifications bot` or `Northflank project X`, and select the channel it will post notifications in. You can also add an avatar, such as your own team/project logo.
  3. Click `copy webhook URL`, return to Northflank, and paste it in the `webhook URL` field in the Northflank form
  4. Click `create notification integration`, and your Discord channel should receive a notification to confirm the integration



Your channel will now receive the configured alerts whenever an event triggers them.

You can edit the events that will send a notification to your Discord channel, or restrict/unrestrict alerts to certain projects. If the webhook is deleted in Discord, or you want to change the channel it posts to, create a new webhook and update the webhook URL in the Northflank integration.

Teams notifications

You can create or update a [Teams ](https://www.microsoft.com/en-gb/microsoft-teams/group-chat-software) integration from the notifications page in your account settings. You will require permission in the workspace to manage connectors.

  1. Select the Teams integration type and the types of event you want to receive notifications about. Enable `handle events only from specific projects` if you want to restrict the integration to selected projects.
  2. Open the channel you want to send notifications to in Microsoft Teams, click the options menu `` and select `connectors`
  3. Search for and `add` the [Incoming Webhook ](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook) connector, then `configure` it
  4. Copy the generated webhook URL and paste it into the `webhook URL` field in the Northflank form and then click `create notification integration`



Your channel will now receive the configured alerts whenever an event triggers them.

You can edit the events that will send a notification to your Teams channel, or restrict/unrestrict alerts to certain projects. If the connector is deleted in Teams, or you want to change the channel it posts to, create a new connector and update the webhook URL in the Northflank integration.

Webhook notifications

You can create a webhook notification integration to send events to a HTTP endpoint for processing. This can be a powerful tool for automating workflows involving Northflank, especially when combined with the [Northflank API](../../api).

You can create or update a webhook integration from the notifications page in your account/team settings.

Select the webhook integration type and enter your webhook URL, and your secret (if required). You can update these later.

You can select the types of event you want to receive notifications about and choose to only receive notifications about events in specific projects, if required.

You could use a webhook notification integration to alert your app:

  * That a job has failed, so your app can create a ticket in your bug tracking software
  * That a backup has succeeded, so your app can download the backup via the Northflank API and store it in an off-site backup system



### Webhook secrets

You can add a secret to your webhook to ensure the request originated from your Northflank notification integration.

Either generate a secret yourself, or generate one on Northflank using the random secret generator `` in the form field.

You can then add this secret to your webhook endpoint application. If your workload is deployed on Northflank, you can add it either as a [runtime variable](../secure/inject-secrets) or in a [secret file](../secure/upload-secret-files).

The secret will be sent to your endpoint as the `X-Northflank-Notification-Integration-Token` header. You can compare the value in the header to your secret to confirm the webhook request is legitimate.

### Request format

Notifications are sent to webhooks as `POST` requests containing the following:

#### Headers

  * `X-Northflank-Notification-Integration-Id` \- ID of the notification integration that the request originated from
  * `X-Northflank-Notification-Integration-Name` \- Name of the notification integration that the request originated from
  * `X-Northflank-Notification-Integration-Token` \- Secret associated with the notification integration that the request originated from.
  * `X-Northflank-Notification-Integration-Event-Id` \- ID of the event contained within the request
  * `X-Northflank-Notification-Integration-Event-Type` \- Type of event contained within the request, e.g. `build:start`



#### Body

Requests contain a JSON encoded body containing the following properties:

  * `event` \- The type of the event, e.g. `build:start`
  * `data` \- An object containing data related to the event



The following is an example of the data you may receive in the body of the request when a build is started:
    
    
    {
      "event": "build:start",
      "data": {
        "build": {
          "id": "social-hour-1312",
          "branch": "master",
          "pullRequestId": null,
          "status": "STARTING",
          "sha": "ca624abed0d5ba0ad6e6fe28c396196b81f0200d",
          "concluded": false,
          "createdAt": "2022-01-19T09:04:40.916Z"
        },
        "service": {
          "id": "website",
          "name": "Website"
        },
        "project": {
          "id": "personal-blog",
          "name": "Personal Blog"
        },
        "user": {
          "id": "thomas"
        }
      }
    }
    

### Error handling

To indicate a webhook has successfully handled a notification it should respond to the request with a `2xx` status code.

If a webhook does not respond with a `2xx` status code the associated notification integration will be marked as failing and the notification will be resent a limited number of times until it is handled successfully or the limit is reached.

Webhooks that continuously fail to handle notifications successfully will be automatically disabled.

#### Recent events

You can find a list of all requests sent to your webhook and their current status when viewing the webhook notification integration.

Click on a specific request to see the request headers and body, as well as a list of the responses received and their status code.

Failing webhooks will be automatically resent several times, and you can also manually resend a webhook request from the event page.

You can expand a response to see the webhook URL, response headers and response body.

### Example webhook handler

The following is an example of a webserver, written using [Express ](https://expressjs.com/), that handles notifications sent via a webhook:
    
    
    // This example uses Express to setup a webserver to receive webhooks.
    const express = require('express');
    const app = express();
    app.use(express.json());
    
    // Setup an endpoint to receive webhooks.
    app.post('/webhook', (request, response) => {
      // Check the request originated from Northflank and reject any that do not.
      const receivedSecret = request.get('X-Northflank-Notification-Integration-Token');
      const actualSecret = process.env.NOTIFICATION_INTEGRATION_SECRET;
    
      if (receivedSecret !== actualSecret) {
        response.sendStatus(401);
        return;
      }
    
      // Handle the different events.
      const { event, data } = request.body;
    
      switch (event) {
        case 'build:start':
          const { project, service, build } = data;
          console.log({ project, service, build });
          // Then define and call a method to handle the event.
          // handleBuildStarted(project, service, build);
          break;
    
        // ... handle other events.
        default:
          console.log(`Unhandled event ${event}.`);
      }
    
      // Flag the notification as being handled successfully.
      response.sendStatus(200);
    });
    
    // Start the webserver.
    app.listen(3000, () => console.log('Running on port 3000.'));
    

Next steps

[Infrastructure alertsSet infrastructure alerts to let you and your team know when there is an issue with your applications or addons.](/docs/v1/application/observe/set-infrastructure-alerts)[Configure health checksMonitor the uptime and success of your deployed services and builds to ensure your code runs correctly and is always available.](/docs/v1/application/observe/configure-health-checks)[View logsView detailed, real-time logs from builds, deployments, and more.](/docs/v1/application/observe/view-logs)[Monitor containersMonitor the health and resource usage of deployments, and view detailed logs and metrics for individual container.](/docs/v1/application/observe/monitor-containers)