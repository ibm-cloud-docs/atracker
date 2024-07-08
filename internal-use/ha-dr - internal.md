---

copyright:
  years: 2019, 2024
lastupdated: "2024-01-18"

keywords:

subcollection: atracker



---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #ha_dr}

{{site.data.keyword.atracker_full_notm}} is a highly available, multi-tenant, regional service. In this topic, you can learn more about {{site.data.keyword.atracker_short}}'s availability and disaster recovery strategies.
{: shortdesc}

## Service high availability (HA)
{: #ha_dr_svc_availability}

An availability zone is a logically and physically isolated location within an {{site.data.keyword.cloud_notm}} region where your data is processed and hosted.
* An availability zone has independent power, cooling, and network infrastructures that are isolated from other zones to strengthen fault tolerance by avoiding single points of failure between zones.
* An availability zone offers high bandwidth and low inter-zone latency within a region.

A region (location) is a geographically and physically separate group of one or more availability zones with independent electrical and network infrastructures isolated from other regions.
* Regions are designed to remove shared single points of failure with other regions and guarantee low inter-zone latency within the region.
* Each region has 3 different data centers (DC) for redundancy.


## Availability zones
{: #ha_dr_locations-atracker}

{{site.data.keyword.atracker_short}} is a highly available, regional, service.
- {{site.data.keyword.atracker_short}} is available in multiple regions. For more information on the regions where {{site.data.keyword.atracker_short}} is available, see [Regions](/docs/atracker?topic=atracker-regions).
- Each region has three different data centers for redundancy configured in `active/active` mode.
- If all the data centers in a location fail, {{site.data.keyword.atracker_short}} becomes unavailable in that location.
- In each supported region, traffic is load balanced across infrastructure in multiple availability zones, with no single point of failure.

For more information about service availability, see [Service Level Agreements (SLAs)](/docs/overview?topic=overview-slas).

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.at_full_notm}} service is available:

| Geography             | Region                   | EU-Supported | HA Status |
|-----------------------|--------------------------|--------------|-----------|
| `North America`       | `Dallas (us-south)`      | `N/A`        | `MZR`     |
| `North America`       | `Washington (us-east)`   | `N/A`        | `MZR`     |
| `Europe`              | `Frankfurt (eu-de)`      | ![Checkmark icon](../images/checkmark-icon.svg "checkmark") | `MZR`     |
| `Europe`              | `London (eu-gb)`         | `N/A`        | `MZR`     |
| `Asia Pacific`        | `Sydney (au-syd)`        | `N/A`        | `MZR`     |
{: caption="Table 1. List of locations where the service is available" caption-side="top"}


Where
* A *geography* is a geographic area or larger political body that contains one or more regions.
* A *region* is a defined geographic territory.

    A region could be a specific postal code area, a town, a city, a state, a group of states, or even a group of countries.

    A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

* `N/A` means feature that is not applicable to that geography.
* `MZR` means multi-zone region. [Learn more](/docs/overview?topic=overview-locations#table-mzr).


## Data availability
{: #ha_dr_data_availability}

The data that is managed by {{site.data.keyword.atracker_short}} in a region is kept in the data centers near that region.

A multizone region (MZR) consist of 3 or more availability zones that are independent from each other to ensure that single failure events affect only a single zone.

By default, {{site.data.keyword.atracker_short}} is deployed across 3 zones. Each zone is setup with active/active/active:
* Each zone is located in a different data center in the region.
* The data in each zone is automatically replicated to the other zones with low latency. You don't need to do anything to enable the replication.
* The service is designed to withstand a single zone failure with no interruption.

The MZR architecture offers automatic failover between zones within the region, and high availability for a auditing instance withing a region.

{{site.data.keyword.atracker_short}} data includes information on where and how to collect and store auditing events in your account for regional services and for global services like IAM.
- A target is a resource where you can collect auditing events.
- A route is a resource that defines the rules that determine where auditing events are routed in your account.

{{site.data.keyword.atracker_short}} does regular backups of the data per region:
- Regular backups are done daily and retained for 30 days.
- Continuous incremental backups are kept for the last 7 days.

{{site.data.keyword.atracker_short}} data is replicated across multiple regions.
- Regular backups are stored across multiple regions, and are restorable to other regions.

The following table shows the regions where the copy of a regular backup is replicated and available:

| Geography             | Region                   | Other regions that keep a copy of the backup   |
|-----------------------|--------------------------|-------------------------|
| `North America`       | `Dallas (us-south)`      | `Sydney (au-syd)` \n`Washington (us-east)`  |
| `North America`       | `Washington (us-east)`   | `Sydney (au-syd)` \n`Dallas (us-south)`     |
| `Europe`              | `Frankfurt (eu-de)`      | `London (eu-gb)`        |
| `Europe`              | `London (eu-gb)`         | `Frankfurt (eu-de)`     |
| `Asia Pacific`        | `Sydney (au-syd)`        | `Frankfurt (eu-de)`     |
{: caption="Table 2. List of locations where a copy of the backup is available" caption-side="top"}



## Disaster recovery (DR) in a region
{: #dr}

Disaster recovery is about surviving a catastrophic failure or loss of availability in a single location.

{{site.data.keyword.atracker_short}} is a platform service, there is no automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, {{site.data.keyword.atracker_short}} becomes unavailable in that location.


In the event of a regional disaster, you must complete the following steps to establish cross-region high availability:

1. Decide which location is going to be your recovery region. Choose 1 of the following options:

    - [Check the suggested DR recovery region](/docs/atracker?topic=atracker-ha_dr#bc-dr-locations) and use that region as your recovery region.

    - If you have configured the {{site.data.keyword.atracker_short}} account settings with a primary location and a secondary backup location, check if either location is still operational and use 1 of those locations as your recovery region.

    - If you have configured the {{site.data.keyword.atracker_short}} account settings with a primary location only, and this location is down, check {{site.data.keyword.atracker_short}} supported regions and choose an active region as your recovery region.

2. You can only define targets in {{site.data.keyword.atracker_short}} supported regions. However, the actual target can be available in a different region and continue to be operational. First, you must check the target's availability. Next, choose 1 of the following options:

    - If a target is available in a different region from the one that is down, and the recovery region that you choose is one configured in the {{site.data.keyword.atracker_short}} account settings, the primary location and backup secondary location include details of your target. You can continue to check the routes that are defined in the account to ensure that events are routed to the target.

    - If a target is available in a different region from the one that is down, and the recovery region that you choose is not a region that is configured in the {{site.data.keyword.atracker_short}} account settings, you must configure the target in any {{site.data.keyword.atracker_short}} supported region that is available, preferably, the region that you choose as your recovery region. Next, you must check the routes that are defined in the account so events are routed to the new target that you have configued.

    - If the target is not available, you must go thorugh the DR recovery process of that type of target and provision a new one in the recovery region that you choose. You must configure the target in any {{site.data.keyword.atracker_short}} supported region that is available, preferably, the region that you choose as your recovery region. Next, you must check the routes that are defined in the account so events are routed to the new target that you have configued.

3. You define routes to indicate how events are routed to the targets that you have configured in the account. These routes are global and not bound to a specific region. Therefore, in the case of a DR scenario, you must check that all the targets that are configured are operational, and that the rules apply to operational targets and locations.

    If the region that goes down is also collecting global events in your account, you must update the route in the recovery region to collect global events.


When {{site.data.keyword.atracker_short}} recovers in the region that is down, your configuration is restored. Complete the following steps to continue operating in the region that went down:
1. You must check that any existing targets in that region are also recovered and operational.
2. If you had to enable collection of global auditing events in the recovery region, you must update the route to stop global events in that region.
3. If you had configured new targets, you can update your configuration to go back to use the targets that went down. You can also decide to continue ussing the targets that you enabled in the recovery region.



In the event of a regional disaster, you must complete the following steps to establish cross-region high availability if you are using {{site.data.keyword.atracker_short}} V1 API:

1. [Check the DR recovery region](/docs/atracker?topic=atracker-ha_dr#bc-dr-locations).

2. If you have a target and a route configured in the recovery region, your auditing events will be routed to the target that is specified for that region.

    If the region that goes down is also collecting global events in your account, you must update the route in the recovery region to collect global events.

3. If the recovery region is not configured, you must configure {{site.data.keyword.atracker_short}} in the region. [Learn more](/docs/atracker?topic=atracker-getting-started).

When {{site.data.keyword.atracker_short}} recovers in the region that is down, your configuration is restored. If you had to enable collection of global auditing events in the recovery region, you must update the route to stop global events in that region.
{: important}



## Suggested DR recovery regions
{: #ha_dr-atracker_recovery_region}

The following table indicates the recovery region in the event of a DR situation:

| Geography             | Source region            | Recovery region   |
|-----------------------|--------------------------|--------------|
| `North America`       | `Dallas (us-south)`      | `Washington (us-east)`  |
| `North America`       | `Washington (us-east)`   | `Dallas (us-south)`     |
| `Europe`              | `Frankfurt (eu-de)`      | `London (eu-gb)`        |
| `Europe`              | `London (eu-gb)`         | `Frankfurt (eu-de)`     |
| `Asia Pacific`        | `Sydney (au-syd)`        | `Frankfurt (eu-de)`     |
{: caption="Table 3. List of locations where a region is recovered" caption-side="top"}



## DR recovery time
{: #ha_dr_atracker_recovery_time}

The following table indicates the estimated recovery times in the event of a DR situation:

| Recovery objective for DR                                         | Estimated time |
|-------------------------------------------------------------------|----------------|
| Maximum Tolerable Downtime (MTD) / Recovery Time Objective (RTO)  | Less than 24 hours |
| Recovery Point Objective (RPO)                                    | Less than 24 hours |
{: caption="Table 4. Recovery objectives for DR" caption-side="top"}
