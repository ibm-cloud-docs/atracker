---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-16"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting an "not_found" error when updating settings?
{: #troubleshoot-14}
{: troubleshoot}
{: support}

When updating settings, the following message is returned: `Your request has failed because the target id target-logdna is not valid.`.
{: shortdesc}



Your request fails with an error message and a code of `not_found`.
{: tsSymptoms}

You are trying to update settings and have specified a target name for `--default-targets` instead of the target IDs.
{: tsCauses}

Retry the request specifying the target IDs instead of the target names.
{: tsResolve}


