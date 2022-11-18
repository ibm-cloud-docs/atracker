---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-11"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Incorrect usage error message when configuring an {{site.data.keyword.messagehub}} target
{: #troubleshoot-16}
{: troubleshoot}
{: support}

When attempting to create an {{site.data.keyword.atracker_full_notm}} `event_streams` target using the CLI, you are unable to do so and are getting errors indicating your command has an incorrect usage.
{: shortdesc}


Your CLI command return the message: `Incorrect usage. Check the command syntax and retry your request.`
{: tsSymptoms}

Configuration of `event_streams` targets using the CLI requires the `atracker` CLI plug-in at 0.3.2 or later.
{: tsCauses}

Upgrade the `atracker` CLI plug-in by running `ibmcloud plugin update atracker` and retry your CLI command.
{: tsResolve}
