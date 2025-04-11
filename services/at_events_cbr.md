---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for context-based restrictions
{: #events_context_based}


{{site.data.keyword.cloud}} services, such as context-based restrictions rules and network zones in {{site.data.keyword.cloud_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



## Viewing activity tracking events for context-based restrictions
{: #at-viewing-cbr}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone-cbr}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Network zone events
{: #network_zone_events}

The following table lists the actions that generate nerwork zone events:

| Action | Description |
| -----  | ----------- |
| context-based-restrictions.zone.create | An event is generated when an initiator creates a CBR zone. |
| context-based-restrictions.zone.list | An event is generated when an initiator lists CBR zones. |
| context-based-restrictions.zone.read | An event is generated when an initiator looks at information that is related with a CBR zone. |
| context-based-restrictions.zone.update | An event is generated when an initiator modifies a CBR zone. Users can identify system initiated updates (vs. user initiated updates) by the initiator name "IBM". |
| context-based-restrictions.zone.delete | An event is generated when an initiator deletes a CBR zone. |
{: caption="Actions generating network zone events" caption-side="bottom"}


## Context-based restrictions rules events
{: #restriction_rules_events}

The following table lists the actions that generate context-based restricitons rule events:

| Action | Description |
| -----  | ----------- |
| context-based-restrictions.policy.create | An event is generated when an initiator creates a CBR rule. |
| context-based-restrictions.policy.list | An event is generated when an initiator lists CBR rules. |
| context-based-restrictions.policy.read | An event is generated when an initiator looks at information that is related with a CBR rule. |
| context-based-restrictions.policy.update | An event is generated when an initiator modifies a CBR rule. |
| context-based-restrictions.policy.delete | An event is generated when an initiator deletes a CBR rule. |
{: caption="Actions generating context-based restrictions rule events" caption-side="bottom"}


## Account settings events
{: #account_setting_events}

The following table lists the actions that generate account settings events:

| Action | Description |
| -----  | ----------- |
| context-based-restrictions.account-settings.read | An event is generated when an initiator looks at information that is related with account settings. |
{: caption="Actions generating account settings events" caption-side="bottom"}
