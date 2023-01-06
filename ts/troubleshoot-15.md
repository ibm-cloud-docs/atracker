---

copyright:
  years: 2019, 2023
lastupdated: "2022-06-21"

keywords:

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you having access issues when you were able to do so before?
{: #troubleshoot-15}
{: troubleshoot}
{: support}

When attempting to manage {{site.data.keyword.atracker_full_notm}}, you are unable to do so and are getting errors indicating you do not have access to do so.
{: shortdesc}


Your requests fail indicating you do not have access or the correct privileges.
{: tsSymptoms}

If Administrator privileges are set to `All Identity and Access enabled services` in {{site.data.keyword.iamshort}} you will be unable to manage the {{site.data.keyword.atracker_full_notm}} configuration. Administrator privileges must be configured for `Activity Tracker` or [`All Account Management Services`](/docs/account?topic=account-account-services) in {{site.data.keyword.iamshort}}.
{: tsCauses}

Reconfigure the Administrator privileges in {{site.data.keyword.iamshort}} and retry your {{site.data.keyword.atracker_full_notm}} requests.
{: tsResolve}
