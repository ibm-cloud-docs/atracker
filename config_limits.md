---

copyright:
  years: 2019, 2023, 2024
lastupdated: "2024-04-10"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Configuration limits
{: #config-limits}

This topic summarizes the configuration limits for {{site.data.keyword.atracker_full}}.
{: shortdesc}

You can define resources in any of the supported locations where {{site.data.keyword.atracker_short}} is available. For more information, see [Locations](/docs/atracker?topic=atracker-regions).
{: note}

## Targets
{: #limits_targets}

Consider the following information about targets:

| Description | Limit |
| -------------- | -------------- |
| Minimum number of targets for each {{site.data.keyword.cloud_notm}} account | 0 |
| Maximum number of targets for each {{site.data.keyword.cloud_notm}} account | 16 |
| Maximum number of default targets for each {{site.data.keyword.cloud_notm}} account | 2 |
| Maximum number of target types for each target | 1 |
{: caption="Table 1. Limitations for targets" caption-side="bottom"}


### Types
{: #limits_targets_types}

List of supported target types:

| Target                                                             | Type                     | Learn more |
|--------------------------------------------------------------------|--------------------------|------------|
| {{site.data.keyword.cos_full_notm}} (COS)                          | `cloud_object_storage`   | [Managing {{site.data.keyword.cos_full_notm}} (COS) targets](/docs/atracker?topic=atracker-target_v2_cos) |
| {{site.data.keyword.atracker_full_notm}} AT hosted event search    | `logdna`                 | [Managing {{site.data.keyword.atracker_full_notm}} hosted event search targets](/docs/atracker?topic=atracker-target_v2_at). |
| {{site.data.keyword.messagehub_full}} (Event Streams)              | `event_streams`          | [Managing {{site.data.keyword.messagehub_full}} (Event Streams) targets](/docs/atracker?topic=atracker-target_v2_ies) |
{: caption="Table 2. List of target types" caption-side="top"}


## Routes
{: #limits_routes}

Consider the following information about routes:

| Description | Limit |
| -------------- | -------------- |
| Minimum number of routes for each {{site.data.keyword.cloud_notm}} account | 0 |
| Maximum number of routes for each {{site.data.keyword.cloud_notm}} account | 30 |
{: caption="Table 3. Limitations for routes" caption-side="bottom"}

### Rules
{: #limits_routes_rules}

Consider the following information about rules that you can define per route:

| Description | Limit |
| -------------- | -------------- |
| Minimum number of rules for each route | 1 |
| Maximum number of rules for each route | 10 |
| Maximum number of locations for each rule | 8 |
| Maximum number of targets for each rule | 3 |
| Wildcard to include all locations in 1 rule | `*` |
{: caption="Table 4. Limitations for rules" caption-side="bottom"}

### Targets
{: #limits_routes_targets}

Consider the following information about targets that you can define per routes:

| Description | Limit |
| -------------- | -------------- |
| Minimum number of targets per rule | 1 |
| Maximum number of targets per rule | 16 |
{: caption="Table 5. Limitations for targets" caption-side="bottom"}


### Locations
{: #limits_routes_locations}

Consider the following information about locations that you can define per rule:

| Description | Limit |
| -------------- | -------------- |
| Minimum number of targets per rule | 1 |
| Maximum number of targets per rule | 16 |
{: caption="Table 5. Limitations for targets" caption-side="bottom"}
