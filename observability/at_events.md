---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.atracker_full_notm}}
{: #at_events}

{{site.data.keyword.cloud}} services, such as {{site.data.keyword.atracker_full_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where activity tracking events are generated
{: #at-locations}

{{site.data.keyword.atracker_full_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}


## Viewing activity tracking events for {{site.data.keyword.atracker_full_notm}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Management events
{: #at_events_mgt_atracker}

### Targets
{: #at_events_mgt_target}

The following table lists the auditing events that are generated when you manage targets:

| Action                                            | Description                |
|---------------------------------------------------|----------------------------|
| `atracker.target.create`       | This event is generated when an administrator creates a new Cloud Object Storage (COS) target with specified COS endpoint information and credentials.  |
| `atracker.target.list` | This event is generated when an administrator lists all Cloud Object Storage (COS) targets defined under a region. |
| `atracker.target.get` | This event is generated when an administrator retrieves a target and its details by specifying the ID of the target.|
| `atracker.target.update` | This event is generated when an administrator updates a target details by specifying the ID of the target. |
| `atracker.target.delete` | This event is generated when an administrator deletes a target by specifying the ID of the target. |
{: caption="Events for managing targets" caption-side="top"}


### Routes
{: #at_events_mgt_route}

The following table lists the auditing events that are generated when you manage routes:

| Action                                            | Description                |
|---------------------------------------------------|----------------------------|
| `atracker.route.create` | This event is generated when an administrator creates a route with rules defined how to route auditing events to targets for a region. |
| `atracker.route.list` | This event is generated when an administrator lists routes defined under this region.  |
| `atracker.route.get` | This event is generated when an administrator retrieves a route and its details by specifying the ID of the route. |
| `atracker.route.update` | This event is generated when an administrator replaces a route details by specifying the ID of the route. You can also get this event when you validate a target by checking the credentials to write to the bucket. |
| `atracker.route.delete` | This event is generated when an administrator deletes a route by specifying the ID of the route. |
{: caption="Events for managing routes" caption-side="top"}


### Settings
{: #at_events_setting}

The following table lists the auditing events that are generated when you manage settings:

| Action                                            | Description                |
|---------------------------------------------------|----------------------------|
| `atracker.setting.set` | This event is generated when an administrator configures the {{site.data.keyword.atracker_short}} settings for an account. |
| `atracker.setting.get` | This event is generated when an administrator gets information about the {{site.data.keyword.atracker_short}} settings for an account. |
{: caption="Events for managing settings" caption-side="top"}
