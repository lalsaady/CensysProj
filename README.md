# CensysProj

## Part One
The following are my findings about the host data given to me for part one of this interview:
- This host is an nginx web server running Confluence version 7.13.2. This information is found within the following HTTP responses:
  - services.http.response.headers.Server: nginx
  - services.http.response.html_tags: <title>主页面 - Confluence</title>
  - services.http.response.html_tags: <meta name="ajs-version-number" content="7.13.2">


## Part Two and Three
The code in censysTechnical.ipynb serves as the part *two* and *three* of my technical interview. All hosts queried are running Confluence on the HTTP service, similar to the host from part one. The goal is to determine out of the distinct count of queried hosts, how many are running a version of Confluence vulnerable to the [CVE-2022-26134](https://nvd.nist.gov/vuln/detail/CVE-2022-26134) vulnerability. This vulnerability has a CVSS of 9.8, as it allows for unathenticated remote code execution.\
This analysis was inspired by [this](https://censys.io/cve-2022-26134-confluenza-omicron-edition/) Censys blog post written by Mark Ellzey.\
**Note**: You must authenticate using your own Censys API ID and secret using the command line before running this code.

## Conclusion
57 distinct hosts were queried using the Censys Search API. These hosts were found using the filters:

> **(1)** at least one running HTTP service and **(2)** contains "Confluence" in the html title of the HTTP response header

The analyst found that **14%** of 57 distinct hosts found were running one or more instances of Confluence vulnerable to CVE-2022-26134. The host with the most vulnerable instances of Confluence can be traced to Russia. This host is likely running many virtual hosts, which are contributing to the high count of **128** vulnerable Confluence instances.

