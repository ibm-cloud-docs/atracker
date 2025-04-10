---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Collecting events in your account
{: #events_collect}

In {{site.data.keyword.atracker_full}}, events are collected automatically for most {{site.data.keyword.atracker_short}}-enabled services. However, some services might require an upgrade of the service plan, a configuration setting, or both, for you to be able to collect and route their events.
{: shortdesc}

To collect and monitor activity in your account by using {{site.data.keyword.atracker_short}}, you can choose any of the following methods:

- You can [configure {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-getting-started) to manage auditing events in your account while maintaining Financial Services Validated status.

    The target resource must be an {{site.data.keyword.cos_full}} bucket that is available in the same account where the auditing events are generated.

    You can also use a bucket that is available in a different account from where auditing events are generated.

    You must follow and comply with the Financial Services Validated requirements for buckets to maintain Financial Services Validated status.
    {: important}

    



- You can configure {{site.data.keyword.atracker_short}} to route all events to {{site.data.keyword.logs_full_notm}} instances to manage auditing events through the UI.

    The {{site.data.keyword.logs_full_notm}} instances can be located in the same account where auditing events are generated or in a different account.


In {{site.data.keyword.atracker_short}}, you can differentiate events by scope as global or location-based events, and by operational impact as either management or data events.

- The scope is determined from where an event is collected.

- Collection of management events is automatic for {{site.data.keyword.atracker_short}}-enabled services, except for Watson services which require a paid plan.

- Collection of data events is also automatic with the exception of some services where you must opt-in to collect those events. To opt-in, you might need to configure the service, upgrade the service plan, or both. For more information, see [Data events](/docs/atracker?topic=atracker-event_types#event_types_data).




## Collecting global events
{: #events_collect_global}

You can collect [global events](/docs/atracker?topic=atracker-event_types#event_types_global) in your account by configuring {{site.data.keyword.atracker_short}} to manage routing of global events to the destination of your choice. [Learn more](/docs/atracker?topic=atracker-getting-started).

Routing can be to 1 or more supported targets such as an {{site.data.keyword.logs_full_notm}} instance so that you can monitor events through the UI or to an {{site.data.keyword.cos_full_notm}} bucket for archival purposes. [Learn more](/docs/atracker?topic=atracker-getting-started).

Routing can be done to a target resource within the account that generates the auditing events, or to a target resource in another {{site.data.keyword.cloud_notm}} account.

## Collecting location-based events
{: #events_collect_location}

Configure {{site.data.keyword.atracker_short}}to collect [location-based events](/docs/atracker?topic=atracker-event_types#event_types_location) in your account.

You can choose the region where location-based events are collected. [Learn more](/docs/atracker?topic=atracker-atracker-resources).

{{site.data.keyword.atracker_short}} routes events based on the location that is specified in the `logSourceCRN` field included in the event. You can define a target, the resource where events are routed to, in any {{site.data.keyword.atracker_short}} supported region. However, the target resource can be located in any region where that type of target is supported, in the same account or in a different account. You can define rules to determine where auditing events are to be routed by configuring 1 or more routes in the account. You can define rules for managing global events and location-based events that are generated in regions where {{site.data.keyword.atracker_short}} is supported.

Routing can be to 1 or more supported targets such as an {{site.data.keyword.logs_full_notm}} instance so that you can monitor events through the UI or to an {{site.data.keyword.cos_full_notm}} bucket for archival purposes. [Learn more](/docs/atracker?topic=atracker-getting-started).

Routing can be done to a target resource within the account that generates the auditing events, or to a target resource in another {{site.data.keyword.cloud_notm}} account.

Routing of location-based events from a given region is only supported for the regions where {{site.data.keyword.atracker_short}} is supported. For more information about supported regions, see [Locations](/docs/atracker?topic=atracker-regions).
