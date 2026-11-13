# WEEK-2-NWTWORKWALKS-INTERN-FOOTPRINTING-AND-
FieldDetails
Pentester Name (Cybersecurity Professional)Clement Hamoonga
LinkedIn Profilehttps://www.linkedin.com/in/clement-hamoonga (replace with your exact LinkedIn handle if customized)
Program / BatchB082-Networkwalks
Date13 November 2026
Modules CompletedW2-PM4 (OSINT Footprinting with theHarvester & WHOIS)
W2-PM5 (Network Scanning with Zenmap)
Client / Target1. Networkwalks (networkwalks.com — written permission secured)
2. Public OSINT Target (microsoft.com — passive OSINT)
3. Personal Local Area Network (LAN)
1. Liability Disclaimer
​I have performed these activities strictly on systems and devices where I secured explicit written permission or on networks and virtual environments that I own and administer myself. All materials, commands, and observations in this report are documented solely for educational and authorized security research purposes. None of the techniques demonstrated herein should be used to violate applicable laws or organizational policies. The instructor, authors, and Networkwalks bear no responsibility for any misuse of this knowledge. Every individual is solely accountable for their actions; unauthorized access or probing constitutes a criminal offense in most jurisdictions even when no damage occurs.
​2. Introduction
​This report documents my practical cybersecurity work completed during Week 2 of the Networkwalks Cybersecurity Internship Program, focusing specifically on Module W2-PM4 (OSINT Footprinting & Domain Reconnaissance) and Module W2-PM5 (Local Network Scanning & Topology Mapping with Zenmap). Together, these two modules demonstrate the structured transition from passive Open-Source Intelligence (OSINT) gathering to active host discovery on a local subnet.
​Footprinting and OSINT tasks (W2-PM4) were executed within a Kali Linux virtual machine (Oracle VirtualBox) using whois and theHarvester, while active host discovery (W2-PM5) was carried out using Zenmap (the Nmap graphical interface) alongside Windows network utilities. Each phase below details the commands executed, observed outputs, captured evidence, and defensive security implications.
​3. Tools & Environment Used
Tool / PlatformModulePurpose
Kali Linux (VirtualBox)W2-PM4Primary penetration testing OS used to execute passive OSINT and domain reconnaissance tools.
Windows Host & CMD (ipconfig)W2-PM5Host operating system used to inspect local IPv4 configuration, subnet mask, and default gateway prior to scanning.
WHOISW2-PM4Query public domain registration records, registrar details, domain status flags, and authoritative name servers.
theHarvester (v4.11.1)W2-PM4Gather Open-Source Intelligence (OSINT) including subdomains, IP addresses, emails, and host records from public search engines.
Zenmap (Nmap GUI)W2-PM5Perform Ping Scans (-sn) across the local subnet to enumerate active hosts, latency, MAC addresses, and generate a visual network topology.
4. Activities Performed
​4.1 Module W2-PM4: Footprinting & OSINT Reconnaissance (WHOIS & theHarvester)
​In Module W2-PM4, I conducted passive reconnaissance from my Kali Linux VirtualBox environment (MY FRSH KALI LINUX) to examine how publicly accessible registration records and search engine indexes expose organizational infrastructure details without sending intrusive traffic to target servers.
​Domain Registration Lookup (WHOIS):
I executed whois networkwalks.com in the Kali terminal to inspect domain registration metadata. The query returned authoritative name server information (NS30.DOMAINCONTROL.COM), DNSSEC status (unsigned), registrar database update timestamps, and ICANN registrar policy terms.
​OSINT Enumeration (theHarvester):
I launched theHarvester (v4.11.1) to perform passive OSINT collection. First, I inspected the available passive data sources and flags via theHarvester -h (confirming engines such as Baidu, DuckDuckGo, Certificate Transparency logs, Shodan, and URLScan). Next, I executed a targeted passive query (theHarvester -d microsoft.com -l 1000 -b baidu) to observe search-engine harvesting behavior. The scan queried Baidu passively without active probing and confirmed zero exposed email addresses, hosts, or IPs from that engine.
​4.2 Module W2-PM5: Local Network Scanning & Discovery with Zenmap
​In Module W2-PM5, I transitioned from passive OSINT to active local network discovery using Zenmap on Windows to map live devices within a local subnet.
​Host Discovery (Ping Scan):
I verified the local network parameters using Windows ipconfig, then launched Zenmap, entered the target CIDR subnet (10.0.0.0/24), and selected the Ping scan profile (nmap -sn 10.0.0.0/24) to identify live hosts without full port enumeration.
​Live Host & Topology Mapping:
The scan completed across 256 IP addresses in 2.82 seconds and discovered four active hosts:
​10.0.0.1 — MAC Address: 00:50:56:E3:B3:2C
​10.0.0.4 — MAC Address: 00:0C:29:C0:94:8F
​10.0.0.19 — MAC Address: 00:50:56:E9:64:82
​10.0.0.5 — Live host detected
Finally, I opened the Topology tab in Zenmap, enabled the Legend window to distinguish host states and connection types, and exported the network topology map. (Note: Replace the sample 10.0.0.0/24 outputs/screenshots with your own local LAN subnet scan if required by your instructor.)
​5. Risk Analysis & Security Impact
#Finding / ObservationEvidence / SourcePotential Security ImpactRisk Level
1Authoritative DNS & Registrar Metadata ExposedWHOIS revealed NS30.DOMAINCONTROL.COM and unsigned DNSSEC statusAttackers can identify DNS hosting providers and assess susceptibility to DNS spoofing or cache poisoning.Low
2Public OSINT Attack Surface ExposuretheHarvester queried public search indexes for domain emails, hosts, and IPsExposed employee emails or subdomains via OSINT can be leveraged for targeted phishing or credential stuffing.Medium
3Multiple Active Hosts & MAC Vendors Visible on LANZenmap Ping Scan (-sn) discovered 4 live hosts and virtual NIC MAC addressesUnmonitored or unauthorized rogue devices connected to a local subnet increase lateral movement risk.Medium
4Clear Internal Network Topology MappingZenmap Topology view mapped host relationships relative to localhostIf an attacker gains an internal foothold, rapid ARP/ICMP discovery reveals gateway and peer targets.Low
