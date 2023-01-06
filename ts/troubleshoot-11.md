---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-13"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting a "setting limit" error when creating a target?
{: #troubleshoot-11}
{: troubleshoot}
{: support}

When creating a default target, the following message is returned: `Your request has failed because default_targets per setting limit 2 is reached.`.
{: shortdesc}


Your request fails with an error message and a code of `invalid_value`.
{: tsSymptoms}

You are trying to create or update your settings and specified more than two default target values (`--default-targets`) on the request.
{: tsCauses}

[Only two default target values are supported.](/docs/atracker?topic=atracker-settings) Retry your request specifying only two default targets for `--default-targets`.
{: tsResolve}
