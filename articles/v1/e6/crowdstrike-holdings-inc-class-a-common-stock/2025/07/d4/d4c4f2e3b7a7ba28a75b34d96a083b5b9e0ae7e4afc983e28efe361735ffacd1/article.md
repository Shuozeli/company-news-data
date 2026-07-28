---
schema_version: "1.0.0"
document_id: "d4c4f2e3b7a7ba28a75b34d96a083b5b9e0ae7e4afc983e28efe361735ffacd1"
company_key: "crowdstrike-holdings-inc-class-a-common-stock"
company: "CrowdStrike Holdings Inc. Class A Common Stock"
source_id: "crowdstrike-holdings-inc-class-a-common-stock-news-import-26dc963e5592"
canonical_url: "https://www.crowdstrike.com/en-us/blog/crowdstrike-detects-blocks-sharepoint-zero-day-exploitation/"
published_at: "2025-07-21T00:00:00+00:00"
first_seen_at: "2026-07-25T01:07:09.054440+00:00"
fetched_at: "2026-07-28T22:01:03.825556+00:00"
content_hash: "sha256:de02eb98b3b83a4b615765052a9dcaf8925545963d88b7a5acce260072074eaa"
---

# CrowdStrike Detects and Blocks Initial SharePoint Zero-Day Exploitation

Beginning on July 18, 2025, at approximately 0700 UTC, CrowdStrike Falcon® Complete Next-Gen MDR and CrowdStrike Falcon® Adversary OverWatch™ identified a wave of Microsoft SharePoint exploitation attempts by an unknown adversary. Two distinct zero-day vulnerabilities were made publicly available: a critical remote code execution vulnerability ([CVE-2025-53770](https://nvd.nist.gov/vuln/detail/CVE-2025-53770) ) and a server spoofing vulnerability ([CVE-2025-53771](https://nvd.nist.gov/vuln/detail/CVE-2025-53771) ). The chaining of these vulnerabilities to exploit a vulnerable SharePoint server is being referred to as “ToolShell.”


Since the start of this exploitation, CrowdStrike has observed and successfully blocked hundreds of exploitation attempts across 160+ customer environments, demonstrating both the scale of this threat and the effectiveness of our protection capabilities.


The CrowdStrike Falcon® platform detects and protects against exploitation of the Microsoft SharePoint zero-days, blocking known behaviors associated with these vulnerabilities. This blog post provides context surrounding this emerging threat, as well as guidance for customers on how they can use the Falcon platform to protect their environments. Customers of CrowdStrike Falcon® Adversary Intelligence Premium can find more detailed analysis in Intel report CSA-250846.


## Observed Exploitation of SharePoint Vulnerability


CrowdStrike has observed widespread exploitation of CVE-2025-53770 involving a deserialisation attack leading to attempts to write a malicious .aspx webshell on the host. That file,` spinstall0.aspx` , is used to steal IIS Machine Keys, which can later be used for other post-exploitation attacks.


This attack begins with a specially crafted POST request to an accessible SharePoint server. The POST request payload will attempt to write the .aspx file via PowerShell. That malicious PowerShell command, spawned from the SharePoint IIS process, is blocked by the Falcon platform.


Figure 1. Blocked PowerShell spawned from the SharePoint worker process w3wp.exe (click to open in new tab)


We have tracked the size and speed of attempted payload delivery over time by mapping detections from the Falcon platform. The following timeline of activity has been observed:


- July 18 (morning UTC): A small number of SharePoint servers were attacked
- July 18 (1330-1845 UTC): Shortly after, likely following the publicity of the zero-day, the campaign ramped up significantly with 177 servers attacked on the same day
- July 19 (0600-0800 UTC): Exploitation recommenced briefly before temporarily ceasing
- July 21 (0740 UTC): Activity resumes with 32 servers attacked in four hours up to 1130 UTC


Figure 2. Observed instances of attempted exploitation of SharePoint servers over time (click to open in new tab)


## Defending Against This Threat


Organizations are strongly encouraged to apply patches that have been released to ensure they are protected. Microsoft has[published customer guidance](https://msrc.microsoft.com/blog/2025/07/customer-guidance-for-sharepoint-vulnerability-cve-2025-53770/) and released patches for[Microsoft SharePoint Server 2019 Core](https://www.microsoft.com/en-us/download/details.aspx?id=108286) ,[Microsoft SharePoint Server Subscription Edition](https://www.microsoft.com/en-us/download/details.aspx?id=108285) , and[Microsoft SharePoint Enterprise Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=108288) .


### CrowdStrike Falcon Endpoint Detection and Response


As mentioned in our opening analysis, this attack relies on specially crafted POST requests to exploit the SharePoint zero-day vulnerabilities. CrowdStrike Falcon® Insight XDR endpoint security successfully detected and blocked these attacks through advanced behavioral analysis rather than relying on signature-based detections.


The attack chain exploits SharePoint servers by executing malicious code to extract authentication keys, enabling attackers to send authenticated system-level commands. Falcon Insight XDR’s behavioral engine identified suspicious activity when SharePoint processes began launching command prompts and PowerShell scripts — a clear deviation from normal SharePoint operations.


Our multi-layered approach detected:


- **Abnormal process behavior** : Suspicious process chains originating from SharePoint services, including webshells and reconnaissance
- **Network anomalies** : Questionable DNS requests that generated alerts in the Falcon console
- **Behavioral correlation** : Multiple indicators confirming malicious intent


Threat actors continuously adapt their techniques based on security vendor responses. CrowdStrike's threat research team proactively enhances our detection capabilities in response. We are deploying additional behavioral detections this week that focus on post-exploitation activities and alternative attack vectors, providing continued coverage as attack methods evolve.


### CrowdStrike Falcon Exposure Management


Customers can find CVE-2025-53770 and CVE-2025-53771 with CrowdStrike Falcon® Exposure Management’s vulnerability management capability.


CrowdStrike has developed a custom dashboard for[Falcon Exposure Management](https://www.crowdstrike.com/en-us/platform/exposure-management/risk-based-vulnerability-management/) customers so they can quickly see which hosts are vulnerable. The dashboard includes threat analysis provided by researchers, detailed information on vulnerable hosts, and the count of vulnerable product versions. As with other custom dashboard releases, customers can access these predefined dashboards by navigating to Exposure management > Vulnerability management > Dashboards, then select this dashboard for ToolShell CVE-2025-53770.


Figure 3. Custom Falcon Exposure Management dashboard providing visibility into CVE-2025-53770 (click to open in new tab)


Falcon Exposure Management has had detections for all supported platforms since the vulnerability was initially disclosed. The vulnerability currently has an ExPRT.AI severity rating of "Critical," with an exploit status of "Actively Used (Critical)" due to confirmed active exploitation in the wild.


To identify vulnerable systems, customers can navigate to the Exposure Management > Vulnerability Management > Vulnerabilities page in the CrowdStrike Falcon platform. From there, they can use the Vulnerability ID filter with a value of "CVE-2025-53770" and/or “CVE-2025-53771.” If any of the managed systems are vulnerable, results will be shown here. If they receive the message "No vulnerabilities found," then all of their managed SharePoint systems have the necessary patches. For any systems found vulnerable, the remediation guidance provided for that system will mention the necessary security updates to apply.


### CrowdStrike Falcon Next-Gen SIEM


As the vulnerabilities discussed target the SharePoint server, ingestion of Microsoft IIS server logs provides a comprehensive view into this emerging threat. CrowdStrike Falcon® Next-Gen SIEM customers are encouraged to ingest IIS logs to gain the necessary visibility and detect malicious actions. Further information about ingesting and parsing this data source is available to customers[here](https://falcon.crowdstrike.com/documentation/page/l5e17e69/data-connector-built-for-microsoft-iis) . The “Microsoft - IIS - Microsoft Sharepoint ToolShell Exploitation CVE-2025-53770” rule template is currently available to customers who wish to detect possible exploitation attempts specific to CVE-2025-53770. This template leverages the following query to identify instances where malicious URLs are being accessed:


```text
#Vendor="microsoft" #event.module="iis" #event.dataset="iis.access" #repo!="xdr*"
| parseUrl(http.request.referrer)
| http.request.method="POST" url.path="/_layouts/15/ToolPane.aspx" url.query="DisplayMode=Edit&a=/ToolPane.aspx" http.request.referrer.path="/_layouts/SignOut.aspx"
| http.response.status_code =~ in(values=[200,302,401])


```


Falcon Next-Gen SIEM users may also leverage a hunting query that uses the recently released[correlate()](https://library.humio.com/data-analysis/functions-correlate.html) capability. This[rule](https://github.com/CrowdStrike/logscale-community-content/blob/main/Queries-Only/Helpful-CQL-Queries/CVE-2025-53770%20-%20SharePoint%20ToolShell.md) , which is also provided below, may be used to identify instances where a SharePoint IIS process results in a PowerShell command being executed, followed by an ASPX file being written.


```text
correlate(
cmd: {
#event_simpleName=ProcessRollup2 event_platform=Win FileName="cmd.exe" ParentBaseFileName="w3wp.exe"
} include: [aid, ComputerName, TargetProcessId, ParentBaseFileName, FileName, CommandLine],
pwsh: {
#event_simpleName=ProcessRollup2 event_platform=Win FileName="powershell.exe"
| aid <=> cmd.aid
| ParentProcessId <=> cmd.TargetProcessId
aspx: {
#event_simpleName=/^(NewScriptWritten|WebScriptFileWritten)$/ event_platform=Win FileName=/\.aspx/i
| aid <=> cmd.aid
| ContextProcessId <=> pwsh.TargetProcessId
} include: [aid, ComputerName, TargetFileName],
sequence=true, within=5m)


```


## Conclusion


The SharePoint vulnerability exploitation demonstrates how critical application threats can provide attackers with initial access to organizations. CrowdStrike customers benefit from multiple layers of protection against these attacks.


While we strongly recommend patching SharePoint instances immediately, the Falcon platform provides comprehensive protection through:


- **Falcon Insight XDR** : Behavioral detection and prevention of exploitation attempts
- **Falcon Exposure Management** : Visibility into vulnerable SharePoint instances
- **Falcon Next-Gen SIEM** : Detection rules for Microsoft IIS logs to identify exploitation attempts


CrowdStrike will continue monitoring this threat and update our guidance as new information emerges.
