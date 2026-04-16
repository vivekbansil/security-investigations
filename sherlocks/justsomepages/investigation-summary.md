# Investigation Summary – JustSomePages

## Scenario Overview  
This investigation simulated a multi-stage intrusion involving a compromised web application and subsequent attacker movement across internal systems. The objective was to analyze network traffic, system logs, and application behavior to reconstruct the attack chain from initial access through persistence.

## Artifacts Analyzed  
- Packet capture (PCAP) data  
- Windows Event Logs (EVTX)  
- HTTP request and response activity  
- Command execution artifacts  
- Web application and web shell behavior  

## Analytical Process  
The investigation began by analyzing HTTP traffic in the PCAP, where suspicious requests revealed the presence of a JSP-based web shell on a public-facing Tomcat server. These requests contained command parameters and returned system output, indicating remote command execution through the web application.

After confirming initial access, analysis focused on understanding the attacker’s activity on the compromised system. Command execution patterns (e.g., system enumeration and directory navigation) were identified through HTTP traffic and log artifacts, confirming elevated access and active system interaction.

Correlation of host logs and execution artifacts revealed the use of Windows Management Instrumentation (WMIC) to execute commands on another internal system, indicating lateral movement from the compromised web server.

Further investigation of network traffic identified the download of a PowerShell script from an external host. Analysis of this script showed that it established a web server-based backdoor, enabling command execution and file transfer over HTTP on a non-standard port.

Using this access, the attacker explored the file system and uploaded an ASPX web shell into the IIS web root, replacing legitimate content and expanding control over the environment.

Events were reconstructed chronologically to map the progression from initial web exploitation through lateral movement, persistence, and continued access.

## Findings  
Correlated evidence confirmed that the attacker successfully exploited a public-facing web application to deploy a JSP web shell and gain remote command execution. The attacker performed system enumeration, pivoted to an internal host using WMIC, and established persistence through a PowerShell-based backdoor.

Additional web shells were deployed within the IIS web root, allowing continued access and control over the system. Observed behavior aligned with common adversary techniques including exploitation of public-facing applications, web shell usage, remote command execution, lateral movement, tool transfer, and HTTP-based command-and-control.

## Lessons Learned  
This investigation reinforced the importance of:

- Identifying web shell behavior in HTTP traffic  
- Correlating network and host-based evidence  
- Recognizing lateral movement through legitimate administrative tools  
- Detecting staged payload delivery and backdoor activity  
- Understanding how attackers establish persistence across multiple layers  
- Reconstructing full attack chains from initial access to post-exploitation  
