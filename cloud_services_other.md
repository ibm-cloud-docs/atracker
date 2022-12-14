---

copyright:
  years: 2019, 2023
lastupdated: "2022-08-08"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.cloud_notm}} services that generate events that are managed through {{site.data.keyword.at_short}} hosted event search
{: #cloud_services_other}

List of {{site.data.keyword.cloud}} services that generate auditing events in an {{site.data.keyword.cloud_notm}} account that you can only manage through {{site.data.keyword.at_short}} hosted event search instances.
{: shortdesc}

{{site.data.keyword.at_short}} hosted event search routes location-based auditing events to an {{site.data.keyword.at_short}} hosted event search instance in the region where they are generated and routes global auditing events to the {{site.data.keyword.at_short}} instance that is provisioned in Frankfurt. Some exceptions may apply, see [IBM Cloud services that generate Activity Tracker events by location](/activity-tracker?topic=activity-tracker-cloud_services_locations&interface=cli).


## Analytics services
{: #cloud_services_other_analytics}

The following table lists analytics services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.iae_full}}](/docs/AnalyticsEngine?topic=AnalyticsEngine-getting-started) | `ibmanalyticsengine` | [Location-based events](/docs/AnalyticsEngine?topic=AnalyticsEngine-at_events) |
| [{{site.data.keyword.sqlquery_full}}](/docs/sql-query?topic=sql-query-overview#overview) | `sql-query` | [Location-based events](/docs/sql-query?topic=sql-query-activitytracker#activitytracker) |
| [{{site.data.keyword.dv_short}}](/docs/data-virtualization?topic=data-virtualization-about) | `data-virtualization` | [Location-based events](/docs/data-virtualization?topic=data-virtualization-activity-tracker) |
{: caption="Table 1. List of analytics services" caption-side="top"}


## Cloud Foundry applications
{: #cloud_services_other_cfapps}

The events that are sent by Cloud Foundry applications to {{site.data.keyword.cloudaccesstrailshort}} are listed in the response area of the `GET /v2/events`, under the body section. The *Type* field lists all actions that generate an event. For more information, see the [Events API](https://apidocs.cloudfoundry.org/270/events/list_all_events.html){: external}.

## Compute serverless services
{: #cloud_services_other_serverless}

The following table lists serverless compute services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.openwhisk}}](/docs/openwhisk?topic=openwhisk-getting-started) | `functions` | [Location-based events](/docs/openwhisk?topic=openwhisk-at_events) |
{: caption="Table 2. List of serverless compute services" caption-side="top"}



## Database services
{: #cloud_services_other_database}

The following table lists database services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.databases-for-enterprisedb_full}}](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-getting-started) | `databases-for-enterprisedb-group` | [Location-based events](/docs/databases-for-enterprisedb?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.databases-for-cassandra_full}}](/docs/databases-for-cassandra?topic=databases-for-cassandra-getting-started) | `databases-for-cassandra-group` | [Location-based events](/docs/databases-for-enterprisedb?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.databases-for-postgresql_full}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started) | `databases-for-postgresql` | [Location-based events](/docs/databases-for-postgresql?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.databases-for-redis_full_notm}}](/docs/databases-for-redis?topic=databases-for-redis-getting-started) | `databases-for-redis-group` | [Location-based events](/docs/databases-for-redis?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.databases-for-etcd_full_notm}}](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) | `databases-for-etcd-group` | [Location-based events](/docs/databases-for-etcd?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.databases-for-elasticsearch_full_notm}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-getting-started) | `databases-for-elasticsearch-group` | [Location-based events](/docs/databases-for-elasticsearch?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.messages-for-rabbitmq_full}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started)  | `messages-for-rabbitmq-group` | [Location-based events](/docs/messages-for-rabbitmq?topic=cloud-databases-activity-tracker) |
| [{{site.data.keyword.databases-for-mongodb_full_notm}}](/docs/databases-for-mongodb) | `databases-for-mongodb-group` | [Location-based events](/docs/databases-for-mongodb?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.databases-for-mysql_full}}](/docs/databases-for-mysql) | `databases-for-mysql-group` | [Location-based events](/docs/databases-for-mysql?topic=cloud-databases-activity-tracker-integration) |
| [{{site.data.keyword.Db2_on_Cloud_long}}](/docs/Db2onCloud?topic=Db2onCloud-about) | `db2oncloud` | [Location-based events](/docs/Db2onCloud?topic=Db2onCloud-activity-tracker) |
| [{{site.data.keyword.dashdblong_notm}}](/docs/Db2whc?topic=Db2whc-getting-started) | `dashdb` | [Global events](/docs/atracker?topic=atracker-at_events_dashdb) |
{: caption="Table 3. List of database services" caption-side="top"}

`[*]` - Events provided by the BSS service.

## Developer tools
{: #cloud_services_other_devops}

The following table lists developer tools and DevOps services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.cloud-shell_full}}](/docs/cloud-shell?topic=cloud-shell-getting-started) | `cloudshell` | [Location-based events](/docs/cloud-shell?topic=cloud-shell-at_events) |
| [{{site.data.keyword.mobilepushfull}}](/docs/mobilepush?topic=mobilepush-getting-started) | `imfpush` | [Location-based events](/docs/mobilepush?topic=mobilepush-at_events#at_actions) |
{: caption="Table 4. List of developer tools services" caption-side="top"}


The following table lists {{site.data.keyword.contdelivery_full}} services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.contdelivery_full}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started) | `continuous-delivery` | [Location-based events](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd-at-events) |
| [Toolchain](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd_about) | `toolchain` | [Location-based events](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd-at-events#toolchain-events) |
{: caption="Table 5. List of developer tools services" caption-side="top"}



## Integration services
{: #cloud_services_other_integration}

The following table lists integration services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [MQ on IBM Cloud](/docs/mqcloud?topic=mqcloud-mqoc_getting_started) |`mqcloud` | [Location-based events](/docs/mqcloud?topic=mqcloud-at_events) |
|[{{site.data.keyword.apiconnect_long}}](/docs/apiconnect?topic=apiconnect-getting-started)| `apiconnect` | [Location-based events](/docs/apiconnect?topic=apiconnect-at_events) |
{: caption="Table 6. List of integration Cloud services" caption-side="top"}



## Network services
{: #cloud_services_other_network}

The following table lists network services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [Content Delivery Network](/docs/CDN#getting-started) | `cdn-powered-by-akamai` | [Global events](/docs/CDN?topic=CDN-at_events)|
{: caption="Table 7. List of network services" caption-side="top"}

## Observability services
{: #cloud_services_other_observability}

The following table lists observability services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.at_full}} hosted event search offering](/docs/atracker?topic=atracker-getting-started) | `logdnaat` | [Location-based events](/docs/atracker?topic=atracker-at_events) |
| [{{site.data.keyword.la_full}}](/docs/log-analysis?topic=log-analysis-getting-started#getting-started) | `logdna` | [Location-based events](/docs/log-analysis?topic=log-analysis-at_events) |
| [{{site.data.keyword.mon_full}}](/docs/monitoring?topic=monitoring-getting-started) | `sysdig-monitor` | [Location-based events](/docs/monitoring?topic=monitoring-at_events) |
{: caption="Table 8. List of observability services" caption-side="top"}


## Security services
{: #cloud_services_other_security}

The following table lists security Cloud services that send auditing events:


| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.keymanagementservicelong}}](/docs/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) | `kms` | [Location-based events](/docs/key-protect?topic=key-protect-at-events) |
| [{{site.data.keyword.cloudcerts_full}}](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) | `cloudcerts` | [Location-based events](/docs/certificate-manager?topic=certificate-manager-at_events#at_events) |
{: caption="Table 9. List of security services" caption-side="top"}




## Watson AI
{: #cloud_services_other_watson_ai}

The following table lists Watson AI services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.DSX_full}}](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/overview-ws.html) | `data-science-experience`  | [Location-based events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html#ws) |
| [IBM Watson&trade; Knowledge Catalog](https://dataplatform.cloud.ibm.com/docs/content/wsj/catalog/overview-wkc.html) | `datacatalog` | [Location-based events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html#wkc) |
| [{{site.data.keyword.languagetranslatorfull}}](/docs/language-translator?topic=language-translator-gettingstarted) | `language-translator` | [Location-based events](/docs/language-translator?topic=language-translator-at_events) |
| [{{site.data.keyword.pm_full}}](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/ml-overview.html) | `pm-20` | [Location-based events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html#wml) |
{: caption="Table 10. List of Watson AI services" caption-side="top"}
