---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-11"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Incorrect permissions message when configuring an {{site.data.keyword.messagehub}} target
{: #troubleshoot-18}
{: troubleshoot}
{: support}

When attempting to create an {{site.data.keyword.atracker_full_notm}} `event_streams` target using the CLI, you are unable to do so and are getting errors indicating your command failed because you do not have the correct permissions to perform the action.
{: shortdesc}


Your CLI command return the message: `You do not have the correct permissions to perform this action. Ask your account administrator to grant you the account management Editor platform role for Activity Tracker Event Routing service and try again.`
{: tsSymptoms}

Your IAM `atracker` permissions for {{site.data.keyword.atracker_full_notm}} are not defined correctly.
{: tsCauses}

[Correct your `atracker` IAM policy definitions](/docs/atracker?topic=atracker-target_v2_ies#target_v2_iam_access_ies) and retry your CLI command.
{: tsResolve}
