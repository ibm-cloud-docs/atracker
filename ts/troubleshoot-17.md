---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-11"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Target details are not valid message when configuring an {{site.data.keyword.messagehub}} target
{: #troubleshoot-17}
{: troubleshoot}
{: support}

When attempting to create an {{site.data.keyword.atracker_full_notm}} `event_streams` target using the CLI, you are unable to do so and are getting errors indicating your command failed because the target details are not valid.
{: shortdesc}


Your CLI command return the message: `Your request to test a target has failed because the target details are not valid. The service could not write to the Event Streams topic that is configured.`
{: tsSymptoms}

If you are limiting access to a specific {{site.data.keyword.messagehub}} topic, you must have an IAM policy defined for both the policy and cluster.
{: tsCauses}

[Correct your {{site.data.keyword.messagehub}} IAM policy definitions](/docs/atracker?topic=atracker-target_v2_ies#target_es) and retry your CLI command.
{: tsResolve}
