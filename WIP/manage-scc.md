---

copyright:
  years: 2019, 2023
lastupdated: "2021-08-09"

keywords:

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}


# Managing security and compliance with {{site.data.keyword.at_short}}
{: #manage-activity-tracker}


{{site.data.keyword.at_short}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.at_short}}
* Define rules for {{site.data.keyword.at_short}} that can help to standardize resource configuration

## Monitoring security and compliance posture with {{site.data.keyword.at_short}}
{: #monitor-activity-tracker}

As a security or compliance focal, you can use the {{site.data.keyword.at_short}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for {{site.data.keyword.at_short}} are added to the {[cloud]} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for {{site.data.keyword.at_short}}
{: #certificate-manager-available-goals}

* Check whether IBM Activity Tracker access is managed only by IAM access groups
* Check whether IBM Activity Tracker has at least # service IDs with the IAM manager role
* Check whether IBM Activity Tracker has at least # users with the IAM manager role
* Check whether IBM Activity Tracker has no more than # service IDs with the IAM administrator role
* Check whether IBM Activity Tracker has no more than # users with the IAM administrator role
* Check whether IBM Activity Tracker logs are encrypted at rest
* Check whether IBM Activity Tracker trails are integrated with LogDNA logs
* Check whether IBM Activity Tracker is provisioned in multiple regions in an account
