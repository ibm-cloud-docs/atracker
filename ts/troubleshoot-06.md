---

copyright:
  years: 2019, 2024
lastupdated: "2024-01-18"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting an "access denied" error when trying to create a COS target?
{: #troubleshoot-06}
{: troubleshoot}
{: support}

When creating an {{site.data.keyword.cos_full_notm}} target using service-to-service authorization, the message `Your request to test a target has failed because the target details are not valid. The service could not write to the Cloud Object Storage bucket that is configured. {'error_code':'403','error_message':'Access Denied'}` is returned.
{: shortdesc}



Your request fails with an error message that indicates access to the {{site.data.keyword.cos_full_notm}} bucket was denied.
{: tsSymptoms}

You define a bucket in an account but have not set up [service-to-service authorization](/docs/atracker?topic=atracker-target_v2_cos&interface=ui#target_v2_cos_s2s_ui) to that bucket.  Then you attempt to create an {{site.data.keyword.cos_full_notm}} target pointing to the bucket using service-to-service authorization (`--service-to-service-enabled TRUE`), instead of using the [COS bucket API key.](/docs/atracker?topic=atracker-cos#cos_bucket_access).
{: tsCauses}

Either setup [service-to-service authorization to the bucket](/docs/atracker?topic=atracker-target_v2_cos&interface=ui#target_v2_cos_s2s_ui) and retry the target create request, or use the [COS bucket API key](/docs/atracker?topic=atracker-cos#cos_bucket_access) on the create request.
{: tsResolve}
