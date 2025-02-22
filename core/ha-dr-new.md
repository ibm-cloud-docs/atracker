---

copyright:
  years:  2021, 2025
lastupdated: "2025-02-22"

keywords: HA for IBM Cloud Activity Tracker Event Routing, DR for IBM Cloud Activity Tracker Event Routing, IBM Cloud Activity Tracker Event Routing recovery time objective, IBM Cloud Activity Tracker Event Routing recovery point objective

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Understanding high availability and disaster recovery for {{site.data.keyword.atracker_full_notm}}
{: #atracker-ha-dr}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state.
{: shortdesc}

{{site.data.keyword.atracker_full_notm}} is a highly available, multi-tenant, regional service. You can find the available region and data center locations in the [Locations](/docs/atracker?topic=atracker-regions) documentation. As a regional service, {{site.data.keyword.atracker_full_notm}} fulfills the defined [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo). The SLO is not a warranty and IBM will not issue credits for failure to meet an objective.

## High availability architecture
{: #ha-architecture}



![Diagram displaying the high availability architecture for {{site.data.keyword.atracker_short}}](../images/AT_HA_diagram.png "High availability architecture"){: caption="High availability architecture" caption-side="bottom"}

{{site.data.keyword.databases-for-postgresql_full}} controls distribution of requests between postgres members, which is outlined in [High availability for PostgreSQL](/docs/databases-for-postgresql?topic=databases-for-postgresql-high-availability)

An availability zone is a logically and physically isolated location within an {{site.data.keyword.cloud_notm}} region where your data is processed and hosted.
* An availability zone has independent power, cooling, and network infrastructures that are isolated from other zones to strengthen fault tolerance by avoiding single points of failure between zones.
* An availability zone offers high bandwidth and low inter-zone latency within a region.

A region (location) is a geographically and physically separate group of one or more availability zones with independent electrical and network infrastructures isolated from other regions.
* Regions are designed to remove shared single points of failure with other regions and guarantee low inter-zone latency within the region.
* Each region has 3 different data centers (DC) for redundancy.

### Availability zones
{: #ha_dr_locations-atracker}

{{site.data.keyword.atracker_short}} is a highly available, regional, service.
- {{site.data.keyword.atracker_short}} is available in multiple regions. For more information on the regions where {{site.data.keyword.atracker_short}} is available, see [Regions](/docs/atracker?topic=atracker-regions).
- Each multi-zone region has three different data centers for redundancy configured in `active/active` mode.
- If all the data centers in a location fail, {{site.data.keyword.atracker_short}} becomes unavailable in that location.
- In each supported region, traffic is load balanced across infrastructure in multiple availability zones, with no single point of failure.

For more information about service availability, see [Service Level Agreements (SLAs)](/docs/overview?topic=overview-slas).

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.atracker_full_notm}} service is available:

| Geography             | Region                   | EU-Supported | HA Status |
|-----------------------|--------------------------|--------------|-----------|
| Asia Pacific        | Chennai `(in-che)`        | `N/A`        | `SZR`     |
| Asia Pacific        | Osaka `(jp-osa)`        | `N/A`        | `MZR`     |
| Asia Pacific        | Sydney `(au-syd)`        | `N/A`        | `MZR`     |
| Asia Pacific        | Tokyo `(jp-tok)`        | `N/A`        | `MZR`     |
| Europe              | Frankfurt `(eu-de)`      | ![Checkmark icon](../images/checkmark-icon.svg "checkmark") | `MZR`     |
| Europe              | London `(eu-gb)`         | `N/A`        | `MZR`     |
| Europe              | Madrid `(eu-es)`         | ![Checkmark icon](../images/checkmark-icon.svg "checkmark")         | `MZR`     |
| North America       | Dallas `(us-south)`      | `N/A`        | `MZR`     |
| North America       | Toronto `(ca-tor)`      | `N/A`        | `MZR`     |
| North America       | Washington `(us-east)`   | `N/A`        | `MZR`     |
| South America       | Sao Paulo `(br-sao)`   | `N/A`        | `MZR`     |
{: caption="List of locations where the service is available" caption-side="top"}


Where
* A *geography* is a geographic area or larger political body that contains one or more regions.
* A *region* is a defined geographic territory.

    A region could be a specific postal code area, a town, a city, a state, a group of states, or even a group of countries.

    A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/){: external} to meet local access, low latency, and security requirements for the region.

* `N/A` means feature that is not applicable to that geography.
* `MZR` means multi-zone region. [Learn more](/docs/overview?topic=overview-locations#table-mzr).




### High availability features
{: #ha-features}

{{site.data.keyword.atracker_full_notm}} supports the following high availability features:



| Feature | Description |
| -------------- | -------------- |
| Multi-zone region deployment | {{site.data.keyword.atracker_full_notm}} is deployed into multi-zone regions (MZRs), and within a MZR, the data plane spans all three zones, ensuring that the loss of a zone does not impact service availability. |
| Auditing event replication across zones | Every event ingested into {{site.data.keyword.atracker_full_notm}} is replicated across three zones within MZRs. This ensures events will be retained in the event of a zone loss. |
| Liveness / readiness monitoring | All microservices are monitored via Kubernetes liveness and readiness probes. |
{: caption="HA features for {{site.data.keyword.atracker_full_notm}}" caption-side="bottom"}


#### *Auditing event replication across zones* for {{site.data.keyword.atracker_full_notm}}
{: #auditing-event-replication-across-zones}

Upon ingestion by {{site.data.keyword.atracker_full_notm}}, every event is pushed to a minimum of two zones, otherwise {{site.data.keyword.atracker_full_notm}} will reject the incoming request. For valid customer configurations, ingested events will not be deleted until the egress layer successfully sends the event to a customer's configured destination.

## Disaster recovery architecture
{: #dr_architecture}

![Diagram displaying the disaster recovery architecture for {{site.data.keyword.atracker_short}}](../images/AT_DR_diagram.png "Disaster recovery architecture"){: caption="Disaster recovery architecture" caption-side="bottom"}

{{site.data.keyword.databases-for-postgresql_full}} controls distrubution of requests between postgres members, which is outlined in [High availability for PostgreSQL](/docs/databases-for-postgresql?topic=databases-for-postgresql-high-availability)

{{site.data.keyword.cos_full_notm}} manages the geo buckets used to store the postgres backups for {{site.data.keyword.atracker_full_notm}}. Geo location bucket management is outlined in [High availability for {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-cos-ha-dr)

## Sinlge zone failure
{: #single-az-failure}

{{site.data.keyword.atracker_full_notm}} is HA and can continue to function through any single zone or
machine failure.

## Regional failure
{: #regional-failure}

{{site.data.keyword.atracker_short}} is a platform service. There is no automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, {{site.data.keyword.atracker_short}} becomes unavailable in that region.

### Disaster recovery features
{: #dr-features}

{{site.data.keyword.atracker_full_notm}} supports the following disaster recovery features:



| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |
| Multiple configurable destinations | Details can be found for customers to create disaster resiliant configurations leveraging {{site.data.keyword.atracker_full_notm}} [here](/docs/atracker?topic=atracker-dr_config)| This must be implemented by the customer. |
| Cross site read-only replica for customer's metadata | Customer target and route configurations within {{site.data.keyword.atracker_full_notm}} are maintained in a regional database instance as well as in a read-only replica in the recovery region. This can be used in the event of a regional disaster to restore the region's metadata| For more information, see [High availability for PostgreSQL](/docs/databases-for-postgresql?topic=databases-for-postgresql-high-availability) |
| Cross site database backup for customer's metadata | Customer target and route configurations within {{site.data.keyword.atracker_full_notm}} are maintained in a cross regional {{site.data.keyword.cos_full_notm}} bucket in the recovery geo. This can be used in the event of a regional disaster to restore the region's metadata| For more information see [{{site.data.keyword.cos_full_notm}} cross region endpoints](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints#endpoints-geo) |
{: caption="DR features for {{site.data.keyword.atracker_full_notm}}" caption-side="bottom"}

### Planning for DR
{: #features-for-disaster-recovery}

The DR steps must be practiced regularly. As you build your plan, consider the following failure scenarios and resolutions.



| Failure | Resolution |
| -------------- | -------------- |
| Hardware failure (single point) | No configuration required. |
| Zone failure | No configuration required. |
| Metadata corruption | In the event of metadata corruption the {{site.data.keyword.atracker_full_notm}} service will first attempt to restore using a point in time backup from the regional database. If the database is no longer available in the region, the cross regional replica will be promoted to primary. If the cross regional replica is unavailable the database will be restored from the cross regional {{site.data.keyword.cos_full_notm}} backup. |
| Regional failure | Follow the steps under [Your responsibilities for HA and DR](#feature-responsibilities). |
{: caption="DR scenarios for {{site.data.keyword.atracker_full_notm}}" caption-side="bottom"}


## Your responsibilities for HA and DR
{: #feature-responsibilities}

Disaster recovery is about surviving a catastrophic failure or loss of availability in a single location. 

{{site.data.keyword.atracker_short}} is a platform service. There is no automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, {{site.data.keyword.atracker_short}} becomes unavailable in that location.

[You can create a configuration to route to a backup target in a different region.](/docs/atracker?topic=atracker-dr_config)
{: tip}

In the event of a regional disaster, you must complete the following steps to establish cross-region high availability:

1. Decide which location is going to be your recovery region. Choose 1 of the following options:

    - [Check the suggested DR recovery region](/docs/atracker?topic=atracker-atracker-ha-dr#ibm-disaster-recovery) and use that region as your recovery region.

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
3. If you had configured new targets, you can update your configuration to go back to use the targets that went down. You can also decide to continue using the targets that you enabled in the recovery region.



To find out more about responsibility ownership between you and {{site.data.keyword.cloud_notm}} for using {{site.data.keyword.atracker_full_notm}}, see [Understanding your responsibilities when using {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-shared-responsibilities). 

## Recovery time objective (RTO) and recovery point objective (RPO)
{: #rto-rpo-features}

The following table indicates the estimated recovery times in the event of a DR situation:

| Recovery objective for DR                                         | Estimated time |
|-------------------------------------------------------------------|----------------|
| Maximum Tolerable Downtime (MTD) / Recovery Time Objective (RTO)  | Less than 24 hours |
| Recovery Point Objective (RPO)                                    | Less than 24 hours |
{: caption="Recovery objectives for DR" caption-side="top"}

## Change management
{: #change-management}



Change management includes tasks such as upgrades, configuration changes, and deletion.

It is recommended that you grant users and processes the IAM roles and actions with the least privilege required for their work. See [How can I prevent accidental deletion of services?](/docs/resiliency?topic=resiliency-dr-faq#prevent-accidental-deletion).

## How {{site.data.keyword.IBM}} helps ensure disaster recovery
{: #ibm-disaster-recovery}

- {{site.data.keyword.IBM}} conducts annual tests of various disaster scenarios and continuously refines our recovery documentation based on findings that are found during these tests.
- 24 × 7 global support is available to customers with {{site.data.keyword.IBM}} Subject Matter Experts who are on call to help in the case of a disaster.

   All {{site.data.keyword.IBM}} Subject Matter Experts are trained annually on business continuity and disaster recovery policies and procedures to ensure preparedness in the event of a disaster.



The metadata that is managed by {{site.data.keyword.atracker_short}} in a region is kept in the data centers near that region.

A multizone region (MZR) consist of 3 or more availability zones that are independent from each other to ensure that single failure events affect only a single zone.

By default, {{site.data.keyword.atracker_short}} is deployed across 3 zones. Each zone is setup with `active/active/active`:
* Each zone is located in a different data center in the region.
* The events sent to the service are automatically replicated to the other zones with low latency. You don't need to do anything to enable the replication.
* The service is designed to withstand a single zone failure with no interruption.

The MZR architecture offers automatic failover between zones within the region, and high availability for a auditing instance within a region.

{{site.data.keyword.atracker_short}} metadata includes information on where and how to collect and store auditing events in your account for regional services and for global services such as IAM.
- A target is a resource where you can collect auditing events.
- A route is a resource that defines the rules that determine where auditing events are routed in your account.

{{site.data.keyword.atracker_short}} does regular backups of the metadata per region:
- Regular backups are done daily and retained for 30 days.
- Continuous incremental backups are kept for the last 7 days.

{{site.data.keyword.atracker_short}} metadata is replicated across multiple regions.
- Regular backups are stored across multiple regions, and are restorable to other regions.

The following table shows the regions where the copy of a regular backup is replicated and available:

| Geography             | Region                   | Other regions that keep a copy of the backup   |
|-----------------------|--------------------------|-------------------------|
| Asia Pacific        | Chennai `(in-che)`        | Tokyo `(jp-tok)`        |
| Asia Pacific        | Sydney `(au-syd)`        | London `(eu-gb)`        |
| Asia Pacific        | Tokyo `(jp-tok)`        | Osaka `(jp-osa)`        |
| Europe              | Frankfurt `(eu-de)`      | Madrid `(eu-es)`        |
| Europe              | London `(eu-gb)`         | Sydney `(au-syd)`       |
| Europe              | Madrid `(eu-es)`         | Frankfurt `(eu-de)`     |
| North America       | Dallas `(us-south)`      | Washington `(us-east)`  |
| North America       | Toronto `(ca-tor)`      | Washington `(us-east)`  |
| North America       | Washington `(us-east)`   | Dallas `(us-south)`     |
| South America       | Sao Paulo `(br-sao)`   | Washington `(us-east)`     |
{: caption="List of locations where a copy of the backup is available" caption-side="top"}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

The following table indicates the recovery region in the event of a DR situation:

| Geography             | Source region            | Recovery region   |
|-----------------------|--------------------------|--------------|
| Asia Pacific        | Chennai `(in-che)`        | Tokyo `(jp-tok)`     |
| Asia Pacific        | Sydney `(au-syd)`        | Frankfurt `(eu-de)`     |
| Asia Pacific        | Tokyo `(jp-tok)`        | Osaka `(jp-osa)`     |
| Europe              | Frankfurt `(eu-de)`      | Madrid `(eu-es)`        |
| Europe              | London `(eu-gb)`         | Frankfurt `(eu-de)`     |
| Europe              | Madrid `(eu-es)`         | Frankfurt `(eu-de)`     |
| North America       | Dallas `(us-south)`      | Washington `(us-east)`  |
| North America       | Toronto `(ca-tor)`      | Washington `(us-east)`  |
| North America       | Washington `(us-east)`   | Dallas `(us-south)`     |
| South America       | Sao Paulo `(br-sao)`   | Washington `(us-east)`     |
{: caption="List of locations where a region is recovered" caption-side="top"}


### How {{site.data.keyword.IBM_notm}} recovers from zone failures
{: #ibm-zone-failure}

In case of zone failure, IBM Cloud will resolve the zone outage. Since the service spans across all three zones in a region, there will be no impact to service availability within a MZR. Upon zone recovery, events and API requests will resume sending to the restored zone. There will be no need for customer action at this time.


### How {{site.data.keyword.IBM_notm}} recovers from regional failures
{: #ibm-regional-failure}

When {{site.data.keyword.atracker_short}} recovers in the region that is down, your configuration is restored. Complete the following steps to continue operating in the region that went down:
1. You must check that any existing targets in that region are also recovered and operational by confirming events are routed to the configured target destinations.
2. If you had to enable collection of global auditing events in the recovery region, you must update the route to stop global events in that region.
3. If you had configured new targets, you can update your configuration to go back to use the targets that went down. You can also decide to continue using the targets that you enabled in the recovery region.

If you follow the above steps and followed [disaster resiliant configuration](/docs/atracker?topic=atracker-dr_config), events should flow to the originally configured destination for the recovered region, once services sending events are restored and begin sending events to the recovered {{site.data.keyword.atracker_full_notm}} instance.





## How {{site.data.keyword.IBM_notm}} maintains services
{: #ibm-service-maintenance}


All upgrades follow the {{site.data.keyword.IBM_notm}} service best practices and have a recovery plan and rollback process in-place. Regular upgrades for new features and maintenance occur as part of normal operations. Such maintenance can occasionally cause short interruption intervals that are handled by [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha). Changes are rolled out sequentially, region-by-region and zone-by-zone within a region. Updates are backed out at the first sign of a defect.


Complex changes are enabled and disabled with feature flags to control exposure.


Changes that impact customer workloads are detailed in notifications. For more information, see [monitoring notifications and status](/docs/account?topic=account-viewing-cloud-status) for planned maintenance, announcements, and release notes that impact this service.
