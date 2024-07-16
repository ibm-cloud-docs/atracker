---

copyright:
  years:  2021, 2024
lastupdated: "2024-07-16"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using {{site.data.keyword.atracker_short}}
{: #shared-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.atracker_short}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.atracker_short}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms of Use](/docs/overview?topic=overview-terms).


## Incident and operations management
{: #incident-and-ops}

| Task              | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-------------------|-------------------------------------------------|-----------------------|
| Incident and operations management | Maintain service instances and infrastructure workloads. | Maintain incident and operations management of your data. |
| Monitor incidents  | Provide notifications for planned maintenance, security bulletins, or unplanned outages. | * Set preferences to [receive emails about platform notifications](/docs/get-support?topic=get-support-viewing-cloud-status).   \n * Monitor the [IBM Cloud status page](https://{DomainName}/status?selected=announcement) for general announcements. |
| Maintain {{site.data.keyword.cloud_notm}} high availability SLA for {{site.data.keyword.atracker_short}}   | * Provide {{site.data.keyword.atracker_short}} functionality across availability zones in a Multi-Zone Region (MZR).  \n * Provide replication, fail-over features, and infrastructure maintenance and updates. | * Keep your {{site.data.keyword.atracker_short}}  configuration in a version control system so that you can reconfigure a region if needed.   \n * Comply with [Operational responsibilities when using {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-shared-responsibilities).  \n * Comply with [Operational responsibilities when using {{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-responsibilities#responsibilities-operational).  \n * Comply with [Operational responsibilities when using {{site.data.keyword.at_short}} hosted event search](/docs/activity-tracker?topic=activity-tracker-shared-responsibilities).  \n * Comply with [Operational responsibilities when using {{site.data.keyword.messagehub_full}}](/docs/EventStreams?topic=EventStreams-event_streams_responsibilities). |
| Monitor events for {{site.data.keyword.atracker_short}}  | [Participating Cloud services](/docs/atracker?topic=atracker-cloud_services_atracker) publish relevant event data to their subscribing clients. Clients have the ability to receive this data once their account is configured. | [Configure your account](/docs/atracker?topic=atracker-getting-started) where Cloud service subscriptions publish events to receive the published events. Notice that {{site.data.keyword.atracker_short}}  can only route events that are generated in [supported regions](/docs/atracker?topic=atracker-regions). Other regions, where {{site.data.keyword.atracker_short}}  is not available, continue to manage events by using {{site.data.keyword.at_short}} hosted event search. |
| Monitor {{site.data.keyword.atracker_short}} targets  |  |  Check the health and status of the targets through {{site.data.keyword.mon_short}} by configuring alerts to notify of problems writing events to a target, and generate notifications, for example, to the {{site.data.keyword.en_full_notm}} service. |
{: caption="Table 1. Responsibilities for incident and operations" caption-side="top"}


## Change management
{: #change-management}

| Task                                                    | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|---------------------------------------------------------|-----------------------|--------|
| Updates to {{site.data.keyword.atracker_short}} | Provide major, minor, and patch version updates for {{site.data.keyword.atracker_short}} interfaces.   \n Document changes in the [IBM Cloud Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter) | `N/A` |
{: caption="Table 2. Responsibilities for change management" caption-side="top"}



## Identity and access management
{: #iam-responsibilities}


| Task                           | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------|-------------------------------------------------|-----------------------|
| Manage permissions for {{site.data.keyword.atracker_short}} | Provide the ability to restrict access to resources.   \n {{site.data.keyword.IBM_notm}} is responsible for the security and compliance of the {{site.data.keyword.atracker_short}} feature. | Restrict access to {{site.data.keyword.atracker_short}} and supported destinations such as Cloud Object Storage resources by using Cloud IAM access policies. Define IAM policies to control which users within your account have access to manage the service and related resources in your account.    \n [Learn more about controlling access through IAM](/docs/atracker?topic=atracker-iam).|
| Validate targets for {{site.data.keyword.atracker_short}} | Provide the ability to check if the credentials that are used by {{site.data.keyword.atracker_short}}  are valid and allow uploading of objects to the bucket or routing of events to an   | [Configure 1 or more targets](/docs/atracker?topic=atracker-atracker-resources&interface=cli#atracker-resources-targets) with valid credentials to store auditing events. [Validate the credentials](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target-validate-cli-cos) that are used by {{site.data.keyword.atracker_short}}. |
{: caption="Table 3. Responsibilities for identity and access management" caption-side="top"}



## Security and regulation compliance
{: #security-compliance}


| Task                                       | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------------------|-------------------------------------------------|-----------------------|
| Meet security and compliance objectives  | Maintain controls that are commensurate to various industry compliance standards such the Financial Services specification. For more information, see [Securing your data](/docs/atracker?topic=atracker-mng-data).| Set up and maintain security and regulation compliance for your apps and data.  \n When using a `cloud_object_storage` target, ensure encryption of auditing data by configuring a COS bucket that has full control over the data encryption keys that are used. [{{site.data.keyword.cos_full}} provides several options to encrypt your data.](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)  |
{: caption="Table 4. Responsibilities for security and regulation compliance" caption-side="top"}



## Disaster recovery
{: #disaster-recovery}


| Task                                                            | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-----------------------------------------------------------------|-------------------------------------------------|-----------------------|
| Restore functionality for {{site.data.keyword.atracker_short}}  | Automatically recover and restart {{site.data.keyword.atracker_short}} components after any disaster event.    \n In case of a regional disaster, {{site.data.keyword.cloud_notm}} service teams, who are responsible for the operations of services that generate auditing events, will point their service to {{site.data.keyword.atracker_short}} endpoints in their alternate region within the same regulatory boundaries. | [Complete the disaster recovery (DR) steps for {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-ha_dr). |
| Backup {{site.data.keyword.atracker_short}} components   | Daily backup of the {{site.data.keyword.atracker_short}} infrastructure and components. | `N/A` |
{: caption="Table 5. Responsibilities for disaster recovery" caption-side="top"}

`[*]` Recovered and restarted service components will not have customer data reloaded.
{: note}
