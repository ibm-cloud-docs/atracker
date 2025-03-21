---

copyright:
  years:  2021, 2025
lastupdated: "2025-03-21"

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

With the change, the new naming convention appends a unique ID to the current naming convention:

```text
<region>/date and hour>/<timestamp>+<offset>_<uuid>.log
```
{: codeblock}

Before 23 April 2025, customers that have a dependency on the current file naming convention might need to update their automation to reference the common file name prefix to handle both the current and new conventions.

- If your automation tool uses the current naming convention to list and download objects (for example, files) in a COS bucket, change the automation to use a common prefix for both naming conventions. For example, use the common prefix `<region>/date and hour>/<timestamp>`.

- If you already use a prefix that is common for both naming conventions, no action is required.
