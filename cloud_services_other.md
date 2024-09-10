---

copyright:
  years:  2021, 2024
lastupdated: "2024-09-10"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.cloud_notm}} services that generate events that are managed through {{site.data.keyword.at_short}} hosted event search
{: #cloud_services_other}

List of {{site.data.keyword.cloud}} services that generate auditing events in an {{site.data.keyword.cloud_notm}} account that you can only manage through {{site.data.keyword.at_short}} hosted event search instances.
{: shortdesc}

{{site.data.keyword.at_short}} hosted event search routes location-based auditing events to an {{site.data.keyword.at_short}} hosted event search instance in the region where they are generated and routes global auditing events to the {{site.data.keyword.at_short}} instance that is provisioned in Frankfurt. Some exceptions may apply, see [IBM Cloud services that generate Activity Tracker events by location](/docs/activity-tracker?topic=activity-tracker-cloud_services_locations).


## Analytics services
{: #cloud_services_other_analytics}

The following table lists analytics services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.sqlquery_full}}](/docs/sql-query?topic=sql-query-overview#overview) [Deprecated]{: tag-deprecated} | `sql-query` | [Location-based events](/docs/sql-query?topic=sql-query-activitytracker#activitytracker) |
{: caption="Table 1. List of analytics services" caption-side="top"}

## Database services
{: #cloud_services_other_database}

The following table lists database services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.Db2_on_Cloud_long}}](/docs/Db2onCloud?topic=Db2onCloud-about) | `db2oncloud` | [Location-based events](/docs/Db2onCloud?topic=Db2onCloud-auditing) |
{: caption="Table 2. List of database services" caption-side="top"}

`[*]` - Events provided by the BSS service.


## Network services
{: #cloud_services_other_network}

The following table lists network services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [Content Delivery Network](/docs/CDN#getting-started) [Deprecated]{: tag-deprecated} | `cdn-powered-by-akamai` | [Global events](/docs/CDN?topic=CDN-at_events)|
{: caption="Table 3. List of network services" caption-side="top"}

## Observability services
{: #cloud_services_other_observability}

The following table lists observability services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.at_full}} hosted event search offering](/docs/activity-tracker?topic=activity-tracker-getting-started) [Deprecated]{: tag-deprecated} | `logdnaat` | [Location-based events](/docs/activity-tracker?topic=activity-tracker-at_events) |
| [{{site.data.keyword.la_full}}](/docs/log-analysis?topic=log-analysis-getting-started#getting-started) [Deprecated]{: tag-deprecated} | `logdna` | [Location-based events](/docs/log-analysis?topic=log-analysis-at_events) |
{: caption="Table 4. List of observability services" caption-side="top"}


## Watson AI
{: #cloud_services_other_watson_ai}

The following table lists Watson AI services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.pm_full}}](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/ml-overview.html) | `pm-20` | [Location-based events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html?context=cpdaas#wml) |
{: caption="Table 5. List of Watson AI services" caption-side="top"}

## Cloud Pak
{: #cloud_pak}


The following table lists Cloud Pak services that send auditing events:

| Service     | Service name |   Events |
|-------------|--------------|--------|
| [{{site.data.keyword.cpd_short}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x){: external} | `cp4d`  | [List of events](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.8.x?topic=data-services-that-support-audit-logging){: external} |
| [{{site.data.keyword.cpd_short}} as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/welcome-main.html?context=cpdaas&audience=wdp){: external} | `cpdaas` | [List of events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html?context=cpdaas&audience=wdp){: external} |
{: caption="Table 6. List of {{site.data.keyword.cpd_full_notm}} services" caption-side="top"}
