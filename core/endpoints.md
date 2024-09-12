---

copyright:
  years:  2021, 2024
lastupdated: "2024-09-12"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Endpoints
{: #endpoints}

The following table lists the endpoints per region for the {{site.data.keyword.atracker_full}} service:
{: shortdesc}

The IP addresses with a date next to them indicate when the IP addresses will be available. IP addresses marked as [Deprecated]{: tag-deprecated} and a date indicate when the IP addresses will no longer be supported and should be removed from any configured allowlists.
{: important}

## Private API endpoints
{: #endpoints_api-atracker-private}

The following table shows the private API endpoints. The port for all endpoints is `https/443` .

| Region                   | ATracker Private endpoint                         | IPs |
|--------------------------|---------------------------------------------------|-------|
| Chennai (`in-che`)      | `https://private.in-che.atracker.cloud.ibm.com` | 166.9.249.118  \n 166.9.249.147  \n 166.9.249.183 |
| Dallas (`us-south`)      | `https://private.us-south.atracker.cloud.ibm.com` | 166.9.58.136 [Deprecated 16 October 2024]{: tag-deprecated}   \n 166.9.51.140 [Deprecated 16 October 2024]{: tag-deprecated}  \n 166.9.48.211 [Deprecated 16 October 2024]{: tag-deprecated}  \n 166.9.228.73 [New 16 October 2024]{: tag-cool-gray}  \n 166.9.229.64 [New 16 October 2024]{: tag-cool-gray}  \n 166.9.230.57 [New 16 October 2024]{: tag-cool-gray} |
| Frankfurt (`eu-de`)      | `https://private.eu-de.atracker.cloud.ibm.com`  | 166.9.30.195 [Deprecated 17 October 2024]{: tag-deprecated}   \n 166.9.28.229 [Deprecated 17 October 2024]{: tag-deprecated}  \n 166.9.32.161 [Deprecated 17 October 2024]{: tag-deprecated}  \n 166.9.209.204 [New 17 October 2024]{: tag-cool-gray}  \n 166.9.209.236 [New 17 October 2024]{: tag-cool-gray}  \n 166.9.210.2 [New 17 October 2024]{: tag-cool-gray} |
| London (`eu-gb`)         | `https://private.eu-gb.atracker.cloud.ibm.com`  | 166.9.38.78 [Deprecated 15 October 2024]{: tag-deprecated}  \n 166.9.34.154 [Deprecated 15 October 2024]{: tag-deprecated}  \n 166.9.36.109 [Deprecated 15 October 2024]{: tag-deprecated}  \n 166.9.245.170 [New 15 October 2024]{: tag-cool-gray}  \n 166.9.245.202 [New 15 October 2024]{: tag-cool-gray}  \n 166.9.245.234 [New 15 October 2024]{: tag-cool-gray} |
| Madrid (`eu-es`)         | `https://private.eu-es.atracker.cloud.ibm.com`  | 166.9.225.11  \n 166.9.226.12  \n 166.9.227.11 |
| Osaka (`jp-osa`)         | `https://private.jp-osa.atracker.cloud.ibm.com`  | 166.9.247.46  \n 166.9.247.71  \n 166.9.247.110 |
| Sao Paulo (`br-sao`)        | `https://private.br-sao.atracker.cloud.ibm.com` | 166.9.246.76  \n 166.9.246.109  \n 166.9.246.157 |
| Sydney (`au-syd`)        | `https://private.au-syd.atracker.cloud.ibm.com` | 166.9.54.51 [Deprecated 14 October 2024]{: tag-deprecated}  \n  166.9.52.48 [Deprecated 14 October 2024]{: tag-deprecated}  \n 166.9.56.53 [Deprecated 14 October 2024]{: tag-deprecated}  \n 166.9.244.119 [New 14 October 2024]{: tag-cool-gray}  \n 166.9.244.151 [New 14 October 2024]{: tag-cool-gray}  \n 166.9.244.183 [New 14 October 2024]{: tag-cool-gray} |
| Tokyo  (`jp-tok`)         | `https://private.jp-tok.atracker.cloud.ibm.com`  | 166.9.249.115   \n 166.9.249.144  \n 166.9.249.180 |
| Toronto  (`ca-tor`)         | `https://private.ca-tor.atracker.cloud.ibm.com`  | 166.9.247.154   \n 166.9.247.183  \n 166.9.247.216 |
| Washington (`us-east`)   | `https://private.us-east.atracker.cloud.ibm.com`  | 166.9.24.96 [Deprecated 15 October 2024]{: tag-deprecated}  \n 166.9.22.84 [Deprecated 15 October 2024]{: tag-deprecated}  \n 166.9.20.212 [Deprecated 15 October 2024]{: tag-deprecated}  \n 166.9.231.252 [New 15 October 2024]{: tag-cool-gray}  \n 166.9.251.89 [New 15 October 2024]{: tag-cool-gray}  \n 166.9.233.28 [New 15 October 2024]{: tag-cool-gray} |
{: caption="Table 1. Lists of private API endpoints for interacting with {{site.data.keyword.atracker_full_notm}}" caption-side="top"}


## Public API endpoints
{: #endpoints_api-atracker-public}

The following table shows the public API endpoints:

| Region                   | ATracker Public endpoint                         | Port         |
|--------------------------|---------------------------------------------------|--------------|
| Chennai (`in-che`)      | `https://in-che.atracker.cloud.ibm.com`         | `https/443`  |
| Dallas (`us-south`)      | `https://us-south.atracker.cloud.ibm.com`         | `https/443`  |
| Frankfurt (`eu-de`)      | `https://eu-de.atracker.cloud.ibm.com`          | `https/443`  |
| London (`eu-gb`)         | `https://eu-gb.atracker.cloud.ibm.com`          | `https/443`  |
| Madrid (`eu-es`)         | `https://eu-es.atracker.cloud.ibm.com`          | `https/443`  |
| Osaka (`jp-osa`)         | `https://jp-osa.atracker.cloud.ibm.com`          | `https/443`  |
| Sao Paulo (`br-sao`)        | `https://br-sao.atracker.cloud.ibm.com` | `https/443`  |
| Sydney (`au-syd`)        | `https://au-syd.atracker.cloud.ibm.com` | `https/443`  |
| Tokyo (`jp-tok`)         | `https://jp-tok.atracker.cloud.ibm.com`          | `https/443`  |
| Toronto (`ca-tor`)         | `https://ca-tor.atracker.cloud.ibm.com`          | `https/443`  |
| Washington (`us-east`)   | `https://us-east.atracker.cloud.ibm.com`          | `https/443`  |
{: caption="Table 2. Lists of public API endpoints for interacting with {{site.data.keyword.atracker_full_notm}}" caption-side="top"}
