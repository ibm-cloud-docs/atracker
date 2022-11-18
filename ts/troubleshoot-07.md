---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-13"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting a "cos_write_test_failed" error when trying to create a COS target?
{: #troubleshoot-07}
{: troubleshoot}
{: support}

When creating or validating an {{site.data.keyword.cos_full_notm}} target, the message `Your request to test a target has failed because the target details are not valid. The service could not write to the Cloud Object Storage bucket that is configured.` with a code of `cos_write_test_failed` is returned.
{: shortdesc}



Your request fails with an error message that indicates a problem with the {{site.data.keyword.cos_full_notm}} bucket.
{: tsSymptoms}

You will receive this error if you try to create an {{site.data.keyword.cos_full_notm}} target that has no quota.  You will also receive this error if the authorization is not set or is misconfigured when using service-to-service authorization (`--service-to-service-enabled TRUE`). This message is also received if run the `ibmcloud atracker target validate --target <target name or ID>` command and there is no quota left to upload the data to the target bucket.
{: tsCauses}

Resolve the quota or authorization issues with your {{site.data.keyword.cos_full_notm}} bucket and retry the request.
{: tsResolve}


