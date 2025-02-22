---

copyright:
  years:  2021, 2025
lastupdated: "2025-02-22"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Enabling Activity Tracker events
{: #events-opt-in}

In {{site.data.keyword.at_full_notm}}, events are collected automatically for most enabled-services. However, some services might require an upgrade of the service plan, a configuration setting, or both, for you to be able to collect and analyze them.
{: shortdesc}




## Management events
{: #events-opt-in_mgt}

The following table lists the services that require additional steps for you to be able to monitor [management events](/docs/atracker?topic=atracker-event_types#event_types_management) that they generate:

| Service                            | Upgrade plan                       | Configure the service              | More info |
|------------------------------------|------------------------------------|------------------------------------|-----------|
| [Watson services](/docs/atracker?topic=atracker-cloud_services_atracker) `[*]`  | ![Checkmark icon](../../icons/checkmark-icon.svg) |  |   |
{: caption="{{site.data.keyword.cloud_notm}} services that require actions for management events" caption-side="top"}

`[*]` You might need to upgrade to a paid plan to enable collection of Watson Activity Tracker events in your account. See [Details per Watson service](/docs/atracker?topic=atracker-cloud_services_atracker) to check requirements by service.


## Data events
{: #events-opt-in_data}

The following table lists the services that require additional steps for you to be able to monitor [data events](/docs/atracker?topic=atracker-event_types#event_types_data) that they generate:

| Service                            | Upgrade plan                       | Configure the service              | More info |
|------------------------------------|------------------------------------|------------------------------------|-----------|
| {{site.data.keyword.appid_full}}   | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg)   | [Monitoring runtime activity](/docs/appid?topic=appid-at-events#at-monitor-runtime-activity)   |
| {{site.data.keyword.cos_full}}     |  | ![Checkmark icon](../../icons/checkmark-icon.svg) | [Enabling {{site.data.keyword.atracker_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-at&interface=ui#at-examples-recommended) |
| {{site.data.keyword.cloudantfull}} |  | ![Checkmark icon](../../icons/checkmark-icon.svg) | [Configuring data events for an IBM Cloudant instance](/docs/Cloudant?topic=Cloudant-at_events#at_event_configure) |
| {{site.data.keyword.messagehub_full}} | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | [Enabling message audit events](/docs/EventStreams?topic=EventStreams-at_events#enable-message-events) |
| [Watson services](/docs/atracker?topic=atracker-cloud_services_atracker)    | ![Checkmark icon](../../icons/checkmark-icon.svg) |  |   |
{: caption="{{site.data.keyword.cloud_notm}} services that require actions for data events" caption-side="top"}


## Details per Watson service
{: #events-opt-in_watson}

The following table lists the Watson services and related information about additional steps that you might need to be able to monitor events:

| Service Name | Paid plan required | Other configuration required |
|--|--|--|
| {{site.data.keyword.conversationfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg)   \n Premium & Enterprise Plans only feature | |
| {{site.data.keyword.discoveryfull}} |   |   |
| {{site.data.keyword.DSX_full}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| IBM Watson&trade; Knowledge Catalog | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.pm_full}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.knowledgestudiofull}} |  |   |
| {{site.data.keyword.languagetranslatorfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.nlufull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.speechtotextfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.texttospeechfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
{: caption="Watson services that require actions for data events" caption-side="top"}

The following table lists Watson services that are deprecated:

| Service Name | Paid plan required | Other configuration required |
| -- | -- | -- |
| {{site.data.keyword.cncfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.visualrecognitionfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.iva_full}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.nlclassifierfull}} | ![Checkmark icon](../../icons/checkmark-icon.svg) |   |
| {{site.data.keyword.wh-acd_full}} |   |   |
{: caption="Watson services that require actions for data events and are deprecated" caption-side="top"}
