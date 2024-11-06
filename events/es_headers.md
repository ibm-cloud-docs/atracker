---

copyright:
  years:  2021, 2024
lastupdated: "2024-11-06"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Using {{site.data.keyword.messagehub}} header data
{: #es_headers}

{{site.data.keyword.atracker_full}} adds header information to activity tracking events routed to {{site.data.keyword.messagehub_full}} targets.
{: shortdesc}

The data included in the {{site.data.keyword.messagehub_full_notm}} header can be used to filter events routed by {{site.data.keyword.atracker_full_notm}} from multiple locations to a single {{site.data.keyword.messagehub_full_notm}}.

Each activity tracking event sent to {{site.data.keyword.messagehub_full_notm}} includes the following header information:



| Key | Value |
|--------------|-------------------|
| `type` | Is always `audit`. |
| `account` | The account where the activity tracking event applies. |
| `region` | The target region where the event was processed. |
| `location` | The location field from the `logSourceCRN` identifying the source of the activity tracking event. |
{: caption="Header key values" caption-side="bottom"}
