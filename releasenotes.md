---

copyright:
  years: 2019, 2024
lastupdated: "2024-04-15"

keywords:

subcollection: atracker

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}



# Release notes for {{site.data.keyword.atracker_full_notm}}
{: #activity-tracker-release-notes}

Use these release notes to learn about the latest updates to {{site.data.keyword.atracker_full}}.
{: shortdesc}

## 20 June 2024
{: #activity-tracker-june2024}
{: release-note}

Configure {{site.data.keyword.atracker_full_notm}} using the IBM Console
:   {{site.data.keyword.atracker_full_notm}} provides a new user interface through the IBM Console where you can configure routes and targets. For more information, see [Getting account settings using the UI](/docs/atracker?topic=atracker-settings&interface=ui#settings-get-ui).

## 15 April 2024
{: #activity-tracker-apr1524}
{: release-note}

Chennai (in-che) region support
:   Chennai is now an online region for {{site.data.keyword.atracker_full_notm}}. Services can now be provisioned Chennai and endpoints in Chennai can be used.

## 11 April 2024
{: #activity-tracker-apr1124}
{: release-note}

Toronto (ca-tor) and Sao Paulo (br-sao) region support
:   Toronto and Sao Paulo are now online regions for {{site.data.keyword.atracker_full_notm}}. Services can now be provisioned in those regions and endpoints in those regions can be used.

Increase routes and rules limits
:   The maximum number of routes for each account is increased to 30 and the maximum number of rules for each route is increased to 10.

## 03 April 2024
{: #activity-tracker-apr0324}
{: release-note}

Osaka (jp-osa) and Tokyo (jp-tok) region support
:   Osaka and Tokyo are now online regions for {{site.data.keyword.atracker_full_notm}}. Services can now be provisioned in those regions and endpoints in those regions can be used.

## 01 March 2024
{: #activity-tracker-mar0124}
{: release-note}

Support for br-sao, ca-tor, jp-osa, jp-tok and in-che regions planned for April 2024
:  If you have services in the br-sao, ca-tor, jp-osa, jp-tok or in-che regions and you have an existing {{site.data.keyword.atracker_full_notm}} configuration, action might be required to continue processing AT events in these regions. To determine if you are impacted, see [Required actions for newly supported regions](/docs/atracker?topic=atracker-new_region_support)

## 26 September 2023
{: #activity-tracker-sep2623}
{: release-note}

Madrid region support
:   Madrid is now an online region for {{site.data.keyword.atracker_full_notm}}. Services can now be provisioned in Madrid and Madrid endpoints can be used. Platform metrics will continue flowing to the Frankfurt region.

## 17 July 2023
{: #activity-tracker-jul1723}
{: release-note}

References to {{site.data.keyword.atracker_short}} V1 API removed.
:   All references to the deprecated V1 API have been removed from the {{site.data.keyword.atracker_short}} documentation.

## 18 November 2022
{: #activity-tracker-nov1822}
{: release-note}

{{site.data.keyword.atracker_short}} support for {{site.data.keyword.messagehub_full}} targets.
:   Using the CLI, API, or Terraform you can configure {{site.data.keyword.atracker_short}} to send events to an {{site.data.keyword.messagehub}} topic. This adds to the existing support for {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.at_short}} hosted event search targets.

New documentation locations for {{site.data.keyword.atracker_short}} and {{site.data.keyword.at_short}} hosted event search
:   There are now two different locations for {{site.data.keyword.at_short}} documentation depending on your use case.

    * For {{site.data.keyword.atracker_short}}, see the [{{site.data.keyword.atracker_short}} documentation.](/docs/atracker)

    * For {{site.data.keyword.at_short}} hosted event search, see the [{{site.data.keyword.at_short}} hosted event search documentation.](/docs/activity-tracker?topic=activity-tracker-getting-started)

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
:   {{site.data.keyword.atracker_short}} is now available in the in Sydney (au-syd) region.  [Learn more](/docs/atracker?topic=atracker-regions).

## 22 March 2022
{: #activity-tracker-mar2222}
{: release-note}

{{site.data.keyword.atracker_short}} available in Frankfurt (eu-de) and London (eu-gb)
:   {{site.data.keyword.atracker_short}} is now available in the Frankfurt (eu-de) and London (eu-gb) regions.  [Learn more](/docs/atracker?topic=atracker-regions).


## 13 August 2021
{: #activity-tracker-aug1321}
{: release-note}

General availability of {{site.data.keyword.atracker_short}}
:   [Learn more about {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-getting-started).
