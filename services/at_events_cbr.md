---

copyright:
  years: 2021, 2022
lastupdated: "2022-06-14"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for context-based restrictions
{: #events_context_based}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full_notm}} to track how users and applications interact with the Context-based restrictions rules and network zones in {{site.data.keyword.cloud_notm}}.

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of these resources in {{site.data.keyword.cloud_notm}}.

To get started monitoring your user's actions, see [IBM Cloud Activity Tracker](https://cloud.ibm.com/docs/services/activity-tracker?topic=activity-tracker-getting-started#getting-started). An initiator can be a user, a service, or an application.


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


## Account settings events
{: #account_setting_events}

The following table lists the actions that generate account settings events:

| Action | Description |
| -----  | ----------- |
| context-based-restrictions.account-settings.read | An event is generated when an initiator looks at information that is related with account settings. |


## Viewing events
{: #cdr_viewing_events}

Events are available in the Frankfurt (eu-de) region. To view these events, complete the following steps:
1. Provision an instance of the {{site.data.keyword.at_full_notm}} service in the Frankfurt (eu-de) region. 
1. Open the {{site.data.keyword.at_full_notm}} UI.
