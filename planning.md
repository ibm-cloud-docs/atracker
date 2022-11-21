---

copyright:
  years: 2022
lastupdated: "2022-10-24"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Planning the account configuration
{: #planning}

Plan the account's {{site.data.keyword.atracker_short}} configuration to manage auditing events in the {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

| Step | Description | Link |
| ---- | -------------- | -------------- |
| **1** | **Location & Services**  \n Identify the locations where you can configure {{site.data.keyword.atracker_full_notm}} to manage auditing events.  \n  \n Identify which services in those locations generate events that you can manage by using {{site.data.keyword.atracker_full_notm}}. | [link](#planning-0) |
| **2** | **Metadata**  \n Decide the location in your  {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.atracker_full_notm}} metadata account configuration metadata is stored.  \n   \n Take into account any corporate or industry compliance requirements such as Financial Services validated locations, or EU-managed regions. | [link](#planning-1) |
| **3** | **Endpoints**  \n Decide whether public endpoints, private endpoints, or both are allowed to manage the {{site.data.keyword.atracker_full_notm}} configuration. | [link](#planning-2) |
| **4** | **Target locations**  \n Define the locations where an account administrator can configure targets to collect auditing events.  \n  \n You can choose any of the supported locations where {{site.data.keyword.atracker_full_notm}} is available. | [link](#planning-3) |
| **5** | **Default targets**  \n Define 1 default target for each account to configure where auditing events that are not explicitly managed in the account's routing rules are routed.  \n   \n Consider defining a second default target for each account when you want to collect the data in a backup location or account. | [link](#planning-4) |
| **6** | **Number and location of targets**  \n Define the targets where you plan to collect auditing events based on your regulatory and corporate requirements. | [link](#planning-5) |
| **7** | **Routing rules**  \n Define the routing rules that indicate how to route events in your account.  \n  \n Decide if you want to drop the collection of auditing events in 1 or more regions. Check any compliance requirements to confirm that you can. | [link](#planning-6) |
{: caption="Table 1. Planning" caption-side="bottom"}

## Locations and services
{: #planning-0}

Check the regions where you operate and identify how you can manage those auditing events in the account:
- Identify the locations where you can configure IBM Cloud Activity Tracker to manage auditing events. Check [Locations](/docs/atracker?topic=atracker-regions).
- Identify which services in those locations generate events that you can manage by using IBM Cloud Activity Tracker. Check [Services generating events](/docs/atracker?topic=atracker-cloud_services_atracker).

You can use {{site.data.keyword.atracker_short}} to manage auditing events at the account-level. {{site.data.keyword.atracker_short}} can only route events that are generated in [supported regions](/docs/atracker?topic=atracker-regions#regions-atracker). Other regions, where {{site.data.keyword.atracker_short}} is not available, continue to manage events by using [{{site.data.keyword.at_short}}](/docs/activity-tracker?topic=activity-tracker-getting-started).



## Metadata location
{: #planning-1}

Decide the location in your {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.atracker_short}} account configuration metadata is stored. 

You can choose any of the supported locations where {{site.data.keyword.atracker_short}} is available. For more information, see [Locations](/docs/atracker?topic=atracker-regions).

Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

If you do not configure a metadata location before you create a target, the location where the first target is created is automatically configured as the metadata location.
{: note}

You can define a primary metadata location and a backup metadata location.


## Endpoints allowed
{: #planning-2}

You can use public endpoints, private endpoints or both to manage the {{site.data.keyword.atracker_short}} account configuration.

Decide whether public endpoints, private endpoints, or both are allowed to manage the {{site.data.keyword.atracker_short}} account configuration. For more information, see [Enforcing private endpoints to configure {{site.data.keyword.atracker_short}} resources](/docs/atracker?topic=atracker-getting-started-mng-endpoints).

Configure private endpoints and disable pub lic endpoints when you require to be Financial Services Validated.
{: tip}

## Target locations
{: #planning-3}

Define the locations where an account administrator can configure targets to collect auditing events. You can choose any of the supported locations where {{site.data.keyword.atracker_short}} is available. For more information, see [Locations](/docs/atracker?topic=atracker-regions&interface=cli).

To enforce target locations in the account, you can configure the account settings and specify the locations that are allowed. See [Locations](/docs/atracker?topic=atracker-regions&interface=cli).
{: tip}

Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

The location of a target definition must be a supported location where {{site.data.keyword.atracker_short}} is available. The target can configure a resource in the same account where the events are located or in a different account. In addition, the resource can be located in any region where that type of resource is supported in {{site.data.keyword.cloud_notm}}.

## Default targets
{: #planning-4}

You can define up to 2 default targets in the account. 
- Each target collects auditing events that are not explicitly managed in the account's routing rules.
- Each target must be defined in the account before you can configure it as default one in the account.
- If you define more than 1 default target, all default targets get a copy of an auditing event that does not have a clearly defined routing rule to indicate where to route events in the account.

Define 1 default target per account to configure where auditing events that are not explicitly managed in the account's routing rules are routed. Consider defining a second default target per account when you want to collect the data in a backup location or account.
{: tip}



## Number and location of targets
{: #planning-5}

Define the targets where you plan to collect auditing events based on your regulatory and corporate requirements.

- You can have 1 target per region to collect auditing events for that region. Use this option to reduce latency and network connectivity issues.

- You can have 1 target to collect auditing events across the entire account.

- You can define targets within the account or in a different account.

For more information, see [Targets](/docs/atracker?topic=atracker-atracker-resources#atracker-resources-targets).


## Routing rules in the account
{: #planning-6}


Define the routing rules that indicate how to route events in your account.

- Routes are global. 

- You can define up to 4 routes per account.
    
- You can define 1 or more routes to configure how auditing events across all regions in your account are collected and stored in 1 or more targets.
    
- For each route that you define, you can configure 4 rules. These rules are applied top down. When a rule is identified for a region, any follow up rules withing that route definition that apply to that region are not considered.

Decide if you want to drop the collection of auditing events in 1 or more regions. Check any compliance requirements to confirm that you can.

- To drop the collection of auditing events in 1 or more regions, you can configure a route for those regions with no targets defined.

For more information, see [Routes](/docs/atracker?topic=atracker-atracker-resources#atracker-resources-routes).

 
## Next
{: #planning-next}

Next, [check samples of different scenarios](/docs/atracker?topic=atracker-atracker-scenarios). 


