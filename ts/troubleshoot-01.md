---

copyright:
  years: 2019, 2022
lastupdated: "2021-08-09"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting a binding_error code when you make a cURL API request?
{: #troubleshoot-01}
{: troubleshoot}
{: support} 

If you use single quotes in an API request, the request fails with a binding error. 
{: shortdesc}


The API request fails and the response returns a binding error.
{: tsSymptoms}

When you use single quotes in the header of a cURL request, for example, `-H 'Authorization:  $ACCESS_TOKEN'   -H 'content-type: application/json'`, you can get the `binding_error` problem.
{: tsCauses}


```text
{"trace":"70684768-53ae-476f-bec7-2d923bb5f14c","errors":[{"code":"binding_error","message":"The input parameters in the request body are either incomplete or in the wrong format. See detailed error: invalid character 'n' looking for beginning of object key string."}]}curl: (6) Could not resolve host: COS
curl: (6) Could not resolve host: target
curl: (3) [globbing] unmatched close brace/bracket in column 389
```
{: screen}


Check the header in your cURL request is set with double quotes.
{: tsResolve}

```text
-H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock} 


