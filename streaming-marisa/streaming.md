---

copyright:
  years: 2019, 2023
lastupdated: "2022-07-21"

keywords:

subcollection: activity-tracker

---

{{site.data.keyword.attribute-definition-list}}

# Streaming data
{: #streaming}


Stream data from an {{site.data.keyword.at_full_notm}} instance to other corporate tools such as Security Information and Event Management (SIEM) tools.
{: shortdesc}

When you stream data to data lakes, other analysis tools, or other SIEM tools, you can add additional capabilities to the ones provided by the {{site.data.keyword.at_short}} service:
- You can gain visibility into enterprise data across on-premises and cloud-based environments.
- You can identify and prioritize security threats that might affect your organization.
- You can detect vulnerabilities by using Artificial Intelligence (AI) to investigate threats and incidents.

You can stream data to an {{site.data.keyword.messagehub}} instance or to an {{site.data.keyword.at_short}} instance. For example, when you enable streaming on an {{site.data.keyword.at_short}} instance, you configure {{site.data.keyword.at_short}} to send data to an {{site.data.keyword.messagehub}} instance. Then, you can configure Kafka Connect to consume the data and forward it to your destination tool. Once the data is persisted within {{site.data.keyword.messagehub}}, you can configure any application or service to create a subscription and take action on log data being streamed.

![Streaming example with {{site.data.keyword.messagehub}}](images/at_streams.svg "Streaming examples with {{site.data.keyword.messagehub}}"){: caption="Figure 1. Streaming example with {{site.data.keyword.messagehub}}" caption-side="bottom"}

You can also also configure streaming from one {{site.data.keyword.at_short}} instance to a second {{site.data.keyword.at_short}} instance.

![Activity Tracker to Activity Tracker streaming](images/at_to_at.svg "Activity Tracker to Activity Tracker streaming"){: caption="Figure 2. Activity Tracker to Activity Tracker streaming" caption-side="bottom"}

You can only stream from one {{site.data.keyword.at_short}} instance to one other {{site.data.keyword.at_short}} instance. You cannot stream from the second {{site.data.keyword.at_short}} instance to another {{site.data.keyword.at_short}} instance.
{: important}

Currently, you can only stream up to 1TB of data per day.
{: note}

If you have any regulatory requirement for data residency and compliance needs, you must control the location where {{site.data.keyword.at_short}}, {{site.data.keyword.messagehub}}, Kafka Connect and the destination tool are available.
{: important}



## Configure streaming
{: #streaming-1}

Consider the following information when streaming data to an {{site.data.keyword.messagehub}} instance:
- You must have **manager** role to configure streaming in the {{site.data.keyword.at_short}}  instance. This role includes the **logdnaat.dashboard.manage** IAM action role that allows a user to perform admin tasks such as configure streaming.
- When you configure streaming, the {{site.data.keyword.at_short}}  instance and the {{site.data.keyword.messagehub}} instance must be provisioned in the same account.
- To connect the {{site.data.keyword.at_short}}  instance to the {{site.data.keyword.messagehub}} instance, you need the following information:

    - Endpoint URLs to call the APIs

    - Credentials for authentication
- To create a topic in {{site.data.keyword.messagehub}}, you must have **manager** role. This role includes the **messagehub.topic.manage** IAM action role that allows an app or user to create or delete topic.
- The credential that {{site.data.keyword.at_short}}  uses to publish data in {{site.data.keyword.messagehub}} must have **writer** role. This role includes the **messagehub.topic.write** IAM action role that allows an app or service to write data to 1 or more topics.

Consider the following information when streaming data to an {{site.data.keyword.at_short}} instance:
- You must have **manager** role to configure streaming in the {{site.data.keyword.at_short}} instance. This role includes the **logdnaat.dashboard.manage** IAM action role that allows a user to perform admin tasks such as configure streaming.
- When you configure streaming, the source {{site.data.keyword.at_short}} instance and the destination {{site.data.keyword.at_short}} instance can be provisioned in the same account or in different accounts.
- To connect the source {{site.data.keyword.at_short}} instance to the destination {{site.data.keyword.at_short}}  instance, you need the following information:

    - Destination {{site.data.keyword.at_short}} ingestion URL

    - Ingestion key for the destination {{site.data.keyword.at_short}}  for authentication

- If you have any regulatory restriction to keep data within specific regions, make sure streaming is only configured to a valid destination.


## Monitor streaming
{: #streaming-2}

To monitor streaming, you can use the following services:

- {{site.data.keyword.mon_full_notm}} service to monitor streaming to an {{site.data.keyword.messagehub}} instance:

    {{site.data.keyword.messagehub}} is integrated with the {{site.data.keyword.mon_short}} service. {{site.data.keyword.mon_short}} provides a default template that you can customize to monitor the {{site.data.keyword.messagehub}} instance, how data is streamed out of {{site.data.keyword.at_short}} and consumed by any application or service that is subscribed to {{site.data.keyword.messagehub}}.

    For more information, see [Monitoring streaming by using {{site.data.keyword.mon_full_notm}}](/docs/activity-tracker?topic=activity-tracker-streaming-monitor#streaming-monitor-1).

- {{site.data.keyword.at_full_notm}}:

    Streaming generates {{site.data.keyword.at_short}} events with the action **logdnaat.streaming-logs.send** to notify of failures sending data. There are different reasons for failure such as invalid credentials and topic deleted.

    For more information, see [Monitoring streaming by using {{site.data.keyword.at_short}}](/docs/activity-tracker?topic=activity-tracker-streaming-monitor#streaming-monitor-2).


## Conditional streaming
{: #streaming-3}

You can configure exclusion rules to filter out data from streaming. For more information, see [Configuring conditional streaming](/docs/activity-tracker?topic=activity-tracker-streaming-conditional).

- You configure streaming exclusion rules through **Settings** &gt; **Streaming** &gt; **Exclusion rules**.
- The exclusion rules that you define for streaming are different from the exclusion rules that you can define at the instance level through **Settings** &gt; **Usage** &gt; **Exclusion rules**.

When you define exclusion rules, either at the instance level, or for streaming, they are applied as follows:
- Exclusion rules that you define at the instance level are applied first.
- Only the data that is retained and available for search is in scope of the exclusion rules that you define for streaming.
- After a streaming exclusion rule is active, data that matches the filter criteria is not streamed.
- Conditions that are applied by a query are enforced.



## {{site.data.keyword.at_short}} events
{: #streaming-4}

The following {{site.data.keyword.at_short}} events are generated when you configure streaming:

| Action | Description |
|--------|-------------|
| `logdnaat.streaming-configuration.validate`   | This event is generated when you configure the connection in {{site.data.keyword.at_short}} to {{site.data.keyword.messagehub}}. |
| `logdnaat.streaming-samples.send`             | This event is generated when sample data is sent to verify the connection. |
| `logdnaat.account-streaming-setting.configure`| This event is generated when you start streaming. |
| `logdnaat.streaming-configuration.deactivate` | This event is generated when you stop streaming. |
| `logdnaat.streaming-logs.send`              | This event is generated when there is a failure streaming data. |
| `logdnaat.exclusion-rule.create`            | This event is generated when an streaming exclusion rule is configured. |
| `logdnaat.exclusion-rule.delete`            | This event is generated when an streaming exclusion rule is deleted. |
{: caption="Streaming events" caption-side="bottom"}
