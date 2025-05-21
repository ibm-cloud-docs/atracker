---

copyright:
  years:  2021, 2025
lastupdated: "2025-05-21"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I receiving email notifications regarding my target configuration?
{: #troubleshoot-20}
{: troubleshoot}
{: support}

You are receiving {{site.data.keyword.cloud_notm}} email notifications regarding your target configuration.
{: shortdesc}


You are receiving {{site.data.keyword.cloud_notm}} email notifications reporting that your target is misconfigured or that the target configuration issue is resolved.
{: tsSymptoms}

Your target is misconfigured, and alerts are not being routed, or the target misconfiguration issue has been resolved.
{: tsCauses}

A misconfigured target can be due to bad credentials, missing authorization permissions, or a target referencing a target instance that does not exist.

If you are receiving emails regarding an incorrectly configured target, review the target configuration [documentation](/docs/atracker?topic=atracker-target_v2&interface=ui) and fix the issues with your target configuration.
{: tsResolve}

If you are receiving messages that an incorrectly configured target issue has been resolved, check your target configuration to make sure the resolution is correct for your environment.
