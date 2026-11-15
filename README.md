# networkwalks-BOO84H-week2-FOOTPRINTING
Week 2 -FOOTPRINTING
student
(bachelor of cyber security)Mapalo mwenso
Program/BatchB082-Networkwalks
Modules completedW2-PM1 (FOOTPRINTING & RECONNAISSANCE ATTACKS)
W2-PM5 (NETWORK SCANNING WITH ZENMAP)
Client/Target1. Networkwalks (secured written permission already)
2. My own local LAN Network
Permission secured from
client?
Phases covered
Yes
Phase 1: Reconnaissance & Footprinting
Phase 2: Scanning & Network Discovery
Phase 3-5: In Progress
1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission
or the devices/systems that I own myself. All these materials are for education and research purpose
only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are
not responsible for what you do with this knowledge. Every action you take is your own responsibility.
Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most
countries unauthorised access is a crime even when nothing is damaged.
Pentesting Project Report | Networkwalks | Page 12. Introduction
This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1)
and scanning my own local network with Zenmap (W2-PM5). One module covers the footprinting phase
and the other covers the scanning phase, so together they show how an attacker moves from gathering
public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship
program at Networkwalks.
All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed
(scanning). Every step below includes the exact command used, the result I observed, a screenshot as
evidence, and a short note on why the finding matters from an attacker's point of view.
3. Tools Used
The table below lists each tool used in this report and its purpose.
ToolPurpose
Kali Linux & WindowsOperating systems used for reconnaissance activities
WHOISFind domain registration details (owner, dates, name servers).
whatwebFingerprint web technologies (server, CMS, plugins, IP).
nslookupResolve the domain name to its IP address using DNS.
curl -IRead the HTTP response headers of the website.
wafw00fDetect whether a Web Application Firewall protects the site.
dnsreconEnumerate all DNS records (NS, MX, SPF, TXT, SRV).
Zenmap (Nmap GUI)Scan the local subnet to find live hosts, IPs and MAC addresses.
Windows CMDLocal IP and MAC address identification
4. Activities Performed
4.1 Footprinting & Reconnaissance
I performed reconnaissance against the networkwalks.com
domain using six Kali Linux tools: WHOIS,
WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon. Each tool was used to collect a different type of
information about the target.
First, i used whois which revealed the registrar, registration and expiry dates, and name servers. Here the name
servers point to HostGator, so an attacker instantly learns the hosting provider. Registration dates
and abuse contacts help with social engineering and planning.
Secondly, i used whatweb to expose the exact software and versions (here Wordpress 7.0.4 and WP Download
Manager
3.3.58). An attacker looks these versions up in vulnerability databases.
.
Thirdly,i used nslookup which turns a domain name into its real IP address (192.232.216.135). Knowing the
IP lets an attacker scan the server directly.
Pentesting Project Report | Networkwalks | Page 2Forthly i used curl -l ,HTTP headers leak the web server, caching stack and hidden endpoints (here the WordPress
REST API at /wp-json/). Attackers read headers to fingerprint the stack and find entry points
without even loading the full page .
.
And then i used HTTP headers leak the web server, caching stack and hidden endpoints (here the WordPress
REST API at /wp-json/).
Finally, I used DNSRecon to enumerate DNS records. The results provided information relating to
name servers, mail servers, SPF/TXT records, service records and DNS software information.
4.2 Network Scanning with Zenmap
For the second activity, I used Zenmap to perform network discovery on my local network. The practical
required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC
addresses, and generate a network topology.
I first used the Windows ipconfigcommand to identify my local IP address and LAN subnet. I then
entered the subnet into Zenmap and selected Ping Scan to identify active hosts.
This is the information i received after running the work.

●10.0.0.1

●10.0.0.2

●10.0.0.10

After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved
the network topology in PDF format as required by the practical task.

Based on the information collected during the footprinting and network scanning activities, I identified
the following potential risks.
Risk / FindingEvidence /
Observation
1
#
Potential ImpactRisk Level
Web technology
information exposedWhatWeb identified
WordPress and WP
Download ManagerAttackers may use exposed
technology/version information to
identify software requiring further
security review● Medium
2Server IP address
identifiableNslookup resolved the
domain to
192.232.216.135Provides information about the
network location of the web service● Low
3HTTP technical
information exposedCurl returned HTTP
response headers and
exposed /wp-json/May assist technology fingerprinting
and further enumeration● Low
4WAF technology
identifiableWafw00f identified
ModSecurity
(SpiderLabs)Reveals information about the web
application’s security architecture● Low
5DNS infrastructure
information exposedDNSRecon identified
DNS, mail and
service-related recordsDNS information can help build a
broader infrastructure profile● Medium
6Multiple live hosts
visible on local
networkZenmap identified four
live hosts in the example
networkUnknown or unauthorized devices
may potentially be present on a
network● Medium
Risk level key: ● Critical ● Medium ● Low
The risks above are observations from the footprinting and scanning exercises, not confirmed
vulnerabilities.
The practical exercises primarily involved information gathering and host discovery. No exploitation or
vulnerability validation was performed as part of these two modules.
Therefore, the presence of information such as a software version, IP address or DNS record does not
by itself mean that the system is vulnerable. Further authorized security testing would be required to
confirm any actual vulnerability.
6. Recommendations
Based on the observations from these activities, I recommend the following security improvements:
1. Review publicly exposed technology information
Organizations should regularly review what information about their web technologies, CMS and
plugins is publicly visible.
 Keep software updated
CMS platforms, plugins and other web technologies should be regularly updated and reviewed
against current security advisories.
3. Review HTTP headers
HTTP response headers should be reviewed to determine whether unnecessary technical
information is being exposed.
4. Review DNS records regularly
DNS records should be checked periodically to ensure that only required information and
services are publicly exposed.
5. Properly configure and monitor the WAF
Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.
6. Perform regular internal network discovery
Organizations should periodically scan their own networks to identify active devices.
7. Investigate unknown devices
Any unexpected device discovered during network scanning should be investigated and verified.
8. Maintain network documentation
Network topology and device information should be documented and updated regularly.
9. Perform security testing with authorization
Reconnaissance and scanning should only be performed against systems and networks where
appropriate authorization has been provided.
7. Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities
covering footprinting, reconnaissance and network scanning.
In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I
learned how WHOIS can provide domain information, WhatWeb can identify web technologies,
Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF,
and DNSRecon can provide additional DNS information.
In the network scanning activity, I used Zenmap to identify my local network configuration and discover
active hosts. I also collected IP and MAC address information and created a network topology.
The exercises showed me that information gathering is an important part of cybersecurity. Even before
attempting to exploit a system, a security professional can learn a significant amount about an
environment by carefully analyzing publicly available information and network responses.
I also learned that technical findings should be documented clearly. A good cybersecurity report should
explain what was performed, what was discovered, what the observation means, what risk it may
create, and what can be done to reduce that risk.
Finally, I learned that reconnaissance and scanning must always be performed within an authorized
scope. These activities were completed as part of the assigned educational cybersecurity lab.
## 3.findings -external footprinting

### 3.1 Task 1: whois -Domain registration
![whois](screenshoot/whois.png)

### 3.2 Task 2: nslookup - Resolution
![nslookup](screenshot/nslookup.png)

### 3.3 Task 3: curl -l -HTTP headers
![curl](screenshot/curl.png)

### 3.4 Task 4: wafw00f -web application firewall
![wafw00f](screenshot/wafw00f.png)

### 3.5 Task 5 : dsrecon
![dsrecon](screenshot/dsrecon.png)
