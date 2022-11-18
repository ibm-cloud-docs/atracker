---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-13"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting a "region_not_allowed" error when creating a target?
{: #troubleshoot-10}
{: troubleshoot}
{: support}

When creating a target, a message similar to `Your request has failed due to the region requested not being permitted. Requested: us-east, Permitted: [eu-gb us-south]` is returned with the code `region_not_allowed`.
{: shortdesc}



Your request fails with an error message and a code of `region_not_allowed`.
{: tsSymptoms}

You are trying to configure a target and the region you requested the target be created in is not a region that has been permitted in the configuration settings.
{: tsCauses}

[Configure the --permitted-target-regions in the configuration settings](/docs/atracker?topic=atracker-settings&interface=cli) to include the the region where you want to configure a target, or specify a target region (`-r`) on your create request in one of the existing permitted target regions.
{: tsResolve}


