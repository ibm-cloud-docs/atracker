---

copyright:
  years:  2021, 2024
lastupdated: "2024-12-09"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Learning about {{site.data.keyword.atracker_short}} architecture and workload isolation
{: #compute-isolation}

Review the following sample architecture for {{site.data.keyword.atracker_full}}, and learn more about different isolation levels so that you can choose the solution that best meets the requirements of the workloads that you want to run in the cloud.
{: shortdesc}



## {{site.data.keyword.atracker_full_notm}} architecture
{: #architecture}

{{site.data.keyword.at_full_notm}} is a multi-tenant, regional service that is available in {{site.data.keyword.cloud_notm}}. With {{site.data.keyword.atracker_short}}, you can manage collection and storage of auditing data to monitor and audit activity in your account.

The following figure shows the high level architecture for {{site.data.keyword.atracker_full_notm}}:

![A diagram that shows a sample {{site.data.keyword.atracker_short}} architecture.](../images/atracker_arch.svg "{{site.data.keyword.atracker_short}} architecture sample."){: caption="{{site.data.keyword.atracker_short}} sample architecture" caption-side="bottom"}

{{site.data.keyword.atracker_short}} is deployed and managed per region. See [List of supported regions](/docs/atracker?topic=atracker-regions). In each region, the service runs in three physically separate data centers to ensure availability.

All data and the configuration for each service deployment is retained within the region in which it is hosted.

You can use the {{site.data.keyword.atracker_full_notm}} CLI, the {{site.data.keyword.atracker_full_notm}} API, and {{site.data.keyword.atracker_full_notm}} Terraform to manage the service in your account. You must define targets and routes to define how to manage auditing events per region in your account.
- A target is a resource where you can collect auditing events.
- A route defines the rules that determine where auditing events that are genererated in the account are routed.

You can define account settings to define global configuration parameters that apply when  you configure the account.

In your account, auditing events are automatically collected from {{site.data.keyword.cloud_notm}} services that run in the account, with the exception of some services that require additional configuration to enable auditing events.
- For more information about services that generate events, see [Cloud services](/docs/atracker?topic=atracker-cloud_services_atracker).
- For more information about services that require additional configuration to generate events, see [Enabling Activity Tracker events](/docs/atracker?topic=atracker-events-opt-in).

After you configure targets and routes in the account, auditing events that are collected are uploaded to the destination target of your choice. You are responsible for managing the auditing data in the target resources.

The flow of all customer data between {{site.data.keyword.atracker_short}} and its dependencies uses private network connections. For more information about private connections, see [Securing your connection to {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-mng-data).


## Connections
{: #compute-isolation-connections}

You can use private and public endpoints to configure {{site.data.keyword.atracker_short}} resources in your account.

### Private connections
{: #compute-isolation-private-connections}

You cannot disable private endpoints.
{: note}


### Public connections
{: #compute-isolation-public-connections}

You can choose to disable public endpoints for {{site.data.keyword.atracker_short}}.

For more information, see [Enforcing private endpoints to configure {{site.data.keyword.atracker_short}} resources](/docs/atracker?topic=atracker-getting-started-mng-endpoints).


## Dependencies to other {{site.data.keyword.cloud_notm}} services
{: #compute-isolation-dependencies-cloud}

Review the {{site.data.keyword.cloud_notm}} services that {{site.data.keyword.atracker_short}} connects to over public or private connections.

| Service name | Description |
|------------|-------------------------------------|
| {{site.data.keyword.cis_full_notm}} | {{site.data.keyword.cis_full_notm}} is used as a provider for DNS and load-balancing capabilities. |
| {{site.data.keyword.containerlong_notm}} | {{site.data.keyword.atracker_short}} uses {{site.data.keyword.containerlong_notm}} to run its service. |
| {{site.data.keyword.mon_full_notm}} | {{site.data.keyword.atracker_short}} integrates with {{site.data.keyword.mon_short}}, by using a private connection, to send platform metrics. For more information, see [Monitoring metrics for {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-monitoring_metrics). |
| {{site.data.keyword.cos_full_notm}} | {{site.data.keyword.atracker_short}} stores customer data in {{site.data.keyword.cos_short}} by using a private connection. All data is encrypted in transit and at rest. For more information, see [Managing your data in {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-mng-data).|
| {{site.data.keyword.at_full_notm}} hosted event search | {{site.data.keyword.atracker_short}} stores customer data in {{site.data.keyword.at_short}} hosted event search by using a private connection. All data is encrypted in transit and at rest. For more information, see [Managing your data in {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-mng-data).|
| {{site.data.keyword.messagehub}} | {{site.data.keyword.atracker_short}} routes customer data to {{site.data.keyword.messagehub}} by using a private connection. All data is encrypted in transit and at rest. For more information, see [Managing your data in {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-mng-data).|
| {{site.data.keyword.cloud_notm}} Platform | To authenticate requests to the service and authorize user actions, {{site.data.keyword.atracker_short}} implements platform and service access roles in {{site.data.keyword.iamshort}} (IAM). For more information about required IAM permissions to work with the service, see [Managing access for {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-iam). Connections from {{site.data.keyword.atracker_short}} to IAM do not use private connections. |
| {{site.data.keyword.databases-for-postgresql_full_notm}} | {{site.data.keyword.atracker_short}} uses {{site.data.keyword.databases-for-postgresql_full_notm}}  for storing metadata. |
| {{site.data.keyword.logs_full_notm}} | {{site.data.keyword.atracker_short}} routes customer data to {{site.data.keyword.logs_full_notm}} by using a private connection. All data is encrypted in transit and at rest. For more information, see [Managing your data in {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-mng-data).|
{: caption="{{site.data.keyword.atracker_short}} dependencies to other {{site.data.keyword.cloud_notm}} services." caption-side="top"}
{: summary="The first column is the service. The second column is a description of the service."}



## Workload isolation
{: #compute-isolation-workload}


Each regional deployment serves multiple tenants that are identified by the {{site.data.keyword.cloud_notm}} account ID.

- There is 1 deployment per region that is responsible for running user workloads in the region.
- In a region, the deployment is highly available.
- The data that is collected is associated with the {{site.data.keyword.cloud_notm}} account ID and not visible to the other users by virtue of this association.
- Data for all tenants is co-located in the same data stores and segmented by the tenant-specific {{site.data.keyword.cloud_notm}} account ID to enforce access control policies.
- You can use IBM Cloud Identity and Access Management (IAM) to control which users see, create, use, and manage resources.
