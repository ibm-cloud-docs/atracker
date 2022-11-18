---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-13"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting a "multiple targets" error when working with a target?
{: #troubleshoot-08}
{: troubleshoot}
{: support}

When working with a target, for example, when validating a target using the `ibmcloud atracker target validate` command and specifying a target name for `--target`, the following message is returned: `Multiple targets were found with the same name - marisa-acc-bucket, use target id instead.`
{: shortdesc}



Your request fails with an error message that indicates you have more than one target defined with the same name.
{: tsSymptoms}

You have more than one target defined with the same name and {{site.data.keyword.atracker_full_notm}} cannot identify the unique target when the target name is specified.
{: tsCauses}

To work with a target, use the target ID instead of the target name when you have multiple targets defined with the same name.
{: tsResolve}


