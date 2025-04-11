---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for service instances
{: #at_events_rc}

{{site.data.keyword.cloud}} service instances generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



## Viewing activity tracking events for {{site.data.keyword.dashdblong}}
{: #at-viewing-rc}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone-rc}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Events for provisioning and managing service instances
{: #rc_provision}

The following table lists the actions that generate an event:

| Action                                   | Description |
|------------------------------------------|---------|
| `service_name.instance.create`           | An event is generated when you provision a service instance. |
| `service_name.instance.update`           | An event is generated when you rename a service instance or when you change the service plan. |
| `service_name.instance.delete`           | An event is generated when a service instance is deleted. |
| `service_name.instance.schedule_reclaim` | An event is generated when a service instance is pending_reclamation. |
| `service_name.instance.restore`          | An event is generated when a service instance is restored. |
{: caption="Actions that generate events" caption-side="top"}


##  Events for managing aliases that are associated to a service instance
{: #rc_alias}

An alias is a connection between your IAM-managed service within a resource group and an application within an org or a space.

The following table lists the actions that generate an event:

| Action                         | Description |
|--------------------------------|---------|
| `service_name.alias.create` | An event is generated when an alias for an instance is created. |
| `service_name.alias.update` | An event is generated when an alias for an instance is updated. |
| `service_name.alias.delete` | An event is generated when an alias for an instance is deleted. |
{: caption="Actions that generate events" caption-side="top"}


##  Events for managing service credentials that are associated to a service instance
{: #rc_keys}

A service credential provides the necessary information to connect an application to a service instance.

The following table lists the actions that generate an event:

| Action                         | Description |
|--------------------------------|---------|
| `service_name.key.create` | An event is generated when an API key is created for a service instance through the *Service credentials* section of the service instance UI. |
| `service_name.key.delete` | An event is generated when an API key that is associated with a service instance is deleted from the *Service credentials* section of the service instance UI. |
{: caption="Actions that generate events" caption-side="top"}



##  Events for binding and unbinding a service instance to an app
{: #rc_bind}

The following table lists the actions that generate an event:

| Action                         | Description |
|--------------------------------|---------|
| `service_name.binding.create` | An event is generated when you bind a service instance to an application. |
| `service_name.binding.delete` | An event is generated when you unbind a service instance from an application. |
{: caption="Actions that generate events" caption-side="top"}



## Analyzing events
{: #rc_analyze}

### Action service_name.instance.delete
{: #rc_analyze_1}

When a service instance is deleted, consider the following information:
* Other actions are automatically triggered to clean up IAM permissions. These actions remove policies that are configured for users and service IDs in the account to work with the service instance.
* The initiator of these actions is an {{site.data.keyword.IBM_notm}} service ID.


When the service instance that is deleted does not have IAM policies configured for users and service IDs, the events that are automatically generated for any of these resources report an outcome of`failure` with a `404` outcome code. The following sample shows the events that are generated when a service instance that does not have policies configured in the account is deleted:

```text
Apr 30 09:04:16 cloudcerts: delete instance Certificate Manager-v1
Apr 30 09:41:20 IAM Access Management: delete policy -failure
Apr 30 09:41:20 IAM Access Management: delete policy -failure
```
{: screen}
