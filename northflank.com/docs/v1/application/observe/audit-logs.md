---
source_url: https://northflank.com/docs/v1/application/observe/audit-logs
title: Audit logs | Observe | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.183694
watsonmd_version: 0.1.0
---

Observe / 

# Audit logs

Audit logs provide a record of events on your Northflank teams and organisation. They provide accountability and transparency, can help you identify issues with your workflow, and enable you to verify that actions were taken by the correct entities.

Log content

The audit log contains a live feed of all events, according to the scope of the log, which can also be filtered.

Each log contains the type of event, the user that triggered it, the event source, a timestamp, and any parent events. Differences are shown in individual event logs.

You can click a log to view it in more detail, or select the event, user, or source to filter by that value.

### Affected resources

Events will list any resources affected by the event.

If the event changed the configuration of a resource the difference will be shown in code as the [template specification](../infrastructure-as-code/write-a-template) for that resource, showing the previous and the updated states.

### Child and parent events

An event log may contain a parent event. This allows you to trace the chain of triggers that caused the event.

Similarly, a log may have one or more child events, these are events triggered by this event.

For example, a `template.run` event may have the child events `projects.put` and `services.put` if the template run creates a project and service. Both `projects.put` and `services.put` will have the `template.run` event as a parent event.

Event types

Event types are defined by their Northflank method, organised by resource type and method. For example, `services.create` is recorded for the creation of a service, and `services.update.secrets` when a service's secrets are updated.

Many events relate directly to those [exposed by the Northflank API](../../api/introduction), while others relate to Northflank system methods that are only available through the Northflank application, or triggered by the Northflank system.

Event triggers and origins

Events are recorded when:

  * a member of the team or organisation performs an action on Northflank, such as scaling a service, running a template, or editing an RBAC role
  * the Northflank system performs an action related to your resources, team, or organisation, such as running a scheduled backup for an addon or regenerating a subdomain's certificate
  * an event on a Git service triggers an action via webhook, such as running a release flow or updating a template with GitOps enabled



Indirectly triggered events will show the parent event that caused them. A deployment in a job with CD enabled, triggered by a new build, will display the build as the parent event. If the job is configured to run when a new image is deployed, the job run event will show both the build and deployment as parent events.

Events from the follow origins are recorded in the audit log:

  * Northflank UI
  * Northflank API/CLI
  * Template runs
  * Release flow template runs
  * Preview environment template runs
  * Version control
  * Northflank system



Log scopes

Audit logs are available, in descending order of scope, for the following:

### Organisation audit log

You can access the audit log for an organisation from the organisation menu. It will display events from all teams in the organisation, as well as organisation events.

### Team audit log

You can access the audit log for a team from the team menu. It will display events from all projects in the team, as well as team events.

### Project audit log

You can access the audit log for a project from the project header. It will display events from all resources in the project, as well as project events.

### Resource audit log

You can access the audit log for a resource from the resource menu. It will display all events affecting the resource.

Resource audit logs are available for services, job, and addons.

Filter log

You can filter audit logs by the following criteria:

Filter| Function  
---|---  
After| Show events created after a certain date and time  
Before| Show events created before a certain date and time  
Event type| Filter events by type of event  
Trigger| Filter events based on what triggered them: user, Git, or Northflank system  
User| Show events triggered by the selected user  
Origin| Filter events by event origin  
Team| Show events triggered by selected team  
Project| Filter events by project  
Resource type| Filter events by selected resource type  
Resource ID| Filter events by given resource ID  
  
The project filter is only available on organisation and team audit logs, while resource type, and resource ID filters are only available on organisation, team, and project audit logs.

Next steps

[View logsView detailed, real-time logs from builds, deployments, and more.](/docs/v1/application/observe/view-logs)[Configure health checksMonitor the uptime and success of your deployed services and builds to ensure your code runs correctly and is always available.](/docs/v1/application/observe/configure-health-checks)[Scale your servicesIncrease the resources available to your services, and the number of instances to deploy.](/docs/v1/application/scale/scale-on-northflank)[Expose a deployment's portConfigure ports and security for your deployments.](/docs/v1/application/network/configure-ports)