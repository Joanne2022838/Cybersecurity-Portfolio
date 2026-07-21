###### **Nmap Vulnerability Scan – Metasploitable2**



&#x20;**Objective**

Perform reconnaissance and service enumeration against an intentionally vulnerable 

target machine to identify open ports, running services, and potential 

vulnerabilities using Nmap.



&#x20;**Environment**

\- \*\*Attacker machine:\*\* Kali Linux (VirtualBox)

\- \*\*Target machine:\*\* Metasploitable2 (VirtualBox)

\- \*\*Network:\*\* Isolated Host-only network (192.168.56.0/24), no internet access

\- \*\*Attacker IP:\*\* 192.168.56.10

\- \*\*Target IP:\*\* 192.168.56.101



&#x20;**Tools Used**

\- Nmap 7.99



&#x20;**Methodology**

1\. Verified connectivity between attacker and target using `ping`

2\. Ran a full port scan with service and script detection:



***nmap -sV -sC 192.168.56.101 -oN nmap\_scan\_metasploitable2.txt***



3\. Reviewed output for open ports, service versions, and notable script results.



&#x20;**Key Findings**



| Port | Service | Version | Notes |

|------|---------|---------|-------|

| 21   | FTP     | vsftpd 2.3.4 | Anonymous login allowed; this version has a publicly known backdoor vulnerability (CVE-2011-2523) |



| 22   | SSH     | OpenSSH 4.7p1 | Old version, multiple known CVEs |



| 139/445 | SMB  | Samba 3.0.20 | Message signing disabled (flagged by Nmap as "dangerous, but default") |



| 5432 | PostgreSQL | 8.3.0–8.3.7 | Expired SSL certificate (valid only until 2010) |



| 5900 | VNC     | Protocol 3.3 | Weak/outdated authentication scheme |



**Full raw scan output:** \[`nmap\_scan\_metasploitable2.txt`](./nmap\_scan\_metasploitable2.txt)



&#x20;**Remediation Recommendations**

\- Update vsftpd to a patched version and disable anonymous FTP access

\- Upgrade OpenSSH and Samba to current supported versions

\- Enable SMB message signing

\- Renew or regenerate expired SSL certificates

\- Disable or restrict VNC access, enforce strong authentication



&#x20;**Lessons Learned**

This was my first hands-on Nmap scan against a real (lab) target. Setting up the 

isolated network and getting all tooling working took real troubleshooting — 

network adapter configuration, DHCP issues, and package installation were all 

learning points beyond just running the scan itself.



**## Disclaimer**

All testing was performed against Metasploitable2, an intentionally vulnerable 

system, within an isolated lab environment owned by the author. No real-world 

systems were targeted.

