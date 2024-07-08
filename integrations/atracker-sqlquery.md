---

copyright:
  years: 2019, 2023
lastupdated: "2021-12-02"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}

# WIP
{: #atracker-sql}

## Step 1. Cover data into Parquet format - WIP
{: #parquet}

```text
SELECT * FROM cleancols(cos://us-south/at-fs-compliance-dallas/us-south/2021-10-04T09/2021-10-04T09:43+00.log STORED AS JSON)
INTO cos://us-south/at-fs-compliance-dallas/RESULTS_BUCKET STORED AS PARQUET
```


## Obtain number of events in a file
{: #obtain_events}

```text
SELECT * FROM cleancols(cos://us-south/at-fs-compliance-dallas/us-south/2021-10-04T09/2021-10-04T09:43+00.log STORED AS JSON)
INTO cos://us-south/at-fs-compliance-dallas/RESULTS_BUCKET STORED AS PARQUET
```

## list all events parsed by JSON field
{: #list_events}

```text
SELECT *
FROM cos://us-south/at-fs-compliance-dallas/RESULTS_BUCKET STORED AS PARQUET
INTO cos://us-south/at-fs-compliance-dallas/RESULTS_BUCKET_DATA STORED AS CSV
```
