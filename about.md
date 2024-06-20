---

copyright:
  years: 2019, 2023, 2024
lastupdated: "2024-05-31"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.atracker_full_notm}}
{: #about}

Use {{site.data.keyword.atracker_full}} to configure how to route auditing events, both [global](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based](/docs/atracker?topic=atracker-event_types#event_types_location) event data, in your {{site.data.keyword.cloud_notm}}.
{: shortdesc}


## Auditing events
{: #about-events}

auditing events are critical data for security operations and a key element for meeting compliance requirements.
{: note}

- auditing events increase your visibility to {{site.data.keyword.cloud_notm}} configuration changes so you can manage the risk of incorrectly configured services more effectively.

- auditing events simplify your understanding of IT complexity and agile development actions in the cloud. The combination of events provides a holistic view of what happened.

- Insights from the auditing event data help accelerate identification of abnormal activities. For example, you can track the frequency and volume of access management events or multi-factor authentication configuration changes.

The auditing data that is collected and routed complies with the Cloud Auditing Data Federation (CADF) standard.
{: note}

The CADF standard defines a full event model that includes the information that is needed to certify, manage, and auditing security of applications and services in cloud environments. The CADF event model includes the following components:
-	Action: The action is the operation or activity that an initiator performs, attempts to perform, or is waiting to complete.
-	Initiator: The initiator is the resource that makes an API call and generates a CADF event. The event that is triggered depends on the action that is requested by the API call.
-	Observer: The observer is the resource that creates and stores a CADF record from information available in a CADF event
-	Outcome: The outcome is the status of the action against the target.
-	Target: The target is the resource against which the action is performed, attempted to perform, or is pending to complete.



## Target locations
{: #about-locations}

Control of the storage location is critical to building enterprise-grade solutions on the {{site.data.keyword.cloud_notm}}.
{: note}

In {{site.data.keyword.atracker_full_notm}}, a target defines where auditing events are collected.  For more information, see [Targets](/docs/atracker?topic=atracker-atracker-resources#atracker-resources-targets).

You can configure different types of targets:

| Target                                      | Type                     | When to use |
|---------------------------------------------|--------------------------|------------|
| {{site.data.keyword.cos_full_notm}} (COS)   | `cloud_object_storage`   | To comply with Financial Services regulations. |
| {{site.data.keyword.logs_full_notm}}| `cloud_logs`   | To view, search, and manage auditing data through the UI. |
| {{site.data.keyword.at_short}} hosted event search | `logdna`   | To view, search, and manage auditing data through the UI. |
| {{site.data.keyword.messagehub_full}} | `event_streams`   | To send auditing data to data lakes, other analysis tools, and to other corporate tools such as Security Information and Event Management (SIEM) tools. |
{: caption="Table 1. List of targets" caption-side="top"}

In {{site.data.keyword.atracker_full_notm}}, a route defines the rules that indicate where auditing events that are generated in an account are routed. For more information, see [Routes](/docs/atracker?topic=atracker-atracker-resources#atracker-resources-routes).


## Features
{: #about-features}

- Consolidate auditing events to the region of your primary operations

- Route auditing events to one or multiple locations

- Improve your data residency compliance stature, keeping data at-rest within certain regions

- Feed a data lake for analytics

- Forward your activity event data to {{site.data.keyword.cos_full_notm}} (COS) for {{site.data.keyword.cloud_notm}} for Financial Services compliance
