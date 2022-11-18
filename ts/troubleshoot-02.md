---

copyright:
  years: 2019, 2022
lastupdated: "2021-08-09"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting an error due to an invalid token when you make an API request?
{: #troubleshoot-02}
{: troubleshoot}
{: support} 

The API request fails if the token that you use does not have permissions to work with the Activity Tracking service.
{: shortdesc}



Your request fails with an error message that indicates that you are not authorized.
{: tsSymptoms}

When you are not authorize to complete a task, you get an error in your response:
{: tsCauses}

```text
{"trace":"53b41915-749c-4af2-b61f-22194d3b56ea","errors":[{"code":"invalid_token","message":"You are not authorize to complete this task. Check you have IAM permissions to work with Activity Tracking in the account.","recovery":"After you check you have permissions, run 'ibmcloud login' to log in to IBM Cloud. Then, run ibmcloud iam oauth-tokens to retrieve your access tokens. Use the IAM token for the Authorization header in your request."} 
```
{: screen}


To resolve the problem, complete the following steps:
{: tsResolve}

1. Check you have IAM permissions to work with Activity Tracking in the account.
2. Get a valid access token. [Learn more about retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
3. Retry the request. Pass the IAM token in the Authorization header of your request.










