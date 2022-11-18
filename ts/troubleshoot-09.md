---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-13"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting a "CosEndpoint.APIKey is not valid" error when creating a COS target?
{: #troubleshoot-09}
{: troubleshoot}
{: support}

When creating an {{site.data.keyword.cos_full_notm}} target, the message `Your request has failed because the value of CosEndpoint.APIKey is not valid. Set a valid value in your target request and try again.` is returned.
{: shortdesc}



Your request fails with an error message and a code of `invalid_value`.
{: tsSymptoms}

You are trying to configure a COS target and have not specified `--api-key` or `--service-to-service-enabled TRUE` on the request.
{: tsCauses}

Retry the request after adding `--api-key` with your [COS bucket API key.](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#cos_apikey) or `--service-to-service-enabled TRUE` as appropriate for your environment. Specifying `--service-to-service-enabled TRUE` requires that you have [service-to-service authorization](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#cos_s2s) configured for your COS bucket.
{: tsResolve}


