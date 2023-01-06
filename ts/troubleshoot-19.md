---

copyright:
  years: 2019, 2023
lastupdated: "2022-11-11"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# No such host message when configuring an {{site.data.keyword.messagehub}} target
{: #troubleshoot-19}
{: troubleshoot}
{: support}

When attempting to create an {{site.data.keyword.atracker_full_notm}} `event_streams` target using the CLI, you are unable to do so and are getting errors indicating there is no such host.
{: shortdesc}


Your CLI command return a message similar to: `Error:  Post "https://xx-xx.atracker.cloud.ibm.com/api/v2/targets": dial tcp: lookup xx-xx.atracker.cloud.ibm.com: no such host.`
{: tsSymptoms}

You are attempting to configure a target in a region that is not supported. For example, by specifying `--region xx-xx` on the command.
{: tsCauses}

[Specify a supported region](/docs/atracker?topic=atracker-regions) and retry your CLI command.
{: tsResolve}
