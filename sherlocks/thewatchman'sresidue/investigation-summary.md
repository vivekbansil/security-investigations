# Investigation Summary – The Watchman's Residue

## Scenario Overview

This investigation simulated a compromise of a Windows workstation following the abuse of remote management software. The objective was to determine how the attacker gained access, identify attacker activity on the system, reconstruct the intrusion timeline, uncover persistence mechanisms, and determine what sensitive data was collected and exfiltrated.

The investigation required correlating evidence across multiple forensic artifact sources, including network traffic, Windows event logs, registry hives, endpoint artifacts, remote access logs, and file system metadata.

---

## Artifacts Analyzed

* Packet capture (PCAP) data
* TeamViewer log files
* Windows Security event logs
* Windows System event logs
* PowerShell Operational logs
* Microsoft Defender Operational logs
* Registry hives (NTUSER.DAT, SOFTWARE, SYSTEM)
* UserAssist artifacts
* RecentDocs artifacts
* Windows shortcut (LNK) files
* USN Journal ($Extend$J)
* KeePass password database
* File system metadata

---

## Analytical Process

The investigation began with packet capture analysis to understand how the attacker obtained information used to access the environment. Evidence revealed abuse of an AI-assisted support workflow that exposed remote management details.

Analysis then shifted to the compromised workstation, where TeamViewer logs were used to establish remote access activity, file transfers, and attacker session timelines. Additional evidence from Windows logs, UserAssist artifacts, RecentDocs entries, and shortcut files helped determine which tools were executed and which files were accessed.

USN Journal analysis was used to reconstruct file creation, staging, and modification activity, including attacker tooling that was no longer present on disk. Registry analysis was performed to identify persistence mechanisms and determine how malicious code was configured to execute during user logon.

The investigation concluded with analysis of an exfiltrated KeePass database, allowing recovery of credentials that could have enabled further access within the environment.

---

## Findings

Correlated evidence showed that the attacker abused remote management software to obtain interactive access to the workstation. Multiple credential-focused utilities were staged and executed to collect browser credentials, operating system credentials, and other sensitive information.

The attacker gathered sensitive files, staged them within a temporary directory, and transferred them out of the environment using the same remote access channel. Persistence was established through modification of the Windows Winlogon Userinit registry value, causing a malicious executable to launch during user logon.

Evidence also indicated preparation for additional access through the collection of credential stores, including a KeePass password database containing credentials for other systems.

Observed behaviors aligned with common adversary techniques involving remote access software abuse, credential dumping, local data staging, exfiltration, registry-based persistence, and credential theft.

---

## Lessons Learned

This investigation reinforced the importance of:

* Correlating evidence across multiple forensic artifact sources rather than relying on a single log source
* Using remote management logs to reconstruct attacker activity and file transfer timelines
* Leveraging the USN Journal when attacker files are no longer present on disk
* Understanding UserAssist, RecentDocs, and LNK artifacts for user activity reconstruction
* Identifying persistence through less common registry locations such as Winlogon Userinit
* Analyzing credential stores and password managers as part of incident response investigations
* Reconstructing complete attack lifecycles from initial access through persistence and data exfiltration
* Applying structured investigative methodology to produce evidence-based conclusions

