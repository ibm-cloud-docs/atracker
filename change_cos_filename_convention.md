---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Changes to {{site.data.keyword.cos_full_notm}} file naming convention
{: #change_cos_filename_convention}

For {{site.data.keyword.cos_full}} targets (target type = `cos`), the auditing events are routed to the corresponding {{site.data.keyword.cos_full_notm}} (COS) buckets and stored in time-based files. The file naming convention is being changed. The format of the data in the files is not changed.

The current naming convention is:

```text
<region>/<date and hour>/<timestamp>+<offset>.log
```
{: codeblock}

The new naming convention prepends the account ID to the file path and appends a unique ID to the current naming convention:

```text
<account_id>/<region>/date and hour>/<timestamp>+<offset>_<uuid>.log
```
{: codeblock}

Before 15 May 2025, customers that have a dependency on the current file naming convention might need to update their automation to reference the common file name prefix to handle both the current and new conventions.

- If your automation tool does not use a prefix to list objects in a COS bucket, no action is required.

- If your automation tool uses a prefix to list objects (for example, files) in a COS bucket, update the automation so that it can list objects with both the old and new naming conventions.
    - A simple approach is to list objects twice, first in the old naming convention and then in the new naming convention, so that you can get the objects regardless of the old or new naming convention.
    - The list call for the old naming convention can be removed after 15 May 2025.
