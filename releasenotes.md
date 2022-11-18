---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-18"

keywords:

subcollection: atracker

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}



# Release notes for {{site.data.keyword.atracker_full_notm}}
{: #activity-tracker-release-notes}

Use these release notes to learn about the latest updates to {{site.data.keyword.atracker_full}}.
{: shortdesc}

## 18 November 2022
{: #activity-tracker-nov1822}
{: release-note}

{{site.data.keyword.atracker_short}} support for {{site.data.keyword.messagehub_full}} targets.
:   Using the CLI, API, or Terraform you can configure {{site.data.keyword.atracker_short}} to send events to an {{site.data.keyword.messagehub}} topic. This adds to the existing support for {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.at_short}} hosted event search targets.

## 25 May 2022
{: #activity-tracker-may2522}
{: release-note}

New V2 API support for {{site.data.keyword.atracker_short}} including the ability to configure service-to-service authorization for {{site.data.keyword.cos_full_notm}} targets.
:   Highlights of this new support include:

    * You are now able to route your global events to any {{site.data.keyword.atracker_short}} hosted event search region even if {{site.data.keyword.atracker_short}} is not present in the region.

    * The {{site.data.keyword.atracker_short}} configuration has been moved to be a global configuration so that all route definitions apply to all regions where the feature is present.  This removes the requirement to configure {{site.data.keyword.atracker_short}} in each region.  Routing based on location is still possible.

    * {{site.data.keyword.cos_full_notm}} targets support service-to-service authorizations which eliminates the need to manage keys for your {{site.data.keyword.cos_full_notm}} targets.

    * The `setting` feature allows the account to choose the location where the {{site.data.keyword.atracker_short}} metadata for their account is stored.

    * The `setting` feature allows the account to choose one or more default targets for routing events.  This removes the requirement to individually define routes in each region if you want to have all events from all regions to flow to a specific target.

    * New `/api/v2` APIs have been introduced to replace the existing V1 APIs.

    * The V1 APIs are now deprecated and will be removed in a future release.

    * For existing {{site.data.keyword.atracker_short}} users, you will need to follow a migration process to use the new V2 features.  For customers that have not yet configured a target using {{site.data.keyword.atracker_short}}, you will default to V2 and will not require a migration.

{{site.data.keyword.atracker_short}} available in Sydney (au-syd)
:   {{site.data.keyword.atracker_short}} is now available in the in Sydney (au-syd) region.  [Learn more](/docs/atracker?topic=atracker-regions#regions-atracker).

## 22 March 2022
{: #activity-tracker-mar2222}
{: release-note}

{{site.data.keyword.atracker_short}} available in Frankfurt (eu-de) and London (eu-gb)
:   {{site.data.keyword.atracker_short}} is now available in the Frankfurt (eu-de) and London (eu-gb) regions.  [Learn more](/docs/atracker?topic=atracker-regions#regions-atracker).


## 13 August 2021
{: #activity-tracker-aug1321}
{: release-note}

General availability of {{site.data.keyword.atracker_short}}
:   [Learn more about {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-getting-started-routing).
