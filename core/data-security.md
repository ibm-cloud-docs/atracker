---

copyright:
  years: 2019, 2023, 2024
lastupdated: "2024-05-31"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}


# Securing your data
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.atracker_short}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored data.
{: shortdesc}



## What data is stored in {{site.data.keyword.atracker_short}}
{: #mng-data-stored}

When you use {{site.data.keyword.atracker_short}} to manage your audit events, you should differentiate between configuration data and audit data.


### Configuration data
{: #mng-data-config}


To configure {{site.data.keyword.atracker_short}}, you must configure account settings, targets, and routes. You can configure {{site.data.keyword.atracker_short}} via REST API calls, CLI commands, or by using terraform scripts. The definitions of these resources are hosted on the {{site.data.keyword.cloud_notm}}.

- You can configure the {{site.data.keyword.atracker_short}} account settings to indicate the primary and backup metadata locations where global definitions are stored such as route definitions and the type of endpoints that are enabled.

    You can set the primary metadata location by configuring the account settings. Alternatively, when you define the first target in the account; the location where the target is defined is automatically set as the primary location.

    You must configure the account settings to define the backup metadata location. This location is optional.

-  You can define [targets](/docs/atracker?topic=atracker-atracker-resources#atracker-resources-targets) in any [supported region](/docs/atracker?topic=atracker-regions).

    You can control the locations in the account where a target is defined by specifying the allowed locations in the {{site.data.keyword.atracker_short}} account settings.

    Targe definitions are stored in the primary metadata location. If you have a backup metadata location, target definitions are also stored there.

- Route definitions are stored in the primary metadata location. If you have a backup metadata location, route definitions are also stored there.


### Auditing data
{: #mng-data-audit}

{{site.data.keyword.atracker_short}} collects management and data events from {{site.data.keyword.cloud_notm}} services and resources:
* **Management Events** are generated when an API call changes the state of a Cloud resource. A resource might be an entire service instance or a resource managed by the service.
* **Data Events** are generated when an API call reads or modifies a resource's data.

Data from [{{site.data.keyword.cloud_notm}} services and resources](/docs/atracker?topic=atracker-cloud_services_atracker) is collected automatically.  However, some services might require an upgrade of the service plan, a configuration setting, or both, for you to be able to collect and analyze them.

{{site.data.keyword.atracker_short}} does not store auditing events. By configuring {{site.data.keyword.atracker_short}}, you define the target where the auditing data that is generated in the account is routed and uploaded. You can route auditing events to targets that are available in the account or in a different account.
{: note}


## How your data is stored and encrypted
{: #data-storage}

### Configuration data
{: #mng-data-storage-config}

You can configure {{site.data.keyword.atracker_short}} resources by using public and private endpoints.

To ensure that you have enhanced control and security over your data, your account must be virtual routing and forwarding (VRF) enabled and you must use private routes to {{site.data.keyword.cloud}} service endpoints. Consider configuring {{site.data.keyword.atracker_short}} resources over a private network connection.
{: note}

{{site.data.keyword.atracker_short}} stores the configuration of settings, targets and routes for your account.
- Connections use TLS/SSL encryption for data in transit. The current supported version of this encryption is TLS 1.2.
- The storage where the configuration is stored is encrypted with LUKS using AES-256.


### Auditing data
{: #mng-data-storage-audit}

You can define 1 or more routing rules that define how auditing events are routed in the account. Auditing data from an {{site.data.keyword.cloud_notm}} service to your target service in {{site.data.keyword.cloud_notm}} is secure via private connection. The connection supports TLS 1.2.

You can route auditing data to any of the following target types:
- An {{site.data.keyword.cos_full_notm}} bucket: You create and manage the bucket, and the data that is collected in the bucket. For more information about COS data security, see [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security).
- An {{site.data.keyword.at_short}} instance: You manage the instance and the data that is collected in the instance. For more information, see [Data security](/docs/activity-tracker?topic=activity-tracker-mng-data).
- An {{site.data.keyword.logs_full_notm}} instance: You manage the instance and the data that is collected in the instance. For more information, see [Data security](/docs/cloud-logs?topic=cloud-logs-mng-data).
- An {{site.data.keyword.messagehub}} topic: You create and manage the topic. For more information, see [Data security](/docs/EventStreams?topic=EventStreams-data_security).


## How can you delete any stored data
{: #mng-data-storage-delete}

### Configuration data
{: #mng-data-storage-delete-config}


{{site.data.keyword.atracker_short}} stores configuration data only.

You can delete any route, target and account setting configuration by using the API, the CLI or terraform scripts.

- To stop {{site.data.keyword.atracker_short}} from routing audit events to the configured targets, you must [remove any default targets](/docs/atracker?topic=atracker-target-default-reset) and delete all routes.
- To delete auditing event destinations, you must delete the target definitions.
- To remove any account setting, you can reset the account default settings.


### Auditing data
{: #mng-data-storage-delete-audit}

To delete auditing data, check the target type instructions.

- For {{site.data.keyword.cos_full_notm}} bucket, see [Data security](/docs/cloud-object-storage?topic=cloud-object-storage-security).
- For {{site.data.keyword.at_short}} instance, see [Data security](/docs/activity-tracker?topic=activity-tracker-mng-data).
- For {{site.data.keyword.messagehub}}, see [Data security](/docs/EventStreams?topic=EventStreams-data_security).
- For {{site.data.keyword.logs_full_notm}}, see [Data security](/docs/cloud-logs?topic=cloud-logs-mng-data).
